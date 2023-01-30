## IntelliJ Users

1. Ensure you have the latest version of Intellij IDEA Community Edition installed. Check the current version on their [downloads page][Link-IntelliJIdeaDownload].{% if include.project-is-lombok != "false" %}
1. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes. You will need to install the lombok plugin. Follow the instructions [here][Link-InstallLombokIntelliJ].{% endif %}
1. Follow these steps to import the cloned project:
   * From the main menu, select `File -> Open...`
   * In the browser dialog pick the `{{ include.project-directory }}` directory (the root of the project)
   * If prompted whether to `Trust and Open Project '{{ include.project-name }}'` select `Trust Project`
   * Select which window you would like to open the project in.

This should enable the building and running of tests in IntelliJ. To verify, in the `Maven` side panel, right click on  `HL7 Core Artifacts -> Lifecycle -> clean` and select `Run Maven Build` from the context menu.

## Apache NetBeans Users

1. Follow the steps in the Intellij Users section above.

[Link-IntelliJIdeaDownload]: https://www.jetbrains.com/idea/download/
[Link-ProjectLombok]: https://projectlombok.org/
[Link-InstallLombokIntelliJ]: https://projectlombok.org/setup/intellij