---
title: "Overview of the HL7 Core Projects"
permalink: /docs/core-libs/overview
excerpt: "Overview of the HL7 Core Projects."
last_modified_at: 2023-01-27
toc: true
---


-----------------------------------------------------------------------

![fhir-dependency-chart](../../assets/images/fhir-dependency-chart.png)

*Core FHIR Projects* : [fhir-test-cases](#fhir-test-cases) &#124; [org.hl7.fhir.core](#orghl7fhircore)  &#124; [fhir-ig-publisher](#fhir-ig-publisher) &#124; [validator-wrapper](#validator-wrapper) &#124; [kindling](#kindling) &#124; [HL7/FHIR](#hl7fhir) &#124; [HAPI-FHIR](#hapi-fhir) &#124; [IG registry](#ig-registry)

-----------------------------------------------------------------------

The above is a chart representing the main FHIR Core Projects and dependencies between them. What follows below is a description of each project, a list of projects it is dependent on, and a list of projects dependent on it.

You may find that the test cases, data models, or utilities you are working on are spread across multiple projects. If you need help working with multiple projects, you can find helpful information in the [working with multiple projects](/docs/core-libs/multiple-projects) documentation.

## fhir-test-cases

{% include overview-fhir-test-cases.md %}

These test cases are imported as a dependency and included in the tests run when building the [org.hl7.fhir.core](#orghl7fhircore) artifacts.

### Dependent Projects
- [org.hl7.fhir.core](#orghl7fhircore)

## org.hl7.fhir.core

{% include overview-org-hl7-fhir-core.md %}

The models and utilities in this code are imported as a dependencies and used for several dependent FHIR projects. 

This project uses the test cases defined in [fhir-test-cases](#fhir-test-cases).

### Dependencies
- [fhir-test-cases](#fhir-test-cases)

### Dependent Projects
- [validator-wrapper](#validator-wrapper)
- [fhir-ig-publisher](#fhir-ig-publisher)
- [kindling](#kindling) 

## fhir-ig-publisher

{% include overview-fhir-ig-publisher.md %}

This tool uses the models, validation, and utilities contained in [org.hl7.fhir.core](#orghl7fhircore).

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

## validator-wrapper

{% include overview-validator-wrapper.md %}

These are all wrappers around the validation code contained in [org.hl7.fhir.core](#orghl7fhircore).

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

## kindling

{% include overview-kindling.md %}

The jar produced from this repository is used within the [HL7/FHIR](#hl7-fhir) project.

### Dependencies
- [org.hl7.fhir.core](#orghl7fhircore)

### Dependent Projects
- [HL7/FHIR](#hl7fhir)

## HL7/FHIR

{% include overview-hl7-fhir.md %}

The publishing utility uses the JAR produced by the [kindling](#kindling) project.

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
This registry is published for human convenience at [https://registry.fhir.org/guides](https://registry.fhir.org/guides)

**Repository**

[https://github.com/FHIR/ig-registry](https://github.com/FHIR/ig-registry)


