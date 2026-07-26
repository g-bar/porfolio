---
title: "Open Brain Platform"
description: "Web-based environment for the simulation of neuronal circuits"
---
**Site:** <a href="https://www.openbraininstitute.org/" target="_blank">openbraininstitute.org</a>

**Role:** Full Stack Developer

**Scope:** Architected and implemented features across the entire technology stack in collaboration with a development team.


---

A web-based environment for the simulation of neuronal circuits. The system utilizes gated workspaces, organized as virtual labs and projects, to control access to specific workflows and datasets, including morphologies, electrical models, and neuronal circuits. An integrated AI agent allows users to query data and automate the configuration and execution of simulations.

---

## Platform Architecture

The platform is composed of four primary systems:

### Core Web App

The primary frontend user interface.

**Stack:** Next.js, React, TypeScript — <a href="https://github.com/openbraininstitute/core-web-app" target="_blank"><img src="https://img.shields.io/badge/GitHub-core--web--app-181717?logo=github" style="display:inline;vertical-align:middle;height:16px;"></a>

### EntityCore

The central data repository providing models and API access to the core datasets.

**Stack:** Python, PostgreSQL — <a href="https://github.com/openbraininstitute/entitycore" target="_blank"><img src="https://img.shields.io/badge/GitHub-entitycore-181717?logo=github" style="display:inline;vertical-align:middle;height:16px;"></a>

### Obi-One

The job orchestration service for executing scientific simulation code.

**Stack:** Python (FastAPI), Pydantic — <a href="https://github.com/openbraininstitute/obi-one" target="_blank"><img src="https://img.shields.io/badge/GitHub-obi--one-181717?logo=github" style="display:inline;vertical-align:middle;height:16px;"></a>

### Virtual Lab API

The access control and data management API for workspaces and projects.

**Stack:** Python, PostgreSQL — <a href="https://github.com/openbraininstitute/virtual-lab-api" target="_blank"><img src="https://img.shields.io/badge/GitHub-virtual--lab--api-181717?logo=github" style="display:inline;vertical-align:middle;height:16px;"></a>

---

## Key Contributions

### [Dynamic UI Generation Framework](../python-to-ui-framework/)

Led the standardization of a dynamic UI pipeline directing a cross-functional team of 4 engineers, decoupling UI logic from workflow parameters and achieving organization-wide adoption.

### [Open Brain Platform Education Engine](../education-engine/)

Designed and built an automated enterprise monetization, entitlement, and environment provisioning system for institutional clients, including concurrency-safe seat allocation, time-gated access control, and distributed background tasks.
