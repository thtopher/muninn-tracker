# JIRA Ticket Reconciliation — March 13, 2026
**Based on:** fledgling-muninn git history + current deployment state

This document maps each existing ticket to its actual status. Use this to batch-update JIRA after the David call.

---

## Legend
- **No change** — ticket status in JIRA is accurate
- **UPDATE** — status needs to change in JIRA
- **REPHASE** — ticket was completed in a different phase than planned
- **REVISE** — ticket scope or description needs updating
- **NEW** — net new ticket needed

---

## P0: Architecture & Guardrails (TH-921–923)

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-921 | GCP architecture validation | Done | Done | No change |
| TH-922 | Cost guardrails & project isolation | Done | Done | No change |
| TH-923 | OpenAI → Gemini transition | In Progress | **Complete** | **UPDATE → Done.** fledgling-muninn agent runs on Gemini 2.5-flash via Vertex AI. Transition is shipped. |

---

## P1: Semantic Foundation (TH-924–946)

### Collect Stage (Wk 5–6)

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-924 | Identify top 25 analytical questions | In Progress | In Progress | No change — concurrent with prototype |
| TH-925 | Bobby query collection | To Do | To Do | No change — outreach sent |
| TH-926 | Andy query collection | To Do | To Do | No change |
| TH-927 | Chris K query collection | To Do | To Do | No change |
| TH-928 | Jenna query collection | To Do | To Do | **REVISE** — this ticket is duplicated (also used for semantic view). Split into two tickets. |
| TH-929 | Tanner query collection | To Do | To Do | No change |
| TH-930 | (SME collection — verify assignment) | To Do | To Do | No change |
| TH-931 | Scrape Greg's Slack questions | To Do | To Do | **REVISE** — add description |

### Build Stage (Wk 7–11) — Partially Pull-In

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-932 | Map questions to BigQuery tables | To Do | **Partially Done** | **UPDATE → In Progress.** Agent already maps billing codes to data fields via data_dictionary.md and agent_config.yaml. Full SME-driven mapping still pending. |
| TH-933–936 | Build semantic views (Bobby, Andy, Chris K, Tanner) | To Do | To Do | No change — depends on SME input |
| TH-937–941 | 5 TBD views defined by leadership | To Do | To Do | No change |
| TH-942 | Design test front-end connection | To Do | **Complete** | **UPDATE → Done. REPHASE to Wk 5.** fledgling-muninn/web is live with authenticated chat proxy to agent backend. This is not just a "design" — it's a deployed, working frontend. |
| TH-943 | Identify view gaps & recollect | To Do | To Do | **REVISE** — add description. Will be informed by prototype testing. |
| TH-944 | Cost validation pass | To Do | To Do | **REVISE** — fix dependency (should depend on view builds, not TH-929) |
| TH-945 | Stress test prompt variations | To Do | **Partially Done** | **UPDATE → In Progress.** Prompt improvements doc shows 7 variations tested. Full stress test pending. |
| TH-946 | Document Analytical Contract v1 | To Do | To Do | No change |

---

## P2: Controlled Interaction (TH-947–950)

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-947 | Build grading framework | To Do | To Do | No change — but can start sooner since prototype is live |
| TH-948 | SME grading cycle 1 | To Do | To Do | No change — **can be pulled into Wk 8–10** now that there's something to grade |
| TH-949 | Triage & fix views | To Do | To Do | No change |
| TH-950 | SME grading cycle 2 | To Do | To Do | No change |

---

## P3: Platform Transition (TH-951–954)

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-951 | Web app scaffolding | To Do | **Complete** | **UPDATE → Done. REPHASE to Wk 5.** Next.js app scaffolded, deployed to Vercel. Resource gap note about Shawn no longer applies — Topher + Courtney shipped it. |
| TH-952 | User auth & access control | To Do | **Partially Done** | **UPDATE → In Progress. REPHASE to Wk 5.** Demo-level password auth is live. Full Firebase Auth with user provisioning still needed for production. |
| TH-953 | Client-specific GCP provisioning | To Do | To Do | No change — still future work |
| TH-954 | Integration & load testing | To Do | To Do | No change — still future work |

---

## P4: Operationalization (TH-955–958)

| Ticket | Description | JIRA Status | Actual Status | Action |
|---|---|---|---|---|
| TH-955 | Pilot deployment — HFMA dataset | To Do | To Do | No change |
| TH-956 | Client UI customization framework | To Do | To Do | No change |
| TH-957 | Operational runbooks & cost alerting | To Do | To Do | No change |
| TH-958 | Production launch & retrospective | To Do | To Do | No change |

---

## Proposed New Tickets (TH-959–969)

| Ticket | Description | Status | Action |
|---|---|---|---|
| TH-959 | P1 cost pro forma | Proposed | No change — still needed |
| TH-960 | Weekly Friday standup cadence | Proposed | **UPDATE → Done.** Standups are happening. |
| TH-961 | Build 30-week timeline | Proposed | **UPDATE → Done.** muninn-tracker is live on GitHub Pages. |
| TH-962 | Build Jira dashboard with timeline visuals | Proposed | No change — in progress with Jira migration |
| TH-963 | Document semantic layer spec template | Proposed | **REVISE** — agent_config.yaml and data_dictionary.md partially fulfill this. Scope should focus on the gap. |
| TH-964 | Document session architecture decision | Proposed | No change |
| TH-965 | Collect past deliverables as training context | Proposed | No change |
| TH-966 | Research enterprise AI pricing models | Proposed | No change |
| TH-967 | Define trackable billing metrics | Proposed | No change |
| TH-968 | Per-user cost controls feasibility | Proposed | No change — deferred to P3 |
| TH-969 | Legal review of third-party terms | Proposed | No change — deferred to P4 |

---

## Net New Tickets to Create

| Proposed ID | Description | Phase | Rationale |
|---|---|---|---|
| TH-970 | Railway backend deployment & monitoring | P3 (Done) | Captures the deployed agent infrastructure — no existing ticket covers this |
| TH-971 | Vercel frontend deployment & CI/CD | P3 (Done) | Captures the deployed web app infrastructure |
| TH-972 | Agent prompt engineering — 7 improvements | P1/P2 | Captures the prompt_improvements_for_courtney.md work (partially approved) |
| TH-973 | BigQuery MCP transition (from Vertex AI Search) | P1 | Near-term architecture evolution — no existing ticket |
| TH-974 | Prototype demo for SME team | P1 | Schedule a walkthrough so SMEs can see what their input will shape |

---

## Summary of Changes

| Action | Count |
|---|---|
| Update to Done | 5 (TH-923, TH-942, TH-951, TH-960, TH-961) |
| Update to In Progress | 3 (TH-932, TH-945, TH-952) |
| Revise scope/description | 5 (TH-928, TH-931, TH-943, TH-944, TH-963) |
| Rephase (completed earlier) | 3 (TH-942, TH-951, TH-952) |
| Net new tickets | 5 (TH-970–974) |
| No change needed | ~25 |
