# ADR-001: Use a Read Replica for Reporting Extraction

- **Status:** Accepted
- **Date:** 2026-11-11
- **Decision owner:** Kloud Kart leadership, with Nana Adjei as business sponsor

## Context

Kloud Kart's website and operational MySQL database run on the same machine. Nana's Monday CSV exports compete with the live website for computing resources, and the website slowed significantly during two exports last month.

The company needs a safer way to extract data for reporting. The second server or read replica has already been pre-approved. The solution must protect the live website and be manageable by a small technical team.

## Decision

Kloud Kart will create a read replica of its production MySQL database and use the replica as the source for reporting extraction instead of running heavy reporting queries directly against the production database.

## Alternatives considered

### Alternative A: Continue extracting directly from the production database

- **How it would work:** Schedule reporting exports during quiet periods, such as midnight, and limit the size or frequency of queries.
- **Why it is attractive:** It avoids the extra cost and administration of a second database server.
- **Why rejected:** Scheduling reduces the chance of disruption but does not eliminate resource competition. Exports may still overlap with website activity, take longer than expected, or affect other database operations. The company has already experienced website slowdowns from this approach.

### Alternative B: Upgrade the existing server

- **How it would work:** Add more CPU, memory and faster storage to the current machine, so it can handle both the live website and the Monday reporting exports.
- **Why it is attractive:** It is quick to arrange, needs no new system to set up or monitor, and the developer already knows how to manage the existing server.
- **Why rejected:** The website and reporting would still share one machine and compete for the same resources. A larger server only delays the problem as orders grow by 15–20% a year and Nigeria is added, and any heavy or badly written report could still slow the live website. It also leaves the pre-approved second server unused.

## Consequences

- **What this buys:**
  - Reduces competition between reporting queries and live website activity.
  - Gives the data engineering process a separate source from which to extract information.
  - Provides a foundation for a more reliable reporting pipeline.
- **What this costs:**
  - Additional server or database hosting costs.
  - Time to configure, secure and monitor replication.
  - The replica may temporarily lag behind the production database, so it must not be treated as the authoritative source for live stock counts.
- **What it costs the client if I am wrong:** If the replica is poorly configured or not monitored, reporting data could be delayed or incomplete. If the company continues extracting from production instead, website slowdowns and potential lost orders may continue.
- **What would make me revisit this:** If reporting volumes grow substantially, replication becomes unreliable, or the cost of maintaining the replica becomes disproportionate to its benefit, the design should be reviewed.

## What this survives

If order volumes continue growing by 15–20% annually, the separation of reporting workloads from production remains useful. The replica can be scaled or its extraction workload adjusted without immediately redesigning the whole architecture.

If the Data Engineer's start is delayed, the existing developer can set up the replica, because MySQL replication is standard MySQL administration rather than a data-engineering specialism. The reporting pressure on the live website can therefore be removed without waiting for the first data hire.
