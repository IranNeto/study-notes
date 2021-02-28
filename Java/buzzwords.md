# Buzzwords

Definition of some tools, libraries or frameworks

## JAX-RS
JAX-RS stands for *Jakarta RESTful Web Service* and is a specification that provides support in creating REST web 
services. By specification it's meant a set of interfaces and annotations offered by Java EE. There are some 
JAX-RS implementation better known as RESTEasy and Jersey.

So, to build a JEE-compliant application server (acording to Oracle guys), you should provide a JAX-RS implementation
for the deployed apps to use. 

[Source](https://www.baeldung.com/jax-rs-spec-and-implementations)

[JAX-RS vs Spring MVC](https://www.baeldung.com/rest-api-jax-rs-vs-spring)

## Grizzly
Grizzly is a tool used to buiilt Java servers using the old Java™ NIO API. Grizzly’s goal was to help developers 
to build scalable and robust servers using NIO as well as offering extended framework components: Web Framework 
(HTTP/S), WebSocket, Comet, and more.

[Source](https://javaee.github.io/grizzly/)

## Feign

Feign is a declarative HTTP client developed by Netflix. Feign uses tools like Jersey and CXF to write java clients for ReST or SOAP 
services. Through some annotations (JAX-RS specificated), Feign uses templatized requests with minimal code and overhead to communicate 
with other services. It's limited to text-based APIs only. Feign also makes easy to perform unit or integration tests.

[Source](https://www.baeldung.com/intro-to-feign)

[Project](https://github.com/OpenFeign/feign)