# Improvement beyond the brief: Customer Data Register

## The problem it solves

Kloud Kart's highest-ranked risk is customer-data governance (Deliverable 1, Problem 1). There is a live Data Protection Commission complaint about a deleted customer's data, with a 90-day response deadline. Marketing also exports a list of about 300,000 customers with no record of where the copies go.

The Commission's real question is: *"Did you remove this customer from every copy you hold?"* Today Kloud Kart cannot answer it, because nobody has a list of where customer data is kept or who owns each copy.

The roadmap makes a personal-data inventory a Q1 outcome, but the 90-day clock started before either data hire can join. Nana needs something she can use now, without technical help.

## What I built

A working, browser-based **Customer Data Register** (`kloud-kart-customer-data-register.html`). It opens in any modern browser with nothing to install, and it has two parts.

**Register.** This is a list of every place customer data is kept: the shop database, read replica, warehouse, Marketing exports, Monday CSV exports, the Finance spreadsheet, backups and email attachments. Each entry records:

- its owner;
- the customer details it holds;
- who can open it;
- how long it is kept;
- how a customer is removed.

A place stays marked *unconfirmed* until its owner confirms the details. The whole register can be downloaded as a CSV file.

**Requests.** Each deletion request or complaint gets three things:

- **A countdown** of days left to respond. It defaults to 90 days and can be changed if legal advice sets a different date.
- **A checklist** with one row for every place in the register. For each place, staff record *Removed*, *Not held there*, *Expires on schedule* (for copies such as backups, which are kept out of use until they expire) or *Kept for a legal reason*, together with the date and who recorded it.
- **A downloadable record of action**: a dated table of what was done, where and by whom, to support the response to the Commission.

A request cannot be closed until every place has been checked, and every expiring or kept copy needs a written note: its expiry date, or the legal reason for keeping it. When a request closes, the register freezes a snapshot of the checklist, so later changes to the register cannot alter a closed record.

The tool follows the plan's own data-minimisation rule. It asks for an account or case reference, never a customer's name or phone number.

## What it is worth to Nana

- **It addresses the most urgent risk first.** The 90-day deadline becomes a visible countdown, so the complaint cannot quietly run late.
- **It produces evidence, not just assurance.** Nana can show the Commission a dated record of the action taken in each place, rather than a general statement that data was deleted.
- **It works from week one.** It needs no technical skills and does not wait for the data hires or the warehouse.
- **It puts responsibility with the right people.** Marketing, Finance and Operations each confirm the copies they control, so the Data Engineer is not expected to find every copy alone.
- **It makes future requests more organised.** Each new deletion request starts from a known list of places and owners, instead of a fresh search.
- **It delivers a roadmap outcome early.** "A personal-data inventory exists" (Q1) is achieved before the roadmap formally starts, and the Data Engineer inherits a map of where personal data lives.

## What it cost

- **Money:** nothing. There are no licences, subscriptions or hosting fees. It is a single file that runs in a browser Kloud Kart already has.
- **Staff time to set up:** each department owner reviews and confirms the entries for the copies they control.
- **Staff time to run:** someone records the action taken for each place whenever a request comes in. Owners add new places when new copies of customer data are created.
- **What it does not do:** it tracks deletions but does not perform them, because owners still remove data in their own systems. It is only as complete as the people who maintain it. The downloadable version saves data in the browser where it is opened, while the hosted version keeps one shared register for the team. It does not replace legal advice on the complaint or predict the Commission's ruling.
