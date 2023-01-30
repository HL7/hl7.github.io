## Eclipse Users

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].{% if include.project-is-lombok != "false" %} 
1. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes.
   This plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up. {% endif %}
1. Run eclipse and select your Eclipse workspace.
1. Follow these steps to import the cloned project:
    * From the main menu, select `File -> Import...`
    * Select `Gradle -> Existing Gradle Project`
    * Click `Next`
    * Under `Project Root Directory`, pick the `{{ include.project-directory }}` directory (the root of the project)
    * Leave all settings as default when prompted. Eclipse should automatically elect to use the gradle wrapper, which will provide the easiest development experience. 
    * Click Finish

This should import the project, and you should be able to build and run of test in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`.
In the Clean window, select the {{ include.project-name }} project. Press `Clean` to run a full build.

[Link-ProjectLombok]: https://projectlombok.org/
[Link-EclipseDownload]: https://www.eclipse.org/downloads/
[Link-InstallLombokEclipse]: https://projectlombok.org/setup/eclipse