---
title: "Open Brain Platform Education Engine"
description: "Automated enterprise monetization, entitlement, and environment provisioning system"
---

**Role:** Lead Architect & Full Stack Engineer

**Project:** [Open Brain Platform](../open-brain-platform/)

**Tech Stack:** Python, PostgreSQL, React, TypeScript, Redis

**Scope:** Architecture, Backend Systems, Database Design, Frontend Implementation

---

## Overview

The Open Brain Platform relied on manual sales operations to provision projects and environments for institutional clients. To scale the platform into higher education, I designed, architected, and built the Education Plan Engine — an automated enterprise monetization, entitlement, and environment provisioning system.

The core challenge was translating complex academic lifecycle rules — such as time-gated access, conditional seat recovery based on credit usage, template asset replication, and strict semester-end credit burning — into a reliable, distributed backend architecture.

---

## Architectural Highlights & Technical Execution

### 1. Concurrency-Safe Seat Allocation & Recovery Engine

Designed a transactional seat-management pipeline in PostgreSQL that handles high-concurrency student assignments and drop workflows safely.

- Implemented row-level pessimistic locking (`SELECT ... FOR UPDATE`) inside atomic transaction boundaries to prevent race conditions during bulk registration periods.
- Built state-dependent seat recovery logic enforcing strict business rules: seats can only be recycled if vacated within a primary grace period and if the student consumed under 50 credits.

### 2. Time-Gated Dynamic Access Control (ACL)

Extended the core project ACL system to support three granular project states: Admin (Faculty), Member (Active Student), and Pending (Pre-Start Date Student).

- Built time-aware access logic that gates environment access until course start dates.
- Engineered a lazy activation flow triggered on platform login that dynamically converts Pending enrollments to Member status without requiring broad bulk-database update sweeps.

### 3. Distributed Background Tasks & Idempotent Credit Depreciation

Developed automated background cron services to execute semester-end teardowns, revoking access and burning unspent credits automatically.

- Secured background jobs using Redis distributed locks to guarantee execution idempotency across horizontally scaled Python application instances.

### 4. Template-to-Student Asset Synchronization

Created cross-project syncing services that clone faculty template projects, isolated workflows, and Jupyter Notebooks into newly allocated student workspace environments upon seat assignment.

---

## Business Impact & Results

- **Eliminated Operational Bottlenecks:** Fully automated environment setup and project provisioning, removing manual intervention entirely for sales and engineering teams.
- **Increased Platform Revenue:** Streamlined institutional onboarding, directly driving higher course purchase volume and faster semester rollouts.
- **Flawless Financial & Access Integrity:** Achieved zero concurrency failures during peak registration periods and guaranteed accurate credit tracking across all institutional accounts.
