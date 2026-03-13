# ODIN / Muninn — Progress Update
**Date:** March 13, 2026 | **Week 6 of 30**

---

## Executive Summary

We are running a **concurrent development model** — building the operational platform in parallel with the semantic foundation work, rather than following the original sequential plan. Infrastructure and deployment are ahead of the original timeline. Agent behavior and data coverage need further work before the system is demo-ready.

---

## What Has Been Shipped (Proof in GitHub)

Below is a plain-English translation of what the engineering team has delivered, mapped to the original phase plan.

### Delivered: Agent Intelligence Engine — Infrastructure
**Originally planned:** P1, Weeks 7–11 (Semantic Foundation — Build stage)
**Actually delivered:** Week 6

The core agent is operational and connected to the Vertex AI Search data store. It can:
- Accept natural-language queries about healthcare rates and route them to the appropriate sub-agent (web search, URL context, or Vertex AI Search)
- Retrieve negotiated rate data for billing codes that exist in the current data sample
- Return rate ranges, carrier names, provider types, and Medicare benchmark comparisons for matched codes

**Current limitations:**
- The data store contains a **randomized 1M-row sample of v7 national data**, not a targeted geographic or code-specific slice. This means many billing code queries return no results — the agent cannot predict which codes have sufficient data density in the sample.
- The agent does not always use its data search tools on the first attempt. In some sessions, it responds with "I cannot access the data" rather than delegating to its Vertex AI Search sub-agent. Starting a fresh session or rephrasing the query typically resolves this.
- Vertex AI Search is a semantic search tool, not a structured database query. It cannot perform aggregation (e.g., "which carriers appear most frequently") or return results in a consistent tabular format.
- Output formatting varies between sessions. The agent sometimes produces structured tables and sometimes returns unstructured text for the same query.
- Most confidence scores in the sample data are 0 (Not assigned) or 1 (Unverified).

**What this means:** The agent infrastructure works end-to-end. When queried with a billing code that has sufficient density in the sample (e.g., CPT 99213), the agent returns a tabular breakdown of negotiated rates across carriers, provider types, and geographies — including rate ranges and Medicare benchmark data. However, queries need to be pre-tested against the sample data, and results vary between sessions.

**Example result (CPT 99213 — established patient office visit):**

When queried for CPT 99213, the agent returned a 26-row comparison table spanning 9 states (CA, TX, KY, KS, TN, IA, CO, ID, IL), with rates ranging from $30.54 (Counselor, nonmetropolitan Kentucky, Anthem BCBS Central) to $267.37 (Plastic Surgery, Sacramento CA, Anthem Blue Cross CA). Carriers represented included Aetna, Cigna, Anthem Blue Cross CA, Anthem BCBS Central, and BCBS TX. Provider types ranged from Family Medicine and Internal Medicine to Surgery and Orthopaedic Surgery. This confirms the data sample is national in scope and contains meaningful rate variation for high-volume codes.

**Tested billing codes:**
- **99213** (established patient office visit): Returns data successfully with tabular output
- **80053** (comprehensive metabolic panel): No results in sample
- **27447** (total knee replacement): No results in sample

Further testing is needed to identify additional codes that return good results from the current sample.

---

### Delivered: Web Application Framework with Authentication
**Originally planned:** P3, Weeks 17–20 (Platform Transition — web app scaffolding & auth)
**Actually delivered:** Week 6

A working web application framework is live at **fledgling-muninn.vercel.app** with:
- Login/logout with session management
- Protected routes (only authenticated users can access the chat)
- A clean chat interface for querying the agent

**What this means:** The framework is in place — we know what the product looks like and can interact with it at this stage. The production deployment will need to move to a Google Cloud-hosted application for cost controls, traffic management, and alignment with our GCP infrastructure. That transition may require someone with cloud deployment experience.

---

### Delivered: Prototype Cloud Deployment (Backend + Frontend)
**Originally planned:** P3–P4, Weeks 17–30 (Platform Transition & Operationalization)
**Actually delivered:** Week 6

- **Backend:** Agent hosted on Railway (cloud platform) with health monitoring and secure credential management
- **Frontend:** Web app deployed on Vercel with automatic updates when code changes
- Both systems are live and connected

**What this means:** We have a working prototype deployment that anyone can access. The production architecture will transition to Google Cloud, but the framework and interaction model are proven.

**Cost note:** On the heaviest usage day (Wednesday), Vertex AI incurred a total charge of **$0.30**. Token costs are negligible — the real cost consideration at scale will be data storage and access, not LLM inference.

---

### Delivered: Semantic Layer — Prompt Engineering & Data Quality Controls
**Originally planned:** P1, Weeks 7–11 (Build stage) and P2, Weeks 13–16 (Controlled Interaction)
**Actually delivered:** Week 6

Seven prompt improvements to the agent's analytical instructions have been developed and most have been approved by Courtney as prompt text changes:
1. Billing code normalization (prevents data mismatches)
2. Confidence scoring (shows data quality per result)
3. Medicare comparison rates (industry-standard "% of Medicare" metric)
4. Rate source transparency
5. Provider taxonomy grouping
6. Metropolitan-area geographic grouping
7. Methodology explanation capability

**Current status:** These improvements are written and incorporated into the agent's prompt instructions. However, **they have not been validated against live query results.** The prompt tells the agent *how* to format and contextualize data, but whether the Vertex AI Search tool returns data in a form that supports these instructions has not been confirmed for most of them. Validation depends on finding billing codes with sufficient data density in the sample and resolving the agent's inconsistent tool usage.

**Key insight from Courtney:** The prompt instructions *are* the semantic layer — they define how the agent interprets and presents data. The underlying data tables (DaaS v7) already embed significant SME logic — Bobby, Chris, and the team built the framework, the metrics, the Medicare benchmarks, and the post-processing rules that the agent draws from. Additional SME feedback will refine and validate, but we are not starting from zero.

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
| **P1: Semantic Foundation** (Wk 5–12) | Active — Collect stage | Active — Collect running concurrently with Build. Prompt improvements written; validation pending. |
| **P2: Controlled Interaction** (Wk 13–16) | Not started | Partially started — prompt quality controls written but not yet validated against live results |
| **P3: Platform Transition** (Wk 17–22) | Not started | **Framework complete** — web app, auth, and prototype deployment live. Production will need Google Cloud hosting. |
| **P4: Operationalization** (Wk 23–30) | Not started | Prototype infrastructure deployed; production hardening not started |

---

## Known Technical Issues

1. **Agent tool delegation** — The agent sometimes says "I cannot access the data" instead of using its Vertex AI Search sub-agent, particularly in longer sessions. Starting a fresh session or rephrasing the query typically resolves this. A prompt fix to add explicit delegation instructions is identified but not yet deployed.
2. **Data sample coverage** — The 1M-row randomized sample means many specific queries (code + geography + carrier) will miss. High-volume codes like 99213 return rich results; less common codes may return nothing. This will be resolved by the BigQuery MCP transition with full dataset access.
3. **Output formatting** — The agent produces structured tables in some sessions but returns unstructured text in others for the same query. Phrasing the request to explicitly ask for a table improves consistency.
4. **Vertex AI Search limitations** — Semantic search cannot perform aggregation, counting, or structured filtering. Questions like "which carriers are most common" or "show me all rates in Houston" are outside its capabilities. The BigQuery MCP transition will resolve this.
5. **Data version** — The current sample is v7 data. The v8 schema (which includes `billing_code_norm` and other improvements) will arrive with the BigQuery MCP transition.

---

## What's Actually Left to Build

Despite the acceleration in infrastructure, significant work remains:

1. **Agent behavior reliability** — Resolving tool delegation issues and output formatting so the agent consistently uses its data tools and returns structured results
2. **Demo-ready query list** — Identifying billing codes and queries that return good results from the current data sample, so demos can be conducted confidently
3. **SME feedback integration** — The prototype needs to be shaped by domain expert input (pending post-processing completion)
4. **Google Cloud production deployment** — Moving from Railway/Vercel prototype to GCP-hosted application for cost controls, traffic management, and infrastructure alignment. May require cloud deployment expertise.
5. **BigQuery MCP transition** — Moving from Vertex AI Search to direct SQL queries for better precision, aggregation capabilities, and full dataset access. This is the single most impactful change for query reliability.
6. **Per-client GCP isolation** — Cost governance and project separation for production clients
7. **Firebase Auth** — Full user provisioning beyond the current demo-level password
8. **Cost validation** — Confirming the <$1/query and $200/mo per-client targets hold (early signal: $0.30 on heaviest usage day)
9. **Grading cycles** — Structured evaluation by internal testers, now blended with SME input (P1.5 approach)
10. **Legal & liability framework** — Disclaimers for data-driven business decisions, hallucination risks, and data representation limitations. Bobby has flagged discomfort with clients making consequential decisions (hiring, pricing) based on this data without appropriate guardrails. Need CYA language similar to AMA's "not legal/consulting advice" disclaimers.
11. **Pilot deployment** — HFMA/MMA dataset onboarding and client-facing rollout

---

## Recommended Next Steps

1. **Fix agent tool delegation** — Deploy the prompt change so the agent uses its Vertex AI Search tool proactively
2. **Build a tested demo query list** — Systematically test common billing codes against the sample to find 5–10 that return good results
3. **Update JIRA tickets** to reflect completed work and revised timeline (reconciliation map prepared)
4. **Update the 30-week tracker** to show concurrent workstreams and pulled-in milestones
5. **Schedule a brief demo** for the broader team once demo queries are validated, so SMEs can see what they're providing input *for*
6. **Continue SME outreach** — their input shapes the *refinement*, not the *foundation*

---

*Prepared by Topher Rasmussen | Third Horizon*
