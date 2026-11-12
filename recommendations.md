# Deliverable 2: Recommendation

### 1. Executive recommendation

Kloud Kart should build a modest, privacy-conscious data warehouse on a managed PostgreSQL service, supported by a read replica and an automated nightly ETL pipeline. BigQuery or Snowflake replace PostgreSQL only if Q1 quotes show a clearly lower three-year cost.

Kloud Kart has approximately 4,000 orders per day, around 40GB of structured MySQL data, only two available data hires and no immediate requirement for machine-learning forecasting. It therefore needs a reliable foundation two people can run, not an enterprise platform.

### 2. Proposed architecture

**Original MySQL database → Read replica → Nightly ETL pipeline → Data warehouse (managed PostgreSQL) → Shared dashboard for Nana and Finance**

- **Original MySQL database:** Continues to run the live website, process orders and manage current stock availability.
- **Read replica:** A separate copy of the live database that handles reporting-related extraction work, reducing competition for computing resources on the live website. Access must be restricted and replication delays monitored.
- **Nightly ETL pipeline:** Fully reloads the small, minimised customer tables each night, which removes deleted customers automatically, and loads orders incrementally. A deletion log on the shop database records every customer deletion, so the pipeline can remove matching records and keep evidence (ADR-003).
- **Data warehouse (managed PostgreSQL):** PostgreSQL is the default because it is close to the MySQL the developer already knows, has a predictable monthly bill, and comfortably handles 40 GB of structured data (ADR-002).
- **Shared dashboard:** A dashboard tool, such as the free open-source edition of Metabase, connected to the warehouse.

### 3. Data protection and privacy

Kloud Kart must follow the Ghana Data Protection Act, 2012 (Act 843). Data controllers must register with Ghana's Data Protection Commission before processing personal data and renew every two years; Kloud Kart's registration status must be confirmed in Q1. The Nigeria pilot also brings Nigerian customers' data under the Nigeria Data Protection Act, 2023, and Nigerian legal advice should confirm whether Kloud Kart must register with the Nigeria Data Protection Commission.

The company should apply data minimisation by transferring only the information genuinely required for reporting. For example, order dates, product information and order amounts may be needed, while customer phone numbers and account numbers generally should not be copied into the warehouse without a justified need.

The company must also maintain an inventory of personal-data locations, including databases, spreadsheets, CSV exports, email attachments and backups. The Customer Data Register (see improvement.md) provides this inventory and deletion tracking from week one.

The existing Data Protection Commission complaint is an immediate priority. Management and the appropriate compliance or legal personnel must oversee the response, with technical support from the Data Engineer, within the complaint's 90-day deadline.

### 4. Reporting and data freshness

Daily warehouse updates are sufficient for ordinary reporting because the business has confirmed that most information can be refreshed daily. Live stock availability is the exception and must be checked against the original operational database.

**What Nana opens on Monday:** a shared dashboard, refreshed overnight, showing last week's orders, revenue by the agreed definition, refunds and cancellations, and (from Q3) a split by country. Finance opens the same dashboard, so both teams start the week from the same numbers. Nana no longer exports CSV files or rebuilds spreadsheets.

### 5. Hiring recommendation

#### First: Data Engineer (hired in Q1)

**First 90 days:**

- Set up the read replica on the pre-approved second server, with restricted access.
- Work with departments to inventory customer-data copies, establish owners and provide technical evidence for the complaint response.
- Start the nightly incremental pipeline, reducing manual Monday exports.

#### Second: Analytics Engineer (joins in Q2)

**First 90 days:**

- Agree revenue, refund and cancellation rules with Finance and Operations.
- Build the shared warehouse reports that Nana and Finance both use.
- Add data quality checks that flag missing or wrong data, and check sample figures against underlying transactions.

A dedicated Data Analyst or Data Scientist should not be hired yet. The immediate priority is to establish trustworthy data and consistent reporting.

### 6. Technology selection and costs

**Decision:** the default warehouse is a managed PostgreSQL service. BigQuery is the alternative to beat on price, and Q1 quotes confirm or overturn the choice.

Estimated costs, from public cloud list prices in November 2026 (not quotes). Cloud services bill in US dollars and are paid by card, so figures are converted at GH₵12.60 to US$1, the card rate in early November 2026 (the Bank of Ghana rate was about GH₵11.64).

| Cost line | Status | Estimated cost |
|---|---|---|
| Two data salaries | Budgeted by the board | Set by the board's budget; likely the largest cost by far |
| Second server (read replica) | Pre-approved | About GH₵630–1,260 a month if hosted as a small cloud database server |
| Data warehouse (managed PostgreSQL) | Default choice; quotes confirm | About GH₵760–1,890 a month (a small instance lists at about GH₵590 a month, plus storage at about GH₵1.50 per GB) |
| Dashboard, backups, monitoring and security | To be included in the operating budget | About GH₵250–1,260 a month |
| **Total systems cost** | | **About GH₵1,640–4,410 a month (about GH₵20,000–53,000 a year)** |
| Current manual reporting (baseline) | Already being paid | About GH₵10,000 a year in Nana's time (illustrative, Deliverable 1) |
| Current website slowdowns (baseline) | Already being lost | About GH₵32,000 a year in lost profit (illustrative, Deliverable 1) |

At 40 GB, storage is a negligible part of any option: BigQuery, for example, charges about GH₵0.25 per GB a month, so storing 40 GB would cost about GH₵10 a month. The choice between options is therefore about predictable billing, staff familiarity and running effort, not storage price.

No money beyond the approved salaries and server is committed until quotes confirm these estimates.

### 7. What Kloud Kart should postpone

- Machine-learning demand forecasting until historical data is sufficiently reliable and a business case exists.
- Real-time dashboards for ordinary business reporting, because daily updates are sufficient.
- A lakehouse or complex data lake architecture, because their additional flexibility and operational complexity are not currently justified.
- A real-time streaming platform, because the only data that must be live, stock, should be checked on the shop database itself.
