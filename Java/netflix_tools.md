# Netflix Spring Cloud Environmnet

* Service Discovery (Eureka)
* Circuit Breaker (Hystrix)
* Intelligent Routing (Zuul) 
* Client Side Load Balancing (Ribbon)

## Feign

Feign is a declarative HTTP client developed by Netflix. Feign uses tools like Jersey and CXF to write java clients for ReST or SOAP 
services. Through some annotations (JAX-RS specificated), Feign uses templatized requests with minimal code and overhead to communicate 
with other services. It's limited to text-based APIs only. Feign also makes easy to perform unit or integration tests.

[Source](https://www.baeldung.com/intro-to-feign)

[Project](https://github.com/OpenFeign/feign)

## Eureka

Netflix eureka is a Netflix OSS module which allows services to be registeres through an eureka server and discoveres through an eureka client. It facilitate this control of an distributed application. Eureka instances can be registered and clients can discover the instances using Spring-managed beans

[Source](https://spring.io/projects/spring-cloud-netflix#overview)

[Project](https://github.com/Netflix/eureka)

## Ribbon
Netflix Ribbon is an Inter Process Comunication (IPC) cloud library. Ribbon primarily provides client-side load balancing algorithms. Beyond that, also other features: Service Discovery Integration (integration with eureka is included in the ribbon library), Fault tolerance, Configurable load-balancing rules (also custom rules).

[Source](https://www.baeldung.com/spring-cloud-rest-client-with-netflix-ribbon)

[Project](https://github.com/Netflix/ribbon)

## Hystrix 
`Maintenance mode`

Hystrix is a latency and fault tolerance library designed to isolate points of access to remote systems, services and 3rd party libraries, **stop cascading failure and enable resilience in complex distributed systems where failure is inevitable.**

[Source](https://spring.io/guides/gs/circuit-breaker/)

[Project](https://github.com/Netflix/Hystrix)

## Zuul
Zuul is a JVM based router and server side load balancer by Netflix. And Spring Cloud has a nice integration with an embedded Zuul proxy – which is what we'll use here.

Zuul is the front door for all requests from devices and websites to the backend of the Netflix streaming application. As an edge service application, Zuul is built to enable dynamic routing, monitoring, resiliency, and security.
