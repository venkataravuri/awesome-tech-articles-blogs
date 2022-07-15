# Multi-tenancy

Isolating tenant data is a fundamental responsibility for Software as a Service (SaaS) providers. 

Implement multi-tenant data isolation using PostgreSQL row level security policies.
https://github.com/aws-samples/aws-saas-factory-postgresql-rls/blob/main/app/src/main/java/com/amazon/aws/partners/saasfactory/pgrls/repository/TenantAwareDataSource.java
https://github.com/aws-samples/aws-saas-factory-postgresql-rls/blob/main/app/src/main/java/com/amazon/aws/partners/saasfactory/pgrls/repository/DataSourceRepository.java

For the pool model, where there are two queues for scalability, the message is published to the queue with th fewest messages in it. This is to show how you can reduce a noisy neighbor problem. The messages have a TenantID attribute to pass the context downstream to the consumer services.

Factors such as noisy neighbor and data isolation influence strategy to store tenant data, either a “silo” model, or a “pool” model.

A silo model an option for compliance or other isolation needs and want to avoid noisy neighbor conditions. Usually  separate tables per tenant.

In a pool model, data resides in a single table, segregated by tenant identifiers. 
Eeffectively distribute tenant data within a single table 
Prevent cross tenant data access

Obvious way to achieve this would be to add TenantID as the partition key. tenant identifier as a partition key could concentrate data in a given partition.  partition key scheme in a way that will better distribute tenant data across multiple partitions, and limit your chances of hitting the hot partition problem.

augment your partition key, by adding a suffix to the original tenant identifier. 

[Building a Multi-Tenant App With NodeJS + MongoDB](https://medium.com/geekculture/building-a-multi-tenant-app-with-nodejs-mongodb-ec9b5be6e737)




## Architecture & Design

|Rating|Type|Topic
------------: | ------------- | -------------
||:tv:|[Architecting Multi-Tenancy](https://www.heroku.com/podcasts/codeish/41-architecting-multi-tenancy)
||:newspaper:|[L33T M10y](https://engineering.salesforce.com/l33t-m10y-f04f38127b82)
||:newspaper:|[The Force.com Multitenant Architecture](https://developer.salesforce.com/page/Multi_Tenant_Architecture)
||:newspaper:|[The Force.com Multitenant Architecture - PDF](https://www.developerforce.com/media/ForcedotcomBookLibrary/Force.com_Multitenancy_WP_101508.pdf)
||:newspaper:|[The Internal Design of Force.com’s Multi-Tenant Architecture](https://www.infoq.com/presentations/SalesForce-Multi-Tenant-Architecture-Craig-Weissman/)

## Engineering Blogs

|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Azure Architecture Walkthrough: Building a multi-tenant Azure Architecture for a B2C scenario](https://techcommunity.microsoft.com/t5/azure-developer-community-blog/azure-architecture-walkthrough-building-a-multi-tenant-azure/ba-p/1278357)
||:newspaper:|[Moving to Multitenancy](https://blend.com/blog/engineering/moving-to-multitenancy/)
||:newspaper:|[Pinterest - Secret management in multi-tenant environments](https://medium.com/pinterest-engineering/secret-management-in-multi-tenant-environments-debc9236a744)
||:newspaper:|[How Freshworks handled its growing database](https://www.freshworks.com/company/freshworks-data-blog/)
||:newspaper:|[Laravel multi-tenancy, avoiding over engineering](https://ollieread.com/articles/laravel-multi-tenancy-avoiding-over-engineering)
||:newspaper:|[Multitenancy with Laravel](https://multitenancy.dev/)
||:newspaper:|[Discovering the Need for an Indexing Strategy in Multi-Tenant Applications](https://www.elastic.co/blog/found-multi-tenancy)
||:newspaper:|[Discovering the Need for an Indexing Strategy in Multi-Tenant Applications](https://www.elastic.co/blog/found-multi-tenancy)
||:tv:|[Scaling Shopify's Multi-Tenant Architecture across Multiple Datacenters](https://www.usenix.org/conference/srecon16europe/program/presentation/weingarten)

## Implementation Choices

||Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Multi-Tenancy Implementation using Spring Boot + Hibernate](https://medium.com/swlh/multi-tenancy-implementation-using-spring-boot-hibernate-6a8e3ecb251a)
||:newspaper:|[How to handle multi-tenancy in Cumul.io](https://blog.cumul.io/2019/08/22/how-to-handle-multi-tenancy-in-cumul-io/)
||:newspaper:|[Providing Multitenancy with Spring Boot](https://bytefish.de/blog/spring_boot_multitenancy/)
