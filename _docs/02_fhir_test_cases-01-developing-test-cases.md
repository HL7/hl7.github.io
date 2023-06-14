---
title: "Developing with fhir-test-cases"
permalink: /docs/fhir-test-cases/developing-test-cases
excerpt: "How to use develop with FHIR test cases."
last_modified_at: 2023-06-14
toc: true
---

## Tests in org.hl7.fhir.core

The `org.hl7.fhir.core` project uses the test cases included in `fhir-test-cases` throughout its unit tests. 

To run the tests for `org.hl7.fhir.core`, follow the steps [here](/docs/core/getting-started) to get the project built on your machine. Then, run the following maven command:

```
mvn test
```

These can take longer that 20 minutes to complete.

## Including local test changes

If you are developing new test cases or changing existing ones, there are several ways to include your changes in the `org.hl7.fhir.core` project.

### Using fhir-settings.json

When setting up to perform tests, the code in `org.hl7.fhir.core` uses the `fhir-settings.json` file. The default location of this file is `~/.fhir/fhir-settings.json`. 


This `fhir-settings.json` file contains many different fields for the customization of FHIR tools, including the `fhirTestCasesPath` field, which you can point to your local `fhir-test-cases` project directory:

```json
{
  "fhirTestCasesPath": "/path/to/my/fhir-test-cases",
}
```

You can also select a different file explicitly using the following vm parameter, either when running tests via Maven, or within an IDE:

```
mvn test -Dfhir.settings.path=/path/to/my/fhir-settings.json
```

### With Maven


By default, the `org.hl7.fhir.core` build uses the version of `fhir-test-cases` defined in the `validator_test_case_version` property in the `org.hl7.fhir.core` [pom.xml](https://github.com/hapifhir/org.hl7.fhir.core/blob/master/pom.xml) file. 

```xml
<properties>
    ...
    <validator_test_case_version>1.3.9</validator_test_case_version>
    ...
</properties>
```

If you are developing locally, you should change the version above, as well as the version in `fhir-test-cases` [pom.xml](https://github.com/FHIR/fhir-test-cases/blob/master/pom.xml) to a SNAPSHOT version (for example: `1.3.10-SNAPSHOT`).

```xml
<groupId>org.hl7.fhir.testcases</groupId>
<artifactId>fhir-test-cases</artifactId>
<version>1.3.10-SNAPSHOT</version>
<packaging>jar</packaging>
```

Once both of these are changed and verified to match, first the `fhir-test-cases` and then the `org.hl7.fhir.core` projects must be rebuilt with updated dependencies:

```shell
mvn clean install -U
```

This should build both projects using local code, and should include any changes you've made to the `fhir-test-cases` project. Any runs of tests using `mvn test` will continue to use the most recent build.

__Important: As you change code in `fhir-test-cases` remember to repeat the steps above (rebuild each project) or you may still be using an older build of the test cases project.__

