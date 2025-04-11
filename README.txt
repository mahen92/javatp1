How to build?
1. You need to have Sawtooth Java SDK installed in your local maven repository
   Steps to do that would be:
   > Clone https://github.com/hyperledger/sawtooth-sdk-java.git
   > From project root folder where pom.xml is found, run
     mvn clean generate-sources package install
     Note: You might need to set proxy settings in maven configuration settings.xml file
           Alternatively supply proxy settings to the mvn command above.
2. Go to contentprotection's pom.xml file location, run
   mvn clean package

sequenceDiagram
    participant User as Console User
    participant Console as Workflow Console
    participant SCM as SCM System
    participant WF as Workflow Engine
    participant Orchestrator as Workflow Orchestrator
    participant TnT as Track & Trace

    User->>Console: Select target system for workflow
    Console->>SCM: Select SCM to fetch product masterdata
    SCM-->>Console: Return product masterdata

    User->>Console: Define Process Pool (aggregated event)
    User->>Console: Define Tasks/Steps in the Pool
    User->>Console: Assign Stakeholders (users/groups)

    User->>Console: Save Workflow
    Console->>WF: Trigger BPMN translation
    WF->>SCM: Convert Pools to Event Profiles + Configure Trigger Points

    SCM->>User: Trigger invoked from SCM UI
    SCM->>Orchestrator: Redirect to Workflow Orchestrator
    Orchestrator->>WF: Execute respective workflow steps

    WF-->>SCM: Notify Process Pool completion

    SCM->>TnT: Display events on Track & Trace screen
    SCM-->>WF: Keep detailed event data in Workflow Engine


=========
Thank You
=========
