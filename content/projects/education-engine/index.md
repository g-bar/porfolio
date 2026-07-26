# Case Study: Open Brain Platform Education Engine

**Role:** Lead Architect & Full Stack Engineer

**Tech Stack:** Python, PostgreSQL, React, TypeScript, Redis

**Scope:** Architecture, Backend Systems, Database Design, Frontend Implementation

---

## Overview

As the Open Brain Platform expanded into higher education, provisioning projects and student environments manually was becoming a bottleneck. I designed and built the Education Plan Engine to automate the entire lifecycle—from licensing and seat management to workspace provisioning, access control, and semester cleanup.

The challenge wasn't simply automating a workflow. Universities have rules around enrollment windows, seat reuse, credit consumption, course start dates, and semester expiration. The goal was to model those rules in a way that remained reliable under heavy concurrent usage while requiring minimal operational overhead.

---

## Concurrency-Safe Seat Allocation

One of the more interesting problems was seat management. During registration periods, hundreds of students could be assigned or removed from courses simultaneously, so the system needed to prevent double allocation and inconsistent seat counts.

I implemented the allocation pipeline using PostgreSQL transactions with row-level pessimistic locking (`SELECT ... FOR UPDATE`) to serialize updates only where necessary. Every seat assignment, release, and entitlement update executes inside a single transaction, ensuring the system always reaches a valid state even under concurrent requests.

Seat recovery also follows strict business rules. A seat can only be returned to the available pool if the student withdraws during a configurable grace period and has consumed fewer than 50 credits. Once those conditions are no longer met, the seat is permanently considered consumed for that semester.

---

## Time-Aware Access Control

The platform already supported project-level permissions, but educational environments required access to change automatically throughout the semester.

I extended the ACL system with three enrollment states:

* **Admin** for faculty members
* **Member** for active students
* **Pending** for students enrolled before the course begins

Rather than running scheduled jobs to activate every enrollment on the start date, I implemented a lazy activation model. When a student logs in, the platform evaluates the enrollment dates and promotes the user to an active member if the course has started. This keeps the database synchronized naturally while avoiding unnecessary bulk update jobs.

---

## Distributed Semester Automation

Academic environments also have a well-defined end of life. At the end of each semester the platform needs to revoke access, expire remaining credits, and clean up active enrollments automatically.

I built a set of background workers responsible for these lifecycle operations. Because multiple Python application instances could execute scheduled jobs simultaneously, each task is protected using Redis distributed locks. This guarantees that credit expiration and access revocation run exactly once, even in a horizontally scaled deployment.

Designing every background task to be idempotent also meant jobs could be safely retried without creating duplicate state changes or inconsistent account balances.

---

## Automated Student Workspace Provisioning

Each student receives an isolated workspace based on templates created by faculty members.

I built synchronization services that automatically clone project structures, workflows, Jupyter notebooks, and other course assets into new student environments whenever a seat is allocated. The provisioning process preserves the original template while giving every student an independent workspace that can evolve without affecting anyone else.

This eliminated manual setup while ensuring every student begins with an identical, reproducible environment.

---

## Results

The Education Plan Engine transformed what had been a manual operational process into a fully automated platform capability.

Some of the biggest improvements included:

* Automated institutional onboarding, workspace provisioning, and entitlement management.
* Reliable seat allocation during high-volume registration periods without concurrency conflicts.
* Consistent enforcement of licensing, access control, and credit consumption policies throughout the academic lifecycle.
* Reduced operational work for both engineering and sales teams by removing manual provisioning from the onboarding process.
* Enabled the platform to support larger university deployments without introducing additional operational complexity.
