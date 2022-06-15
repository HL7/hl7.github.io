---
title: "Setting up your IDE to build org.hl7.fhir.core"
permalink: /docs/core/ide
excerpt: "How to set up your local IDE to build the core."
last_modified_at: 2021-04-27
toc: true
---

The [core][Link-GithubCoreProject] uses a variety of tools and plugins during its build process. This sometimes requires users to make changes to their IDE so that they can compile.

## Prerequisites

You should have the core project cloned locally using git.

```shell
git clone https://github.com/hapifhir/org.hl7.fhir.core.git
```

## Eclipse Users

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].
2. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes. As we move to more using more Kotlin, this will be removed. 
   However, for now, the plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up.
3. Run eclipse and select your Eclipse workspace.
4. Follow these steps to import the cloned project:
   * From the main menu, select `File -> Import...`
   * Select `Maven -> Existing Maven Projects`
   * Click `Next`
   * Under `Select Root Directory`, pick the `org.hl7.fhir.core` directory (the root of the project)
   * Click Finish
5. If you are prompted to install the `m2e-connector plugin`, you should do so.

This should import the project, and you should be able to build and run of test in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`. 
In the Clean window, select the `Clean all projects` option, and the `Start a build immediately` and `Build the entire workspace` options as well. Press `Clean` to run a full build.

## IntelliJ Users

1. Ensure you have the latest version of Intellij IDEA Community Edition installed. Check the current version on their [downloads page][Link-IntelliJIdeaDownload].
2. Ensure you have the Java 8 JDK installed on your system, and your JAVA_HOME environment variable pointed to the Java 8 SDK.
   If you do not have the Java 8 JDK installed, please follow the instructions [here][Link-OpenJDKInstall].
3. You will need to install the lombok plugin. Follow the instructions [here][Link-InstallLombokIntelliJ].
4. Follow these steps to import the cloned project:
   * From the main menu, select `File -> Open...`
   * In the browser dialog pick the `org.hl7.fhir.core` directory (the root of the project)
   * If prompted whether to `Trust and Open Project 'org.hl7.fhir.core'` select `Trust Project`
   * Select which window you would like to open the project in.

This should enable the building and running of tests in IntelliJ. To verify, in the `Maven` side panel, right click on  `HL7 Core Artifacts -> Lifecycle -> clean` and select `Run Maven Build` from the context menu.

## Apache NetBeans Users

1. Follow the steps in the Intellij Users section above.

[Link-GithubCoreProject]: https://github.com/hapifhir/org.hl7.fhir.core
[Link-EclipseDownload]: https://www.eclipse.org/downloads/
[Link-ProjectLombok]: https://projectlombok.org/
[Link-InstallLombokEclipse]: https://projectlombok.org/setup/eclipse
[Link-EclipseMarketplaceKotlin]: https://marketplace.eclipse.org/content/kotlin-plugin-eclipse
[Link-EclipseMarketplaceAspectJ]: https://marketplace.eclipse.org/content/aspectj-development-tools
[Link-OpenJDKInstall]: https://openjdk.java.net/install/
[Link-IntelliJIdeaDownload]: https://www.jetbrains.com/idea/download/
[Link-InstallLombokIntelliJ]: https://projectlombok.org/setup/intellij
