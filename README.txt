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
    participant Admin as Admin
    participant Modeler as Web Modeler
    participant Adapter as Adapter
    participant Engine as Workflow Engine
    participant DB as Database

    Admin->>Modeler: Open workflow modeler UI
    Admin->>Modeler: Create new workflow
    Admin->>Modeler: Define steps and I/O for each step

    Modeler->>Adapter: Validate and transform BPMN
    Adapter->>Engine: Prepare executable workflow definition

    Admin->>Modeler: Deploy workflow
    Modeler->>Engine: Deploy workflow definition
    Engine->>DB: Store workflow metadata and I/O schema

    Note over Admin,Engine: Workflow is now ready for execution

sequenceDiagram
    participant User as Application User
    participant App as Parent Application
    participant Adapter as Adapter
    participant Engine as Workflow Engine
    participant DB as Database

    User->>App: Perform action (e.g., Start Process / Submit Input)
    App->>Adapter: Send event data / trigger
    Adapter->>Engine: Start or continue workflow execution

    Engine->>DB: Update workflow state
    Engine-->>Adapter: Respond with next task and input requirements
    Adapter-->>App: Provide next step info and required inputs
    App-->>User: Show next task and collect inputs

    Note over Engine,DB: Engine maintains and updates process state in DB
    Note over Adapter,App: Adapter acts as intermediary, managing orchestration




=========
Thank You
=========
