# K Container Shipment Use Case

This solution implementation illustrates the deployment of real time analytics on event streams in the context of container shipment in an event driven architecture with event backbone, functions as service and microservices.

As part of producing the IBM event driven point of view and reference architecture, we wanted to bring together a complete scenario which would cover all aspects of developing an event driven solutions including extended connections to devices/IOT  and blockchain for trusted business trading networks. We felt that the shipping business could provide a good foundation for this and would enable us to show how to develop event driven solutions following the architecture patterns.

The high level process can be represented in the following diagram, and is described in detailed in [this section](analysis/readme.md#high-level-view-of-the-shipment-process-flow):

![](analysis/shipment-bp1.png)

In developing the scenario, it became apparent that the event driven nature of business, extends across the business network, so we have widened the view in the scenario to consider the chain of parties involved in the shipping process, including importer, exporter, land transport and customs. To keep the scenario easy to understand, we have only considered the following cases:

1. Importer Orders goods from exporter overseas
2. Exporter becomes the customer of the shipping agent and uses 'ToDoor' shiping service
3. Shipping agent manages process of land transport loading, unloading and shipping. Through the scenario we can see the impact of “events”, which may delay or change the shipping process across all three parties.  

## Table Of Content

* [Target Audiences](#target-audiences)
* [Analysis](./analysis/readme.md)
* [Architecture](#architecture)
* [Deployment](#deployment)
* [Demonstration script](./docs/demo.md)

## Target Audiences

You will be greatly interested by the subjects addressed in this solution if you are...

* An architect, you will get a deeper understanding on how all the components work together, and how to address resiliency, high availability.
* A developer, you will get a broader view of the solution end to end and get existing starting code, and practices you may want to reuse during your future implementation. We focus on event driven solution in hybrid cloud addressing patterns and non-functional requirements as CI/CD, Test Driven Development, ...
* A project manager, you may understand all the artifacts to develop in an EDA solution, and we may help in the future to do project estimation.

## Architecture

Leveraging the Event Driven Architecture high level architecture foundation the solution is using the following components:

![High level component view](docs/kc-hl-comp-view.png)

* Top left represents the user interface to support the demonstration of the KC solution, with a set of widgets to present the ships movements, the container tracking / monitoring and the event dashboards. The botton of the UI will have controls to help performaing the step by step demonstration.
* The event backbone is used to define a set of topics used in the solution and as event sourcing for microservice to microservice data consistency support.
* Each service supports the top-level process with context boundary defining the microservice scope.
* Streamaing analytics is used to process aggreates and analytics on containers and ships movement data coming in real time.

## Deployment

The solution support a set of related repositories including user interface, a set of microservices to implement event sourcing, saga and SQRS patterns, and to implement simulators and analytics content.
In each repository we are explaining the design and some code approach used.

### Related repositories

* [User Interface in Angular 7 and Backend For Frontend server used for demonstration purpose](https://github.com/ibm-cloud-architecture/refarch-kc-ui)
* All the [Supporting microservices and functions](https://github.com/ibm-cloud-architecture/refarch-kc-ms) are grouped in one repository. We may change that later if we need it.
* [Real time analytics with IBM Streams Analytics](https://github.com/ibm-cloud-architecture/refarch-kc-streams)

The command `./scripts/clone.sh` clones the dependant repositories. 

### Configurations

To make the solution running we need to have a set of components installed and ready. We can deploy the components of the solution into three environments:

* **Public cloud (IBM Cloud)**, [see the article](docs/prepare-ibm-cloud.md) for details.
* **Private cloud** (we are using IBM Cloud Private) and [see this article](docs/prepare-icp.md) for details.
* Local to your laptop, mostly using docker images and docker compose. See next section.

### Run locally

To run locally you can use a kubernetes like Minikube or Docker Edge, or we propose to use docker-compose for local deployment, and here are the instructions to launch backbone and solution components:

1. Get [docker and install](https://docs.docker.com/install/) it (if not done yet)
1. Get [docker compose](https://docs.docker.com/compose/install/)
1. Use our compose file to start the backend components:   
  ```shell
  $ cd docker
  $ docker-compose -f backbone-compose.yml up
  ```

  Once the backend is started, you need to configure the Kafka topics. The local script: `scripts/createLocalTopics.sh` will create the necessary Kafka Topics so the solution will work.

4. Use our second compose file to start the web server and the other microservices.
 ```
  $ docker-compose -f kc-solution-compose.yml up
 ```

## Contribute

As this implementation solution is part of the Event Driven architeture reference architecture, the [contribution policies](https://github.com/ibm-cloud-architecture/refarch-eda#contribute) apply the same way here.

**Contributors:**
* [Jerome Boyer](https://www.linkedin.com/in/jeromeboyer/)
* [Martin Siegenthaler](https://www.linkedin.com/in/martin-siegenthaler-7654184/)
* [David Engebretsen](https://www.linkedin.com/in/david-engebretsen/)
* [Francis Parr](https://www.linkedin.com/in/francis-parr-26041924)
* [Hemankita Perabathini](https://www.linkedin.com/in/hemankita-perabathini/)

Please [contact me](mailto:boyerje@us.ibm.com) for any questions.
