# Proposed New Jira Tickets — From Mar 2 Full Team Meeting

These tickets were identified from discussion in the March 2 full-team meeting and are **not covered** by the existing TH-921 through TH-958 sprint board.

**Note:** The existing board runs TH-921 through TH-958. These new tickets start at TH-959.

---

## Sprint Operations — This Week (Wk 5)

### TH-959: Prepare P1 Development Cost Pro Forma
**Owner:** Topher + Courtney
**Target Week:** Wk 5 (this week)
**Description:** Greg requested a ballpark budget for the P1 sprint — new subscriptions, Vertex AI token costs, exploratory BigQuery scan costs, and any incremental spend beyond existing infrastructure. Courtney estimated Vertex AI at ~$100-150/month; Chris K noted model training costs within Vertex AI should also be accounted for. Deliverable: one-page cost breakdown.
**Est. Hours:** 2 hrs
**Priority:** High — Greg and Cheryl need this for business planning

### TH-960: Set Up Weekly Friday Standup Cadence
**Owner:** David (Topher to support)
**Target Week:** Wk 5 (this week)
**Description:** David directed weekly Friday calls for development progress tracking. Attendees: David, Courtney, Topher (open invite to others). Create recurring calendar invite, define lightweight agenda format (timeline status, blockers, unknowns), and determine how progress reads out to broader team via CSOG.
**Est. Hours:** 1 hr
**Priority:** High — starts this week

### TH-961: Build 30-Week Detailed Timeline
**Owner:** Courtney + Topher
**Target Week:** Wk 5 (this week) — DONE
**Description:** David requested a week-by-week milestone plan across all phases (P1-P4), with heavier detail on the near-term phases. Each week should define "what needs to be true at the end of this week to stay on time." Should include gates/checkpoints between phases.
**Est. Hours:** 6 hrs
**Priority:** High — core planning deliverable
**Status:** Complete. See `ODIN_30_Week_Timeline.md`.

---

## Sprint Operations — Wk 5–6

### TH-962: Build Jira Dashboard View with Timeline Visuals
**Owner:** Courtney + Topher
**Target Week:** Wk 5–6 (after Jira migration)
**Description:** Courtney committed to building a Jira-based dashboard view of the timeline with visual aids and capacity measurement. Replaces the current Excel sprint board. Should include Gantt view, sprint tracking, and capacity indicators. Depends on Jira migration completing first.
**Est. Hours:** 4 hrs
**Priority:** Medium — after Jira migration

### TH-963: Document Semantic Layer Spec Template
**Owner:** Topher + Courtney
**Target Week:** Wk 5–6 (before Build stage starts Wk 7)
**Description:** Define what a complete semantic layer spec looks like for a given domain: which data subset tables are needed, what documentation and training rules accompany them, and what the acceptance criteria are for "this domain is ready." This becomes the repeatable template for all future semantic layer builds.
**Est. Hours:** 3 hrs
**Priority:** High — foundational to all P1 build work. Must be done before semantic views start in Wk 7.

### TH-964: Document Session Architecture Decision (No Cross-Session Memory)
**Owner:** Topher
**Target Week:** Wk 5–6
**Description:** Document the architectural decision that each ODIN session starts clean — no persistent cross-instance memory. Include rationale (prevents context contamination per Greg's concern), implications for user experience (no "continue from last time" by default), and note that this may evolve in P2/P3 as thread-based interactions are explored.
**Est. Hours:** 1 hr
**Priority:** Medium

---

## Parallel Tracks — Wk 6–8

### TH-965: Collect Past Client Deliverables as Training Context
**Owner:** Topher
**Target Week:** Wk 6–8
**Description:** Greg suggested loading past client deliverables (research papers, decks, analytic outputs, spreadsheets) into the training context for ODIN. Identify the most relevant deliverables across HFMA, MMA, MHPI, and DaaS engagements. Coordinate with Greg, Bo, and Cheryl on what exists. Trim irrelevant content and organize for semantic layer ingestion.
**Est. Hours:** 4 hrs
**Priority:** Medium — enhances training quality

### TH-966: Research Enterprise AI Pricing Models
**Owner:** Topher (+ Cheryl, Greg for input)
**Target Week:** Wk 6–10 (parallel to P1)
**Description:** Greg and Cheryl emphasized the need to study how AI companies price enterprise access — token-based, tiered, usage-based, subscription, etc. Research should include Vertex AI pricing structures, comparable enterprise AI product pricing (Snowflake Cortex, Databricks, etc.), and identify which model fits Starset's client deployment. Deliverable: pricing model comparison doc.
**Est. Hours:** 4 hrs
**Priority:** Medium — parallel to P1, feeds into P3/P4

### TH-967: Define Trackable Billing Metrics for Client Deployment
**Owner:** Courtney + Topher
**Target Week:** Wk 6–10 (parallel to P1)
**Description:** Chris K noted the team needs to determine what usage metrics can be tracked at the endpoint level — prompt volume, query volume, BigQuery scan cost, session count — to support variable pricing. Identify what GCP/Vertex AI/BigQuery natively expose and what additional instrumentation is needed.
**Est. Hours:** 3 hrs
**Priority:** Medium — needed before client pricing decisions

---

## Deferred — P3/P4 Concerns

### TH-968: Investigate Per-User Cost Controls and Lockout Mechanisms
**Owner:** Courtney
**Target Week:** Wk 13–16 (P2/P3 timeframe)
**Description:** Greg raised that some clients will want per-user usage caps, not just per-client caps. Courtney confirmed per-client lockout is feasible via GCP project isolation. Per-user requires Firebase-style user token management. Investigate options and document feasibility.
**Est. Hours:** 3 hrs
**Priority:** Low — P3 concern, but good to understand early

### TH-969: Legal Review of Third-Party Dependency Terms
**Owner:** Cheryl + Greg (to scope), David (to approve spend)
**Target Week:** Wk 23+ (before client contracts are signed)
**Description:** Greg and Cheryl flagged the growing complexity of stacking third-party terms (Candor, Paces, GCP/Gemini, client MSAs). Need legal review of: (a) flow-down clause requirements, (b) what rights we can contractually grant given third-party limitations, (c) risk mitigation for policy/pricing changes by cloud providers. Greg suggested using the same firm that helped on tax matters.
**Est. Hours:** TBD — external counsel
**Priority:** Medium — becomes urgent before client contracts are signed

---

## Notes

- Ticket numbers TH-959+ are **proposed** — actual numbers will be assigned when created in Jira.
- The existing sprint board (TH-921 through TH-958) already covers P0 through P4.
- TH-959–964 are immediate or near-term — create these under the P1 Epic.
- TH-965–967 (pricing/billing/deliverables) are parallel workstreams, also under P1 Epic.
- TH-968 (per-user controls) is a P3 concern — can live under a future Epic or standalone.
- TH-969 (legal) is standalone — not a sprint task, it's a flag for David/Cheryl/Greg.

---

## Issues Found in Existing Sprint Board (CSV)

The following issues were identified in `ODIN_Sprint_Board (1)(Sprint Board) (2).csv` and should be corrected during Jira migration:

1. **TH-928 is duplicated** — Used for both "Query Collection: Jenna" (P1, row 6) and "Build semantic view: Jenna" (P2, row 36). The Jenna semantic view needs its own ticket number.
2. **TH-941 missing Phase** — "Build View: TBD #5" has no phase listed. Should be P1.
3. **TH-944 and TH-945 dependency is wrong** — Both list TH-929 (Chris K query submission) as dependency. Should depend on the semantic view build tickets (TH-933–940 range).
4. **Jenna and Chris H are SMEs in TH-924** but don't appear in any other documentation or team tables. Confirm whether they should have query collection tickets and semantic views.
5. **TH-925 and TH-931 have sparse/missing descriptions** — flesh out during Jira entry.
6. **TH-943 has no description** — just a title ("Identify view Gaps and recollect").
