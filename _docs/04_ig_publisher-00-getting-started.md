---
title: "Getting Started with IG Publisher"
permalink: /docs/ig_publisher/getting-started
excerpt: "How to set up your local IDE to build the FHIR IG Publisher."
last_modified_at: 2023-01-30
toc: true
---

## Overview

{% include overview-fhir-ig-publisher.md %}

This project uses a variety of tools and plugins during its build process. This sometimes requires users to install software and make changes to their IDE so that they can compile.

## Prerequisites

{% include prerequisites-jekyll.md %}

### Sushi

Ensure you have the latest stable Sushi installed.
If you do not have the Sushi installed, please follow the instructions [here](https://fshschool.org/docs/sushi/installation/)

{% include prerequisites-java.md %}

{% include prerequisites-git.md project-git-link='https://github.com/HL7/fhir-ig-publisher.git' %}

{% include prerequisites-maven-idea.md project-name='fhir-ig-publisher' project-directory='fhir-ig-publisher' %}

{% include prerequisites-maven-eclipse.md project-name='fhir-ig-publisher' project-directory='fhir-ig-publisher' %}

[Link-GithubProject]: https://github.com/HL7/fhir-ig-publisher