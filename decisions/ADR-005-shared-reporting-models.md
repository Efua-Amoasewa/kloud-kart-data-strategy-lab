# ADR-005: Use Shared Curated Reporting Models for Nana and Finance

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Kloud Kart leadership, with Finance and Operations responsible for agreeing business definitions

## Context

Nana and Finance currently calculate revenue differently, resulting in reports that do not match. This creates extra reconciliation work and makes it difficult for management and investors to rely on the figures.

A warehouse alone will not solve this problem if each department continues using its own definitions. The company needs shared definitions for important business measures.

## Decision

Kloud Kart will build shared, curated reporting models in the warehouse for important business measures, starting with revenue, using business rules that Finance and Operations agree. The Analytics Engineer will implement those agreed definitions as reusable models, so both departments use the same logic.

## Alternatives considered

### Alternative A: Allow each department to maintain its own reporting calculations

- **How it would work:** Nana and Finance would continue building separate spreadsheets or queries based on their individual reporting needs.
- **Why it is attractive:** Each department would retain flexibility and could make changes without waiting for a central reporting process.
- **Why rejected:** This would preserve the current problem of inconsistent figures. It would also continue creating duplicated work and make it harder to establish a trusted company-wide view of performance.

### Alternative B: Let the Data Engineering team define revenue independently

- **How it would work:** The technical team would choose a revenue formula and implement it in the warehouse without requiring Finance and Operations to agree first.
- **Why it is attractive:** It could speed up technical implementation and create one calculation quickly.
- **Why rejected:** Revenue is a business concept, not just a technical calculation. Finance and Operations must agree on the rules, such as how refunds, cancellations and order dates are treated. The technical team should implement the agreed definition rather than make business decisions on behalf of those departments.

## Consequences

- **What this buys:**
  - One agreed calculation for important business measures.
  - Reduced disagreement between Nana and Finance.
  - Less manual reconciliation and duplicated reporting work.
  - More confidence in figures used for management and investor discussions.
- **What this costs:**
  - Time for Finance and Operations to agree on definitions.
  - Work for the Analytics Engineer to implement and maintain the reporting models.
  - Documentation and testing to ensure that the models follow the agreed rules.
- **What it costs the client if I am wrong:** If the agreed definitions are incorrect or do not reflect the business, both departments may consistently report the same wrong figures. Agreement between departments does not automatically prove accuracy, so the figures must also be checked against transaction records and business rules.
- **What would make me revisit this:** If the business changes its revenue recognition rules, introduces new sales channels or expands into Nigeria with different reporting requirements, the definitions should be reviewed and updated through a documented decision process.

## What this survives

If the company expands into Nigeria or adds more departments, shared reporting models can be extended with additional measures and country-specific rules. The principle of using agreed definitions remains important as reporting needs grow.
