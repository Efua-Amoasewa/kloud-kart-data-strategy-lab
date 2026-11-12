# Deliverable 1: Situation Diagnosis — Kloud Kart

## 1. Executive summary

Kloud Kart's main challenge is not the absence of a sophisticated data platform or real-time dashboard. Its current problems are unreliable reporting processes, competition between reporting workloads and the live website, inconsistent business definitions, inadequate control over customer-data copies, a gap between what investors expect and what the company can currently deliver, and dependence on a single developer.

These issues affect customer experience, management decision-making, operational efficiency and regulatory compliance.

The recommended priority is to address customer-data governance first because of the existing Data Protection Commission (DPC) complaint and its 90-day response deadline. The expectation gap comes second, because it is the biggest risk to Nana's credibility in the board conversation itself. Website performance, revenue consistency and key-person risk follow.

## 2. Key problems and root causes

### Problem 1: Customer-data governance and deletion

**Evidence from the brief:** Marketing exports customer lists containing approximately 300,000 people without tracking where copies are stored or who has access to them. Kloud Kart also has an existing DPC complaint concerning a deleted customer's information, with 90 days to respond.

**Root cause:** Kloud Kart lacks adequate processes for tracking, controlling and managing customer-data copies outside its main database.

**Business consequences:**

- Customer information may remain in spreadsheets, employee laptops, email attachments and other locations after the original database record has been deleted.
- The company may struggle to locate and manage all copies when responding to deletion requests.
- Failure to handle the complaint appropriately could expose the company to regulatory consequences.
- Negative publicity could damage customer confidence, reduce repeat purchases and harm the company's reputation.

**Cost and risk:** Exact financial exposure cannot be established from the available information. Potential costs include staff investigation time, locating and managing copies, legal advice, regulatory consequences and lost customer trust.

**Further compliance obligations:**

- Under the Data Protection Act, 2012 (Act 843), data controllers must register with Ghana's Data Protection Commission before processing personal data and renew that registration every two years. Kloud Kart's registration status is not stated in the brief and must be confirmed.
- The Nigeria pilot brings Nigerian customers' data under the Nigeria Data Protection Act, 2023, overseen by the Nigeria Data Protection Commission (NDPC). Organisations designated as data controllers of "major importance" must register with the NDPC. Whether Kloud Kart's Nigerian operations qualify requires Nigerian legal advice.

**Information still needed:** A complete inventory of customer-data copies, their locations, owners, access permissions, retention periods and deletion procedures; Kloud Kart's registration status with Ghana's DPC; and its obligations under Nigeria's law.

### Problem 2: Live website performance

**Evidence from the brief:** Kloud Kart's orders, inventory and customer accounts are stored in one MySQL database on the same machine as its live website. Twice in the previous month, Monday reporting exports slowed the live website significantly.

**Root cause:** Production website activity and reporting workloads compete for the same server resources, including CPU, memory, storage and network capacity.

**Business consequences:**

- Customers may experience slow page loading and difficulty completing purchases.
- Some customers may abandon purchases and move to competitors.
- Nana's reporting process also becomes slower.
- Repeated performance problems could reduce customer satisfaction and trust.

**Cost and risk:** The company incurs wasted staff time and may lose sales when customers abandon purchases. The actual financial loss cannot be calculated from the brief because the number of affected customers, abandoned orders and contribution per order are unknown.

**Information still needed:** Frequency and duration of slowdowns, number of affected customers, abandoned orders, average order value and contribution margin.

### Problem 3: Inconsistent revenue reporting

**Evidence from the brief:** Nana rebuilds Monday figures using CSV exports, but Finance's spreadsheet does not match hers.

**Root cause:** Kloud Kart lacks an agreed business definition of revenue and a shared calculation process. Different teams may apply different rules when deciding which orders and amounts to include.

For example, teams may disagree about whether revenue should be counted when an order is placed, paid for or shipped, and how refunds or cancelled orders should be treated.

**Business consequences:**

- Finance and Operations cannot confidently rely on the same figures.
- Employees waste time reconciling reports.
- Management may make poor financial or operational decisions based on conflicting numbers.
- Investors may lose confidence in the company's reporting.

**Cost and risk:** The company loses staff time through repeated reconciliation. The potential cost of poor management decisions cannot be reliably quantified without knowing the differences between the reports and the decisions made using them.

**Information still needed:** An agreed revenue definition, the formulas currently used by each team, and the financial differences between their reports.

### Problem 4: Investor expectations the company cannot yet meet

**Evidence from the brief:** Investors asked about "data strategy" and "real-time analytics", and Nana nodded. The wish list (a warehouse or lakehouse, real-time dashboards, machine-learning forecasting, and buying Snowflake or BigQuery) was assembled from investor and developer comments, not from a requirements process.

**Root cause:** Kloud Kart's data ambitions have been driven by what investors and the developer have seen elsewhere, not by the company's own business needs. No one has translated those expectations into a plan that fits a company of Kloud Kart's size and team.

**Business consequences:**

- If the board expects real-time dashboards and forecasting this year, a foundations-first plan may look like under-delivery.
- Nana's credibility depends on giving clear, honest answers this time, not another nod.
- Money could be spent on impressive tools that the company cannot staff or does not yet need.

**Cost and risk:** This is primarily a credibility and capital-allocation risk rather than a direct cash cost. Buying platforms before they are needed would add licence, implementation and staffing costs with little return.

**Information still needed:** Which investor expectations are firm commitments and which were exploratory questions.

### Problem 5: Dependence on a single developer

**Evidence from the brief:** Kloud Kart has one PHP/MySQL developer. Nobody else has run a warehouse or written Python professionally.

**Root cause:** All technical knowledge of the shop database and website sits with one person, and the company has no in-house data skills.

**Business consequences:**

- If the developer is unavailable or leaves, the website, the database and any reporting fixes are at risk.
- The developer cannot run the website and build a data platform at the same time.
- The new data hires will depend on the developer's knowledge in their first months.

**Cost and risk:** The cost of losing the developer would include recruitment, lost knowledge and possible downtime. It cannot be quantified from the brief, but the risk is real for a company whose revenue depends on one website.

**Information still needed:** How much of the system is documented, and whether any external support arrangement exists.

## 3. Estimated operational costs and financial exposure

The following calculation illustrates the cost of manual reporting labour.

Assumptions:

- Nana spends approximately four hours every Monday preparing reports.
- There are 50 reporting Mondays per year.
- An illustrative loaded labour cost of GH₵50 per hour is used. This is not Nana's confirmed pay rate.

Calculation:

4 hours × 50 Mondays = 200 hours annually.

200 hours × GH₵50 = **GH₵10,000 annually.**

This represents an estimated value of staff time spent on the current reporting process.

**Website slowdowns (illustrative):**

Lost contribution per slowdown = orders per hour × hours slowed × share of those orders abandoned × contribution per order.

Assumptions:

- 4,000 orders a day averages about 167 orders an hour. Monday daytime traffic is probably higher, so this is conservative.
- Each slowdown lasts about two hours.
- 20% of orders placed during a slowdown are abandoned rather than delayed.
- Each order contributes an illustrative GH₵20 of profit after product and delivery costs. This is not a confirmed figure.

Calculation:

167 orders × 2 hours × 20% × GH₵20 = **about GH₵1,340 per slowdown.**

At two slowdowns a month, that is about GH₵2,700 a month, or **about GH₵32,000 a year** if the problem continues. Lost profit is used rather than lost revenue, because an abandoned sale also saves its product and delivery costs. Every input should be replaced with Kloud Kart's actual figures.

For customer-data governance, an exact exposure figure would be misleading without an inventory of data copies and an assessment of the possible regulatory, legal and reputational consequences.

All financial assumptions should be validated with Kloud Kart before being treated as actual company costs.

## 4. Risk-based prioritisation

| Rank | Problem                   | Reason for priority                                                                                                                                               |
|----------|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1        | Customer-data governance      | Existing DPC complaint and 90-day response deadline create immediate compliance urgency. Potential reputational damage could extend beyond the affected customer. |
| 2        | Investor expectations         | The biggest risk to the board conversation itself. Nana has already nodded to "real-time analytics"; the plan must reset expectations with clear, honest answers. |
| 3        | Website performance           | Reporting exports have already slowed the live website twice in one month, creating a direct risk to customer experience and sales.                               |
| 4        | Revenue reporting consistency | Conflicting figures undermine management decisions and investor confidence. A shared definition is necessary for trustworthy reporting.                           |
| 5        | Single-developer dependence   | One person holds all technical knowledge. Lower immediate urgency, but it limits how fast the plan can move and is a standing risk to the website.               |

These priorities do not mean that work on the other problems should stop. Where possible, actions should proceed in parallel.

## 5. Key assumptions and information gaps

This diagnosis is based on the supplied brief. Nana was unavailable for follow-up questions, so the following assumptions and gaps must be acknowledged:

- The four-hour weekly reporting estimate and GH₵50 hourly rate are illustrative assumptions, not confirmed company figures.
- The actual number of customer-data copies and their locations is unknown.
- The precise financial impact of website slowdowns has not been supplied.
- The current revenue calculation rules used by Nana and Finance have not been verified.
- The exact regulatory outcome of the existing DPC complaint cannot be predicted from the brief.
- Kloud Kart's registration status with Ghana's Data Protection Commission, and its obligations under Nigeria's Data Protection Act, have not been confirmed.
- We assume stock is checked against the live database today. The brief's note that stale stock "is how the company oversells" suggests this may not always be true, and it must be verified.
- The slowdown cost uses illustrative figures for duration, abandonment and profit per order.
- We assume a deleted customer is removed from the shop database outright, rather than being flagged as deleted.
- Kloud Kart's stated annual growth assumption is approximately 15–20%, unless otherwise specified.

These gaps should be investigated during implementation rather than replaced with unsupported figures.

## 6. Overall conclusion

Kloud Kart should address its existing data governance, operational performance and reporting consistency problems, and reset investor expectations honestly, before investing in advanced real-time dashboards or machine learning.

A sophisticated dashboard would not automatically correct inconsistent revenue definitions, prevent reporting exports from slowing the live website or ensure customer information is properly managed.

The immediate focus should be protecting customer information, reducing the impact of reporting on the live website, and establishing trustworthy business figures. These foundations will give Kloud Kart a more reliable and defensible starting point for its data strategy.
