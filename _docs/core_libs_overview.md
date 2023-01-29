---
title: "Overview of the HL7 Core Libraries"
permalink: /docs/core-libs/overview
excerpt: "Overview of the HL7 Core Libraries."
last_modified_at: 2023-01-27
toc: true
---

The main core libraries are as follows:

|| [fhir-test-cases](#fhir-test-cases)       ||
|| [org.hl7.fhir.core](#orghl7fhircore)                                     ||
| [fhir-ig-publisher](#fhir-ig-publisher) | [validator-wrapper](#validator-wrapper) | [kindling](#kindling) |
|                                      || [HL7/FHIR](#hl7-fhir) |

## fhir-test-cases

This project contains cases that can be used to test FHIR reference implementations/validators. These test cases are imported as a dependency and included in the tests run when building the [org.hl7.fhir.core](#orghl7fhircore) artifacts.

### Repository
[https://github.com/FHIR/fhir-test-cases/](https://github.com/FHIR/fhir-test-cases/)

### Downstream Projects
- [org.hl7.fhir.core](#orghl7fhircore)


## org.hl7.fhir.core

This is the java core object handling code. It includes Java models of all FHIR resources, as well as utilities (including the FHIR validator) for the FHIR specification. The models and utilities in this code are imported as a dependencies and used for several downstream FHIR projects. This project uses the test cases definied in [fhir-test-cases](#fhir-test-cases).

### Repository
[https://github.com/hapifhir/org.hl7.fhir.core](https://github.com/hapifhir/org.hl7.fhir.core)

### Dependencies
- [fhir-test-cases](#fhir-test-cases)

### Downstream Projects
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

### Downstream Projects
- [HL7/FHIR](#hl7-fhir)

## HL7/FHIR

This project contains the spreadsheet files that define the current version of the HL7 FHIR specification, as well as a simple publishing utility. The publishing utility uses [kindling](#kindling) to process these spreadsheets and build a fully publishable web page containing all necessary URLs and their content for the HL7 FHIR specification.

### Repository
[https://github.com/HL7/fhir](https://github.com/HL7/fhir)

### Dependencies
- [kindling](#kindling) 


