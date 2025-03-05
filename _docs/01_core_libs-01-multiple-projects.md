---
title: "Working with multiple core projects"
permalink: /docs/core-libs/multiple-projects
excerpt: "Working with multiple core libraries."
last_modified_at: 2023-01-30
toc: true
---

Though individual projects in the HL7 core libraries can be worked on independently, certain projects are dependent on others, and it may be necessary to do development work with several projects at the same time. To see which projects depend on each other, read the [Overview of the HL7 Core Projects](/docs/core-libs/overview).

## Multiple Projects in IntelliJ IDEA

### Prerequisites

1. Ensure you have the latest version of Intellij IDEA Community Edition installed. Check the current version on their [downloads page][Link-IntelliJIdeaDownload].
2. Ensure you have the necessary version of Java to build each project. Check individual project documentation for details on the Java version and any other necessary software required to build.
3. Some projects use [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes. For these, you will need to install the lombok plugin. Follow the instructions [here][Link-InstallLombokIntelliJ].


### Creating a multi-project workspace
To load multiple projects in IntelliJ IDEA, you can use a single parent directory to contain multiple projects. To illustrate how this is done, we will use the example of loading, both the [org.hl7.fhir.core](/docs/core/ide) project and the [kindling]() project in the same workspace.

To begin, we will create a parent directory called `fhir-projects` and use git to clone both projects.

```shell
$ mkdir fhir-projects
$ cd fhir-projects
$ git clone https://github.com/hapifhir/org.hl7.fhir.core.git
$ git clone https://github.com/HL7/fhir.git
```

This gives us a directory that looks like the following:

```
 fhir-projects
 ├ fhir	
 └ org.hl7.fhir.core
```

You can add other projects to the fhir-projects directory at any time, but be aware that  IntelliJ IDEA processes like file indexing will take longer the more projects are loaded.

### Loading a multi-project workspace in IntelliJ IDEA

To load both these projects in IntelliJ, follow these steps:

- From File menu select File -> Open... and use the dialog to select the `fhir-projects` directory. 
- If prompted to `Trust and Open Project` select `Trust Project`
- Select which window you would like to open the project in.

You should now see both your projects in the `Project Files` panel. Though these projects  and their files will be visible, they will not be indexed for IDE work, and they will not be automatically built. You must import these projects following the relevant steps below.



### Importing multiple projects

Projects must be added or linked depending on the project build system used for each project. `org.hl7.fhir.core` is a Maven project, and `kindling` is a Gradle project. The `README.md` file in each project directory will describe the build system used. 


#### Maven Projects

To add a Maven project such as `org.hl7.fhir.core` in IntelliJ IDEA, use following steps:

- Using the `Project Files` panel, find the `pom.xml` file at the root of the project.
- Right click on the `pom.xml` file and select `+ Add as Maven Project` from the context menu.

A `Maven` panel will become available in your IDEA workspace. It may not expand by default, but can normally be found on the right hand side of your workspace. In it, you will see a list of all available modules, with `Lifecycle`, `Plugins`, and `Dependencies` sub-headings in each. You will now be able to use standard maven commands like `install`. 

For details about building and using different features of each project, read the project documentation.

#### Gradle Projects

To link a Gradle project such as `fhir` in IDEA, use the following steps:

- Using the `Project Files` panel, find the `build.gradle.kts` file at the root of the project.
- Right click on the `build.gradle.kts` file and select `Link Gradle Project` from the context menu.

A `Gradle` panel will become available in your IDEA workspace. It may not expand by default, but can normally be found on the right hand side of your workspace. In it, you will see a list of all available Gradle projects. The first time you link a project it may take some time to fully load. Once a project is loaded, you will see sub-headings for `Tasks` and `Dependencies`, and will be able to use standard Gradle commands like `build`.

For details about building and using different features of each project, read the project documentation.

### Important IDEA Tips

#### Managing dependencies

Working with projects that are dependent upon each other can often be frustrating. To minimize this, the following steps can be used verify that the code you are working on is in fact being used by projects dependent on it.

- Ensure that you are working with a consistent SNAPSHOT version of each project in your workspace. For example, if you are working with version `5.6.93-SNAPSHOT` of the `org.hl7.fhir.core` project, you should ensure that dependent projects such as `kindling`, `fhir-publisher`, etc. are all using this version.
- Ensure that you have built and installed projects that other projects may be dependent upon. This can be done using the command line, or by using the `Maven` and `Gradle` panels in IDEA.
   - Maven: `mvn install`
- Ensure that dependent Maven projects are being built with the most recent dependencies.
  - Find your project in the `Maven` panel.
  - Right click on your project and select `Reload Project` from the context menu.
  - Alternatively, in the terminal you can build with the following options: `mvn clean install -U`
- Ensure that dependent Gradle projects are being built with the most recent dependencies.
   - Find your project in the `Gradle` panel.
   - Right click on your project and select `Refresh Gradle Dependencies` from the context menu.
   - Alternatively, in the terminal you can build with the following options: `gradlew build --refresh-dependencies`

[Link-IntelliJIdeaDownload]: https://www.jetbrains.com/idea/download/
[Link-ProjectLombok]: https://projectlombok.org/
[Link-InstallLombokIntelliJ]: https://projectlombok.org/setup/intellij

## Multiple Projects in IBM Eclipse

### Prerequisites

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].
2. Ensure you have the necessary version of Java to build each project. Check individual project documentation for details on the Java version and any other necessary software required to build.
3. Some projects use [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes.
   This plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up.

### Loading Multiple Projects in Eclipse

To illustrate how this is done, we will use the example of loading, both the [org.hl7.fhir.core](/docs/core/ide) project and the [kindling]() project in the same workspace.

To begin, we will clone these two projects using Git.

```shell
$ git clone https://github.com/hapifhir/org.hl7.fhir.core.git
$ git clone https://github.com/HL7/fhir.git
```

Once these projects are cloned, you will be able to import them into Eclipse.

Run eclipse and select your Eclipse workspace.

Projects must be imported in a different way depending on the project build system used for each project. `org.hl7.fhir.core` is a Maven project, and `kindling` is a Gradle project. The `README.md` file in each project directory will describe the build system used.

#### Maven Projects

Follow these steps to import the cloned project:
  * From the main menu, select `File -> Import...`
  * Select `Maven -> Existing Maven Projects`
  * Click `Next`
  * Under `Select Root Directory`, pick the `{{ include.project-name }}` directory (the root of the project)
  * Click Finish 

If you are prompted to install the `m2e-connector plugin`, or the `maven-checkstyle-plugin plugin connector`, you should do so, and approve any necessary and valid code signings. You may be asked to restart Eclipse at this point, and you should do so.

#### Gradle Projects

Follow these steps to import the cloned project:
* From the main menu, select `File -> Import...`
* Select `Gradle -> Existing Gradle Project`
* Click `Next`
* Under `Project Root Directory`, pick the project directory (the root of the project)
* Leave all settings as default when prompted. Eclipse should automatically elect to use the gradle wrapper, which will provide the easiest development experience.
* Click Finish

This should import the project, and you should be able to build and run of test in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`.
In the Clean window, select the project. Press `Clean` to run a full build.

### Important Eclipse Tips

#### Required Projects

In Eclipse some projects require that their dependencies are also loaded into the Eclipse workspace. If a project has a red `!` symbol attached to it in the `Package Explorer` panel, this may be one of the causes. If this is the case, the `Problems` panel will include errors such as the following:

```
Project 'kindling' is missing required Java project: 'org.hl7.fhir.convertors'	kindling
```

To resolve this issue, find the project that is required and import it. In this case `org.hl7.fhir.core` contains the `org.hl7.fhir.convertors` modules, so `org.hl7.fhir.core` should be imported).

#### Managing dependencies

Working with projects that are dependent upon each other can often be frustrating. To minimize this, the following steps can be used verify that the code you are working on is in fact being used by projects dependent on it.

- Ensure that you are working with a consistent SNAPSHOT version of each project in your workspace. For example, if you are working with version `5.6.93-SNAPSHOT` of the `org.hl7.fhir.core` project, you should ensure that dependent projects such as `kindling`, `fhir-publisher`, etc. are all using this version.
- Ensure that you have built and installed projects that other projects may be dependent upon. This can be done using the command line, or in Eclipse by using the `Build` menu for Maven projects or `Gradle Tasks` panel for Gradle projects.
  - Maven: `mvn install` or `Build -> Build Project` (if `Build Automatically` isn't selected)
- Ensure that dependent Maven projects are being built with the most recent dependencies.
  - Find your project in the `Package Explorer` panel.
  - Right click on your project and select `Maven -> Update Project` from the context menu.
  - Alternatively, in the terminal you can build with the following options: `mvn clean install -U`
- Ensure that dependent Gradle projects are being built with the most recent dependencies.
  - Find your project in the `Package Explorer` panel.
  - Right click on your project and select `Gradle -> Refresh Gradle Project` from the context menu.
  - Alternatively, in the terminal you can build with the following options: `gradlew build --refresh-dependencies`

[Link-EclipseDownload]: https://www.eclipse.org/downloads/
[Link-ProjectLombok]: https://projectlombok.org/
[Link-InstallLombokEclipse]: https://projectlombok.org/setup/eclipse