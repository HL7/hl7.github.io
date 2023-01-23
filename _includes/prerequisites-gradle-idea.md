## IntelliJ Users

1. Ensure you have the latest version of Intellij IDEA Community Edition installed. Check the current version on their [downloads page][Link-IntelliJIdeaDownload].
2. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes. 
   You will need to install the lombok plugin. Follow the instructions [here][Link-InstallLombokIntelliJ].
3. Follow these steps to import the cloned project:
   * From the main menu, select `File -> Open...`
   * In the browser dialog pick the `{{ include.project-directory }}` directory (the root of the project)
   * If prompted whether to `Trust and Open Project '{{ include.project-directory }}'` select `Trust Project`
   * Select which window you would like to open the project in.

When the project first loads, it will attempt an initial build, and may take several minutes to complete. Once complete, the project should allow the building and running of tests in IntelliJ. To verify, in the `Gradle` side panel, right click on  `{{ include.project-name }} -> Tasks -> build -> build` and double click to initiate another build.

## Apache NetBeans Users

1. Follow the steps in the Intellij Users section above.

[Link-ProjectLombok]: https://projectlombok.org/
[Link-IntelliJIdeaDownload]: https://www.jetbrains.com/idea/download/
[Link-InstallLombokIntelliJ]: https://projectlombok.org/setup/intellij