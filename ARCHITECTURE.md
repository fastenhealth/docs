# Network Diagram

```mermaid
C4Container
title Fasten Network Architecture Diagram

Container_Boundary(homeNetwork, "Home Network") {
    Person(fastenUser, "Fasten User", "A Fasten user")
    
    Container_Boundary(dockerImage, "Fasten Docker Container") {
      System(fastenSelfhosted, "Fasten Self-hosted", "Fasten running on a server or home computer")
      ContainerDb(database, "SQLite", "SQLite Database", "Stores medical records and provider credentials")
    }
}

Container_Boundary(publicInternet, "Public Internet") {
    Container_Boundary(fastenLighthouseNetwork, "Fasten Lighthouse Network") {
      System(fastenLighthouse, "Fasten Lighthouse", "callback server")
    }
  
    System(healthCare, "Healthcare Provider", "A healthcare provider, storing EHR/EMRs.")
}


```
# Data-flow Diagram

```mermaid
sequenceDiagram
User->>Fasten Self-Hosted: Open Fasten in Browser
Fasten Self-Hosted->>User: Respond with Angular Frontend
User->>Healthcare Provider: Attempt connection to Healthcare provider
Healthcare Provider-->>Fasten Lighthouse: Redirect

loop Wait for temp auth code
    Fasten Self-Hosted->>Fasten Lighthouse: Continously check for auth code
end
Fasten Self-Hosted-->>Healthcare Provider:Retrieve private healthcare data
```