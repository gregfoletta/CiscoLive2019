#


# Notes

## Standards

* [ISA-95](https://en.wikipedia.org/wiki/ANSI/ISA-95) is the model for the levels, similiar to the ISO layer-1 through 7.
* IEC-62443 (formerly ISA-99)
* NIST Special Publication 800-82 revision 2 - have us the 'industrial DMZ' which is the zone between the enterprise and the manufacturing zone.

For east/west, 62443 talks about breaking up the industrial network into zones/cells, configuring 'conduits' between the zones, and applying security controls on the conduits.

## What's Different

Two main items:
* Maintain safe production environments
* Sustain production

You can't turn things off. Have to talk about the cells/zones in terms of a 'minimum viable product'. 

## Security Challenges

* Antiquated systems - unpatched and legacy
* IT / OT divide
* Lack of visibility
* Access control
* Change control (24/7/365 operations)

Take production systems with production systems outcomes, and merge that into the security.

## Domains of Responsibility

Start with the organisation, what are the domains of control? Who's accountable?

## Common Security Issues

Types of attacks in 2018 and 2019:
* Prodiction systems targeted with sophisticated modular software (state sponsored)
* Ransomware

**Tactics and Prodedures**:
Documented [here](https://www.us-cert.gov/ncas/alerts/TA18-074A):
* Spear-phishing
* [Watering-hole domains](https://en.wikipedia.org/wiki/Watering_hole_attack)
* Credential gathering

Porous boundaries - a lot of the machines now have LTE built in. It isn't just the northbound surface that you have to be concerned about.

## Remediation

* Human factors - HR systems immediately remove access to terminated employees
* Control systems patching
* Software patching
* IT systems software patching
* Timely backups

Technical controls:
Systems separation
MFA
Scanning of emaila nd web
whitelist DNS
active monitoring

## Protect

Cisco [SAFE](https://www.cisco.com/c/en/us/solutions/enterprise/design-zone-security/landing_safe.html) guideliens
Harden network elements
Disable unecessary services
Switching - restrict broadcast domains, STS security, ARP inspection, anti-spoofing, disable unused ports

## Visibility

Can't effectively secure what you can't see. The visibility allows you to create a baseline. It then feeds into the security tools.

A pitch for StealthWatch, taking in NetFow. Used to be sampled NetFlow, now the IE switches can do full netflow.

## Stability

Talked about layer 2 functionality to minimise impact: spanning tree, DHCP snooping, ARP inspection, etc.

Talked about VRF-Lite - need to think about the number of VRFs that the routing platform can support.

## East-West Traffic

Pitch for TrustSec and security group tags. Within a process control network I think this is a good fit given the pervasive layer 2 requirements.

## Complexity

Cisco Industrial Network Director. Can talk to ISE using pxGrid. An example was shown where a number of OT elements were grouped together in a zone. This zoning is combined into a security group and the details of each host are then sent to ISE.
