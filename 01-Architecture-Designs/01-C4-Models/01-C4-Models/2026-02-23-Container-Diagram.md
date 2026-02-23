# C4 Model - Level 2: Container Diagram (The Data Migrator)

## 🎯 Objective
This diagram illustrates the high-level boundaries of the migration system and how data flows from the legacy VMDS storage to the modern PostGIS landing zone.

```mermaid
graph LR
    subgraph Smallworld_GNM [Smallworld Environment]
        VMDS[(VMDS Database)] -- "4kb Blocks" --> Magik[Magik Metadata Service]
    end

    subgraph Java_Orchestrator [The Data Migrator - Java]
        Adapter[SQL Adapter / JDBC] -- "Mapping" --> Converter[Spatial Translator]
    end

    subgraph Cloud_Persistence [PostgreSQL Landing Zone]
        PostGIS[(PostgreSQL / PostGIS)]
    end

    %% Interaction Flow
    Magik -- "JNI / Interoperability API" --> Adapter
    Converter -- "SQL INSERT / WKT" --> PostGIS

    %% Styles
    style VMDS fill:#f9f,stroke:#333
    style PostGIS fill:#00b2a9,color:#fff
    style Java_Orchestrator fill:#005da9,color:#fff
