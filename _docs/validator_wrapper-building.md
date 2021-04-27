---
title: "validator-wrapper"
permalink: /docs/validator-wrapper/building
excerpt: "How to locally build the validator-wrapper."
last_modified_at: 2021-04-27
toc: true
---

The validator-wrapper project contains the CLI, Desktop GUI, and Standalone Validation Server for the FHIR Validator. The tool can be run locally, or accessed online at the hosted [validator-wrapper website][Link-ValidatorWrapperWeb].

## Building Locally
This project uses the [gradle build tool][Link-GradleWebpage] to build. In particular, we take advantage of
[Gradle's Kotlin DSL][Link-GradleKotlinDSLPrimer] as an alternative syntax to the traditional Groovy DSL.

### Steps
To generate the jar containing all resources locally:
1. Ensure you have Gradle [installed on your system][Link-GradleInstall]
2. Generate the [Gradle Wrapper files][Link-GradleWrapper] locally by running the command `gradle wrapper --gradle-version=6.7`
3. Build the project by running the command `./gradlew build`
4. This will generate three jar files in the `/build/libs/` directory. The only one we care about is
   `validator-wrapper-jvm-{$project-version}.jar`


[Link-ValidatorWrapperWeb]: https://fhirvalidator.org
[Link-GradleWebpage]: https://gradle.org/
[Link-GradleKotlinDSLPrimer]: https://docs.gradle.org/current/userguide/kotlin_dsl.html
[Link-GradleInstall]: https://gradle.org/install/
[Link-GradleWrapper]: https://docs.gradle.org/current/userguide/gradle_wrapper.html
