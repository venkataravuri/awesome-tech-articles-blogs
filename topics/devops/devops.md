# DevSecOps & SRE

## Table of Contents
* [DevSecOps](#devsecops-pipelines)
	* [GitOps](#gitops)
* [SRE](#sre)
	* [Observability](#observability)
* [Kubernetes](docker-kubernetes.md)
	* [Storage — PV, PVC and Storage Class](docker-kubernetes.md#storage-types)
	* [k8s Authentication & Authorization](docker-kubernetes.md#kubernetes-authentication--authorization)

DevOps  extends  continuous development goals of the Agile movement to continuous integration and release. In order to accommodate continuous releases, DevOps encourages automation of the change, configuration and release processes.

https://newrelic.com/devops/what-is-devops 

### DevSecOps Pipelines

### Pre-Build Stage
* Automated Code Quality Inspection
	- SonarCube
		- Cyclomatic Complexity calculated based on the number of paths through the code. Whenever the control flow of a function splits, the complexity counter gets incremented by one. 
 
- Security Scanning -  Static application security testing (SAST), also referred to as static analysis to find security and quality issues by analyzing source code automatically with low false positives. 
	- Coverity - is the SAST solution for web application security. CWE, OWASP

- Static code analysis for application security
	- Fortify

### Build Stage

- OSS Scan
	- Source Composition Analysis
		* Black Duck

Static image analysis
- Carbon Black

Static workload analysis
- Carbon Black

Artifact signing using CoSign
Image signing using CoSign

Image Verification via Sigstore

- Container Security
	- Octane

Secure infrastructure provisioning via Saltstack

### GitOps

GitOps pattern of using Git repositories as the source of truth for defining the desired application state.

ArgoCD & Flux uses GitOps methodology to automate deployment of the desired application states in the specified target environments. Application deployments can track updates to branches, tags, or pinned to a specific version of manifests at a Git commit.

ArgoCD is implemented as a kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the Git repo). A deployed application whose live state deviates from the target state is considered OutOfSync. Argo CD reports & visualizes the differences, while providing facilities to automatically or manually sync the live state back to the desired target state. 

Features¶
- Automated deployment of applications to specified target environments
- Support for multiple config management/templating tools (Kustomize, Helm, Jsonnet, plain-YAML)
- Automated configuration drift detection and visualization
- Automated or manual syncing of applications to its desired state
- PreSync, Sync, PostSync hooks to support complex application rollouts (e.g.blue/green & canary upgrades)

Argo Rollouts is a Kubernetes controller and a set of CRDs which provides progressive delivery features along with advanced deployments such as blue-green, canary, canary analysis. It has the potential to control and shift traffic to a newer version of software through ingress controllers and service meshes.

Argo Rollout is a Kubernetes controller and has several options for Blue/Green deployments, but the most interesting one is the “preview” service that allows you to test the new color before making the traffic switch to live users.

- [Argo Blue Green Deployment](https://www.infracloud.io/blogs/progressive-delivery-argo-rollouts-blue-green-deployment/)
- [Argo Canary Deployment](https://www.infracloud.io/blogs/progressive-delivery-argo-rollouts-canary-deployment/)


https://blog.algolia.com/one-year-load-balancing/

### DNS GSLB

Basic DNS Load Balancing provides a basic load balancing capability - round robin DNS. It also does not factor in data center availability, resulting in end users getting directed to unavailable services. It does not factor in the location of the end user, so without a georouting component users will be connected to data centers that could be very far away. 

DNS based Global Server Load Balancing (GSLB) can provide an effective way to manage workloads across data centers, 

Uses [Anycast DNS](https://www.cloudflare.com/learning/dns/what-is-anycast-dns/) technique.

### Load balancers

GTM (Global Traffic Manager) - industry name is "Global Load Balancer"

GTM load balancer balances traffic for application servers across Data Centers. GTM is used as an **Intelligent DNS** server, handling DNS resolutions based on intelligent monitors and F5’s own iQuery protocol used to communicate with other BIGIP F5 devices. It is used in multiple data centre infrastructures, deciding where to resolve to request traffic to.

LTM (Local Traffic Manager) - industry name is "Server load balancer"

LTM load balances servers and also does cache, compression, persistence, etc. LTM network is a full reverse proxy, handling connections from clients. The F5 LTM uses Virtual Services (VSs) and Virtual IPs (VIPs) to configure a load balancing setup for a service.

LTMs can handle load balancing in two ways, the first way is an nPathconfiguration, and second is a Secure Network Address Translation (SNAT) method. LTM load balances servers and also does caching, compression, persistence, etc.

## SRE

Performance Budgets

SLI, SLO, SLI

### Observability

observability is a property of a system, similar to testability, operability, usability, etc. A **_system that’s observable is instrumented and emits telemetry_**, so systems that capture that telemetry can be used to interrogate the system about its behavior and derive answers (e.g. an observable system supports analytics and diagnostics).


#### What are most important metrics/SLIs & KPIs you monitor? What is your monitoring strategy?

We focus on USE & RED metrics

USE metrics - Utilization, Saturation, and Errors. “For every resource, check utilization, saturation, and errors.”
- Utilization: the average time the resource was busy servicing work
- Saturation: the degree to which the resource has extra work which it can't service, often queued
- Errors: the count of error events

USE metrics (resource-scoped) provides internal, service-centric view. The goal is to understand how resources behave while handling the workload. 

The RED metrics is about the workload itself (request-scoped). These are request-scoped, not resource-scoped as the USE method is. 

- R = Request Throughput, in requests per second
- E = Request Error Rate, as either a throughput metric or a fraction of overall throughput
- D (Duration) = Latency, Response Time

### Do you have business metrics? How do you capture them?

Spring boot provides Micrometer can help you take measurements from your application, and publish those metrics ready to be scraped by many different applications, including Prometheus.

To instrument our application to collect metrics to send to Prometheus, we need to add a few dependencies first.

The first dependency we need to add is the Spring Boot Actuator. This is the part of Spring Boot which exposes some APIs, for health-checking and monitoring of your apps.

https://www.tutorialworks.com/spring-boot-prometheus-micrometer/

Prometheus is one way of solving this problem. It is a time-series database, which stores a sequence of data points, across time
Prometheus polls your application for its latest metrics data – this is known as scraping
Prometheus uses a pull-based approach for getting metrics.


#### How do you SSH to Bastion servers?
SSH Bastions as the entry point. The network path originates from the On-Prem network, goes through DX/VPN to the transit gateway (TGW), and then is routed to the Shared Services VPC. 
