## Eclipse Users

1. Ensure you have the latest version of Eclipse installed. Check the current version on their [downloads page][Link-EclipseDownload].
2. This project uses [lombok][Link-ProjectLombok] annotations to help reduce lines of code in some of the larger classes.
   This plugin needs to be manually added to Eclipse. Please follow the [instructions on their website][Link-InstallLombokEclipse] to set this up.
3. Run eclipse and select your Eclipse workspace.
4. Follow these steps to import the cloned project:
    * From the main menu, select `File -> Import...`
    * Select `Maven -> Existing Maven Projects`
    * Click `Next`
    * Under `Select Root Directory`, pick the `{{ include.project-name }}` directory (the root of the project)
    * Click Finish
5. If you are prompted to install the `m2e-connector plugin`, you should do so.

This should import the project, and you should be able to build and run of test in the Eclipse IDE. To verify, in the `Project` drop-down menu, select `Clean...`.
In the Clean window, select the `Clean all projects` option, and the `Start a build immediately` and `Build the entire workspace` options as well. Press `Clean` to run a full build.

[Link-ProjectLombok]: https://projectlombok.org/
[Link-EclipseDownload]: https://www.eclipse.org/downloads/
[Link-InstallLombokEclipse]: https://projectlombok.org/setup/eclipse