---
title: "Overview of the HL7 Core Projects"
permalink: /docs/core-libs/overview
excerpt: "Overview of the HL7 Core Projects."
last_modified_at: 2023-01-27
toc: true
---


-----------------------------------------------------------------------

![fhir-dependency-chart](../../assets/images/fhir-dependency-chart.png)

*Core FHIR Projects* : [fhir-test-cases](#fhir-test-cases) &#124; [org.hl7.fhir.core](#orghl7fhircore)  &#124; [fhir-ig-publisher](#fhir-ig-publisher) &#124; [validator-wrapper](#validator-wrapper) &#124; [kindling](#kindling) &#124; [HL7/FHIR](#hl7-fhir) &#124; [HAPI-FHIR](#hapi-fhir) &#124; [IG registry](#ig-registry)

-----------------------------------------------------------------------

The above is a chart representing the main FHIR Core Projects and dependencies between them. What follows below is a description of each project, a list of projects it is dependent on, and a list of projects dependent on it.

You may find that the test cases, data models, or utilities you are working on are spread across multiple projects. If you need help working with multiple projects, you can find helpful information in the [working with multiple projects](/docs/core-libs/multiple-projects) documentation.

## fhir-test-cases

This project contains cases that can be used to test FHIR reference implementations/validators. These test cases are imported as a dependency and included in the tests run when building the [org.hl7.fhir.core](#orghl7fhircore) artifacts.

### Repository
[https://github.com/FHIR/fhir-test-cases/](https://github.com/FHIR/fhir-test-cases/)

### Dependent Projects
- [org.hl7.fhir.core](#orghl7fhircore)


## org.hl7.fhir.core

This is the java core object handling code. It includes Java models of all FHIR resources, as well as utilities (including the FHIR validator) for the FHIR specification. The models and utilities in this code are imported as a dependencies and used for several dependent FHIR projects. This project uses the test cases definied in [fhir-test-cases](#fhir-test-cases).

### Repository
[https://github.com/hapifhir/org.hl7.fhir.core](https://github.com/hapifhir/org.hl7.fhir.core)

### Dependencies
- [fhir-test-cases](#fhir-test-cases)

### Dependent Projects
- [validator-wrapper](#validator-wrapper)
- [fhir-ig-publisher](#fhir-ig-publisher)
- [kindling](#kindling) 

## fhir-ig-publisher

This is the code for the HL7 IG publisher: a tool to take a set of inputs and create a standard FHIR IG. This tool uses the models, validation, and utilities contained in [org.hl7.fhir.core](#orghl7fhircore).

### Repository
[https://github.com/HL7/fhir-ig-publisher/](https://github.com/HL7/fhir-ig-publisher/)

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

## validator-wrapper

This project contains the CLI, Desktop GUI, and Standalone Validation Server for the FHIR Validator. These are all wrappers around the validation code contained in [org.hl7.fhir.core](#orghl7fhircore).

A publicly hosted instance of the Web interface for this validator is available here: https://validator.fhir.org/

### Repository
[https://github.com/hapifhir/org.hl7.fhir.validator-wrapper/](https://github.com/hapifhir/org.hl7.fhir.validator-wrapper/)

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

## kindling

This is the core publishing code for the HL7 FHIR specification itself. The jar produced from this repository is used within the [HL7/FHIR](#hl7-fhir) project to take the spreadsheet data in that project and generate a fully publishable web page containing all necessary URLs and their content for the HL7 FHIR specification.

### Repository
[https://github.com/HL7/kindling](https://github.com/HL7/kindling)

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

### Dependent Projects
- [HL7/FHIR](#hl7-fhir)

## HL7/FHIR

This project contains the spreadsheet files that define the current version of the HL7 FHIR specification, as well as a simple publishing utility. The publishing utility uses [kindling](#kindling) to process these spreadsheets and build a fully publishable web page containing all necessary URLs and their content for the HL7 FHIR specification.

### Repository
[https://github.com/HL7/fhir](https://github.com/HL7/fhir)

### Dependencies
- [kindling](#kindling) 

## Other Projects

### hapi-fhir

HAPI FHIR is a complete implementation of the HL7 FHIR standard for healthcare interoperability in Java. It uses org.hl7.fhir.core models and logic as part of this implementation. It also contains parent `pom.xml` build files that are used in org.hl7.fhir.core.

**Website**

[https://hapifhir.io/hapi-fhir/](https://hapifhir.io/hapi-fhir/)

**Repository**

[https://github.com/hapifhir/hapi-fhir](https://hapifhir.io/hapi-fhir/)

### ig-registry

Registry of published implementation guides.
This registry is published for human convenience at https://registry.fhir.org/guides

**Repository**

[https://github.com/FHIR/ig-registry](https://github.com/FHIR/ig-registry)


