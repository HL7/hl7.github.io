---
title: "validator-wrapper"
permalink: /docs/validator-wrapper/configuring
excerpt: "How to configure the validator-wrapper."
last_modified_at: 2025-04-02
toc: true
---
## ENVIRONMENT Variables
There are several environment variables that can configure validator-wrapper functionality.

Normally these can be set as follows:

*Linux/MacOS*:
```bash
export SESSION_CACHE_SIZE=6
```

*Windows*:
```bat
set SESSION_CACHE_SIZE=6
```

### ktor

Ktor is the server which provides the back end for the application.

{% include env-variable.md
name='KTOR_DEPLOYMENT_ENVIRONMENT'
description='a string'
possible-values='dev, prod'
default-value='dev' %}

This sets the environment for the ktor server. This selects which host and port are used when the application is run.

{% include env-variable.md
name='KTOR_DEPLOYMENT_DEV_HOST'
description='an http/https host name'
default-value='0.0.0.0' %}

Sets the host for the ktor server when in `dev` mode.

{% include env-variable.md
name='KTOR_DEPLOYMENT_DEV_PORT'
description='an http/https port number'
default-value='8082' %}

Sets the port for the ktor server when in `dev` mode.

{% include env-variable.md
name='KTOR_DEPLOYMENT_PROD_HOST'
description='an http/https host name'
default-value='0.0.0.0' %}

Sets the host for the ktor server when in `prod` mode.

{% include env-variable.md
name='KTOR_DEPLOYMENT_PROD_PORT'
description='an http/https port number'
default-value='3500' %}

Sets the port for the ktor server when in `prod` mode.

### Session Caching 

When users submit a validation, a validation engine is created and persisted in the session cache. If the user submits 
more data for validation, and their options are unchanged, the cache provides the engine instead of creating a new one.


{% include env-variable.md
name='SESSION_CACHE_IMPLEMENTATION'
description='a string'
possible-values='GuavaSessionCacheAdapter, PassiveExpiringSessionCache'
default-value='GuavaSessionCacheAdapter' %}

This selects the cache implementation that manages user sessions. 

`GuavaSessionCacheAdapter` is the preferred implementation, which uses the Google Guava's 
`com.google.common.cache.Cache`. `PassiveExpiringSessionCache` is available for backwards compatibility, and uses Apache 
Common's `org.apache.commons.collections4.map.PassiveExpiringMap`

{% include env-variable.md
name='SESSION_CACHE_DURATION'
description='an integer'
default-value='60' %}

The duration in minutes that a session will be kept in the cache. If negative, sessions will not expire. If unspecified, 
the default is 60 minutes.

{% include env-variable.md
name='SESSION_CACHE_SIZE'
description='a positive integer'
default-value='4' %}

This option is only available in `GuavaSessionCacheAdapter` and is the maximum number of sessions that will be kept in 
the cache in "last accessed last out" order.

### Validation Service

{% include env-variable.md 
name='VALIDATION_SERVICE_PRESETS_FILE_PATH' 
description='any valid file path' 
default-value='(empty)' %}

This sets the path to a valid validation service presets file. See [Presets](#presets)

{% include env-variable.md
name='VALIDATION_SERVICE_ENGINE_RELOAD_THRESHOLD'
description='a positive integer or 0'
default-value='250000000' %}

A value in bytes that represents the threshold for available memory that triggers a reload of the validation engine. 
This can be useful if overly resource hungry engines are being generated, but may result in degraded services or missed 
validation results.

## Configuration File

The application is packaged with a default configuration file, `application.conf`, located  at 
`src/jvmMain/resources/application.conf` in the source code, which uses a json-based format called HOCON 
(Human-Optimized Config Object Notation).

You can override this file by setting the `VALIDATOR_CONFIG_FILE_PATH` environment variable to a path specifying a new 
configuration. Any values supplied by the new configuration will override the default values provided by the packaged 
`application.conf`.

For example, the following configuration file will set the development port to `6000`, while leaving all other settings 
unchanged:

```hocon
ktor {
    deployment {
        dev {
            port = 6000
        }
    }
}
```

## Presets

The application can keep a set of validation engine instances in memory for use in common validation tasks. These are 
normally selected using the 'Common Validation Options' box in the web interface. When one of these presets is selected 
the application uses a copy of the existing engine instead of building a new instance. Building a new engine is a time 
intensive process, while copying is not.

The application is packaged with a set of default presets, which are defined in `src/jvmMain/resources/presets.json`

You can use your own preset file by setting the `VALIDATION_SERVICE_PRESETS_FILE_PATH` environment variable. 

```hocon
[
  # A list of presets.
  {
    "key": # the key that identifies this preset in the web interface,
    "localizedLabels": {
      # a map of key and value pairs for each language you wish to support.
      "en" : # the localized label for the preset. 
    },
    "cliContext": {
      # defines the validation engine as it should be provided by the validation service
      "baseEngine": # the key that identifies this engine on the server,
      "sv": # the version of FHIR to use for this engine,
      "igs": [
        # a list of IGs using "name#version" format to be loaded by the engine
      ],
      "extensions": [
        # a list of extensions to include in the engine
      ],
      "checkIPSCodes": # true if the IPS codes should be checked during validation,
      "bundleValidationRules": [
        # a list of bundle validation rules
        {
          "rule": # The resource type or index (or both) of the entry to validate,
          "profile": # the canonical URL of the profile to use to validate the entry
        }
      ]
    },
    "igPackageInfo": [
      # a detailed list of IG packages to be used for validation
      # this has the same content as the "igs" field, but provides necessary information for the web interface
      {
        "id": # the ID of the IG,
        "version": # the version of the IG,
        "fhirVersion": # this FHIR version of the IG,
        "url": # the canonical URL of the IG
      }
    ],
    "extensionSet": [
      # a list of extensions to be used for validation
    ],
    "profileSet": [
      # a list of canonical URLs of profiles to be used for validation
    ]
  }
]
```