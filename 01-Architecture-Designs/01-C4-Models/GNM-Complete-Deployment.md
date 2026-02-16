# GNM Complete Deployment Diagram

This diagram represents the "Complete" deployment architecture for Smallworld GNM as per GE Vernova official documentation.

```mermaid
graph TD
    subgraph External_Users [External Users]
        Web[Web & Mobile Browsers]
        VDI[Desktop VDI: Citrix/Azure]
    end

    subgraph Security_Layer [Security Layer]
        FW[Firewall / DMZ]
        Auth[LDAP / Corporate Authentication]
    end

    subgraph Kubernetes_Cluster [Kubernetes Cluster]
        GSS[GSS Services]
        Adapter[GIS Adapter Server]
        WebApp[GE Vernova Web Apps]
    end

    subgraph Core_Servers [Core Servers]
        SWMFS[Datastore Server - swmfs]
        JobServer[Job Server: Merge/Post]
        GSA[GeoSpatial Analysis Server]
    end

    subgraph Data_Services [Data Services]
        FS[File Systems / Persistence]
        DB[(Oracle / PostgreSQL)]
    end

    %% Connections
    Web --> FW
    FW --> Auth
    Auth --> Kubernetes_Cluster
    VDI --> Core_Servers
    Kubernetes_Cluster --> Core_Servers
    Core_Servers --> Data_Services
