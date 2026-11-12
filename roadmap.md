# Deliverable 2: 12-Month Roadmap

## Part B: 12-Month Roadmap

| Quarter              | Main activities                                                                                                                                                                                                                                                                            | Outcomes Nana can verify                                                                                                                                                                                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Q1: Months 1–3**   | Recruit the Data Engineer. Set up the Customer Data Register. Investigate the existing DPC complaint and identify relevant copies of customer data. Confirm DPC registration and obtain Nigerian legal advice. Verify that stock checks use the live database. Establish the read replica. Document personal-data locations, access and deletion procedures. Begin the automated data pipeline. Start recruiting the Analytics Engineer. | The DPC complaint has been responded to within its deadline, with evidence of actions taken. A personal-data inventory exists. The replica is operational. Initial automated data transfers are working, reducing manual exports and reporting pressure on the live database. |
| **Q2: Months 4–6**   | Onboard the Analytics Engineer. Agree on revenue and other business definitions with Finance and Operations. Build warehouse reporting models and automated daily reports. Introduce data quality checks.                                                                                  | Nana and Finance use the same agreed revenue definition and shared reporting tables. Their reports agree for the same period and definition, and sample figures are checked against underlying transactions to confirm accuracy. Daily reports are available without repeatedly rebuilding CSV spreadsheets. Data quality problems can be detected.               |
| **Q3: Months 7–9**   | Extend reporting to support Nigeria's operations. Monitor pipeline performance, data quality, system capacity and costs. Review access controls and deletion processes.                                                                                                                    | Nigerian orders can be included in reporting. Revenue can be viewed separately by country, with agreed currency conversion rules for combined reporting. The nightly update succeeds on at least 95% of nights, and every failure triggers an alert. No reporting-related website slowdowns occur during the quarter. Systems costs stay within the estimated GH₵1,640–4,410 a month, or the variance is explained.          |
| **Q4: Months 10–12** | Review the year's business and data-system performance. Assess costs and benefits. Identify unresolved problems and agree on priorities for the next year.                                                                                                                                 | Nana's Monday reporting time falls from about four hours to under one hour. Finance and Operations report one revenue figure, with no unexplained differences in the year's last quarter. Every deletion request in the year is closed before its deadline, with a record of action. The company has a documented list of improvements and an agreed plan for the next year, including whether forecasting is justified.                                       |

### Roadmap success measures

Management should review:

- Whether the DPC complaint was handled within the required deadline.
- Whether the live website has stopped suffering from reporting-related slowdowns.
- Whether Nana's manual reporting workload has reduced.
- Whether Nana and Finance use consistent, agreed figures.
- Whether daily data transfers are reliable.
- Whether customer-data copies are known, controlled and manageable.
- Whether the system remains affordable as the company grows.

The roadmap should be reviewed regularly. If a quarter's outcome is delayed, management should understand why and adjust the plan rather than simply moving unfinished work into the next quarter.
