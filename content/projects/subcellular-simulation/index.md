---
title: "Subcellular Simulation Web App"
description: "System Architecture & Design for a molecular network simulation platform"
---

Repository: <a href="https://github.com/BlueBrain/BlueNaaS-Subcellular" target="_blank"><img src="https://img.shields.io/badge/GitHub-BlueBrain/BlueNaaS--Subcellular-181717?logo=github" style="display:inline;vertical-align:middle;height:16px;"></a> — <small><em>no longer maintained</em></small>

![Subcellular Simulation](../../../images/subcellular-simulation.png)

**Role:** Main Architect & Maintainer



A web application enabling scientists to define mathematical models and execute high-throughput simulations of molecular networks.

---

## Technology Stack

- **Frontend:** Vue.js
- **Backend:** Python
- **Database:** PostgreSQL (migrated from MongoDB)
- **Task Queue:** Redis Queue (migrated from custom implementation)

---

## System Architecture & Core Components

### Asynchronous Simulation Engine

Users define custom molecular models via the Vue.js interface. Simulation execution is decoupled from the main application thread using a distributed job queue. The queue architecture was migrated from a custom implementation to Redis Queue to guarantee fault tolerance and handle concurrent, resource-intensive execution efficiently.

### High-Volume Data Pipeline

Each simulation yields up to 10 million discrete data points. Data layer migrated from MongoDB to PostgreSQL to leverage advanced querying, transactional integrity, and native data aggregation functions.

### Dynamic Aggregation Layer

Designed a PostgreSQL-based aggregation system to compute statistical summaries (min, max, averages). Aggregations operate at dynamic data scales (e.g., 100, 1,000, 10,000 points). This layer minimizes network payload and browser memory consumption, allowing the frontend to render massive datasets without degradation.

### Real-Time Visualization Interface

Vue.js UI consumes the pre-aggregated data streams. Enables low-latency, real-time visualization of ongoing simulations while maintaining high overall system throughput.
