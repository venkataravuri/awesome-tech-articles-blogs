## DevOps & SRE

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

What are most important metrics/SLIs & KPIs you monitor? What is your monitoring strategy?

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

### SRE

Performance Budgets

SLI, SLO, SLI





Blue green
Canary Releases
A/B Testing
