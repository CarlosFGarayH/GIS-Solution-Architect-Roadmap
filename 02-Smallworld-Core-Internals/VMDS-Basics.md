# Smallworld Core: VMDS Fundamentals

### What is VMDS?
The **Version Managed Data Store** is the heart of Smallworld. Unlike SQL databases, it is designed for long-term transactions and complex network topologies.

### Architect's Take: Why it matters
As a Solution Architect, I must understand that VMDS handles concurrency through **Alternatives**. 

### Key Concept: Alternatives
- They allow multiple users to edit the same area without locking the "Top" (Production) database.
- Integration services (Java/GridOS) must be aware of which alternative they are reading from to ensure data consistency.
