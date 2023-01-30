---
title: "FHIR GitHub Branches"
permalink: /docs/fhir/github-branches/
excerpt: "How to contribute to FHIR using Github"
last_modified_at: 2021-04-26
toc: true
---

As far as git is concerned, master and R4B are just branches in the FHIR repository. Github layers functionality on top of git for features like pull requests to help with managing repositories.

## First time
Pull requests in Github can be done from a branch, or from a fork. The description below is for pull requests from a branch. As far as I know, forks are not used in the current process.

### Cloning the repo
Clone the repository - note that it will bring information about all branches. 

```shell
git clone https://github.com/HL7/fhir.git
```

**Note:** You can also clone the repository using ssh with the command `git clone git@github.com:HL7/fhir.git`.
{: .notice--info}

### Which branch?
When you first clone the repository, you are placed in the `master` branch. If you need to do work that will go in the `R4B` branch, you can switch to it using

```shell
git checkout R4B
```

Now, make sure you can successfully build the branch you are interested in, to confirm that your local setup is working.

**Note:** We recognize that labels such as `master` and `slave` are not appropriate branch naming conventions. We're in the process of updating our repositories and build pipelines to use more appropriate labels. We appreciate your patience during the transition.
{: .notice--primary}

## Local Development

Now that you have the repository cloned and running on your local machine, it's time to make your updates. However, we don't want to do this directly on the `master` or `R4B` branch, we will need to create our own local branch to work on. 

### Creating your local development branch
You can confirm that you are starting from the correct branch using the `git branch` command, which will list all local branches, and show you which the currently checked out branch is. At this point you can create you own branch:

```shell
git checkout -b myCoolBranch
```
You will be in the new branch, and ready to make your changes.

**Note:** `myCoolBranch` is just the example branch name we're using in the documentation. You can, _and should_ give your branch a more descriptive name, so that it's easy to determine what the purpose of that branch is.
{: .notice--info}

### Committing your changes locally
To view what files have changed locally, you can run the `git status` command. This will list all files within the project that have been modified, and not committed.

Once you're ready to add your changes to the local branch, you can run the `git add .` command. This lets git know that these changes are ready to be committed to the local branch.

Once added, subsequent changes can be committed with a single command:

```shell
git commit -am "helpful message"
```

## Pushing your changes to the remote repository
Right now, you've committed your changes to the current working branch. This means that they are only saved locally, and still need to be pushed to the remote repository for everyone to see your branch. There are a few things we need to do before that can happen though...

### Re-sync with original branch
Due to the nature or open source, many people could be working on `R4B` or `master` while we've been doing our work locally. We need to make sure that our branch is up-to-date with any changes that might have occurred while we were working on our branch.

The following commands will make sure any changes to `R4B` (or `master`) since the last time you pulled them from Github are accounted for:

```shell
git checkout R4B
git pull origin R4B
git checkout myCoolBranch
```

If there were changes to R4B (or master), you must merge them to your branch (make sure that you are in your development branch, in this example `myCoolBranch`):

```shell
git merge --no-ff R4B
```

The `--no-ff` flag is optional, it preserves individual commits.

Now that we have the latest changes merged into our local branch, we need to test one final time if we can still build. This will maximize the chances that the changes are going to be successfully merged in the end.

## Push your branch

Once merged and built locally, we can push our branch to the remote repository:

```shell
git push origin myCoolBranch
```

Now, if you got to Github you will see your branch, and you can create the pull request.
