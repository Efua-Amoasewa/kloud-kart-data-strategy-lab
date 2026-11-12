# ADR-004: Use Daily Batch Reporting and Keep Live Stock in the Operational Database

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Kloud Kart leadership, with Operations and the Data Engineer

## Context

Kloud Kart's stock counts must remain current because stale stock information can result in overselling. However, the brief states that other reporting information can refresh daily.

Investors have expressed interest in real-time analytics, but the company has not demonstrated that most business decisions require second-by-second reporting. The company also has limited staffing capacity.

## Decision

Kloud Kart will use scheduled daily batch processing for ordinary analytical reporting, while the website keeps checking live stock availability against the operational database rather than the daily warehouse. Kloud Kart will not introduce a broad real-time streaming platform at this stage.

## Alternatives considered

### Alternative A: Introduce real-time streaming for all reporting

- **How it would work:** Continuously process database changes and update analytical reports and dashboards as events occur.
- **Why it is attractive:** It provides fresher information and may support more immediate business decisions.
- **Why rejected:** Most current reporting needs can be met with daily refreshes. Streaming introduces additional infrastructure, monitoring and operational complexity without a demonstrated business requirement.

### Alternative B: Use daily batch processing for all data, including live stock

- **How it would work:** Refresh all reporting and stock information once per day.
- **Why it is attractive:** It would create a simpler and more consistent processing schedule.
- **Why rejected:** Stock information cannot safely be treated like ordinary daily reports. A daily delay could cause customers to purchase items that are no longer available.

## Consequences

- **What this buys:**
  - A simpler and more affordable data processing design.
  - Less operational complexity for a small team.
  - Daily reporting freshness for Nana and Finance.
  - Protection against using stale warehouse data for live stock decisions.
- **What this costs:**
  - Ordinary reports will not provide second-by-second updates.
  - The company must maintain reliable stock checks in the operational system.
  - The daily pipeline must be monitored to ensure that reports refresh successfully.
- **What it costs the client if I am wrong:** If daily batch reporting is insufficient for a future business decision, management may act on outdated information. If live stock is moved to a daily refreshed warehouse, customers may purchase unavailable items, leading to overselling and customer dissatisfaction.
- **What would make me revisit this:** If Kloud Kart identifies a specific business process that requires faster information, such as a decision that must change within minutes rather than a day, the company should assess a targeted near-real-time solution for that process.

## What this survives

If order volumes grow or the company expands into Nigeria, daily batch reporting can continue for ordinary metrics while live stock remains in the operational system. A targeted streaming solution can be introduced later if evidence justifies it.
