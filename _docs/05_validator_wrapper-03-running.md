---
title: "validator-wrapper"
permalink: /docs/validator-wrapper/running
excerpt: "How to locally run the validator-wrapper."
last_modified_at: 2025-08-26
toc: true
---
## Running Locally
There are three possible ways this jar can be utilized:

### As a full-stack hosted server:
Execute the jar by providing the argument `'-startServer'`. This boots the Ktor validation back end and KotlinJS
front-end. Refer to the `jvmMain/resources/application.conf` file in the resources directory to view the different deployment flavours available.
These deployment types can be set through the environment variable `ENVIRONMENT`. If no such environment variable is
set, the application will default to a `dev` type deployment.

### As a locally run, short-lived, desktop application:
Execute the jar by providing the argument `'-gui'`. This boots the Ktor server locally on the port 8080, and starts a
wrapped instance of the KotlinJS front end within a Chromium web window to appear as a desktop application. This
wrapped website should mimic all the same functionality of the full KotlinJS website in the full-stack hosted server.
Once the Chromium browser window is closed, the local Ktor server is also shutdown.

**Note:** If you attempt to run this as both a full-stack server and a locally hosted application (by including both the
`startServer` and `-gui` commands from the cli), the full-stack server takes priority, and the desktop version will
not be booted.
{: .notice--warning}


[Link-ValidatorWrapperWeb]: https://validator.fhir.org/
[Link-GradleWebpage]: https://gradle.org/
[Link-GradleKotlinDSLPrimer]: https://docs.gradle.org/current/userguide/kotlin_dsl.html
[Link-GradleInstall]: https://gradle.org/install/
[Link-GradleWrapper]: https://docs.gradle.org/current/userguide/gradle_wrapper.html
[Link-ValidatorConfluence]: https://confluence.hl7.org/display/FHIR/Using+the+FHIR+Validator