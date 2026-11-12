# ADR-003: Load the Warehouse Nightly with Data Minimisation and Explicit Deletion Capture

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Kloud Kart leadership, with the Data Engineer responsible for implementation

## Context

Kloud Kart processes customer information, including names, telephone numbers and addresses. Marketing currently exports customer lists without tracking where copies are stored.

The company also has an existing Data Protection Commission complaint concerning deleted customer data, with a 90-day response deadline. When a customer is deleted, we assume the shop database removes the row outright (a "hard delete"); this has not been verified.

The warehouse must contain only the personal information necessary for its reporting purposes, and a customer deleted from the shop must also disappear from the warehouse. A load that only picks up new and changed records cannot see a row that no longer exists, so deletions need their own mechanism.

## Decision

Each night, Kloud Kart will fully reload the small, minimised customer-related tables from the read replica and load orders incrementally, carrying only the fields approved reporting needs and leaving out unnecessary personal information. A deletion log on the shop database will record every customer deletion, and the nightly load will apply it to the incrementally loaded tables and keep it as evidence of what was removed.

## Alternatives considered

### Alternative A: Incremental loading of new and changed records only

- **How it would work:** Each night, copy only rows created or updated since the last load, identified by a "last updated" timestamp.
- **Why it is attractive:** It moves the least data, finishes quickly and scales well as orders grow.
- **Why rejected:** It cannot detect hard deletes. A deleted customer simply stops appearing in the source, so their record would remain in the warehouse indefinitely. This would break the deletion promise in the plan and weaken the response to the Data Protection Commission.

### Alternative B: ELT with raw personal data loaded first

- **How it would work:** Load raw source data into the warehouse or a raw storage area first, then perform transformations and remove unnecessary personal information afterwards.
- **Why it is attractive:** It preserves more original data and allows transformations to be rebuilt later.
- **Why rejected:** It creates an additional location containing personal data before unnecessary fields are removed. This increases the number of copies that must be secured, inventoried and considered when handling deletion requests.

## Consequences

- **What this buys:**
  - Deletions reach the warehouse in two independent ways: the nightly full reload of customer tables, and the deletion log.
  - A dated record of every deletion applied, which supports the complaint response.
  - Reduced exposure of personal information in the warehouse.
  - Efficient loading of the large, fast-growing orders table.
  - A better foundation for demonstrating compliance with Ghana's Data Protection Act, 2012 (Act 843).
- **What this costs:**
  - A small change to the shop database: a deletion log table, filled automatically whenever a customer is deleted.
  - Nightly full reloads of the minimised customer tables, which is modest at the current size of about 300,000 customers.
  - Documentation of where personal data is stored, who can access it and how it is removed.
  - Secure handling of personal data on the read replica, which still contains a full copy of the operational database.
- **What it costs the client if I am wrong:** If deletions are missed, personal information may remain in the warehouse after it has been deleted from the shop. This would make it difficult for Kloud Kart to demonstrate that it has handled the complaint properly and met its data protection obligations. Copies outside the pipeline, such as spreadsheets, email attachments and backups, are not covered by this mechanism and are tracked in the Customer Data Register instead.
- **What would make me revisit this:** If the customer tables grow too large to reload each night, the company should switch them to incremental loading and rely on the deletion log, or adopt change data capture from the database's own change history. If reporting genuinely requires more personal information, the purpose and lawful basis must be assessed and documented before those fields are added.

## What this survives

As the customer base grows and Nigeria adds customer records, the orders table continues to load incrementally, and the deletion log keeps working at any size. The full reload of customer tables is the part to review first under growth, and the fallback (incremental loading with the deletion log) is already designed.
