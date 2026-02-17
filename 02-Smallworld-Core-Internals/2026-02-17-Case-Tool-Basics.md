# CASE Tool: Architectural Foundations & Object Mapping
**Date:** 2026-02-17
**References:** 
- CASE Tool Tutorial (P. 3-11)
- CASE Tool Reference (P. 1-4, 3-3)
- Delivering Data Model Updates (P. 6)

## 🌐 1. Global Context: The Data Lifecycle
After analyzing the core documentation suite, I have identified the strategic flow of GIS data management in Smallworld:

1.  **Isolation:** Schema design happens in the `case` partition, isolated from production data.
2.  **Abstractions:** A `Case Object` acts as a blueprint that eventually becomes a `dd_table` (Data Dictionary Table).
3.  **Evolution:** Structural changes are versioned. "Hard changes" (physical shifts) generate conversion scripts to maintain integrity across alternatives.

## 🔍 2. Technical Observations (Deep Dive)

### A. The Object Editor (GUI to Core mapping)
From the Tutorial, I analyzed the definition of a `road` asset:
- **Naming Convention:** Internal name (`road`) for Magik/Java vs. External name (`Road`) for UI.
- **Physical Precision:** Assets use specific types like `ds_charci_vec(20)`. 
- **Architect's Insight:** To maintain parity in my **Phase 1 (Data Migrator)**, the PostgreSQL target must mirror these constraints (e.g., using `VARCHAR(20)`). Any mismatch here could lead to data truncation during migration.

### B. Metadata Extraction Strategy
The Reference manual confirms that a `case_object` maps directly to a `dd_table`.
- **Strategic Impact:** For an automated "Data Migrator," the Java code should not hard-code table names. Instead, it must programmatically query the `dd_table` metadata to discover asset structures dynamically.

## 🏛️ 3. Architect's Perspective on Migration
Smallworld's ability to treat PostgreSQL as an "External Dataset" (via the *Adding External Tables* manual) is the cornerstone for my roadmap. Understanding how Smallworld resolves **Joins** as object pointers rather than standard Foreign Keys will be the primary challenge when replicating topology in PostGIS.

---

## 🛠️ Saturday Lab Preparation
- **Task:** Implement the `road` and `town` objects (Tutorial, Chapter 3).
- **Goal:** Verify if modifying a field from "Key: No" to "Key: Yes" triggers a "Hard Change" and analyze the generated Magik conversion logic.
