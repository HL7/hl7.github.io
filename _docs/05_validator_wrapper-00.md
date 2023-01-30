---
title: "validator-wrapper"
permalink: /docs/validator-wrapper
excerpt: "The validator-wrapper project."
last_modified_at: 2021-04-27
toc: true
---

This project contains the CLI, Desktop GUI, and Standalone Validation Server for the FHIR Validator.

## About the Project

The code for this project is located in the [hapifhir][Link-GithubRepo] organization.

The validator CLI will still be generated and hosted as normal within the [hapifhir/core.hl7.fhir.core][Link-CoreGithubLatestRelease]
_for now_. Be advised that, eventually, we will stop publishing the cli as part of the core, and users will be expected to download the cli jar from the [latest release][Link-ValidatorWrapperGithubLatestRelease] of this project.
{: .notice--info}

### Build Status

| CI Status (master) | Website Docker Image |
| ------------------ | -------------------- |
| [![Build Status][Badge-BuildPipelineMaster]][Link-BuildPipelineMaster] | [![Docker Status][Badge-DockerHub]][Link-DockerHub] |

**Warning:** This project is still not yet "officially" released, and may contain errors/bugs/dragons/smooth-jazz. During this initial
period, your patience is __greatly appreciated__.
{: .notice--danger}

### CI/CD
All integration and delivery done on Azure pipelines. Azure project can be viewed [here][Link-AzureProject].

### Docker
Docker image for the fullstack website is stored [on DockerHub][Link-DockerHub], and can be downloaded and run locally.

Updates to the docker image are triggered through the Azure Pipelines CI/CD.

### Bugs and Issues

Have you found an issue not listed above? Do you have a feature request? Great! 
Submit it [here][Link-GitHubIssues] and we'll try to fix it as soon as possible.

[Link-GithubRepo]: https://github.com/hapifhir/org.hl7.fhir.validator-wrapper
[Link-AzureProject]: https://dev.azure.com/fhir-pipelines/validator-wrapper
[Link-BuildPipelineMaster]: https://dev.azure.com/fhir-pipelines/validator-wrapper/_build/latest?definitionId=38&branchName=master
[Link-DockerHub]: https://hub.docker.com/repository/docker/markiantorno/validator-wrapper/general
[Link-CoreGithubLatestRelease]: https://github.com/hapifhir/org.hl7.fhir.core/releases/latest
[Link-ValidatorWrapperGithubLatestRelease]: https://github.com/hapifhir/org.hl7.fhir.validator-wrapper/releases/latest
[Link-GitHubIssues]: https://github.com/hapifhir/org.hl7.fhir.validator-wrapper/issues

[Badge-BuildPipelineMaster]: https://dev.azure.com/fhir-pipelines/validator-wrapper/_apis/build/status/Master%20Branch%20Pipeline?branchName=master
[Badge-DockerHub]: https://img.shields.io/docker/v/markiantorno/validator-wrapper