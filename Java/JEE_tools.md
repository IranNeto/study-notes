# JEE tools definition

Definition of some tools, libraries or frameworks from JEE

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