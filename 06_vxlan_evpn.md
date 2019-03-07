#



# Notes

## Taxonomy

Leaf/spine visible to the underlay topology, not visible to the overlay. The VTEP is the VXLAN tunnel endpoint (NV1 on the Cisco devices). The overlay is a tunnel encapsulation with a VNI namespace.

## Overlay Technologies

* Overlay
    * Layer-2
    * Layer-3
    * Layer-2 and Layer-3
* Data-Plane
    * Overlay L2/L3 unicast
    * Overlay BUM traffic - multiple ways to replicate, can do multicast or ingress replication with unicast. The ingress switch replicates the packet.

EVPN is fully in the control plane:
* Peer discovery
* Route-learning and distribution
* Remote learning

## What is:

### VXLAN

Standards based encapsulation (RFC7348), used UDP encapsulation. Transport is independent, and has a flexible namespace (24bit).

### EVPN

Standards based control plane (RFC 8365 and 7432), used MP-BGP. Supports various data planes (VXLAN, MPLS, Provider Backbone [PBB]). Many use cases are covered including bridging and MAC-mobility.

Two different use cases for EVPN - L2 and L2/L3. L2 is asymmetric IRB, L2/L3 is symmetric IRB.

## IRB

Provides symmetric inter-subnet forwarding. Bridge -> Route/Route -> Bridge. The VNI is symmetric in both directions.

The host route and MAC is advertised with two route targets, one for the L2 VNI and one for the L3 VNI.

## Control and Data Plane

### Host Advertisements

MAC address is learnt on the switch, and its advertised into EVPN. It is given an L2VNI/route target, and the next-hop is the VTEP. This is in a route type 2 BGP update.

Host will come up and most likely ARP/ND for the default gateway. The switch now has IP information, and can add IP/length (length is /32) and an L3VNI/route-target. L3 VNI will match if the hosts are in the same VRF. This is still inside a route type 2.

External prefixes (external to the switch fabric) are advertised as a route type 5.

### VXLAN

* Src/dst MAC is hop-by-hop through the routed netwok
* Src/dst IP is the the src/dst VTEP IP addresses.
* UDP dst port is 4789
* UDP src is a hash of the l2/l3/l4 headers.
    * This gives the packet some entropy to allow for hashing across the ECMP links.
* VXLAN contains the VNI (plus other things)

The router MAC for the NV1 interface (which will be needed for the src/dst MAC of the inner frame in a routed context) is sent as an extended community in EVPN. This means the routers don't have to ARP across the VXLAN tunnel when routing.

## Silent Host Discovery

You won't have the type-2 IP information, only the type-5 subnet informationm. The source host will send a packet, but ECMP may send it to switch that doesn't have the host attached. The switch will then send out a 'glean' and send out a broadcast ARP for the host to all switches (239.0.0.1). The host the responds, the ARP table is updated, and a type-2 is sent out.

## Distributed Anycast Gateway

All edge devices sahre the same gateway IP and MAC address. The gateway is always active, so no first-hop redundancy protocol is required. No one is ARPing for the first hop in the fabric. Every SVI interface will have the same MAC address.

## VPC 

In vPC on the fabric side they share a common anycast VTEP. From EVPN perspective they look like two switches, from the VXLAN perspective they look like one. There is a primary VTEP IP which is different, and a secondary VTEP IP which is shared.

EVPN will always advertise the shared virtual IP as the VTEP.

In **vPC^2** there is no peer link. There is a virtual peer link that goes through the spine. In this instance only type-2 host routes are advertised by the vip. Other orphan and vPC type-2 and type-5 are advertised with the primary VTEP IP of the host.

## Underlay Considerations

Routed ports and interfaces, each one is a point to point layer3. Can use IP unnumbered /32 assigned to a loopback.

Prepare an IP addressing plan and assign specific subnets to features (RID, P2P links).

Suggestion: use OSPF or IS-IS.

Wth OSPF, watch the network type. Use point-to-point so there is no DR/BDR election. 

The main issue with eBGP is you cannot do the route-target: auto anymore as the AS is different.

IS-IS gives you no SPF calculation on link change.

## VXLAN EVPN Multi Site

Overlays evolve and spread, and then you end up with one data centre in a single failure domain. The VXLAN tunnel is end-to-end.

The multi-site overlay has tunnels from spine to spine through the super-spine. This allows for policies to be applied from the DC local overlay to the multi-site overlay.

