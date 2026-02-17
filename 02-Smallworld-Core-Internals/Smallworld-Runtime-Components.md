# Smallworld GNM Runtime Components

Based on the official **Smallworld Geo Network Management (5.3.5)** deployment guidelines, these are the core elements that sustain an enterprise GIS solution.

## 🏗️ Core Server Components

### 1. Datastore Server (swmfs)
*   **Role:** The foundation of the Smallworld architecture.
*   **Function:** It is a high-performance database server that supports massive concurrent user write access.
*   **Architect's Note:** Since it manages data persistence, it is the most critical component for system stability.

### 2. Job Server
*   **Role:** Background processing engine.
*   **Function:** Handles automated and heavy-duty tasks such as **Merge and Post** operations (synchronizing changes from child alternatives to the top-level database).
*   **Benefit:** Offloading these tasks from the main session ensures the UI remains responsive for professional users.

### 3. GeoSpatial Analysis (GSA) Server
*   **Role:** Advanced analytics engine.
*   **Function:** Provides high-level spatial analysis capabilities. It has desktop, web, and server components to serve different types of users.

---

## 💾 Data Services & Infrastructure

### Storage Performance (Critical)
The documentation emphasizes the requirement for **Low Latency Storage**. 
*   **Requirement:** High-speed file systems for data persistence.
*   **Infrastructure Insight:** When deploying on Cloud (AWS/Azure), selecting the right storage tier (e.g., **SSD / Premium SSD**) is mandatory. Using standard HDD will lead to bottlenecks in `swmfs` performance.

### Modern Deployment: Kubernetes Cluster
Modern Smallworld GNM environments leverage **Kubernetes (K8s)** to host:
*   GE Vernova Web Applications.
*   GIS Adapter Servers.
*   GSS Services.

> **Architectural Takeaway:** Transitioning from standalone VM servers to Kubernetes allows for better scalability and reliability, aligning GIS with modern Cloud-Native IT standards.
