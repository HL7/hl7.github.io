---
title: "Getting Started with fhir-test-cases"
permalink: /docs/fhir-test-cases/getting-started
excerpt: "How to set up your local IDE to build the FHIR test cases."
last_modified_at: 2022-06-15
toc: true
---

The [fhir-test-cases][Link-GithubProject] project uses Maven as its build tool. Note that although this project compiles to Java based artifacts, there is no actual Java code included. Maven packages the included files such that they can be accessed as a Maven dependency by other projects.

## Prerequisites

{% include prerequisites-git.md project-git-link='https://github.com/hapifhir/org.hl7.fhir.core.git' %}

{% include prerequisites-maven-idea.md project-name='fhir-test-cases' project-directory='fhir-test-cases' project-is-lombok='false' %}

{% include prerequisites-maven-eclipse.md project-name='fhir-test-cases' project-directory='fhir-test-cases' project-is-lombok='false'%}


[Link-GithubProject]: https://github.com/FHIR/fhir-test-cases/
[Link-OpenJDKInstall]: https://openjdk.java.net/install/

