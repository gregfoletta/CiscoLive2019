# Digital Network Architecture for Securing Enterprise Networks

# Summary and Key Takeaways

# Session Notes

## Securing Access

Poor context awareness: IP

Good context awareness: username, device, IP, time, date, connection method.

Pitch for Cisco ISE - get the who, what whe where how, health, threats, cvss.
Access policy applied to wired, wireless and VPN.

* Visibility - context about everything touching the network.
* Control - network access control and segmentation.
* Compliance

**Device Sensor** - Listens to the traffic from the endpoint and provides the information to ISE.

**ACIDex** - AnyConnect Identity Extensions.

### Building User Context

Acive identity gathered using 802.1x agent.

Passive identity can be gleaned using WMI events, syslog or SPAN sessions.

Applications on the user's machine can be gathered using AnyConnect 'Posture' module.

### Authorisation

* **DACL or Named ACL** - downloadable ACL on wired or named ACL (wired + wireless)
* **VLANs** - dynamic VLAN assignments.
* **Security Group Tags** - Cisco 'SD Access'.

## Behaviour Analysis

Use flexible NetFlow to gain information on behaviour. StealthWatch can take this NetFlow information to perform behavioural analysis.

Use [NBAR](https://www.cisco.com/c/en/us/products/ios-nx-os-software/network-based-application-recognition-nbar/index.html) to get deeper context into the data and pass this on to StealthWatch.

ISE and StealthWatch communicate with [pxGrid](https://www.cisco.com/c/en/us/products/security/pxgrid.html).

### Encrypted Traffic Analytics

Two uses cases discussed - cryptographic and malware in encrypted traffic. Similar discussion to what was in the [Solving the Encrypted Traffic Problem](02_security_with_privacy.md) session. Discussed 'Sequence of Packet Lengths and Times' (SPLT). There's some good information on it [here](https://groups.google.com/forum/#!topic/traffic-obf/-Zk7YVhFx5U).

## Segmentation

Discussed the 'traditional' model of segmenting VLANs and enforcing policy on a firewall. Then contrasted against Cisco's new 'software defined access' design. 

With dynamic classificationCisco ISE assigns a security group tag to the port based on the user's authorisation profile. With static assignment it is done using VLAN or L3 interface to SGT.

Tags can be propagated in-band (i.e. the tag can be attached to the frame) using:
* Ethernet
* MACSec
* LISP
* VxLAN
* IPSec
* DMVPN
* GETVPN

Tags can be propagated out of band using:
* SXP
* pxGrid


## Securing Branch Offices 
