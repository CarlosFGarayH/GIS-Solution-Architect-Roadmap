# Core Dive: Programmatic Metadata Discovery (Real Data Trace)
**Date:** 2026-02-24
**Focus:** Final Metadata Trace for `min_road` Collection.

## 🔍 Discovery Results: Smallworld 5.3.5 Output
I have successfully executed the `metadata_discovery.magik` script. The trace revealed the following physical structure for the Road assets:

### Metadata Trace Summary
| FIELD | CORE TYPE | PHYSICAL STORAGE | MANDATORY |
| :--- | :--- | :--- | :--- |
| `min_road_id` | `sys_id` | `ds_uint` | True |
| `name` | `primitive_unset` | `ds_charci` | True |
| `carriage_type` | `carriage_type` | `ds_uint` | True |
| `road_type` | `road_type` | `ds_uint` | True |
| `rwo_id` | `gis_id` | `ds_uint` | True |
| `ds!version` | `ds_vstamp` | `ds_vstamp` | True |

## 🏛️ Architect's Perspective: The Transformation Logic
Based on this trace, I have established the **Type Mapping Strategy** for the Java SQL Adapter:

1. **Numeric Parity:** `ds_uint` fields will be migrated as `BIGINT` or `INTEGER` in PostgreSQL.
2. **String Handling:** `ds_charci` (Case Insensitive) maps directly to `VARCHAR` in SQL.
3. **Integrity Enforcement:** Since all fields are `REQ: True`, the PostgreSQL schema will implement `NOT NULL` constraints across all columns to maintain 100% parity with the VMDS source.
4. **Identity Preservation:** The `rwo_id` and `min_road_id` are both physical unsigned integers. I will preserve these values to ensure that external GridOS applications can still reference the original Smallworld objects.

## 📁 Source Code Link
The fixed and tested Magik discovery script is archived here:
👉 [metadata_discovery.magik](https://github.com/CarlosFGarayH/The-Data-Migrator/blob/main/infrastructure/magik/metadata_discovery.magik)

---
**Next Step (Wednesday):** Java Day - Building the "Type Resolver" to automate the translation from these Magik symbols to Java Objects.
