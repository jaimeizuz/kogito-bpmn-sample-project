# Issue when looping back 4th time to an user task

## Description
Given the diagram "SampleProcess.bpmn", there's an issue when looping back. The first three times the user task is cimpleted with "validData=false" everything goes fine.
However, the next time the user task is completed with the same output we observe that no new instance of the user task is created.

![Alt text](./src/main/resources/SampleProcess-svg.svg)

### Prerequisites
* git
* JDK 17
* Maven 3.9.6+

### Steps to reproduce

* Clone the project: \
   ``git clone -b bug/user-task-not-found https://github.com/jaimeizuz/kogito-bpmn-sample-project.git``  
  
* Start the quarkus application: \
   ``mvn "-Pbamoe-community" "-Pbamoe-persistence" "-Pdevelopment" quarkus:dev``

* Start a new process instance using the request #1 in the Postman Collection inside src/postman

* Execute requests #2 and #3 in the Postman collection. Repeat the same sequence 3 times. After that, the new expected user task instance will not be created.