---
title: "Security"
permalink: /docs/core-libs/security
excerpt: "Security considerations"
last_modified_at: 2025-08-07
toc: true
---

## Signed Release Artifacts and Assets

To ensure the authenticity of Maven artifacts and downloaded tools such as the org.hl7.fhir.core Validator or the IG 
Publisher, we provide .asc signatures. These signatures can be verified using GPG (GNU Privacy Guard) to confirm that 
the files have not been tampered with and are indeed from the official source.

You can download the public key used for signing [here](../../assets/keys/public.pgp)

Keys are also available on the [Ubuntu keyserver](https://keyserver.ubuntu.com/pks/lookup?search=85D1C17CF1152107B272386C8FDFA68281399B5D&fingerprint=on&op=index).