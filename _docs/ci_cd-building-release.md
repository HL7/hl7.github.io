---
title: "Building CI/CD Releases"
permalink: /docs/ci-cd-building-release
excerpt: "Building CI/CD Releases"
last_modified_at: 2022-06-15
toc: true
---

## Building a Release

#### 1. Ensure the RELEASE_NOTES.md file is updated with the up-to-date release notes for the upcoming release.
This file is in the base directory of the project, and will look something like this:
![Image tool tip](/assets/images/ci/ReleaseNotesExample.png)

It is important to ensure this file is up to date, as the release notes are generated directly from this file. Additionally, some of the [Zulip](https://chat.fhir.org/#) notifications regarding the release are formatted to include these notes.

#### 2. Trigger the release pipeline.
* Navigate to the [FHIR Azure Pipelines Landing Page](https://dev.azure.com/fhir-pipelines/), and select the project your are releasing.
  ![Image tool tip](/assets/images/ci/FHIRPipelinesLandingPage.png)

* On the side menu, select the pipelines option from the Pipelines menu icon (it kinda looks like a spaceship)
  ![Image tool tip](/assets/images/ci/NavigatingToPipelines.png)
* You should see a list of pipelines displayed here:
    * **Pull Request Pipeline**
    * **Master Branch Pipeline**
    * **Release Branch Pipeline**
* Select the `Release Branch Pipeline`, and then [manually trigger a build](/docs/ci-cd-manually-triggering).



