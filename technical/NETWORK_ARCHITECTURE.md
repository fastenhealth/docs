---
title: Network Architecture
parent: Technical
---

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
