# ODIN / Muninn — Progress Update
**Date:** March 27, 2026 | **Week 9 of 30**

---

## Executive Summary

Cheryl joined the Friday standup for the first time and completed a live prototype walkthrough, testing queries against the current 1M-row v7 sample. David gave an explicit green light for direct SME outreach — schedule 30-minute calls with each data team member. The data expansion scope widened significantly: Virginia, Utah, Indiana, and Chicago MSA are all now in scope, with David approving a 10M+ row starting point and a testing budget up to $1,000. Greg has acquiesced on the behavioral health direction, and Cheryl and David aligned on forming a beta group of ~15 BH providers. Branding was clarified: Odin is the external product name, Muninn is the internal project name only.

---

## What Happened This Week

### Cheryl's First Prototype Walkthrough
**Date:** March 27, 2026

Cheryl logged into the prototype at **fledgling-muninn.vercel.app** and tested queries. The 1M-row randomized v7 sample limited results — queries for specific codes in specific cities often returned no data, and Medicare benchmarks were sparse. Courtney recommended querying by state rather than city for better coverage at this sample size.

Key observations:
- The login flow worked (name-based tracking with shared password)
- Queries for CPT 99213 by city (Houston) returned no results with Medicare benchmarks
- State-level queries perform better against the current sample
- Cheryl understood the architecture after David's explanation — Odin connecting BigQuery through Vertex, with a swappable backend LLM

### Data Expansion Scope Widened
David approved a significant expansion beyond the original 5M-row plan:

| Parameter | Previous Plan | New Plan |
|---|---|---|
| **States** | Illinois + Virginia | Virginia + Utah + Indiana + Chicago MSA |
| **Row count** | 5M | 10M+ (start at 10M, scale up iteratively) |
| **Reason** | Demo coverage | Real client use cases — Utah and Indiana have live client deliveries |
| **Budget** | Not defined | David: "try not to go over $1,000" |

- **Utah** — Cheryl's request: two clients going live next week, Intermountain right behind them. Real-time client questions to test against.
- **Indiana** — Cheryl's request: MJ going live, another real use case.
- **Virginia** — Chris Hart's recommendation, good national representation.
- **Chicago MSA** — David's original request from Week 7.

Courtney confirmed scaling is trivial — changing the table reference takes ~10 minutes. She wants to scale iteratively (start at 10M, monitor costs for 24 hours, then expand).

### SME Outreach — Green Light Given
David gave explicit permission for direct outreach:
- "You've got a green light. Start scheduling 30 minutes with each one of them."
- Courtney should be CC'd on all outreach
- Strategy: half will start peppering with questions once they feel engaged
- Best approach is sending the prototype link once data is expanded, then logging interactions on the backend

### Query Logging Gap Identified
Currently, the system logs BigQuery SQL queries but **not** the verbatim user questions typed into the chat. This was identified as a critical gap — the natural-language questions are the gold for defining the semantic layer. Topher committed to figuring out the feasibility of capturing these without creating friction.

### Behavioral Health Accelerating
- Greg acquiesced after a one-on-one with David — moving forward on BH
- Cheryl raised the importance of including Greg in the semantic layer process for BH-specific concerns (rev codes vs per diem, provider interpretation)
- Cheryl and David aligned on forming a **beta invitation group** of ~15 BH providers at ~$2,500/pop
- Cheryl flagged that the BH community is currently oversensitive to AI — messaging needs to be careful
- David instructed Topher to email Spencer Case via Lumen to fork the BH rate book repo from David's GitHub

### Branding Clarified
- **Odin** = the product name (external, client-facing)
- **Muninn** = the project name (internal only, never shared externally)
- Action: change the UI from "Chat with Muninn" to "Chat with Odin"

### Cost Dashboard Committed
Topher committed to building a preliminary cost dashboard by next Friday — a UI showing per-query costs. Courtney confirmed the BigQuery cost data is already available; the project is already isolated in GCP with cost alerts in place.

### Other Items
- Courtney wants to integrate Chris Hart's lineage tables into Odin for internal data tracing
- David wants a fractional CIO to ensure infrastructure is in order before outside users
- Payment infrastructure being evaluated through Continuous Scale / NetSuite integration
- Courtney transitioning some GCP billing pieces to the new contracted cloud administrator

---

## What Has Changed Since Last Week

| Item | Mar 20 Status | Mar 27 Status |
|---|---|---|
| Data expansion scope | 5M rows, IL + VA | 10M+ rows, VA + Utah + Indiana + Chicago MSA |
| SME engagement | Strategy agreed, not started | Cheryl active, green light for all SME outreach |
| Behavioral health | Rate book concept identified | Greg on board, beta group forming (~15 providers) |
| V8 data load | V8 posted, load pending | Transfers in progress, targeting Tuesday |
| Branding | Muninn/Odin used interchangeably | Clarified: Odin external, Muninn internal only |
| Cost dashboard | Not started | Committed for next Friday |
| Query logging | Not identified as gap | Identified as critical, solution in progress |

---

## True by Next Friday (Apr 3)

1. **Preliminary cost dashboard** — per-query cost visibility UI ready for review (Topher committed)
2. **V8 data loaded** — VA + Utah + Indiana + Chicago MSA (~10M rows) in BigQuery (Courtney targeting Tuesday)
3. **SME outreach started** — 30-min calls scheduled with data team members (David: green light)
4. **Query logging solution** — capture verbatim user questions for semantic layer development
5. **UI branding updated** — "Chat with Odin" (not Muninn)
6. **Stretch:** BH rate book repo forked from David's GitHub and integrated into prototype

---

*Prepared by Topher Rasmussen | Third Horizon*
