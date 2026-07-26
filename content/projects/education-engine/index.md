# Open Brain Platform Education Engine

**Role:** Lead Architect & Full Stack Engineer

**Project:** [Open Brain Platform](../open-brain-platform/)

**Tech Stack:** Python, PostgreSQL, React, TypeScript, Redis

**Scope:** Architecture, Backend Systems, Database Design, Frontend Implementation

---

## Overview

Open Brain is a collaborative AI platform where users work inside isolated virtual lab environments. Each workspace is backed by a **Project**, which acts as the platform's security boundary and contains datasets, Jupyter notebooks, workflows, experiment results, and other project assets.

Projects are protected by an ACL system with two primary roles:

* **Admin** — Can manage the project and its members.
* **Member** — Can access and collaborate within the project.

In the standard commercial model, customers subscribed to a plan, created projects, invited collaborators, and purchased compute credits that could be consumed by members of those projects.

The goal of this project was to extend that model for universities.

---

## The Education Model

Higher education introduced a completely different set of requirements.

Instead of users creating their own projects, institutions purchase an **Education Plan** with a fixed number of student seats. Faculty members own a master course project containing notebooks, datasets, workflows, and other teaching material.

Students don't work directly inside the faculty project. When they're assigned a seat, the platform automatically provisions an isolated workspace by cloning the course template into a new project owned by that student.

This model introduced several new concepts:

* **Education Plans** define how many students can enroll.
* **Seats** represent individual student licenses.
* **Enrollments** track which student owns a seat and their lifecycle throughout the semester.
* **Template Projects** provide the source material used to provision every student workspace.

The platform also needed to enforce academic policies such as course start dates, enrollment windows, credit consumption limits, seat recovery, and automatic semester expiration.

I designed and built the Education Engine to manage this entire lifecycle while integrating cleanly with the existing platform architecture.

---

## Concurrency-Safe Seat Allocation

Assigning a student to a course involved much more than inserting an enrollment record.

Each enrollment needed to:

* Allocate an available seat from the Education Plan.
* Create the student's enrollment.
* Provision a new project from the faculty template.
* Grant the correct project permissions.
* Initialize compute credits and entitlement metadata.

Because registration periods could generate hundreds of concurrent enrollment requests, these operations had to remain consistent even under heavy load.

I implemented the enrollment pipeline as a single PostgreSQL transaction. Critical rows were protected using pessimistic row locking (`SELECT ... FOR UPDATE`), ensuring seat allocation remained serialized while allowing unrelated enrollments to proceed concurrently.

This guaranteed that seat counts, enrollments, project memberships, and provisioning state could never become inconsistent due to race conditions.

Seat recovery introduced additional business logic. If a student withdrew during a configurable grace period and had consumed fewer than 50 compute credits, their seat was automatically returned to the available pool. Otherwise, the seat remained permanently consumed for the remainder of the semester.

---

## Time-Based Access Control

The existing ACL model supported project administrators and members, but educational workflows required permissions to change automatically over time.

I extended the authorization model with a third state:

* **Admin** — Faculty members.
* **Pending** — Students enrolled before the course begins.
* **Member** — Active students.

Rather than running scheduled database migrations when courses started, the platform evaluates enrollment dates whenever a student authenticates. If the course has started, the user's enrollment is promoted from **Pending** to **Member** and access is granted immediately.

This lazy activation approach eliminated unnecessary bulk updates while ensuring permissions always reflected the current academic schedule.

---

## Distributed Background Processing

Academic environments have a well-defined lifecycle. At the end of each semester the platform must revoke project access, expire unused credits, and close enrollments automatically.

I implemented a suite of background workers responsible for these operations.

Since the application could run across multiple Python instances, every scheduled task was coordinated using Redis distributed locks to prevent duplicate execution. Each worker was also designed to be idempotent, allowing jobs to be retried safely without corrupting platform state or credit balances.

---

## Automated Workspace Provisioning

Every student receives an independent working environment while faculty maintain a single source of truth for course content.

To support this, I built provisioning services that clone faculty template projects into new student projects during enrollment. The cloning process copies notebooks, workflows, datasets, and project configuration while preserving complete isolation between student workspaces.

This approach ensured every student started with an identical environment without risking changes to the original teaching materials or other students' work.

---

## Results

The Education Engine transformed a manual onboarding process into a fully automated platform capability.

Key outcomes included:

* Automated student enrollment and workspace provisioning.
* Reliable seat allocation during peak registration periods.
* Time-aware access control with no operational intervention.
* Automated semester cleanup and credit lifecycle management.
* A scalable architecture that enabled institutional deployments without increasing operational complexity.
