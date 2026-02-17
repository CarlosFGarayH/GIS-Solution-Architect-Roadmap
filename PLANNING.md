# 🗺️ Master Backlog - Phase 1: Data Architect (Integrated Core Study)
**Focus:** VMDS to PostgreSQL Migration & Deep Smallworld Internals.
**Core Docs:** CASE Tool Tutorial, CASE Tool Reference, Adding External Tables, Data Model Evolution, Quality Manager.

## 📅 Month 1: The Environment & Schema Foundations
*Goal: Master CASE Tool basics and initial DB mapping.*
- [x] **Week 1 (Feb 16):** Repo Setup & C4 Context.
    - *Tuesday Study:* [CASE Tool Tutorial] Chap 3: Simple road network.
    - *Saturday Lab:* Create "Road & Town" model in Smallworld.
- [ ] **Week 2 (Feb 23):** Advanced Modeling & Metadata.
    - *Tuesday Study:* [CASE Tool Reference] Chap 3: Case Entities details.
    - *Saturday Lab:* Extracting CASE metadata via Magik (Collections & Fields).
- [ ] **Week 3 (Mar 02):** Java Collections & Mapping Logic.
    - *Tuesday Study:* [CASE Tool Tutorial] Chap 6: Object and field properties.
    - *Saturday Lab:* Build Java Map structures to hold VMDS metadata.
- [ ] **Week 4 (Mar 09):** SQL Schema Generation.
    - *Tuesday Study:* [Adding External Tables] Chap 1-3: Reverse Engineering Basics.
    - *Saturday Lab:* First "Hello World" Migration (Extract 1 Smallworld table to SQL).

## 📅 Month 2: Deep Extraction & External DBs
*Goal: Understand how Smallworld interacts with SQL (PostgreSQL).*
- [ ] **Week 1:** Mapping Smallworld Joins to SQL FKs.
    - *Tuesday Study:* [CASE Tool Tutorial] Chap 8-10: Join Relationships.
- [ ] **Week 2:** Handling External Tables.
    - *Tuesday Study:* [Adding External Tables] Chap 5: Joins involving external objects.
- [ ] **Week 3:** Spatial Data Fundamentals.
    - *Tuesday Study:* [CASE Tool Tutorial] Chap 19: Geometry field mapping.
- [ ] **Week 4:** Multi-threading for High-Volume Extraction.
    - *Tuesday Study:* [CASE Tool Reference] Chap 4: The Apply Operation (Performance context).

## 📅 Month 3: Connectivity & Topology Internals
*Goal: Replicate the Smallworld network logic in PostGIS.*
- [ ] **Week 1:** Connectivity Sets.
    - *Tuesday Study:* [CASE Tool Tutorial] Chap 16: Multiple geometry relationships.
- [ ] **Week 2:** Manifolds and Rules.
    - *Tuesday Study:* [CASE Tool Reference] Chap 20: Default and explicit manifold rules.
- [ ] **Week 3:** Topology Replication in PostGIS.
    - *Tuesday Study:* [Data Model Evolution] Chap 3: The Merge operation (Topology impact).
- [ ] **Week 4:** Project 1 Alpha Release.

## 📅 Month 4: Evolution & Versioning
*Goal: Manage data changes without losing integrity.*
- [ ] **Week 1:** Hard vs Soft Changes.
    - *Tuesday Study:* [Data Model Evolution] Chap 4: Conversion scripts.
- [ ] **Week 2:** Handling Schema Updates in Java.
- [ ] **Week 3:** Automated Migration Testing.
- [ ] **Week 4:** Disaster Recovery Logic for GIS Data.

## 📅 Month 5: Quality Management & Validation
*Goal: Use the Quality Manager logic to validate the migrated data.*
- [ ] **Week 1:** Info Flags & QA.
    - *Tuesday Study:* [Quality Manager] Chap 1-3: Installation and Styles.
- [ ] **Week 2:** Writing Quality Check Routines.
    - *Tuesday Study:* [Quality Manager] Chap 5: Writing a quality check routine.
- [ ] **Week 3:** Validating SQL Data against VMDS Source.
- [ ] **Week 4:** Refactoring for Clean Architecture.

## 📅 Month 6: Final Consolidation & Project Release
- [ ] **Week 1:** Performance Tuning (Indexing VMDS vs PostGIS).
- [ ] **Week 2:** Final Documentation (ADRs for all decisions).
- [ ] **Week 3:** Portfolio Review (C4 Level 1, 2, 3).
- [ ] **Week 4:** PROJECT 1 COMPLETION: The Data Migrator.
