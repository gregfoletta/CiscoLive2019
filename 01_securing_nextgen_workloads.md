# Securing Next-Gen Workloads

Stefan Avg

## Observations

Moved: Bare Metal -> Virtual Machines -> Containers -> Functions

As we move left to right, the time to provision drops, and the time the workload exists drops.

## Application Evolution

Previously, applications were monolithic, with some separation between the UI, business logic and data layer. This was generally split into the 'presentation', 'application' and 'database' tiers. 

Applications are now moving towards microservices, with well-defined APIs between different parts of the application.

## Policy

When we're using VMs, we're using virtual machine attributes from the hypervisor to determine the policies. Moving down into functions we're using 'sidecars'.

## Differences

With a hypervisor, each VM gets its own guest. With a container, the kernel has some 'secret sauce' to allow processes to pretend that they're living by themselves. The kernel features are cgroups, namespaces and 

## Linux Namespaces - Network Namespace

* A logical copy of the network stack with its own routes, firewall rules and network devices.
* Process inherits its network snamspace from its parrent.

### Bridge Mode

* Virtual ethernet bridge (*docker0*)
* Creates **peer interfaces**
    * eth0 is in the container
    * veth0 is in the host
* External communication needs to go via iptables - NAT to the host's IP address.

Hard to do this at scale.

## Kubernetes

The Kubernetes cluster has nodes, these are the physical machines. Wihtin the node you have PODs, and containers run within the POD.

There is a master node and a worker node. Master node has etcd which is the key/value store so the node knows where a container lives.

## Container Networking

* CNM - proposed by Docker
* CNI - proposed by CoreOS

These describe the way in which you wish to interact with the network.

In Kubernetes there are [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) which configure how groups of PODs are allowed to communicate with each other.

## Service Mesh

Data plane: is composed of a set of intelligent proxies (Envoy) deployed as sidecars. These mediate and control all network communication between microservices along with Mixer.

Control plane: managed and configured the proxies to route traffic.

For further information, refer to [Istio](https://istio.io/docs/concepts/what-is-istio/).

The service mesh capabilities:
* Traffic management
* Rule configuratio and traffic routing
* Underlying secure communication channel, managing authentication, authorisation and encryption.
* Policy enforcement componenet can be extended and customised to integrate with existing solution for ACLs, logging, monitoring quotas, auditing and more.

# Visibility

* Integration of Kubernetes into StealthWatch

