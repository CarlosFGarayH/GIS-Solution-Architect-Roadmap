# System Context Diagram (Level 1)

This diagram represents how the **Smallworld GIS** interacts with other enterprise systems in a standard GE Vernova environment.

```mermaid
graph TD
    User((Field Engineer)) -->|Updates Assets| SW[Smallworld GIS]
    SW -->|Sync Data| SAP[SAP ERP]
    SW -->|Export Network| GridOS[GE GridOS]
    SW -->|Log Events| DB[(VMDS Database)]
    
    style SW fill:#005da9,color:#fff,stroke-width:2px
    style GridOS fill:#00b2a9,color:#fff
