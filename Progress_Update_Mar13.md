# ODIN / Muninn — Progress Update
**Date:** March 13, 2026 | **Week 6 of 30**

---

## Executive Summary

We are **ahead of schedule.** Work originally planned for Phases 3–4 (Weeks 17–30) has been completed in Weeks 5–6 due to accelerated prototyping. The original 30-week plan assumed a strictly sequential build; instead, we have been running a **concurrent development model** — building the operational platform in parallel with the semantic foundation work.

**The term for this in project management is a "schedule pull-in"** — planned work was completed earlier than projected because conditions allowed it. The plan isn't broken; it has been compressed in key areas.

---

## What Has Been Shipped (Proof in GitHub)

Below is a plain-English translation of what the engineering team has delivered, mapped to the original phase plan.

### Delivered: Agent Intelligence Engine
**Originally planned:** P1, Weeks 7–11 (Semantic Foundation — Build stage)
**Actually delivered:** Week 5

The core "brain" of the platform is operational. It can:
- Query ~1 million rows of real healthcare rate data (Starset Analytics DaaS v8)
- Return structured comparison tables with negotiated rates, provider types, top carriers, and Medicare benchmarks
- Distinguish between carrier-sourced, provider-sourced, and actuarially-estimated rates
- Group results by metropolitan area and provider specialty (not just raw provider names)
- Surface data quality scores so users know how reliable each result is
- Explain its methodology (CMS-mandated Transparency in Coverage data)

**What this means:** A user can ask a question like *"Compare negotiated rates for billing code 99213 in Texas"* and receive a formatted, analyst-grade response — today.

---

### Delivered: Web Application Framework with Authentication
**Originally planned:** P3, Weeks 17–20 (Platform Transition — web app scaffolding & auth)
**Actually delivered:** Week 5

A working web application framework is live at **fledgling-muninn.vercel.app** with:
- Login/logout with session management
- Protected routes (only authenticated users can access the chat)
- A clean chat interface for querying the agent

**What this means:** The framework is in place — we know what the product looks like and can interact with it at this stage. The production deployment will need to move to a Google Cloud-hosted application for cost controls, traffic management, and alignment with our GCP infrastructure. That transition may require someone with cloud deployment experience.

---

### Delivered: Prototype Cloud Deployment (Backend + Frontend)
**Originally planned:** P3–P4, Weeks 17–30 (Platform Transition & Operationalization)
**Actually delivered:** Week 5

- **Backend:** Agent hosted on Railway (cloud platform) with health monitoring and secure credential management
- **Frontend:** Web app deployed on Vercel with automatic updates when code changes
- Both systems are live and connected

**What this means:** We have a working prototype deployment that anyone can access. The production architecture will transition to Google Cloud, but the framework and interaction model are proven.

**Cost note:** On the heaviest usage day (Wednesday), Vertex AI incurred a total charge of **$0.30**. Token costs are negligible — the real cost consideration at scale will be data storage and access, not LLM inference.

---

### Delivered: Semantic Layer — Prompt Engineering & Data Quality Controls
**Originally planned:** P1, Weeks 7–11 (Build stage) and P2, Weeks 13–16 (Controlled Interaction)
**Actually delivered:** Week 5–6

Seven major improvements to the agent's analytical capabilities have been developed, with most approved by Courtney:
1. Billing code normalization (prevents data mismatches)
2. Confidence scoring (shows data quality per result)
3. Medicare comparison rates (industry-standard "% of Medicare" metric)
4. Rate source transparency
5. Provider taxonomy grouping
6. Metropolitan-area geographic grouping
7. Methodology explanation capability

**What this means:** The agent doesn't just return numbers — it returns *contextualized, trustworthy analysis* with the quality controls that a healthcare data analyst would expect.

**Key insight from Courtney:** The prompt instructions *are* the semantic layer — they define how the agent interprets and presents data. Furthermore, the agent is already understanding the context of the data far beyond initial expectations with minimal prompt engineering. The underlying data tables (DaaS v8) already embed significant SME logic — Bobby, Chris, and the team built the framework, the metrics, the Medicare benchmarks, and the post-processing rules that the agent draws from. In a meaningful sense, SME input is already present in the data itself. Additional SME feedback will refine and validate, but we are not starting from zero.

---

## What's Running Concurrently (Not Blocked)

The original plan treated SME input gathering (P1 Collect stage) as a prerequisite for everything else. In practice, we are treating it as a **parallel workstream**:

| Workstream | Status | Why It's Not a Blocker |
|---|---|---|
| SME query collection (Bobby, Andy, Chris K, Tanner, Jenna) | Outreach emails sent; awaiting responses | We have a working prototype that can be refined based on their input rather than waiting to start |
| Greg's Slack question scraping | To do | Same — input will refine, not gate, the build |
| Top 25 question prioritization | In progress | Prototype allows us to test questions as they come in rather than batching |

**The shift:** Instead of *"collect all input → then build"*, we are doing *"build a working prototype → collect input → iterate based on feedback."* This is faster and produces better results because SMEs can react to something tangible rather than filling out forms in the abstract.

**Why SME responses are pending:** The data team is still in post-processing — they were expected to finish last week but are still working through it. Once post-processing wraps, SMEs will have freed capacity to engage with the prototype and provide input. We are ready to launch the prototype for testing as soon as that window opens.

**Important nuance:** The controlled interaction phase (P2) and SME input gathering are now blended — not sequential. Instead of completing P1 Collect, then P1 Build, then P2 Grading, we are running a "P1.5" where SMEs can begin interacting with the prototype, grading responses, and surfacing gaps concurrently with the build.

---

## Revised Phase View

| Phase | Original Timeline | Actual Status |
|---|---|---|
| **P0: Architecture** (Wk 1–4) | Complete | Complete |
| **P1: Semantic Foundation** (Wk 5–12) | Active — Collect stage | Active — Collect running concurrently with Build |
| **P2: Controlled Interaction** (Wk 13–16) | Not started | Partially started — prompt quality controls in place |
| **P3: Platform Transition** (Wk 17–22) | Not started | **Framework complete** — web app, auth, and prototype deployment live. Production will need Google Cloud hosting. |
| **P4: Operationalization** (Wk 23–30) | Not started | Partially started — production infrastructure deployed |

---

## What's Actually Left to Build

Despite the acceleration, significant work remains:

1. **SME feedback integration** — The prototype needs to be shaped by domain expert input (pending post-processing completion)
2. **Google Cloud production deployment** — Moving from Railway/Vercel prototype to GCP-hosted application for cost controls, traffic management, and infrastructure alignment. May require cloud deployment expertise.
3. **BigQuery MCP transition** — Moving from Vertex AI Search to direct SQL queries for better precision and cost efficiency
4. **Per-client GCP isolation** — Cost governance and project separation for production clients
5. **Firebase Auth** — Full user provisioning beyond the current demo-level password
6. **Cost validation** — Confirming the <$1/query and $200/mo per-client targets hold (early signal: $0.30 on heaviest usage day)
7. **Grading cycles** — Structured evaluation by internal testers, now blended with SME input (P1.5 approach)
8. **Legal & liability framework** — Disclaimers for data-driven business decisions, hallucination risks, and data representation limitations. Bobby has flagged discomfort with clients making consequential decisions (hiring, pricing) based on this data without appropriate guardrails. Need CYA language similar to AMA's "not legal/consulting advice" disclaimers.
9. **Pilot deployment** — HFMA/MMA dataset onboarding and client-facing rollout

---

## Recommended Next Steps

1. **Update JIRA tickets** to reflect completed work and revised timeline (reconciliation map prepared)
2. **Update the 30-week tracker** to show concurrent workstreams and pulled-in milestones
3. **Schedule a brief demo** for the broader team so SMEs can see what they're providing input *for*
4. **Continue SME outreach** — their input shapes the *refinement*, not the *foundation*

---

*Prepared by Topher Rasmussen | Third Horizon*
