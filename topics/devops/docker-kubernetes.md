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

https://stackoverflow.com/questions/57798267/kubernetes-persistent-volume-access-modes-readwriteonce-vs-readonlymany-vs-read

How users authenticate with Kubernetes cluster without k8s service accounts? Trough IDPs, AD, LDAP, …
https://medium.com/upstream-engineering/kubernetes-authentication-using-ldap-and-oauth2-83c3457becf8

#### Deployments Vs. ReplicaSets

Deployment, under the hood, creates a ReplicaSet object which manages pods from this Deployment.
During a Deployment update, it will create another ReplicaSet with a new configuration, and this ReplicaSet in its turn will create new pods.

Argo Rollouts uses Rollout resource instead of Deployment resource. Similar to Deployment, Rollout uses ReplicaSet to spin up new pods.

# Docker

## Satefulset, Persistent Volumes, Headless Services
||| Topic
------------ | ------------- | -------------
:star: | :link: | [Conquering Statefulness on Kubernetes](https://medium.com/capital-one-tech/conquering-statefulness-on-kubernetes-26336d5f4f17)
