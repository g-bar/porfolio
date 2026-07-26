---

title: "Dynamic UI Generation Framework"
description: "Dynamic UI generation architecture for workflow configuration pages"
----------------------------------------------------------------------------------

**Role:** Lead Engineer

**Project:** [Open Brain Platform](../open-brain-platform/)

**Technologies:** Python, FastAPI, Pydantic, TypeScript, JSON Schema, CI/CD

---

## Context

The product required workflow configuration pages to be generated dynamically from JSON schemas produced by a FastAPI backend. At the time, the implementation was heavily tied to a single workflow, making it difficult to extend, causing integration friction between backend and frontend teams, and leading to recurring regressions whenever new workflows were introduced.

---

## Architecture & Leadership

Proposed and led the redesign of the dynamic UI generation pipeline after aligning on the approach with the CTO. Coordinated a cross-functional team of four engineers (2 Backend, 2 Frontend) to establish a scalable, shared architecture.

### Schema Specification

Designed a JSON schema specification that mapped backend models to a standardized library of TypeScript UI components. The specification clearly defined component behavior, validation rules, and interaction patterns, giving both frontend and backend teams a common contract to build against.

### Backend Foundation

Built the core backend infrastructure in Python using Pydantic, ensuring schemas were strongly validated, consistent, and predictable across workflows.

### Reference Implementation

Implemented the first end-to-end workflow, covering both backend schema generation and frontend rendering. This served as the reference implementation for future workflow development across the platform.

### CI Integration

Added automated schema validation to the CI pipeline, allowing structural issues and breaking changes to be detected before deployment.

### Extension Process

Introduced a lightweight process for evolving the schema, making it straightforward for engineers to add new UI capabilities without breaking existing workflows or deviating from the standard.

---

## Results

* The schema specification became the standard approach across the engineering organization.
* Reduced coupling between workflow logic and UI implementation, making new workflows significantly easier to develop.
* Lowered the number of structural regressions and post-deployment fixes through standardized validation and automation.
