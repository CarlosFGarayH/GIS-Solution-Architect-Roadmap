# CASE Tool Deep Dive: Architectural Abstraction Layer

Based on official documentation for Smallworld Core Spatial Technology 4.3.

## 🏗️ 1. The Metadata Engine
The CASE Tool operates on a dedicated partition (`case.ds`) managed by `sw_case_manager`. 
- **Architect's Insight:** This separation allows versioning of the schema itself. We can test "Hard Changes" in a Case Alternative without locking the production GIS database.

## 🧬 2. Logical vs. Physical Mapping Analysis
| Layer | Entity | Responsibility |
| :--- | :--- | :--- |
| **Logical** | `dd_table` | Defines Magik methods, triggers, and validators. |
| **Physical** | `ds_collection` | Manages byte-level storage in VMDS files. |

### Key Architectural Discovery: The Join Field
Unlike SQL Foreign Keys, Smallworld Joins are **Object Pointers**. 
- **Internal implementation:** Uses an "Intermediate Table" for N:M or optional relationships.
- **Migration Challenge:** To move this to PostgreSQL, we must resolve these pointers into relational IDs.

## 🔄 3. Data Model Evolution & "Hard Changes"
When applying a design, the system categorizes changes:
1. **Soft:** Metadata only (low impact).
2. **Hard:** Physical record change. Requires table recreation and data copying via **Conversion Scripts**.
3. **Semi-hard:** Adding geometry to existing objects.

> **Solution Architect Note:** For the "Data Migrator" project (Phase 1), I must analyze the `merge_table_changes()` method logic described in the documentation. This Magik core method is the blueprint for how we will handle data mapping in Java.

## 🛠️ 4. Quality Manager Integration
The documentation highlights the `info_flag` class. 
- **Strategic Use:** We can add "flags" to any object by inheriting from `info_flag_owner_mixin`. This is essential for data validation during automated migrations from VMDS to SQL.
