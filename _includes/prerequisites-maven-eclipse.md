## Eclipse Users

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].{% if include.project-is-lombok != "false" %} 
1. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes.
   This plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up. {% endif %}
1. Run eclipse and select your Eclipse workspace.
1. Follow these steps to import the cloned project:
    * From the main menu, select `File -> Import...`
    * Select `Maven -> Existing Maven Projects`
    * Click `Next`
    * Under `Select Root Directory`, pick the `{{ include.project-directory }}` directory (the root of the project)
    * Click Finish
1. If you are prompted to install the `m2e-connector plugin`, or the `maven-checkstyle-plugin plugin connector`, you should do so, and approve any necessary and valid code signings. You may be asked to restart Eclipse at this point, and you should do so.


This should import the project, and you should be able to build and run of test in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`.
In the Clean window, select the `Clean all projects` option, and the `Start a build immediately` and `Build the entire workspace` options as well. Press `Clean` to run a full build.

[Link-EclipseDownload]: https://www.eclipse.org/downloads/
[Link-ProjectLombok]: https://projectlombok.org/
[Link-InstallLombokEclipse]: https://projectlombok.org/setup/eclipse