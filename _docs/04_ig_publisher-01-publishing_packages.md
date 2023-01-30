---
title: "Publishing Packages"
permalink: /docs/ig_publisher/publishing-packages
excerpt: "How to publish packages using the IG-Publisher."
last_modified_at: 2021-06-23
toc: true
---

## Background
On [fhir.org][Link-FhirDotOrg] there is a [registry][Link-FhirDotOrgRegistry] of published implementation guides for 
users to browse. One of the more popular exapmles of this would be the [US Core Implmentation Guide][Link-UsCoreIG].

These guides are maintained by the community, however, once changes are made and committed to the appropriate 
repositories, these updates then need to be released as versioned, web source files that can be displayed as part of the
[registry][Link-FhirDotOrgRegistry]. This is done through a series of defined steps.

## Moving Parts

### website source

The website source for [fhir.org][Link-FhirDotOrg] is stored in the [web-source][Link-GithubWebSource] repository. It's
a [Jekyll][Link-Jekyll] website, which is generated using the script contained in the committed [run-jekyll.bat][Link-GithubJekyllFile]
file. Running this command will generate a folder called `output` in the source folder.

### package entry list

Within the [packages repository][Link-GithubPackagesRepo] there are a series of package 
[directories][Link-GithubPackagesDirectory], containing the package data for the various published terminology and 
support packages. Within in each of these directories, exists a file named `package-list.json`, that contains the list 
of all published versions for that given package. For example, the package list for the r4 test data package is located
[here][Link-GithubPackagesExampleFile]. 

Each of the entries in the list of released packages contains information like the `version`, `desc`, `date`, and others.
The most important thing to note with these entries is that, _for packages_, there can be only one entry marked as 
`"current": true`. When creating a new release by adding a new entry in the list, the `"current": true` field **must be
removed** from the previous release, and then added to the new entry.

The reason for this is that implementers can point to a specific version of a given implementation guide, such as `0.2.1`,
they can specify that they want the `current`, or not specify a version at all (in which case `current` is used).
Having to instances of `current` will cause errors in the build process.

### package releaser tool

In the [IG Publisher][Link-GithubIgPublisherRepo] repository, there is a tool that looks at the released packages 
according to the source. It then decides what changes it needs to make in the source to generate a new website. This is
done by running the [PackageReleaser tool][Link-GithubPackageReleaser]. 

This tool takes in two arguments, a _source_ and a _destination_. The _source_ is the local path on your computer, to 
the cloned [packages directory][Link-GithubPackagesDirectory] in the packages project. The _destination_ is the local 
path on your computer, to the cloned [packages directory][Link-GithubWebSourcePackagesDirectory] in the web-source 
project.

## Publishing and Uploading a Release

At some point, someone will contact you to let you know that changes have been made to the packages, and a new release 
needs to be cut and published. When this happens, do the following:

1. Clone the [packages repository][Link-GithubPackagesRepo], and the [web-source][Link-GithubWebSource], and ensure they
   are up to date.
2. Update the appropriate `package-list.json` file entry list with the new entry for that release.
3. Run the [PackageReleaser tool][Link-GithubPackageReleaser] with the in _source_ defined as the local 
   [packages directory][Link-GithubPackagesDirectory] within the packages repository, and the out _destination_ pointing
   to the local [packages directory][Link-GithubWebSourcePackagesDirectory] in the web-source repository.
4. In the web-source project, run the [run-jekyll.bat][Link-GithubJekyllFile] script to generate the new Jekyll website.
   This will generate the `output` folder in the source directory.
5. sftp the contents of the generated `output` folder to the `/var/www/html/` directory on `fhir.org`. You will need 
   the proper credentials to do this. Currently, this is done by either [Grahame][Link-grahameGithub] or 
   [Mark][Link-markGithub], so please contact them to get this done.
   

[Link-GithubWebSource]: https://github.com/FHIR/web-source
[Link-GithubPackagesRepo]: https://github.com/FHIR/packages
[Link-GithubPublisherRepo]: https://github.com/HL7/fhir-ig-publisher
[Link-GithubIgPublisherRepo]: https://github.com/HL7/fhir-ig-publisher

[Link-GithubJekyllFile]: https://github.com/FHIR/web-source/blob/master/run-jekyll.bat
[Link-GithubPackagesDirectory]: https://github.com/FHIR/packages/blob/master/packages/
[Link-GithubWebSourcePackagesDirectory]: https://github.com/FHIR/web-source/tree/master/source/packages
[Link-GithubPackagesExampleFile]: https://github.com/FHIR/packages/blob/master/packages/fhir.test.data.r4/package-list.json
[Link-GithubPackageReleaser]: https://github.com/HL7/fhir-ig-publisher/blob/master/org.hl7.fhir.publisher.core/src/main/java/org/hl7/fhir/igtools/publisher/utils/PackageReleaser.java

[Link-FhirDotOrg]: www.fhir.org
[Link-FhirDotOrgRegistry]: http://fhir.org/guides/registry/
[Link-UsCoreIG]: http://hl7.org/fhir/us/core/
[Link-Jekyll]: https://jekyllrb.com/

[Link-grahameGithub]: https://github.com/grahamegrieve
[Link-markGithub]: https://github.com/markiantorno