# ODIN / Muninn — Progress Update
**Date:** April 10, 2026 | **Week 11 of 30**

---

## Open Questions & Decisions Needed

### 1. Guided Onboarding Flow
Should Odin prompt users with setup questions on first login (region, provider class, plan type, etc.) to set defaults? Chris referenced the Age of May tool — requiring users to set defaults before exploring reduced confusion significantly. Could be a first-login flow or an optional skip.

**Who decides:** David / Cheryl
**Urgency:** Before external users

### 2. Methodology Context in Agent
The agent does not reference Confluence methodology docs. Courtney flagged a specific gap: users cannot understand *why* certain providers appear (e.g., the outpatient taxonomy filter). Full Confluence documentation would be overkill, but condensed key concepts could help.

**Who decides:** Courtney
**Urgency:** Medium — becomes more important with external users

### 3. Limitation Awareness Prompting
Chris suggested the agent proactively offer to explain the parameters and limitations behind each result (e.g., "If you'd like to know what went into this search, I can explain"). This addresses users who do not know what questions to ask about why results look the way they do.

**Who decides:** Topher / Courtney
**Urgency:** Backlog — UX enhancement

### 4. Data Partitioning Strategy
At 700M rows (~0.5 TB for Utah alone), each query costs ~$3 at current configuration. Courtney proposes splitting tables by the 9 census geographic regions so users select a region first and Odin queries only that partition. Network-based splitting is less useful if users want cross-network comparisons. Bobby and Andy input needed on how to split accurately.

**Who decides:** Courtney / Bobby / Andy
**Urgency:** High — blocks the scale-up David wants

### 5. End-Game Architecture
David wants to map out the full ecosystem next Friday (Apr 17): how tables are structured at scale, how queries traverse them, cost estimates per configuration. He needs to understand boundaries and limitations before he can move on the business side. "The faster I can understand the limitations, boundaries and allowances, the faster I can get to work on the business side."

**Who decides:** David / Courtney / Topher
**Urgency:** Apr 17 — David will be on screen for the first time in weeks

### 6. Self-Service Client Onboarding
How important is it for clients to onboard themselves vs. requiring manual data provisioning from Courtney? David says he cannot answer yet — needs a clearer picture of Odin's cost and scale limitations first. Revisit in a couple of weeks.

**Status:** Deferred — David needs architecture clarity first.

---

## Decisions Made

| Decision | Date | Rationale |
|---|---|---|
| **Default to bar charts** — remove scatter/line options | Apr 8 | Bar is the most universally readable. Scatter and line rendered the same data with no added clarity. Pie may be useful for proportion questions later. |
| **Keep confidence score filtering at 2–3** | Apr 8 | Including 1s would expand coverage in smaller MSAs but risks users drawing bad conclusions. Credibility risk outweighs the coverage gain, especially for less-familiar users. Revisit at V10+. |
| **Scale up to 700M rows for testing** | Apr 10 | David: "You guys set the pace. Do it. I want to know where our limits are." Green light to test full Utah table. |
| **Third Horizon branding confirmed** — navy/gold | Apr 10 | David confirmed. Starset pink/orange retired. |
| **MMA already has direct data access** | Apr 10 | Courtney confirmed MMA has BigQuery service account + file exports. No new API needed. David acknowledged. |

---

## What Happened Since Last Update (Weeks 10–11)

### Week 10 — Async Update (Apr 3)
The Friday standup did not happen as a full group. Topher sent an async email update to David and Cheryl.

- **Admin dashboard live on production** — all user queries logged with latency tracking. Cost-per-query not yet populating (needs service account wiring for bytes processed — Courtney).
- **Utah (8M rows) + Chicago (2M rows) loaded into BigQuery** — Indiana can be incorporated in the next rollout. Smaller samples isolated by location so rows contribute more meaningfully.
- **Dev/prod environment separation** — Production: odin-sandbox-app.vercel.app | Development: odin-sandbox-app-dev.vercel.app
- **Inline charts and tables** — chat responses now render visualizations, making rate comparisons easier to read at a glance.
- **All branding updated to "Odin"** — no more Muninn references in the product.
- **Verbatim query logging resolved** — user questions now captured alongside SQL and latency data in admin dashboard.
- **V8 semantic layer updates finalized** by Courtney and pushed to production.

### Week 11 — Data Team Walkthrough (Apr 8)
Courtney walked the data team through Odin live. Ashley drove queries; Chris, Bobby, and Topher provided input.

- **Ashley tested CPT 99213 and H0015 queries** — results returned correctly with appropriate sample-size caveats.
- **UI feedback captured:**
  - Charts elongate on scroll — should stay fixed dimensions with internal scrolling
  - Blue gradient artifacts appearing in chat on both sides
  - Bar/scatter/line all showing same data — consensus: bar only as default
- **Guided onboarding idea surfaced** — Chris's 5-question intake concept well-received by the group.
- **Agent correctly referenced sample data limitations** when H0015 returned no results — a recent prompt improvement.
- **BigQuery job logging demonstrated** — the team can see which queries are from the Odin agent vs. individual users via the service account identifier.

### Week 11 — Friday Standup with David (Apr 10)
David joined on audio (not screen). Courtney stayed after for a follow-up.

- **David: green light to scale up to 700M rows** — "You guys set the pace. Do it. I want to know where our limits are." Wants to understand cost and performance boundaries ASAP so he can plan the business side.
- **Utah alone = ~700M rows (~0.5 TB) = ~$3/query** at current configuration without table partitioning.
- **Apr 17: David will be on screen** for end-game architecture mapping — how tables are structured at scale, query traversal, cost estimates. First time on screen in 2-3 weeks.
- **Courtney: Vertex AI audit tracking turned on Apr 8** — per-interaction cost tracking now active. Needs more query volume to produce meaningful forecast. Will have a cost forecast model by Apr 17.
- **Region-based table partitioning** — Courtney proposes splitting by 9 census geographic regions. Users select a region first, Odin queries only that partition. Reduces per-query cost significantly. Bobby/Andy input needed on best split strategy.
- **Thumbs up/down feedback UI** — Topher proposed adding inline response rating (like ChatGPT). No objections.
- **Thinking/loading indicator** — adding shimmer or processing steps during query execution. David liked the idea.
- **Bobby/Andy session confirmed for Apr 20** — both out next week (PTO + spring break).
- **David offered to create urgency** — "If you guys need help creating urgency and immediacy anywhere in the company, just say the word."
- **David on HFMA dashboard** — holding off on further investment once Odin is working; "it's just a function of an app" at that point.

### Other (Apr 9)
- David's MMA API question raised — resolved on Apr 10 call. Courtney confirmed existing BigQuery + export access.
- Greg and non-market team session to be scheduled for UI and application feedback.
- Client Readiness SOP work initiated — building on existing DaaS Confluence docs and Jira templates (Tanner's process), adding Odin-specific steps (deployment, authentication, data segmentation).

---

## What Has Changed Since Last Update

| Item | Mar 27 Status | Apr 10 Status |
|---|---|---|
| Data loaded | V8 transfers in progress | Utah (8M) + Chicago (2M) live. 700M scale-up approved. |
| Query logging | Identified as gap | Resolved — verbatim queries captured in admin dashboard |
| Cost tracking | Not started | Admin page live; Vertex AI per-interaction audit on since Apr 8. Forecast model by Apr 17. |
| Branding | Clarified but not shipped | Shipped — all UI says "Odin." Navy/gold confirmed by David. |
| Dev/prod separation | Single environment | Two Vercel URLs: prod + dev |
| SME engagement | Green light given | Team walkthrough completed (Apr 8). Bobby/Andy session Apr 20. |
| Chart rendering | N/A | Inline charts live; bar only per team consensus |
| Semantic layer | V7 data, limited sample | V8 with Utah + Chicago integrated, agent config updated |
| Data scale strategy | Not discussed | 9 census regions proposed for table partitioning. ~$3/query at 700M unpartitioned. |
| Architecture planning | Not started | David: end-game ecosystem mapping session Apr 17 |

---

## Data Pipeline Alignment

Odin data updates are dependent on the Starset Analytics National production schedule (Confluence: "Starset Analytics National Production Development 2026"). Key Odin milestones:

| Version | Odin Data Mapping | National Dataset Release | Data Team Break |
|---|---|---|---|
| **V8** (current) | Mar 30 – Apr 3 | Mar 25 (DONE) | Apr 6 – Apr 17 |
| **V9** | Jun 15 – 19 | Jun 1 – 5 | Jun 29 – Jul 17 |
| **V10** | Sep 14 – 18 | Sep 2 – 4 | — |

V9 method sprint begins Apr 20. Next Odin data mapping window is mid-June.

---

## True by Next Friday (Apr 17)

1. **End-game architecture prep** — come prepared to map the full ecosystem with David on screen: table structure at scale, query traversal, cost estimates
2. **Scale-up testing** — load 700M-row Utah table in dev environment, run test queries, document cost and latency
3. **Courtney: Vertex AI cost forecast model** — per-interaction data from Apr 8 onward, present cost projections at scale
4. **Bar chart as default visualization** — remove scatter/line options
5. **Chart scroll fix** — fixed dimensions with internal content scrolling
6. **Thinking/loading indicator** — shimmer or processing steps during query execution
7. **UI cosmetic updates** — navy/gold Third Horizon branding, updated logo
8. **Stretch:** Thumbs up/down inline feedback UI for query responses

---

*Prepared by Topher Rasmussen | Third Horizon*
