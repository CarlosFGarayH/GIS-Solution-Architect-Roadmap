# Core Dive: Programmatic Metadata Discovery (Real Data Trace)
**Date:** 2026-02-24
**Target Collection:** `min_road` (Roads)

## 🔍 Metadata Extraction Results
I successfully executed a Magik discovery script to interogate the `:gis` database. Below is the technical breakdown of the `min_road` collection:

### Field Mapping Analysis
| Smallworld Field | Magik Core Type | Mandatory? | Architect's Implementation Strategy |
| :--- | :--- | :--- | :--- |
| `min_road_id` | `sys_id` | True | Map to `UUID` in PostgreSQL to preserve GIS pointers. |
| `name` | `unset` (Primitive) | True | Map to `VARCHAR(n)`. Requires fetching `f.type.size`. |
| `road_type` | `road_type` | True | **Challenge:** User-defined type. Java must resolve the underlying `storage_class`. |
| `rwo_id` | `gis_id` | True | Primary link to PostGIS geometry records. |
| `ds!version` | `ds_vstamp` | True | Map to `TIMESTAMP` or `INTEGER` for version control. |

## 🏛️ Architect's Perspective: The "Unset" Type & Custom Schemas
During extraction, the `name` field returned an `unset` type name. 
- **Finding:** This indicates an anonymous primitive type. 
- **Solution:** The "SQL Adapter" in Java must be programmed to handle `unset` symbols by querying the `.type.storage_class` instead of just the `.type.name`.

### Strategic Alignment with GridOS
GE Vernova's **VMDS Cloud** roadmap (Slide 29) requires replacing "block persistence" with "record persistence." 
The presence of `rwo_id` and `ds!version` confirms that our PostgreSQL schema must include these metadata columns to support the **Version Manager** logic within the Java Orchestrator.

---
**Next Step (Wednesday):** Java Metadata API - Implementing a "Type Resolver" to handle the `road_type` and `carriage_type` custom enumerations.
