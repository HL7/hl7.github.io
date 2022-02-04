---
title: "Hosting your own validator-wrapper"
permalink: /docs/validator-wrapper/hosting
excerpt: "How to stand up your own validator-wrapper server."
last_modified_at: 2021-04-27
toc: true
---
There may be a case where you are working with sensitive data, but still wish to take advantage of the new validator-wrapper website ui.

We've provided instructions on how to setup and host your own copy of the website on a [Google Cloud Compute Engine VM][Link-GoogleComputeEngine]. These instructions are just as an example, and can be applied to locally hosted instances, as well as other hosting providers.

## Setting up a GCP VM with NGINX and Docker

### Install and Configure NGINX
NGINX is going to sit in front of our docker website, so all traffic will be directed through it. This is helpful, as we don't want to expose the port, or different instances of the VM to the external world. We just want someone to go to the url for our website, and be seamlessly directed to the correct page.

1. SSH into the compute engine VM, either through the [Google Cloud Console][Link-GoogleCloudConsole], or by installing the [Google Cloud SDK][Link-GoogleCloudSDK] on your local machine.
2. Install NGINX by running the following commands:
* `sudo apt update`
* `sudo apt upgrade`
* `sudo apt-get install nginx`
3. Configure NGINX
* `cd /etc/nginx/sites-enabled/`
* Edit the **default** file (in our example, we use vi to edit) `sudo vi default`
* In the `server` section of this file, put the following:

```shell
server {
        server_name <space separated list of urls you want to use for your website>;
        location / {
                proxy_set_header Host $host;
                proxy_pass http://localhost:<the port on your running docker image you want to expose>/;
                proxy_redirect off;
                access_log /var/log/nginx/validator.log;
        }
}
```

So, in the case of the validator-wrapper website, our file looks like this:

```shell
server {
        server_name fhirvalidator.org www.fhirvalidator.org fhirvalidator.com www.fhirvalidator.com;
        location / {
                proxy_set_header Host $host;
                proxy_pass http://localhost:3500/;
                proxy_redirect off;
                access_log /var/log/nginx/validator.log;
        }
}
```
* Reload NGINX `sudo nginx -s reload`
* Check everything is running as intended by running: `sudo systemctl status nginx`
  
You should get an output that looks something like this:

```shell
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2021-04-15 17:47:07 UTC; 19h ago
       Docs: man:nginx(8)
   Main PID: 2345 (nginx)
      Tasks: 5 (limit: 17996)
     Memory: 11.9M
     CGroup: /system.slice/nginx.service
             ├─2345 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             ├─7356 nginx: worker process
             ├─7357 nginx: worker process
             ├─7358 nginx: worker process
             └─7359 nginx: worker process

Apr 15 17:47:06 fhir-validator systemd[1]: Starting A high performance web server and a reverse proxy server...
Apr 15 17:47:07 fhir-validator systemd[1]: Started A high performance web server and a reverse proxy server.
``` 

### Troubleshooting
1. SSH into the compute engine VM, either through the [Google Cloud Console][Link-GoogleCloudConsole], or by installing the [Google Cloud SDK][Link-GoogleCloudSDK] on your local machine.
2. Navigate to your log directory `cd /var/log/nginx`
3. Tail the logs to see what's going on `tail -f *`

From these logs, you should be able to get a better idea of what is happening.

### Set-up Your DNS Entries

_At some point you should have bought the domains you intend to you for this website. In our case, we own both `fhirvalidator.com` and `fhirvalidator.org`, and we want them to both point to our docker image running on our compute engine instance on Google Cloud._

1. Set up a static IP address on your compute engine instance.
* In the [Google Cloud SDK][Link-GoogleCloudSDK], go to `VPC network` -> `External IP addresses`
* At the top of the page, select `RESERVE STATIC ADDRESS`
* Give the static address a name and description that makes sense, and then from the `Attached to` drop down menu, select the compute engine VM instance you want to attach this address to
2. View the list of Compute Engine VM instances, find the instance you just assigned the IP address to, and write down the value in the `External IP` column. This is the static address we will use in our DNS settings.
3. Log into your account on whatever domain name service provider your bought your domain names from. In our case, we chose [Dynadot][Link-Dynadot], because that's where I currently hoard all my other unused domain names _like an ancient dragon sleeping on a pile of gold he will never spend_.
4. Update your DNS settings for the chosen domain names
* On the domain name entry, modify your DNS settings
* Change the domain record to `Record Type: A`, and set the `IP Address or Target Host` to the static IP address you wrote down before
* If you have the option to set `Subdomain Records`, set the `Subdomain` to `www`, the `Record Type` to `A`, and the `IP Address or Target Host` to the static IP address you wrote down before

### Install and Configure Docker

1. SSH into the compute engine VM, either through the [Google Cloud Console][Link-GoogleCloudConsole], or by installing the [Google Cloud SDK][Link-GoogleCloudSDK] on your local machine.
2. Install Docker by running the following commands:
* `sudo apt update`
* `sudo apt upgrade`
* Install docker, `sudo apt-get install docker.io`
3. Configure your docker installation
* Set docker to start on system boot, `sudo systemctl enable --now docker`
* Add your user to the docker group, `sudo usermod -aG docker markiantorno`
4. Pull your docker image `docker pull <image name here>`
5. Start your docker image `docker run -d -p <port you want to expose>:<port you want to expose> <image name here>`
6. Execute `docker ps` to ensure your image is up. You should see something that looks like this:

```shell
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS              PORTS                    NAMES
e628fe9c7d62        markiantorno/validator-wrapper   "java -server -XX:+U…"   20 hours ago        Up 20 hours         0.0.0.0:3500->3500/tcp   jolly_engelbart
```

7. We verified our container starts and runs as expected, we need to now set an actual name, and make sure it comes up every time we restart the box.
* Stop the running container `docker stop jolly_engelbart`
* Start the container with a chosen name, and set it to restart on reboot, `docker run -d -p <port you want to expose>:<port you want to expose> --restart always --name <choose a name for the conatiner> <image name here>`
* Verify you image is running `docker ps`

### Configure SSL
This can be a complicated process. Luckily, there is a tool called certbot we can use to set up SSL.
1. Follow the install instructions [here][Link-CertBotInstallInstructions].
2. Verify your config file has been updated
* `cd /etc/nginx/sites-enabled/`
* Open the **default** file (in our example, we use vi to edit) `sudo vi default`
* You should see a bunch of additional settings added by certbot in this file. For the validator-wrapper, our file now looks like this:

```shell
server {
        #listen [::]:80 default_server;
        #root /var/www/html;
        #index index.html index.htm index.nginx-debian.html;
        server_name fhirvalidator.org www.fhirvalidator.org fhirvalidator.com www.fhirvalidator.com;
        location / {
                proxy_set_header Host $host;
                proxy_pass http://localhost:3500/;
                proxy_redirect off;
                access_log /var/log/nginx/validator.log;
        }
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/fhirvalidator.org/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/fhirvalidator.org/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
server {
    if ($host = www.fhirvalidator.org) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    if ($host = www.fhirvalidator.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    if ($host = fhirvalidator.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    if ($host = fhirvalidator.org) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
        listen 80 default_server;
        server_name fhirvalidator.org www.fhirvalidator.org fhirvalidator.com www.fhirvalidator.com;
    return 404; # managed by Certbot
}
```

### Setup docker-compose
Previously, we set up our docker instance to run with an exposed port, and restart every time the host machine reboots. This can also be done using [docker-compose][Link-DockerCompose].

1. In the root directory, create a file named `docker-compose.yml`
2. In this file, we want to define the image name, tell it to restart always, and set the exposed port. For example, here is the docker-compose.yml file we use in the validator-wrapper project:

```shell
version: '3'
services:
  validator:
    image: markiantorno/validator-wrapper
    restart: always
    ports:
      - 3500:3500
```

3. Compile your project, and publish the new docker image containing the docker-compose.yml file.
4. SSH into the compute engine VM, either through the [Google Cloud Console][Link-GoogleCloudConsole], or by installing the [Google Cloud SDK][Link-GoogleCloudSDK] on your local machine.
5. Install docker-compose `sudo apt install docker-compose`
6. Stop your currently running image.
   _Be mindful not to start images with both docker and docker-compose. If an image already exists and occupies the required port, a new image may start without obvious errors, but the old image will still be providing the website._
   * Execute `docker ps` to see the list of running images
   * From that list, find the name of your image, and stop it by running `docker stop <image name here>`
8. Start the image using docker-compose by running `docker-compose up --build -d`
9. Verify the image is running by executing `docker ps`

### Automating Updates
We don't want to have to _manually_ go in and type:
* `docker pull <image name>:latest`
* `docker-compose up --build -d`
  like a chump every time we want to update the server.
  _We can automate this process._

1. SSH into the compute engine VM, either through the [Google Cloud Console][Link-GoogleCloudConsole], or by installing the [Google Cloud SDK][Link-GoogleCloudSDK] on your local machine.
2. Create a bash script in the base directory of your compute engine vm containing the following:

```shell
#!/bin/bash
docker pull markiantorno/validator-wrapper:latest &&docker-compose up --build -d
```

3. Configure your CI/CD process to log in and run this command when you want a new image pulled and run. **Or**, if you cannot give access to your pipeline, setup a cron job on the compute engine instance to run the script every day at a set time to pull the latest version and update.

[Link-GoogleComputeEngine]: https://cloud.google.com/compute
[Link-GoogleCloudConsole]: https://console.cloud.google.com/
[Link-GoogleCloudSDK]: https://cloud.google.com/sdk
[Link-Dynadot]: https://www.dynadot.com/
[Link-CertBot]: https://certbot.eff.org/
[Link-CertBotInstallInstructions]: https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx
[Link-DockerCompose]: https://docs.docker.com/compose/