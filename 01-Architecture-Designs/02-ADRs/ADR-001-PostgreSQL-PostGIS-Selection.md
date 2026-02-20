# ADR 001: Selection of PostgreSQL/PostGIS as Target for VMDS Migration

## Status
**Accepted**
**Date:** 2026-02-20
**Author:** Carlos Garay

## Context
Traditional GE Smallworld VMDS stores data in proprietary 4kb binary blocks (SWMFS). This creates a "data silo" where GIS information is inaccessible to standard enterprise tools (BI, Web Apps, Cloud Services) without Magik translation. 

To align with **GE Vernova’s GridOS Data Fabric** strategy, we need to transition to a cloud-native, record-based persistence layer. We evaluated three primary options:
1. **Oracle Spatial:** High cost, proprietary licensing.
2. **SQL Server:** Limited spatial support compared to GIS industry standards.
3. **PostgreSQL/PostGIS:** Open standard, high performance, and cloud-native.

## Decision
We will implement **PostgreSQL with the PostGIS extension** as the primary landing zone for the "Data Migrator" project (Phase 1).

### Justification:
- **Spatial Logic Parity:** PostGIS provides native spatial functions (`ST_Intersects`, `ST_Buffer`) that mirror Smallworld’s topological manifold logic.
- **Industry Standard:** It is the core database recommended in the GridOS roadmap for scalable GIS data access.
- **Cost-Efficiency:** Eliminates proprietary license overhead for cloud deployments (AWS RDS / Azure Database for PostgreSQL).
- **Data Integrity:** Support for the `UUID` data type allows us to preserve Smallworld Object IDs (OID pointers) during the migration process.

## Consequences
- **Positive:** GIS data becomes "democratized," allowing direct SQL access for GridOS applications.
- **Negative:** Hierarchical versioning (Smallworld Alternatives) is not native to SQL. 
- **Mitigation:** We will implement a custom **SQL Adapter** in Java (designed on Wednesday) to bridge the gap between VMDS versions and SQL records.
- **Risk:** Large network datasets will require partitioning and GIST index tuning to ensure sub-second performance.

## References
- GE Vernova VMDS Cloud Roadmap (2024-2026).
- Smallworld CASE Tool Reference Manual (Physical Model Analysis).
