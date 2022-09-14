## DevSecOps & SRE


### GitOps

GitOps pattern of using Git repositories as the source of truth for defining the desired application state.

ArgoCD & Flux uses GitOps methodology to automate deployment of the desired application states in the specified target environments. Application deployments can track updates to branches, tags, or pinned to a specific version of manifests at a Git commit.

ArgoCD is implemented as a kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the Git repo). A deployed application whose live state deviates from the target state is considered OutOfSync. Argo CD reports & visualizes the differences, while providing facilities to automatically or manually sync the live state back to the desired target state. 

Features¶
Automated deployment of applications to specified target environments
Support for multiple config management/templating tools (Kustomize, Helm, Jsonnet, plain-YAML)
Automated configuration drift detection and visualization
Automated or manual syncing of applications to its desired state
PreSync, Sync, PostSync hooks to support complex application rollouts (e.g.blue/green & canary upgrades)


https://blog.algolia.com/one-year-load-balancing/


What is DevOps?
What is DevOps?
Is it a culture? Is it a job title? Is it a way of organizing? Or just a way of thinking? We think it’s a still-evolving movement...

DevOps movement emphasizes communication, collaboration and integration between software developers and IT operations. Rather than seeing these two groups as silos who pass things along but don’t really work together.

Agile software development paved the way, steering away from the waterfall method of software development toward a continuous development cycle. But it didn’t include the operations side so while development could be continuous, deployment was still waterfall-oriented.

DevOps essentially extends the continuous development goals of the Agile movement to continuous integration and release. In order to accommodate continuous releases, DevOps encourages automation of the change, configuration and release processes.

https://newrelic.com/devops/what-is-devops 


### DevSecOps Tools

### Prior to build
* Automated Code Quality Inspection
	- SonarCube
 
- Security Scanning -  Static application security testing (SAST), also referred to as static analysis to find security and quality issues by analyzing source code automatically with low false positives. 
	- Coverity - is the SAST solution for web application security. CWE, OWASP

- Static code analysis for application security
	- Fortify

### Build Time

- OSS Scan
	- Source Composition Analysis
		* Black Duck

- Container Security
	- Octane



## Observability

observability is a property of a system, similar to testability, operability, usability, etc. A **_system that’s observable is instrumented and emits telemetry_**, so systems that capture that telemetry can be used to interrogate the system about its behavior and derive answers (e.g. an observable system supports analytics and diagnostics).


#### What are most important metrics/SLIs & KPIs you monitor? What is your monitoring strategy?

We focus on USE & RED metrics

USE metrics - Utilization, Saturation, and Errors. “For every resource, check utilization, saturation, and errors.”
- Utilization: the average time the resource was busy servicing work
- Saturation: the degree to which the resource has extra work which it can't service, often queued
- Errors: the count of error events

USE metrics (resource-scoped) provides internal, service-centric view. The goal is to understand how resources behave while handling the workload. 

The RED metrics is about the workload itself (request-scoped). These are request-scoped, not resource-scoped as the USE method is. 

R = Request Throughput, in requests per second
E = Request Error Rate, as either a throughput metric or a fraction of overall throughput
D (Duration) = Latency, Response Time

### Do you have business metrics? How do you capture them?

Spring boot provides Micrometer can help you take measurements from your application, and publish those metrics ready to be scraped by many different applications, including Prometheus.

To instrument our application to collect metrics to send to Prometheus, we need to add a few dependencies first.

The first dependency we need to add is the Spring Boot Actuator. This is the part of Spring Boot which exposes some APIs, for health-checking and monitoring of your apps.

https://www.tutorialworks.com/spring-boot-prometheus-micrometer/



Prometheus is one way of solving this problem. It is a time-series database, which stores a sequence of data points, across time

Prometheus polls your application for its latest metrics data – this is known as scraping

Prometheus uses a pull-based approach for getting metrics.


### SRE

Performance Budgets

SLI, SLO, SLI





Blue green
Canary Releases
A/B Testing
