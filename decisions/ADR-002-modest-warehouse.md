# ADR-002: Use a Modest Data Warehouse on Managed PostgreSQL for Shared Reporting

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Kloud Kart leadership, with Nana Adjei as business sponsor

## Context

Kloud Kart has approximately 40GB of mostly structured MySQL data and needs reliable answers to known business questions such as revenue, orders and inventory performance.

Nana and Finance currently produce different revenue figures. The company needs a shared reporting environment with cleaned and consistently defined data.

The company has only two data hires available this financial year and does not currently have a machine-learning requirement or a demonstrated need to store large amounts of varied data.

The developer wants to "just buy Snowflake or BigQuery", and Finance is concerned about cost. The board needs a decision, not an open question.

## Decision

Kloud Kart will implement a modest data warehouse on a managed PostgreSQL service as its central reporting environment, loaded from the read replica for both Nana and Finance. Kloud Kart will not introduce a lakehouse or complex data lake, and will move to BigQuery or Snowflake only if Q1 quotes show a clearly lower three-year cost.

## Alternatives considered

### Alternative A: Build a data lake or lakehouse

- **How it would work:** Store raw and varied data in low-cost object storage, or introduce a lakehouse platform that combines data-lake storage with warehouse-like capabilities.
- **Why it is attractive:** This could support more varied data, flexible analysis and future machine-learning workloads.
- **Why rejected:** Kloud Kart's current data is mostly structured, its immediate reporting questions are known, and it has no immediate machine-learning requirement. A lake or lakehouse would introduce additional governance, tooling and operational complexity that the two-person team may struggle to maintain.

### Alternative B: Continue reporting directly from the read replica without a warehouse

- **How it would work:** Nana and Finance would query the replica directly or maintain separate reporting queries and spreadsheets.
- **Why it is attractive:** It avoids the initial cost of a separate analytical storage system.
- **Why rejected:** A replica is primarily a copy of operational data, not a curated reporting environment. Different users could continue applying different definitions and producing inconsistent results. Reporting queries could also place additional pressure on the replica.

### Alternative C: Buy Snowflake or BigQuery as the default

- **How it would work:** Use a pay-per-use cloud data warehouse, billed mainly by the amount of data each query processes or the compute time used.
- **Why it is attractive:** These platforms need little database administration, scale far beyond Kloud Kart's needs, and BigQuery's storage is very cheap at about GH₵0.25 per GB a month, so 40 GB costs about GH₵10 a month to store.
- **Why rejected as the default:** At 40 GB of mostly structured data, Kloud Kart does not need their scale. Usage-based billing makes monthly costs harder for Finance to predict, and the platforms are less familiar to a MySQL developer than PostgreSQL. They remain the alternative to beat: if Q1 quotes show a clearly lower three-year cost, including the effort to run them, the company should switch.

## Consequences

- **What this buys:**
  - A central place for cleaned and organised reporting data.
  - A shared reporting foundation for Nana and Finance.
  - A place to implement agreed business definitions and data quality checks.
  - A simpler architecture that better matches the company's current data and staffing capacity.
- **What this costs:**
  - An estimated GH₵760–1,890 a month for the managed PostgreSQL service, based on public list prices for a small instance (about GH₵590 a month for 2 processors and 4 GB of memory) plus storage at about GH₵1.50 per GB a month, converted at GH₵12.60 to US$1 (Deliverable 2, §6). At 40 GB, storage is a negligible part of this. Q1 quotes confirm the figure.
  - Data transfer, backup and monitoring costs.
  - Time to design and maintain the reporting structures.
  - Additional work to secure the warehouse and manage personal data appropriately.
- **What it costs the client if I am wrong:** If the warehouse is unnecessary or poorly sized, Kloud Kart may spend money maintaining a system that provides little value. At the estimated cost, the financial downside of a wrong choice is small next to two salaries; the larger cost would be staff time spent on migration. If the company avoids a shared reporting environment, inconsistent figures and manual reporting work may continue.
- **What would make me revisit this:** If Kloud Kart begins collecting substantial amounts of unstructured data, develops a genuine machine-learning requirement, or outgrows the proposed warehouse, the storage architecture should be reassessed.

## What this survives

If the company expands into Nigeria and its reporting requirements grow, the warehouse can be extended with additional reporting models and country-specific data. The company does not need to introduce a lakehouse simply because it expands.
