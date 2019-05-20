# Hybrid Cloud Security

**BRKSEC-2719**

# Summary and Key Takeaways

# Notes

Cisco data centre security

* **Visibility**
* **Segmentation**
* **Threat Protection**

## Visibility

### Cloud Centre

Hybrid cloud creates complexity. Cloud Centre (CC) has the mantra of 'author once, assemble many'.

You have a set of inputs - devops tooling, applications, etc. CC acts as the middleware between these inputs and the destinations where the applications can be layed down over.

**Workload Manager** - end-to-end infrastructure and application lifecycle management.

**Cost optimiser** - cloud usage optimisation and cost reduction across multiple clouds.

**Arction orchestrator** - ecosystem integration standardised using adapters and workflows.

Where does it fit? It's the larger umbrella that's wrapped around the smaller piece-parts.

### AMP for Endpoints

Behind AMP for endpoint is the security research organisation TALOS.

* Prevent - antivirus, IOCs
* Detect - sandboxing

All about fileless malware - monitor process activity and guard against attempts to hijack legitimate documents.

Dynamic analysis and sandboxing. Suspicious files (unknown) are sent up to the threat grid.

It's a cloud based tool, which has the monitoring dashboard.

### Tetration Analytics - ADM

Application dependency mapping (ADM). Customers don't know what their applications are doing. Agent based ingestion on the host and moves it into a big data platform.

Available as a SaaS model - no need to purchase, install manage hardware or software. Tetration takes the bare-metal, VM and switch telemetry and creates a map of an application. It can then create a baseline policy.

### StealthWatch Cloud

Public and private network monitoring as a SaaS. Data can be ingested using native cloud logs, as well as on-premise network logs. Can also send NetFlow.

## Segmentation

### ACI + TrustSec

In the campus we're concerns about people and things. In tehe DC it's servers.

### NGFW

## Tetration Analyitics - Enforcement

The Tetration agent became enforcement enabled. Shims in to the firewalls (Windows FW or IPTables). Segmentation policy written in 'natural language' and translated.

## Cloudlock

SaaS based cloud protection platform.

## Umbrella
