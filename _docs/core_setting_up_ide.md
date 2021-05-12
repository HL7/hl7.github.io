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
3. Out of the box, Eclipse has no idea what to with Kotlin, and we need to install a plugin to assist with our build. Please install the [plugin for Kotlin][Link-EclipseMarketplaceKotlin] from the Eclipse marketplace.
4. On some versions of Eclipse, the Kotlin plugin doesn't work on its own, and requires the AspectJ plugin to function. Please install the [plugin for AspectJ][Link-EclipseMarketplaceAspectJ] from the Eclipse marketplace.
5. Eclipse still does not recognize `src/main/kotlin` as a valid source directory. Right click on the modules that contain kotlin code (as of writing this, only the convertors module), select `build path` -> `configure build path`.
   In the properties window, select the source tab. Select `Add Folder`, then in the list of available source folders, ensure the `src/main/kotlin` folder is selected. Press `Apply`.
6. Still in the properties window, select the `Order and Export` tab. Ensure that the entry `org.hl7.fhir.convertors/src/main/kotlin` is above `org.hl7.fhir.convertors/src/main/java`. Use the `Up` and `Down` buttons to do this.
7. Press `Apply and Close`. Do not rebuild the project yet.
8. The versions of JDK that the Java and Kotlin code are using to compile might not be aligned, so we need to ensure that they are using the same version (in our case, 1.8).
* In the `Window` drop down menu, select `Preferences`.
* From the list on the left of the preferences window, select `Kotlin` -> `Compiler`.
* Set the `JVM target version` to `1.8`.
* Ensure the `Language version` and `API Version` are set to `1.4`.
* Set the `JDK Home` path to point to the location where you have installed Java 8 JDK on your system. If you do not have the Java 8 JDK installed, please follow the instructions [here][Link-OpenJDKInstall].
* Press `Apply`.
* From the list on the left of the preferences window, select `Java` -> `Compiler`
* Ensure the `Compiler compliance level` is set to `1.8`.
* Press `Apply and Close`. Do not rebuild the project yet.
9. In multi-module projects, we need to explicitly define the inter-module dependencies, so that Eclipse can build.
* Right click on the `org.hl7.fhir.validation` project and select `Properties`.
* In the properties window, select the `Projects` tab.
* Press the `Add` button.
* Select all other modules except `org.hl7.fhir.report` and `org.hl7.fhir.validation.cli`, and press `OK`
* Press `Apply and Close`. Do not rebuild the project yet.
10. We now just need to verify that `Kotlin Nature` is enabled on the appropriate modules.
* Right click on each of the modules in the library
* Under the `Configure Kotlin Nature` option, make sure it says `Remove Kotlin Nature`, and not `Add Kotlin Nature`. If it says `Add Kotlin Nature`, select it.

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
