graph TD
    subgraph External_Users
        Web[Web & Mobile Browsers]
        VDI[Desktop VDI: Citrix/Azure]
    end

    subgraph Security_Layer
        FW[Firewall / DMZ]
        Auth[LDAP / Corporate Authentication]
    end

    subgraph Kubernetes_Cluster
        GSS[GSS Services]
        Adapter[GIS Adapter Server]
        WebApp[GE Vernova Web Apps]
    end

    subgraph Core_Servers
        SWMFS[Datastore Server - swmfs]
        JobServer[Job Server: Merge/Post]
        GSA[GeoSpatial Analysis Server]
    end

    subgraph Data_Services
        FS[File Systems / Persistence]
        DB[(Oracle / PostgreSQL)]
    end

    Web --> FW
    FW --> Auth
    Auth --> Kubernetes_Cluster
    VDI --> Core_Servers
    Kubernetes_Cluster --> Core_Servers
    Core_Servers --> Data_Services
