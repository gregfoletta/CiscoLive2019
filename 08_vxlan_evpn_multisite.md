# VXLAN BGP EVPN Based Multi-Site

**BRKDCN-2035**

# Summary and Key Takeaways

# Notes

The key point was to make the overlays hierarchical rather than flat between the sites.

## Inter-X Connectivity Background

**VXLAN Multi-Pod** - Single fabric with end to end encapsulation. Build hierarchy in the underlay, flatted it in the overlay. 

**VXLAN Multi-Fabric** - the next step was to use two fabrics, but a DCI interconnect solution between them. 

**VXLAN Multi-Site** - multiple fabrics with integrated DCI.

## Introduction

Site-internal fabric is the standard fabric, site external is the DCI. These are connected by the **border gateways**. These stitch the VXLAN tunnels together and is the key component of the multi-site design.

We have multiple:
* Overlay domains
* Control planes (different AS in each site)
* Underlay domains
* Replication domains for BUM traffic
* VNI administrative domains.

**Main Use Cases**

Scale up model to build a large intra-DC network, standard data centre interconnects, integration with legacy networks (coexistence or migration).

The border gateways use an anycast VTEP to represent themselves. Site 1 underlay only knows about the VTEPs in Site 1. Northbound of the border gateways, they only have visibility of they border gateways.

There is a single VTEP for each site northbound of the BGWs.

## Support

10 sites, 4 BGWs per site, 256 VTEPs per site.

## Deeper Dive

BGW deployment consideratons - anycast border gateways, or VPC border gateways.

### Anycast

Up to 4, originally deployed at the leaf (border leaf), now with a newer version you can do it in the spine. The multi-site virtual IP shared across the BGWs is used for communcation between BGWs in different sites, and comms betwen BGWs and leaf nodes within a site.

The Individual primary IP (PIP) is used for BUM replication and with singe-homed endpoints (routed only, route-type 5) intra- and inter-site.

Route type 4 allows for a per-VNI eletion for the designated forwarder for BUM traffic. Each BGW can serve as DF for a single or set of layer-2 VNIs.

### VPC Border Gateways

**NXOS Release 9.2(1)**

Good for small deployments and brownfield migrations where there is a current VPC design in place. Classic ethernet/fabricpath to VXLAN.

The vPC BGW is is essentially a VPC leaf. There is 2 PIPs, one multi-site VIP and a vPC VIP.

### BUM Traffic Replication

Can use mulitcast within the sites, then ingress replication between the sites. There's storm control can be applied on the BGWs.

### Control and Data Plane

Two main options - [IGP, EBGP, IGP] and [EGP, EGP, EGP].

### Failure Detection on BGWs

Lose the site internal links on the BGWs, the site-internal prefixes are removed. The same happens with the external links.

### VPC Failure Scenarios

There are many and it is complex. If there is a specific failure case, look it up and investigate.

### Migration Scenarios

Some very interesting brownfield to greenfield migration scenarios.
