---
title: "Open Brain Platform"
description: "Web-based environment for the simulation of neuronal circuits"
---

**Role:** Full Stack Developer

**Scope:** Architected and implemented features across the entire technology stack in collaboration with a development team.

---

A web-based environment for the simulation of neuronal circuits. The system utilizes gated workspaces, organized as virtual labs and projects, to control access to specific workflows and datasets, including morphologies, electrical models, and neuronal circuits. An integrated AI agent allows users to query data and automate the configuration and execution of simulations.

---

## Platform Architecture

The platform is composed of four primary systems:

### Core Web App

The primary frontend user interface.

**Stack:** Next.js, React, TypeScript

### EntityCore

The central data repository providing models and API access to the core datasets.

**Stack:** Python, PostgreSQL

### Obi-One

The job orchestration service for executing scientific simulation code.

**Stack:** Python (FastAPI), Pydantic

### Virtual Lab API

The access control and data management API for workspaces and projects.

**Stack:** Python, PostgreSQL

---

## Key Contributions

### Automated Python-to-UI Framework (Lead Developer)

Engineered a system to automatically generate frontend user interfaces from backend Pydantic schemas. Defined specifications mapping schemas (JSONSchema) to UI behavior and implemented the core UI framework and components.

- **Impact:** Accelerated new workflow implementation, increased system reliability, and reduced bug incidence.
- **Stack:** Python, Pydantic, JSONSchema, React, TypeScript

### AI-to-UI Communication Interface

Directed the technical specification and frontend execution for AI integration. Collaborated with the machine learning team to engineer a system enabling the AI chat agent to dynamically populate forms and configure system parameters based on user interactions.

- **Stack:** React, TypeScript

### Education Platform Architecture

Designed and engineered the education platform feature end to end, including full frontend implementation. Built a course management module supporting Jupyter notebook distribution, automated workspace initialization, and institutional capacity control.

- **Data Modeling:** Engineered database schema additions in the Virtual Lab API (Institution, Seat, Seat_Allocation) to track purchased capacity, expiration dates, and student assignments.
- **State Logic:** Developed state-dependent capacity calculations to handle recoverable (early) versus unrecoverable (late) seat drops based on strict deadlines.
- **Automated Workflows:** Implemented bulk student provisioning, automated project creation with credit assignment, and a cron-based scheduling system for automated access and credit revocation at course end dates.
- **Stack:** Python, PostgreSQL, React, TypeScript
