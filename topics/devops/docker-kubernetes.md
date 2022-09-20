# Kubernetes

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

# Docker
