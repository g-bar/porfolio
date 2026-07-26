---
title: "Education Platform"
description: "Course management module for the Open Brain Platform"
---

**Project:** [Open Brain Platform](../open-brain-platform/)

---

Designed and engineered the education platform feature end to end, including full frontend implementation. Built a course management module supporting Jupyter notebook distribution, automated workspace initialization, and institutional capacity control.

- **Data Modeling:** Engineered database schema additions in the Virtual Lab API (Institution, Seat, Seat_Allocation) to track purchased capacity, expiration dates, and student assignments.
- **State Logic:** Developed state-dependent capacity calculations to handle recoverable (early) versus unrecoverable (late) seat drops based on strict deadlines.
- **Automated Workflows:** Implemented bulk student provisioning, automated project creation with credit assignment, and a cron-based scheduling system for automated access and credit revocation at course end dates.
- **Stack:** Python, PostgreSQL, React, TypeScript
