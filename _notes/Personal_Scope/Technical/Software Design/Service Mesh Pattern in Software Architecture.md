Link :https://azeynalli1990.medium.com/service-mesh-pattern-in-software-architecture-b68c2c21869

In software architecture, a *service mesh* is a dedicated infrastructure layer for facilitating service-to-service communications between services or microservices, using a proxy

The main idea is isolate application-independent cross-cutting concerns such as communication, monitoring, security, authentication/authorization etc. from core business logic. This kind of dedicated infrastructure layer adds value to low latency, configurability.

Circuit Breaker is a popular tactics that prevent service of network failure from cascading. By applying a failure threshold it avoids redundant calls to failed service, and responses back from back up service or default values.

![[Open_Close_Principle.png]]

This functionality is also rate limiting but on conditions:
- Limiting requests based on business requirement, such as enforcing SLA, Contracts
- Limiting by quote

*Traffic Shifting*
This functionality is very handy when migrating from old version of microservice to newer one. It gradually shifts traffic from old service call to new service call.

