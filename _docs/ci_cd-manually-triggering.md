---
title: "Manually Triggering a Pipeline"
permalink: /docs/ci-cd-manually-triggering
excerpt: "Manually Triggering a Pipeline"
last_modified_at: 2022-06-15
toc: true
---

For whatever reason, there may be times when a pipeline does not trigger as expected, or a pipeline needs to be manually started to verify a branch is in a good state. This is a straightforward process.

#### 1. Open the FHIR project page.
Navigate to the [FHIR Azure Pipelines Landing Page](https://dev.azure.com/fhir-pipelines/), and select the project containing the pipeline you with to trigger manually.

![Image tool tip](/assets/images/ci/FHIRPipelinesLandingPage.png)

#### 2. Open the Pipelines Page for that Project.
On the side menu, select the pipelines option from the Pipelines menu icon (it kinda looks like a spaceship)

![Image tool tip](/assets/images/ci/NavigatingToPipelines.png)

You should see a list of pipelines displayed here:
* **Pull Request Pipeline**
* **Master Branch Pipeline**
* **Release Branch Pipeline**

#### 3. Open the Run Pipeline Menu.
Select the three vertical dots on the right of the pipeline entry. From that drop down menu, select "Run pipeline".

![Image tool tip](/assets/images/ci/PipelineMenu.png)

#### 4. Select Branch and Run
Ensure that the correct Branch/tag is selected for the pipeline you wish to run. (_for our case, it will always be master_), and press "Run".

![Image tool tip](/assets/images/ci/SelectBranchAndRun.png)