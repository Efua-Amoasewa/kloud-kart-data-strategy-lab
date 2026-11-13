# Kloud Kart Data Strategy Lab

A practical data strategy and governance package for Kloud Kart, a growing e-commerce business facing reporting inconsistency, customer-data compliance risk, and live-website performance problems.

This repository documents the diagnosis, the recommended architecture, the execution roadmap, and a lightweight operating tool for managing customer-data deletion requests and data-location tracking.

## Overview

Kloud Kart's challenge is not a lack of ambition; it is a lack of a safe, affordable, and well-governed foundation for reporting and customer-data handling. The project addresses three core issues:

- Customer-data governance and deletion risk
- Reporting workload conflicts with the live website
- Inconsistent revenue reporting and weak data foundations

The recommended path is intentionally modest and realistic: protect the live website, separate reporting from transactional workloads, establish a shared reporting model, and comply with data-protection obligations before investing in more advanced analytics.

## What this repository contains

This project is organized around a set of decision and planning documents:

- [Situational-diagnosis.md](./Situational-diagnosis.md) — identifies the business and technical risks, root causes, cost exposure, and prioritisation of actions.
- [recommendations.md](./recommendations.md) — presents the proposed architecture and the recommended data strategy.
- [roadmap.md](./roadmap.md) — outlines a 12-month delivery plan and measurable success criteria.
- [improvement-beyond-brief.md](./improvement-beyond-brief.md) — explains the extra deliverable: a Customer Data Register used to track data copies, deletion obligations, and compliance evidence.
- [customer-data-register.html](./customer-data-register.html) — a browser-based register for managing customer-data locations and deletion-request checklists.
- [decisions/](./decisions/) — architecture decision records (ADRs) covering the recommended foundations:
  - [ADR-001-read-replica.md](./decisions/ADR-001-read-replica.md)
  - [ADR-002-modest-warehouse.md](./decisions/ADR-002-modest-warehouse.md)
  - [ADR-003-incremental-etl.md](./decisions/ADR-003-incremental-etl.md)
  - [ADR-004-batch-and-live-stock.md](./decisions/ADR-004-batch-and-live-stock.md)
  - [ADR-005-shared-reporting-models.md](./decisions/ADR-005-shared-reporting-models.md)

## Recommended architecture at a glance

The core proposal is simple and practical:

- Keep the operational MySQL database for the live website and live stock checks
- Create a MySQL read replica for reporting extraction
- Use a nightly ETL process to load curated data into a modest warehouse
- Use a shared dashboard for Nana and Finance
- Keep only the data needed for reporting, and track data copies and deletions explicitly

This reduces operational risk while keeping costs manageable for a small team.

## Why this matters

Kloud Kart's current environment creates several problems:

- Reporting queries compete with live website traffic
- Revenue figures differ across teams
- Customer data may exist in unmanaged spreadsheets, exports, and backups
- The company has a pressing data-protection complaint and limited technical capacity
- Investor expectations are broader than the company's current operating maturity

The strategy avoids overbuilding. It starts with governance, reporting trust, and operational stability before moving into advanced analytics or real-time dashboards.

## Key decision themes

The strategy is guided by a few strong principles:

1. Protect the live website from reporting load
2. Prefer a modest, managed PostgreSQL warehouse over a more complex lakehouse or enterprise platform
3. Use data minimisation and explicit deletion tracking for personal data
4. Use daily batch reporting unless a real business need justifies real-time updates
5. Build a shared definition of revenue and reporting metrics across teams

## Quick start

### Read the documents in this order

1. [Situational-diagnosis.md](./Situational-diagnosis.md)
2. [recommendations.md](./recommendations.md)
3. [roadmap.md](./roadmap.md)
4. [kloud-kart-board-presentation.pptx](./kloud-kart-board-presentation.pptx)
5. [improvement-beyond-brief.md](./improvement-beyond-brief.md)

### Open the customer-data register

Open [customer-data-register.html](./customer-data-register.html) in a browser to view and use the register for data-copy tracking and deletion-request handling.

## Success criteria

The plan is successful when the business can demonstrate that:

- the website no longer suffers reporting-related slowdowns
- Nana and Finance use one agreed revenue definition
- customer-data copies are tracked and deletions are documented
- reporting is automated and shared across teams
- the architecture remains affordable and easy to operate for a small team

## Project status

This repository represents a strategic design and planning artefact rather than a production application. It is best treated as a decision-making and implementation blueprint for Kloud Kart's data foundation.

