---
title: "Publishing Templates"
permalink: /docs/publishing_templates/
excerpt: "How to publish templates using the IG-Publisher."
last_modified_at: 2021-06-23
toc: true
---
## Background
Implementation guides require templates to build. When you build an ig implementation guide, one of the three parameters
you provide is the id of the template to use. In general, the template ID generally points to one of 
[these templates][Link-GithubTemplatesDirectory].

During publishing of your IG, when you define which template you want to use, you can specify a version. This version can
be either one of the release versions, or current. It is important to understand the distinction between the two. 
**Current** is the latest mutable CI build. If you label the IG as current it grabs the latest package off of 
[build.fhir.org][Link-BuildFhirOrg]. Otherwise, if you can specify one of the built versions in the 
[template directory][Link-GithubTemplatesDirectory]. If you don’t specify a specific version, you will get the latest,
immutable, published version.

## Moving Parts

### package templates

The templates used for publishing are located in the [templates directory][Link-GithubTemplatesDirectory] in the 
[web source][Link-GithubWebSource] repository on GitHub. If you look in the [templates directory][Link-GithubTemplatesDirectory],
you're going to see a bunch of different built templates, each with their own sub-directory:
```
- hl7.au.base.template
- hl7.au.fhir.template
- hl7.base.template
- hl7.cda.template
- hl7.fhir.template
- hl7.utg.template
- ihe.fhir.template
- fhir.base.template
```
Each of these directories contains a list of published versions, each with their own sub-directory. For example, if we
look in [fhir.base.template][Link-GithubFhirBaseTemplateDir], you should see a list of directories for the published
versions, including `0.0.2`, `0.1.0`, `0.1.1`, and so on. These directories contain the [Jekyll][Link-Jekyll] html file,
in addition to any necessary templates and assests used to build the pages required by the implementation guides.

### template entry list

Similar to packages, templates also use a `package-list.json` file to manage release versioning. An example of this 
would be the [package-list.json][Link-GithubPackageListJsonHl7Fhir] file for the `hl7.fhir.template` project.

Each of the entries in the list of released packages contains information like the `version`, `desc`, `date`, and others.
The key difference here between package publishing and template publishing is that there are two entries labelled 
`current`. The actual current CI build, and the current release.

Looking at our [example we mentioned above][Link-GithubPackageListJsonHl7Fhir], the first two entries in the 
`package-list.json` are:
```json
    {
      "version": "current",
      "desc": "Continuous Integration Build (latest in version control)",
      "path": "https://build.fhir.org/ig/HL7/ig-template-fhir",
      "status": "ci-build",
      "current": true
    },
    {
      "version": "0.3.2",
      "desc": "Fix search link",
      "path": "http://fhir.org/templates/hl7.fhir.template/0.3.2",
      "status": "release",
      "sequence": "Publications",
      "current": true,
      "date": "2020-09-29"
    },
```
You will never need to touch that top entry during the publication process, only the bottom one. When publishing a new
template, you would just need to add a new 2nd entry that is labelled `current: true`, and then take away the 
`current: true` from the 0.3.2 entry (in this example).

### template releaser tool

In the [IG Publisher][Link-GithubIgPublisherRepo] repository, there is a tool that does the necessary change analysis
and publishes the resulting templated for us. It is called the [TemplateReleaser][Link-GithubTemplateReleaser].

This tool takes in two arguments, a _source_ and a _destination_. The _source_ is the local path on your computer, to
a directory that contains all the cloned template directories from the [templates][Link-GithubTemplatesDirectory] in 
the [web source][Link-GithubWebSource] project **and nothing else**. You need to copy these directories into their own 
folder on your computer, such that you get a folder structure that looks like this:
```
C:\work\org.hl7.fhir\templates\hl7.au.base.template
C:\work\org.hl7.fhir\templates\hl7.au.fhir.template
C:\work\org.hl7.fhir\templates\hl7.base.template
C:\work\org.hl7.fhir\templates\hl7.cda.template
C:\work\org.hl7.fhir\templates\hl7.fhir.template
C:\work\org.hl7.fhir\templates\hl7.utg.template
C:\work\org.hl7.fhir\templates\ihe.fhir.template
C:\work\org.hl7.fhir\templates\fhir.base.template
```
The _destination_ is the local path on your computer, to the cloned 
[packages directory][Link-GithubWebSourcePackagesDirectory] in the [web source][Link-GithubWebSource] project.

### inter-template dependencies
One important thing to note about the template publication process is that the templates can have dependency 
relationships between them...unlike the packages. Some templates depend on other templates, so if you make a change to 
a template that other templates depend on, it does a cascading release. This is all done automatically by the code, and 
will generate any output directories.

## Publishing and Uploading a Release

At some point, someone will contact you to let you know that changes have been made to the packages, and a new release
needs to be cut and published. When this happens, do the following:

1. Clone the [IG Publisher][Link-GithubIgPublisherRepo], and the [web-source][Link-GithubWebSource], and ensure they
   are up to date.
2. Update the appropriate `package-list.json` file entry list with the new entry for that template release.
3. Run the [TemplateReleaser][Link-GithubTemplateReleaser] with the in _source_ defined as the local
   directory that contains all the up-to-date, cloned template directories from the 
   [templates][Link-GithubTemplatesDirectory], and the out _destination_ pointing
   to the locally cloned [packages directory][Link-GithubWebSourcePackagesDirectory] in the [web source][Link-GithubWebSource] 
   project.
4. In the web-source project, run the [run-jekyll.bat][Link-GithubJekyllFile] script to generate the new Jekyll website.
   This will generate the `output` folder in the source directory.
5. sftp the contents of the generated `output` folder to the `/var/www/html/` directory on `fhir.org`. You will need
   the proper credentials to do this. Currently, this is done by either [Grahame][Link-grahameGithub] or
   [Mark][Link-markGithub], so please contact them to get this done.


[Link-GithubWebSource]: https://github.com/FHIR/web-source
[Link-GithubIgPublisherRepo]: https://github.com/HL7/fhir-ig-publisher

[Link-GithubJekyllFile]: https://github.com/FHIR/web-source/blob/master/run-jekyll.bat
[Link-GithubFhirBaseTemplateDir]: https://github.com/FHIR/web-source/tree/master/source/templates/fhir.base.template
[Link-GithubTemplatesDirectory]: https://github.com/FHIR/web-source/tree/master/source/templates
[Link-GithubWebSourcePackagesDirectory]: https://github.com/FHIR/web-source/tree/master/source/packages
[Link-GithubPackageListJsonHl7Fhir]: https://github.com/FHIR/web-source/blob/master/source/templates/hl7.fhir.template/package-list.json
[Link-GithubTemplateReleaser]: https://github.com/HL7/fhir-ig-publisher/blob/master/org.hl7.fhir.publisher.core/src/main/java/org/hl7/fhir/igtools/publisher/utils/TemplateReleaser.java

[Link-FhirDotOrg]: www.fhir.org
[Link-BuildFhirOrg]: www.build.fhir.org
[Link-FhirDotOrgRegistry]: http://fhir.org/guides/registry/
[Link-Jekyll]: https://jekyllrb.com/

[Link-grahameGithub]: https://github.com/grahamegrieve
[Link-markGithub]: https://github.com/markiantorno
