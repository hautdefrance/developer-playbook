# Services/API

The core business functions are develop in services either using microservices or event driven actors.These can be implemented on the [platform ](../plattform.md)either as _serverless_ or _containers_.

### **Architectural Decisions**

1. Languages: 
   1. Python as we want to build data driven application and in this domain python is the standard
   2. Exception: BFF that only orchestrate calls from data apis / function \(lambdas\). There the improved performance of Node as well as the familiarity of the frontend team with Javascript matters more.

## Understand the domain 

[Create a lean diagram](../architecture/) with a domain diagram \(events, commands, actors, aggregates\), interaction diagram and a first deployment diagram, \(squnce diagram? not at this stage right?\).

## Decide if you go serverless or container and setup the project 

If it is a [strategic component](https://den.gitbook.io/developerplaybook/~/edit/primary/bootstraping) use _containers_ else use _serverless. Depending on your evaluation use the correct Bootstrap template to setup you project._

## Principles for API Development 

Principle of Good API Development vs Bad API Development

* Bad API Developers start by write code and tackle the technical challanges. Good API designer enable fast feedback by designing the interfaces showing it to the \(API\) customer and itterate on that. 
* Bad API Developer design for days and weeks until "perfection". Good API Developers find the the point of minimal agreement with the customer and then write the code, find new challanges based on the technology and itterated again with the customer over the best solution. 
* Bad API Developer on initial implementation speed, Good API Developer focus on reduced cycle times \(with api customers and technology\).
  * [https://www.youtube.com/watch?v=SEQeovx5z\_A](https://www.youtube.com/watch?v=SEQeovx5z_A)
  * Use API First Frameworks: [https://github.com/swagger-api/swagger-codegen/wiki/server-stub-generator-howto](https://github.com/swagger-api/swagger-codegen/wiki/server-stub-generator-howto)

## Design the API / Events in Swagger

First we start designing the API with Swagger. The best tool to do this is the [swagger editor](https://github.com/swagger-api/swagger-editor). I suggest adding the swagger editor to the docker-compose file in your project:

```text
services:
  swaggereditor:
    image: swaggerapi/swagger-editor
    ports:
      - "80:8080"
```

Create your swagger file: [basic swagger file structure](https://swagger.io/docs/specification/2-0/basic-structure/)

