# Kubernetes

## Kubernetes Networking

Kubernetes platform include nodes, applications, containers, and pods. These components communicate using different networking methods such as,

- Internet-to-service networking
- Container-to-container networking
- Pod-to-pod networking
- Pod-to-service networking

Kubernetes Network Model has a few general rules to keep in mind:

- Every Pod gets its own IP address: There should be no need to create links between Pods and no need to map container ports to host ports.
- Pods on a node should be able to communicate with all Pods on all nodes without NAT.
- Agents on a node (system daemons, Kubelet) can communicate with all the Pods in that node.
- Containers within a Pod share a network namespace (IP and MAC address), so they can communicate with each other using the loopback address.

### Internet-to-service networking

<img src="https://opensource.com/sites/default/files/2022-05/3internettoservicenets.jpg" height="80%" width="80%" />

### Container-to-container networking

Container-to-container networking happens through the Pod network namespace. Every Pod has its own network namespace, and containers inside that Pod share the same IP address and ports. All communication between these containers happens through localhost, as they are all part of the same namespace.

<img src="https://opensource.com/sites/default/files/2022-05/1containerandpodnets.jpg" />

### Pod-to-Pod networking

With Kubernetes, every node has a designated CIDR range of IPs for Pods. This ensures that every Pod receives a unique IP address that other Pods in the cluster can see. When a new Pod is created, the IP addresses never overlap. Unlike container-to-container networking, Pod-to-Pod communication happens using real IPs, whether you deploy the Pod on the same node or a different node in the cluster.

The diagram shows that for Pods to communicate with each other, the traffic must flow between the Pod network namespace and the Root network namespace. This is achieved by connecting both the Pod namespace and the Root namespace by a virtual ethernet device or a veth pair (veth0 to Pod namespace 1 and veth1 to Pod namespace 2 in the diagram). A virtual network bridge connects these virtual interfaces, allowing traffic to flow between them using the Address Resolution Protocol (ARP).

### Pod-to-Service networking

Pods are very dynamic. They may need to scale up or down based on demand. They may be created again in case of an application crash or a node failure. These events cause a Pod's IP address to change, which would make networking a challenge.

Kubernetes solves this problem by using the Service function, which does the following:
- Assigns a static virtual IP address in the frontend to connect any backend Pods associated with the Service.
- Load-balances any traffic addressed to this virtual IP to the set of backend Pods.
- Keeps track of the IP address of a Pod, such that even if the Pod IP address changes, the clients don't have any trouble connecting to the Pod because they only directly connect with the static virtual IP address of the Service itself.

<img src="https://opensource.com/sites/default/files/2022-05/2podtoservicenets.jpg" height="80%" width="80%" />

The in-cluster load balancing occurs in two ways:

- IPTABLES: In this mode, kube-proxy watches for changes in the API Server. For each new Service, it installs iptables rules, which capture traffic to the Service's clusterIP and port, then redirects traffic to the backend Pod for the Service. The Pod is selected randomly. This mode is reliable and has a lower system overhead because Linux Netfilter handles traffic without the need to switch between userspace and kernel space.
- IPVS: IPVS is built on top of Netfilter and implements transport-layer load balancing. IPVS uses the Netfilter hook function, using the hash table as the underlying data structure, and works in the kernel space. This means that kube-proxy in IPVS mode redirects traffic with lower latency, higher throughput, and better performance than kube-proxy in iptables mode.



Ever notice some “pause” containers running on your Kubernetes nodes? They are called “sandbox containers”, whose only job is to reserve and hold a network namespace (netns) which is shared by all the containers in a pod. This way, a pod IP doesn’t change even if a container dies and a new one in created in it’s place.

K8s isn’t responsible for network connectivity between containers: for this, various CNI (Container Networking Interface) plugins are used.

For example, the most popular of such plugins, Flannel, enables full network connectivity between all cluster nodes by running a small binary agent on each node. With it, Flannel allocates a subnet to each host. However, full and unregulated network accessibility is not always good. To ensure minimum isolation in the cluster, you have to deal with the firewall configuration. Generally, the CNI itself is in charge of such a configuration, that is why any third-party attempts to modify iptables rules might be interpreted incorrectly or ignored altogether.

#### Kubernetes Network Policies vs. Firewalls: What Is the Difference?

Kubernetes NetworkPolicy resource allows you to limit traffic to and from pods.

NetworkPolicy in a Kubernetes cluster, it is not a replacement for firewalls. A NetworkPolicy controls traffic within the cluster (known as east-west traffic) while a firewall restricts ingress and egress traffic to or from the cluster (known as north-west traffic).

**In TKG ** Antrea is default CNI.

https://medium.com/geekculture/k8s-node-ip-vs-pod-ip-vs-cluster-ip-65f75d4432b8

### Calico

Calico plugin as a stand-alone tool or with Flannel (via Canal subproject) to implement network connectivity features and to manage accessibility.

Well, here is the list of NetworkPolicy’s features:
- policies are limited to an environment (namespaces);
- policies are applied to pods marked with labels;
- you can apply rules to pods, environments or subnets;
- the rules may contain protocols, numerical or named ports.

## Storage Types

Kubernetes has below storage types for running stateful containers,
- Persistent Volumes (PV) - low level representation of a storage volume.
- Persistent Volume Claims (PVC) -  binding between a Pod and Persistent Volume.
- Storage Classes (SC) - allows for dynamic provisioning of Persistent Volumes.

### Persistent Volumes (PV)
 - PV is an abstraction for the physical storage device that attached to the cluster. 
 - PV is independent of the lifecycle of the Pods. It means that data represented by a PV continue to exist as the cluster changes and as Pods are deleted and recreated.
- PV is not Namespaced, it is available to whole cluster. i.e. PV is accessible to all namespaces.
- PV is resource in the cluster that can be provisioned dynamically using Storage Classes, or they can be explicitly created by a cluster administrator.
- Unlike Volumes, the PVs lifecycle is managed by Kubernetes.

### Access Modes
- ReadWriteOnce(RWO) — If a pod mounts a volume with ReadWriteOnce access mode, no other pod can mount it. In GCE (Google Compute Engine) the only allowed modes are ReadWriteOnce and ReadOnlyMany.
- ReadOnlyMany(ROX) — Multiple pods running on multiple nodes can use a single volume and read data. If a pod mounts a volume with ReadOnlyMany access mode, other pod can mount it and perform only read operation.
- ReadWriteMany(RWX) — Multiple pods running on multiple nodes can use a single volume and read/write data. If a pod mounts a volume with ReadWriteMany access mode, other pod can also mount it.
- ReadWriteOncePod(RWOP) — volume can be mounted as read-write by a single Pod.

### Persistent Volume Claims (PVC)
- PVC is binding between a Pod and PV. Pod request the Volume through the PVC.
- PVC is the request to provision persistent storage with a specific type and configuration.
- Kubernetes looks for a PV that meets the criteria defined in the PVC, and if there is one, it matches claim to PV.
- Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany or ReadWriteMany).

### Storage Classes (SC)
- StorageClass allows dynamic provisioning of Persistent Volumes, when PVC claims it.
- StorageClass abstracts underlying storage provider.
- StorageClass is used in conjunction with PVC that allow Pods to dynamically request a new storage.
- StorageClass use provisioners that are specific to the storage platform or cloud provider to give Kubernetes access to the physical storage.

#### Reclaim Policy
- PV that are dynamically created by a StorageClass will have the reclaim policy specified in the reclaimPolicy field of the class, which can be either Delete or Retain.

## Kubernetes Authentication & Authorization

Role-based access control (RBAC) is commonly used to enforce authorization in the Kubernetes control plane, for both users and workloads (service accounts). Roles and RoleBindings are Kubernetes objects that are used at a namespace level to enforce access control in your application.

**_Kubernetes does not have objects which represent normal user accounts._**
Ofcourse you need RBAC to user
https://devopstales.github.io/kubernetes/k8s-user-accounts/

Any user that presents a valid certificate signed by the cluster’s certificate authority (CA) is considered authenticated. So you need to create a certificate for you username.

- Service accounts on the other hand are tied to a specific namespace.
- Default service account created in the default namespace of a Kubernetes cluster.

When the process in the pod wants to communicate with the API server, the API server expects an Authorization header with a value of Bearer THETOKEN . The bearer token is the JWT token that is mounted to the pod as a secret. (/var/run/secrets/kubernetes.io/serviceaccount)

### AWS IAM + K8s Service Account

AWS Identity and Access Management (IAM) allows you to assign permissions to AWS services: for example, an app can access an S3 bucket. 

In the context of Kubernetes, the complementary system to define permissions towards Kubernetes resources is Kubernetes Role-based Access Control (RBAC).

IAM Roles for Service Accounts (IRSA) makes pods first class citizens in IAM
you can now use IAM roles at the pod level.
AWS identity APIs to recognize Kubernetes pods.

IAM roles for service accounts by completing the following procedures:

Creating an IAM OIDC provider for your cluster – You only complete this procedure once for each cluster.
Configuring the AWS Security Token Service endpoint for a service account – Complete this procedure for each unique set of permissions that you want an application to have.
Configuring pods to use a Kubernetes service account – Complete this procedure for each pod that needs access to AWS services.

### How users authenticate with Kubernetes cluster without k8s service accounts? Trough IDPs, AD, LDAP, …

https://rafay.co/the-kubernetes-current/diy-access-management-using-dex-and-kubelogin/

Kubernetes provides solid authorization using RBAC and provides several authentication strategies for integrating with an external user store.

kubernetes and LDAP integrated through Dex, an identity service that uses OpenID Connect (OIDC) to drive authentication for other apps. Dex was developed and open-sourced by CoreOS.

In the OAuth2/OIDC flow, Dex is the authorization server, kubectl is the client and the Kubernetes API server is the resource server. As stated in Dex github repo, Dex acts as a portal to other Identity Providers (IdP) through connectors. This lets Dex defer authentication to LDAP servers, SAML providers, or established Identity Providers like GitHub, Google, and Active Directory.

Reference: https://medium.com/upstream-engineering/kubernetes-authentication-using-ldap-and-oauth2-83c3457becf8

### Kubernetes - Vault Integration

1. Initally we use Spring Vault, vault token is loaded through spring yaml files backed by Github & DevOps pipeline based Kubernetes ConfigMap.
2. Later, we took InitContainer approach (https://blog.picnic.nl/hitchhikers-guide-to-hashicorp-vault-in-kubernetes-part-1-system-integration-ce17800049da). Query Valut API for 'Vault token' using authenting Kubernetes Service Account JWT token (KUBE TOKEN).
3. Now switched to, Agent Sidecar Injector
 *  At a minimum, every container in the pod will be configured to mount a shared memory volume. This volume is mounted to /vault/secrets and will be used by the Vault Agent containers for sharing secrets with the other containers in the pod.
 *  The Vault Agent Injector alters pod specifications to include Vault Agent containers that render Vault secrets to a shared memory volume using Vault Agent Templates. By rendering secrets to a shared volume, containers within the pod can consume Vault secrets without being Vault aware.

#### Deployments Vs. ReplicaSets

Deployment, under the hood, creates a ReplicaSet object which manages pods from this Deployment.
During a Deployment update, it will create another ReplicaSet with a new configuration, and this ReplicaSet in its turn will create new pods.

Argo Rollouts uses Rollout resource instead of Deployment resource. Similar to Deployment, Rollout uses ReplicaSet to spin up new pods.

> Docker Engine only runs on Linux, developers who use Windows and macOS for software development cannot run the engine until they spin up a virtual machine (VM) that runs linux.

> Minikube on macOS uses Docker, using HyperKit as the hypervisor. We can switch to Containerd

minikube start --container-runtime=containerd

#### Docker Images Without Docker

Docker Daemon with root privileges. It actually binds to a Unix socket instead of a TCP port. By default, users can only access the Unix socket using sudo command, which is owned by the user root.

Docker alternatives to combat those, namely:
- Buildah
- Podman
- Buildpacks: Buildpacks is a Cloud Native Computing Foundation (CNCF) project that focuses on building container images from source code. I

**Buildah** can be used to create and run images from a Dockerfile and without.

Buildah focuses on building OCI container images while Podman specializes in the management of the entire container lifecycle. 


#### Docker <-> Dockerd <-> Containerd <-> runC

[Docker, Dockerd, Containerd, runC](https://stackoverflow.com/questions/46649592/dockerd-vs-docker-containerd-vs-docker-runc-vs-docker-containerd-ctr-vs-docker-c)


### Kubernetes Cluster Deployment Tools


#### kOps

kOps, or Kubernetes Operations, can be compared to Rancher RKE, it’s an installer to create, destroy, upgrade and maintain production-grade Kubernetes clusters in public cloud.

AWS and GCP are currently official supported while Azure is in Alpha status.

 kOps provisions (and destroys) the necessary cloud infrastructure and has extensive possibilities to customize your cluster and enable all kinds of add-ons, such as AWS Load Balancer Controller, Cluster Autoscaler, Cert-manager, Metrics Server, Snapshot Controller etc.

kOps stores the state and representation of your cluster to a dedicated S3 bucket. This bucket will become the source of truth for the cluster configuration for automatic idempotency and makes it possible to do dry-runs before applying changes.

#### VMware TKG

VMware Tanzu Kubernetes Grid (TKG) provisions and manages the lifecycle of Tanzu Kubernetes clusters making use of Cluster API.

Tanzu Kubernetes Grid uses a management cluster to create and manage workload clusters, and has different deployment options based on where that management cluster runs. 

https://docs.vmware.com/en/VMware-Tanzu-Kubernetes-Grid/index.html

#### Kind

Kind is a tool for running local Kubernetes clusters. Kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.


