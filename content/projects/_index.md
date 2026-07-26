---
title: "Projects"
description: "A snapshot of recent work"
---

## [Elementary](elementary-robotics/)

{{< img src="images/elementary-robotics.png" alt="Elementary" >}}

A web platform for launching, browsing, and reviewing automated product inspections using machine vision to detect defects on factory production lines. Architected a high-throughput TypeScript/React frontend capable of processing thousands of inspected items per hour, backed by a real-time Redis/WebSocket data pipeline. Built on Django and PostgreSQL with custom API endpoints and a seamless data layer bridging historical and live inspection results.

## [Subcellular Simulation Web App](subcellular-simulation/)

{{< img src="images/subcellular-simulation.png" alt="Subcellular Simulation" >}}

A web application enabling scientists to define mathematical models and execute high-throughput simulations of molecular networks. Architected on Python and PostgreSQL with a Redis Queue for fault-tolerant async execution, handling up to 10 million data points per simulation. A dynamic PostgreSQL aggregation layer minimizes frontend payload, enabling real-time visualization via a Vue.js interface without performance degradation.

## [Open Brain Platform](open-brain-platform/)

A web-based environment for the simulation of neuronal circuits. The system utilizes gated workspaces, organized as virtual labs and projects, to control access to specific workflows and datasets, including morphologies, electrical models, and neuronal circuits. An integrated AI agent allows users to query data and automate the configuration and execution of simulations.

## [Automated Python-to-UI Framework](python-to-ui-framework/)

Engineered a system to automatically generate frontend UIs from backend Pydantic schemas, accelerating workflow implementation and reducing bug incidence. Part of the Open Brain Platform.

## [Education Platform](education-platform/)

Designed and engineered end to end a course management module supporting Jupyter notebook distribution, automated workspace initialization, and institutional capacity control. Part of the Open Brain Platform.
