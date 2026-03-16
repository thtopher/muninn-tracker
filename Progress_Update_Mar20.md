# ODIN / Muninn — Progress Update
**Date:** March 20, 2026 | **Week 7 of 30**

---

## Executive Summary

The prototype received its first live CEO demo and the reaction was strongly positive. David interacted with the agent in real time, querying billing codes and seeing tabular results with confidence indicators. The conversation surfaced a concrete near-term use case — rate book generation — and established a clear data expansion plan: moving from 1M randomized rows to 5M rows of V8 data covering Illinois and Virginia. V8 post-processing is nearly complete, which will also unblock SME engagement.

---

## What Happened This Week

### CEO Demo — Live Prototype Walkthrough
**Date:** March 13, 2026

David logged into the prototype at **fledgling-muninn.vercel.app**, queried negotiated rates for CPT 99213, and received structured results including confidence indicators and Medicare benchmarks. His reaction was emphatic — he called out the confidence indicators as a standout feature and said the team was "the first people in seven hours that actually got my heart pumping."

Key observations from the demo:
- The password-protected login worked seamlessly
- The agent returned meaningful results for CPT 99213 with IP Medicare benchmarks and OP data
- Confidence indicators surfaced naturally in the response — David noticed and praised them unprompted
- David attempted additional queries that hit the edges of the 1M-row sample, confirming the need for a larger, geographically targeted dataset

### Data Expansion Plan Agreed
Based on the demo, the following data plan was agreed upon:

| Parameter | Current | Next |
|---|---|---|
| **Row count** | 1M (randomized, v7) | 5M (targeted, v8) |
| **Geography** | National (random scatter) | Illinois + Virginia |
| **Data version** | v7 | v8 (post-processing nearly complete) |
| **Purpose** | Proof of concept | Demo-ready with predictable coverage |

- **Illinois** was a direct request from David ("let me play a CEO card — do Chicago")
- **Virginia** was a prior recommendation from Chris Hart (though Courtney noted some confusion between data versions and state selections during the call — may need confirmation)
- Courtney confirmed V8 post-processing is nearly complete and will align with the data expansion

### Cost Benchmarking Priority
David requested a structured cost analysis across data sizes to inform the business model:

- **1M rows** — current baseline ($0.30 peak day)
- **5M rows** — next milestone
- **10M rows** — projection target

The goal is three data points to extrapolate cost-per-inquiry at production scale. This will feed directly into the development cost pro forma (TH-959) and enterprise pricing model (TH-966).

### Rate Book Use Case Emerged
David identified rate book generation as a practical, near-term application of the platform. The concept: load a complete behavioral health (BH) rate book for a small market and test whether the agent can serve it effectively. This could be a more practical first use case than open-ended Q&A.

**Action items:**
- Chris to provide an extract of what would go into a rate book for a state like Virginia
- Test with the smallest market we can find for a full BH rate book
- Evaluate row count requirements (likely significantly more than 5M for a full rate book)

### Cross-Model Capability Flagged
David asked whether Vertex can wire API calls with Anthropic/Claude. This aligns with the future need for:
- **Visuals and charts** — not high priority now, but needed at launch
- **Data export** — ability to port and download results
- **Research-grade LLM** — market analysis, trend identification
- **Template mapping** — auto-populating parity rate book templates

Feasibility assessment is needed but multi-model architectures are common in production systems.

### SME Outreach — No Responses Yet
No SME responses were received this week. However:
- V8 post-processing is nearly complete, which was the primary reason SMEs were unavailable
- David noted the data team is entering a ~30-day window of reduced workload
- Plan is to share the prototype link with SMEs once the data expansion is loaded, so they can react to something tangible rather than answering in the abstract

---

## What Has Changed Since Last Week

| Item | Mar 13 Status | Mar 20 Status |
|---|---|---|
| CEO demo | Not yet conducted | Completed — strong positive reaction |
| V8 post-processing | In progress | Nearly complete |
| Data expansion plan | Not defined | Agreed: 5M rows, IL + VA, v8 |
| Cost benchmarking | Single data point ($0.30) | Three-tier analysis requested (1M/5M/10M) |
| Rate book use case | Not identified | Emerged as practical near-term application |
| Cross-model capability | Not discussed | Flagged as future need |
| SME responses | Outreach sent, awaiting | Still awaiting — window opening soon |

---

## Revised Phase View

| Phase | Original Timeline | Actual Status |
|---|---|---|
| **P0: Architecture** (Wk 1–4) | Complete | Complete |
| **P1: Semantic Foundation** (Wk 5–12) | Active — Collect stage | Active — Build running ahead of Collect. Data expansion to 5M/v8 in progress. Prompt improvements written; validation pending against expanded dataset. |
| **P2: Controlled Interaction** (Wk 13–16) | Not started | Partially started — CEO completed first live interaction with prototype. SME testing pending data expansion. |
| **P3: Platform Transition** (Wk 17–22) | Not started | **Framework complete** — web app, auth, and prototype deployment live. Production GCP transition not started. |
| **P4: Operationalization** (Wk 23–30) | Not started | Rate book use case identified as potential first pilot vehicle. |

---

## Known Technical Issues

1. **Agent tool delegation** — Still inconsistent. The agent sometimes says "I cannot access the data" instead of using its Vertex AI Search sub-agent. Prompt fix identified but not yet deployed.
2. **Data sample coverage** — The 1M-row randomized sample means many queries miss. The 5M-row IL+VA expansion will provide predictable coverage for demos.
3. **Output formatting** — Varies between sessions. Structured tables appear when the query is well-matched to available data.
4. **Vertex AI Search limitations** — Cannot perform aggregation or structured filtering. BigQuery MCP transition remains the most impactful fix.
5. **Cross-model integration** — Vertex + Anthropic API feasibility not yet assessed.

---

## True by Next Friday (Mar 27)

Based on the Mar 13 discussion, the agreed commitments for this week:

1. **Dev environment with larger tables** — 5M-row V8 dataset loaded with Illinois and Virginia coverage, available for testing
2. **Begin rounding up data team** — Leverage the 30-day post-processing window to schedule SME interactions with the prototype

**Also discussed (not explicitly committed as "true by Friday"):**
- **Cost benchmarking** — David requested a three-tier cost analysis (1M/5M/10M rows) to inform the business model. This was discussed earlier in the meeting but was not part of the formal "true by Friday" alignment.

*Note: The alignment was cut short — Topher had to leave unexpectedly. David asked "what else needs to be true for next week?" but the conversation ended before additional items could be agreed upon.*

---

## What's Actually Left to Build

1. **Data expansion** — Load 5M V8 rows (IL + VA) and validate agent performance against larger, targeted dataset
2. **Agent behavior reliability** — Fix tool delegation and output formatting inconsistencies
3. **Cost benchmarking** — Three-tier analysis (1M/5M/10M) to inform business model
4. **Rate book feasibility** — Assess whether the agent can serve a complete BH rate book for a small market
5. **SME feedback integration** — Launch prototype testing with data team during the 30-day window
6. **Cross-model evaluation** — Assess Vertex + Anthropic integration for research-grade analysis and visual generation
7. **BigQuery MCP transition** — Still the single most impactful change for query reliability and aggregation
8. **Google Cloud production deployment** — Move from Railway/Vercel to GCP for production
9. **Legal & liability framework** — Disclaimers and CYA language before pilot
10. **Pilot deployment** — Rate book use case may accelerate this timeline

---

*Prepared by Topher Rasmussen | Third Horizon*
