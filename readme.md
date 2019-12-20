# Microservices with Spring Boot and Spring Cloud on Kubernetes Demo Project [![Twitter](https://img.shields.io/twitter/follow/piotr_minkowski.svg?style=social&logo=twitter&label=Follow%20Me)](https://twitter.com/piotr_minkowski)

In this project I'm demonstrating you the most interesting features of [Spring Cloud Project](https://spring.io/projects/spring-cloud) for building microservice-based architecture that is deployed on Kubernetes. All the samples may be easily deployed on local Kubernetes single-node cluster - Minikube.


## Getting Started 
Currently you may find here some examples of microservices implementation using different projects from Spring Cloud. All the examples are divided into the branches and described in a separated articles on my blog. Here's a full list of available examples:
1. Using Spring Boot and Spring Cloud for building microservices that may be easily deployed on Kubernetes. The example is available in the branch [master](https://github.com/piomin/sample-spring-microservices-kubernetes/tree/master). A detailed guide may be find in the following article: Detailed description can be found here: [Quick Guide to Microservices with Kubernetes, Spring Boot 2.0 and Docker](https://piotrminkowski.com/2018/08/02/quick-guide-to-microservices-with-kubernetes-spring-boot-2-0-and-docker/) 
2. An introduction to Spring Cloud Kubernetes project, that shows its the most interesting features like discovery across many namespaces or Spring Boot property sources based on ConfigMap and Secret. The example is available in the branch [hybrid](https://github.com/piomin/sample-spring-microservices-kubernetes/tree/hybrid). A detailed guide may be find in the following article: Detailed description can be found here: [Microservices with Spring Cloud Kubernetes](https://piotrminkowski.com/2019/12/20/microservices-with-spring-cloud-kubernetes/)

### Usage
1. Download and run **Minikube** using command: `minikube start --vm-driver=virtualbox --memory='4000mb'` 
2. Build Maven project with using command: `mvn clean install`
3. Build Docker images for each module using command, for example: `docker build -t piomin/employee:1.1 .`
4. Go to `/kubernetes` directory in repository
5. Apply all templates to Minikube using command: `kubectl apply -f <filename>.yaml`
6. Check status with `kubectl get pods`

## Architecture

Our sample microservices-based system consists of the following modules:
- **gateway-service** - a module that Spring Cloud Netflix Zuul for running Spring Boot application that acts as a proxy/gateway in our architecture.
- **employee-service** - a module containing the first of our sample microservices that allows to perform CRUD operation on Mongo repository of employees
- **department-service** - a module containing the second of our sample microservices that allows to perform CRUD operation on Mongo repository of departments. It communicates with employee-service. 
- **organization-service** - a module containing the third of our sample microservices that allows to perform CRUD operation on Mongo repository of organizations. It communicates with both employee-service and organization-service.

The following picture illustrates the architecture described above including Kubernetes objects.

https://piotrminkowski.files.wordpress.com/2018/07/micro-kube-1.png

You can distribute applications across multiple namespaces and use Spring Cloud Kubernetes `DiscoveryClient` and `Ribbon` for inter-service communication.

https://piotrminkowski.files.wordpress.com/2019/12/microservices-with-spring-cloud-kubernetes-discovery.png