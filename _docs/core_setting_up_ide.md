---
title: "Setting up your IDE to build org.hl7.fhir.core"
permalink: /docs/core/ide
excerpt: "How to set up your local IDE to build the core."
last_modified_at: 2021-04-27
toc: true
---

The [core][Link-GithubCoreProject] uses a variety of tools and plugins during its build process. This sometimes requires users to make changes to their IDE so that they can compile.

## Eclipse Users

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].
2. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes. As we move to more using more Kotlin, this will be removed. 
   However, for now, the plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up.

This should enable building and running of tests in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`. 
In the Clean window, select the `Clean all projects` option, and the `Start a build immediately` and `Build the entire workspace` options as well. Press `Clean` to run a full build.

## IntelliJ Users

1. Ensure you have the latest version of Intellij IDEA Community Edition installed. Check the current version on their [downloads page][Link-IntelliJIdeaDownload].
2. Ensure you have the Java 8 JDK installed on your system, and your JAVA_HOME environment variable pointed to the Java 8 SDK.
   If you do not have the Java 8 JDK installed, please follow the instructions [here][Link-OpenJDKInstall].
3. You will need to install the lombok plugin. Follow the instructions [here][Link-InstallLombokIntelliJ].

This should enable the building and running of tests in IntelliJ.

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
