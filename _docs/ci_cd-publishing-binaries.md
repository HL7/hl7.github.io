---
title: "Publishing Release Binaries"
permalink: /docs/ci-cd-publishing-binaries
excerpt: "Publishing Release Binaries"
last_modified_at: 2022-06-15
toc: true
---

FHIR libraries rely on [Azure Pipelines](https://dev.azure.com/fhir-pipelines/) for both SNAPSHOT and release deployments. These are automated, and all releases should be done via these pipelines, not locally.

Built binaries are hosted on [OSSRH](https://oss.sonatype.org/).

### Publishing Locally:
To test your changes locally before pushing to the remote repo, you can publish locally. As with most maven projects, running `mvn install` from the root directory will install the built SNAPSHOT version in your local `~/.m2/repository` directory.

### How SNAPSHOT Builds are Generated:
All successful merges and pushes to `master` branch result in a SNAPSHOT build being published to [OSSRH](https://oss.sonatype.org/). SNAPSHOT version is determined by the artifact `version` specified in the base directory `pom.xml` file. The following `pom.xml` file will generate version `1.1.15-SNAPSHOT`:
```xml
    <groupId>org.hl7.fhir.testcases</groupId>
    <artifactId>fhir-test-cases</artifactId>
    <version>1.1.15-SNAPSHOT</version>
    <packaging>jar</packaging>
```

### Publishing Release Builds:
Releases are triggered through Azure pipelines from the master branch. All release pipeline runs result in a release build being published to [OSSRH](https://oss.sonatype.org/). The release version is derived from the current `version` in the base directory `pom.xml` file. This value will then be incremented by the deployment pipeline. For example, if a release is published with the following `pom.xml`:

```xml
    <groupId>org.hl7.fhir.testcases</groupId>
    <artifactId>fhir-test-cases</artifactId>
    <version>1.1.15-SNAPSHOT</version>
    <packaging>jar</packaging>
```

The deployment pipeline will release version `1.1.15` to maven, as a non-SNAPSHOT release, then increment the version number to `1.1.16-SNAPSHOT` and commit the new pom.xml changes to master.

This release is tagged and pushed to GitHub, and the release notes are pulled from the `RELEASE_NOTES.md` file in the base directory of the project. This file is then automatically cleared and committed by Azure after each release.

For more details on creating releases, please see the [detailed release instructions](/docs/ci-cd-building-release).