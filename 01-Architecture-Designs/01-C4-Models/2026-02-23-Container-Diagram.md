# C4 Model - Level 2: Container Diagram (The Data Migrator)

## 🎯 Objective
This diagram illustrates the high-level boundaries of the migration system. It shows how the **Java Orchestrator** acts as a bridge between the legacy binary storage (VMDS) and the modern GridOS-ready persistence layer (PostGIS).

```mermaid
graph LR
    subgraph Smallworld_Internal [Smallworld 4.3 Environment]
        VMDS[(VMDS Database)] -- "Binary 4kb Blocks" --> Magik_Srv[Magik Metadata Service]
    end

    subgraph Java_Middleware [The Data Migrator - Java Engine]
        JNI[Java Native Interface / JNI] -- "Metadata Extraction" --> Logic[Transformation Logic]
        Logic -- "SQL Adapter" --> JDBC[JDBC Driver]
    end

    subgraph Target_Persistence [GridOS Persistence Layer]
        PostGIS[(PostgreSQL / PostGIS)]
    end

    %% Connections
    Magik_Srv -- "Dynamic Collections" --> JNI
    JDBC -- "Record-Based Persistence" --> PostGIS

    %% Styles
    style VMDS fill:#f9f,stroke:#333
    style PostGIS fill:#00b2a9,color:#fff
    style Java_Middleware fill:#005da9,color:#fff
