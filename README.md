# Issue with Link Events

## Description

Given a BPMN diagram that includes link events, it's been noticed that the "Name" field is always stored as "null" in the Kogito database (both data-index and data-audit tables).

![Alt text](./SampleProcess-svg.svg)
<p align="center"><img src="./SampleProcess-svg.svg"></p>

### Prerequisites
* git
* JDK 17
* Maven 3.9.6+

### Steps to reproduce

* Clone the project
  
* Start the quarkus application: \
   ``mvn clean quarkus:dev -Pdevelopment``

* Start a new process instance: \
``curl --location 'http://localhost:8080/SampleProcess'`` \\\
``--header 'Accept: application/json'`` \\\
``--header 'Content-Type: application/json'`` \\\
``--data '{}'``

* Query the database using the connection string contained in the application.properties file:
`` select process_id, process_instance_id, id,node_instance_id,`` \
``	 event_date, node_name, node_type, event_type``\
``from kogito.process_instance_node_log``\
``order by event_date;``\
\
``select id, enter, exit, name, node_id, type``\
``from kogito.nodes;``

Here we'd expect the nodes with type = "ThrowLinkNode" or "CatchLinkNode" having a the value "Start validation subprocess" and "Validation subprocess" respectively.

Additionally, we see that some nodes, which "Name" value has not been set in the diagram, do contain a value in the database (Start node of the embedded subprocess)