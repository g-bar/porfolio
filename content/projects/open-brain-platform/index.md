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
