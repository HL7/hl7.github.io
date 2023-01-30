---
title: "hapi.fhir.org"
permalink: /docs/hapi_fhir_org
excerpt: "HAPI FHIR example server."
last_modified_at: 2022-09-19
toc: true
---

### hapi.fhir.org server
[hapi.fhir.org][Link-HapiFhirOrg] is a FHIR server intended for demonstration purposes.

### Server monitoring and restarting.

The FHIR server is routinely monitored by the HL7 UptimeRobot service ([stats.hl7.org][Link-Monitoring]). If it does not respond correctly, a list of maintainers will be contacted, and one of them will restart the server.

To be become one of these maintainers, contact [David][Link-davidGithub]. The following will need to be arranged:
* Addition to the maintainers notification list
* ssh access to the hapi.fhir.org server.

Once you have access to the server, all restart and troubleshooting information is available in the following location: `server/README.txt`

[Link-HapiFhirOrg]: http://hapi.fhir.org/
[Link-Monitoring]: https://stats.hl7.org/790505375
[Link-davidGithub]: https://github.com/dotasek