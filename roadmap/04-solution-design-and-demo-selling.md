> **Stage 4 of 9 · Solution design & demo selling** — enterprise AI architecture, evals, observability, MCP connectors, and the discovery/demo rounds.
> [← 3 · AI prototypes](03-customer-facing-ai-prototypes.md) · [Back to roadmap](../README.md) · Next: [5 · AEO/GEO/SEO →](05-aeo-geo-seo-for-growth.md)

# 🎯 Solution design & demo selling

**The model is one component, not the system.** An enterprise AI solution succeeds or fails on the *supporting stack* — retrieval, evals, connectors, observability, governance — not on which foundation model you picked. This is the architecture round of a solutions-engineer interview *and* the whiteboard you draw in front of a customer. The candidate who opens a design review debating GPT-vs-Claude has lost the room; the one who opens with the seven layers and the SLOs has earned it.

## The seven-layer reference architecture

Draw them in order — each maps to one scoring axis. Turn them on one at a time (the **walking skeleton**), and *never* open with "we'll fine-tune."

```
request -> [gateway] -> [orchestrator] -> [model] -> response   (1) baseline
                     +-> [retrieval]     ground the answer      (2) + RAG
                     +-> [tools/MCP]     take actions           (3) + connectors
                     +-> [evals/guardrails]  gate quality       (4) + safety
                     +-> [observability] trace every span       (5) + telemetry
```

| Layer | What it buys | The senior detail |
|---|---|---|
| Edge / API gateway | TLS, WAF, OAuth, per-token rate limiting | the **denial-of-wallet** boundary |
| Orchestrator | agent runtime, memory, tool registry | retries, timeouts, circuit breakers |
| Retrieval | hybrid search, RBAC filtering, re-ranking | where **zero-trust retrieval** lives |
| Model | routing over ≥1 model, prefix + semantic caching | model choice is the *cheapest* thing to change |
| Tools / connectors | every external system as an MCP tool | governed, allow-listed |
| Evals & guardrails | pre-deploy checks, LLM-judge, safety filters | the differentiator round |
| Observability | span-level tracing with LLM attributes | how you explain a Friday-night incident |

> [!WARNING]
> **Security lives at the retrieval filter and the tool gateway, not the prompt.** To stop tenant A retrieving tenant B's docs, filter to `tenant_id` and the caller's ACL *before* similarity runs (Confluent's filter-then-retrieve). A permission check written into the system prompt is advisory — the model can be talked out of it. Anything you ask the model to enforce in natural language is advisory; anything you enforce in a metadata predicate or an IdP-checked tool call is a control.

**Design backwards from the SLO, not forwards from the model.** State four numbers before you draw a box — **time-to-first-token, total latency, accuracy, $/request** — and route short/cheap classification and long/hard reasoning to different models and caches. **Semantic caching** cuts $/request by an order of magnitude on repetitive traffic; **back-pressure + max-tokens** stop an agent loop from becoming a denial-of-wallet bill. And prefer **streaming CDC ingestion** over nightly ETL when the freshness SLA demands it (the "stale brain" problem) — the SLA sizes the pipeline.

## Evals: the differentiator round

The round AI-native SEs get that traditional ones don't: **"how do you know your AI is actually working?"** A thumbs-up button is one bit; an eval suite is a measurement instrument. Compose 2–3 of five metric classes:

| Class | Measures | Example |
|---|---|---|
| Deterministic / exact | did it follow the rules | JSON parses? tool called? |
| Semantic / statistical | retrieval & similarity | recall@k, NDCG, hit-rate |
| LLM-as-a-judge | open-ended quality | rubric score, pairwise win |
| Behavioral | end-to-end task success | did the agent close the task |
| Safety | harm & leakage | hallucination, jailbreak, PII |

> [!TIP]
> **The grader is production software.** Anthropic's own eval scores jumped **42% → 95% after fixing grading bugs and ambiguous task specs** — the model never changed. So: version-control graders, write a **meta-eval** (~50 fixed cases) that gates any grader change, and treat a pass-rate that leaps without a model change as a grader bug until proven otherwise. Calibrate an LLM judge to **≥80% human agreement** on a 30–50 case labeled set and use it as a *first pass*, not an oracle. You need **both** offline gates (frozen golden set in CI) and online detection (sample >5% of traffic, drift dashboard). Grade agents on the **trajectory**, not just the outcome.

## Observability: TTFT is the new p95

Observability is what lets you tell a customer, in a Friday-night incident review, *exactly* what the system did. **Aggregates hide the problem** — instrument the span, not the dashboard average. The minimum LLM span schema: `model.id`, `prompt.version` + hash, `retrieval.chunk_ids` + scores, `tool.calls`, token counts (in/out/cached/total), and **TTFT split from total latency**, plus `tenant`/`cohort`. Intercom cut **median response time by 2 seconds** on Fin.ai by wrapping TTFT as its own span. Close the loop: capture multi-bit signals on traces → classify into named failure modes with an LLM → fix the top bucket → **feed fixes back as new golden-set eval cases.** A team without this loop relearns the same failure every quarter.

## MCP & enterprise connectors: N×M → N+M

The **Model Context Protocol** is the default substrate for connecting AI to a customer's systems: a **host / client / server** model over **JSON-RPC 2.0** (stdio or streamable HTTP). Servers expose **Resources / Prompts / Tools**. Its value is **uniformity** — integration collapses from N×M bespoke glue to **N+M** conforming endpoints (5 servers × 3 agents without MCP = 15 OAuth implementations, 15 credential stores, 15 audit trails).

| | Without a gateway | With an MCP gateway |
|---|---|---|
| Credentials | 15 OAuth implementations | 1 credential broker |
| Policy | per-agent raw tokens (risk) | 1 allow-list + IdP RBAC |
| Audit | 15 scattered trails | 1 unified log |

> [!NOTE]
> **A tool call is arbitrary code execution.** MCP names three security principles in the spec: **user consent, tool-exec caution, sampling control.** Enterprise adds IdP + zero-trust on top. Past ~5 servers, route through a gateway (**Runlayer** raised $11M to run 18,000+ servers behind Okta/Entra; or compose one with **Speakeasy/Tyk**). Build vs buy is the same axis everywhere: **buy the governance layer for time-to-compliance, compose open primitives for portability** — and name the tradeoff, don't just pick.

## Discovery & demo selling: you earn the right to demo

The deals you win are the ones where the champion can re-tell your value story to their CFO when you're not in the room. The SE discovery stack is five overlapping frameworks; the senior skill is knowing which to lead with:

- **MEDDPICC** — qualification baseline; the high-leverage letters are **I** (Implicate pain), **C** (Champion), **D** (decode the RFP scorecard).
- **SPIN** — the **Implication question** is the SE's signature move: it turns a complaint into a *quantified downstream cost in the customer's own voice* ("noisy alerts cost 8–12 hrs/eng/week"). You write *their* number on the whiteboard.
- **Challenger** — the **Reframe**: change how the buyer thinks *before* showing the product (when they pattern-match your AI agent to "another rules bot we tried").
- **Command of the Message** — Before / Required Capabilities / Positive Business Outcomes, in the champion's vocabulary.
- **ValueSelling** — talk to the economic buyer in dollars.

> [!TIP]
> **Anchor ROI in a credible range — 200–600% is realistic; 50% loses the room** (high enough to need approval, low enough to feel optimistic — the worst combination). Attach one dollar figure per value lever (**productivity, revenue, cost reduced, risk mitigated**) as a **From → To → Gap** worksheet with the *customer's* numbers, and **hand it to the champion in their language** so they deliver it as their own. A story only you can tell dies in committee. AI discovery adds a filter: **data readiness** — scope a fixed-scope data validation as milestone one, or the PoC fails in week three after the champion has spent political capital.

The demo round (30–45 min) is scored on **substance over tour**: 5–7 min of slides, ~10 min of a focused hero/problem/resolution demo on the three capabilities that map to *quantified pains*, then Q&A and re-anchor on the customer's number. Cut any capability the customer never named. When asked something you're unsure of: **summarize it back, answer what you can, commit to verify against the docs** — never fabricate on the record.

## 📚 Resources

- 💻 [Agents Towards Production](https://github.com/NirDiamant/agents-towards-production) — **repo · MIT.** The build → eval → deploy → monitor → security playbook behind the seven layers.
- 🎬 [Lessons from a Year of Building with LLMs](https://youtube.com/watch?v=c0gcsprsFig) — Vanishing Gradients (Hamel Husain, Eugene Yan, Jason Liu). The stack-over-model thesis, from practitioners.
- 🎬 [How to Construct Domain-Specific LLM Evaluation Systems](https://youtube.com/watch?v=eLXF0VojuSs) — Hamel Husain & Emil Sedgh (AI Engineer). The eval harness, end to end.
- 📘 [Evidently LLM evaluation docs](https://docs.evidentlyai.com/) — the five metric classes, LLM-as-judge calibration to >80% human agreement. Open-source.
- 🎬 [Building Agents with Model Context Protocol — Full Workshop](https://youtube.com/watch?v=kQmXtrmQ5Zg) — Mahesh Murag, Anthropic (AI Engineer). MCP host/client/server, hands-on.
- 📘 [Model Context Protocol spec](https://modelcontextprotocol.io/) — **docs.** The topology, primitives, transports, and the named security principles.
- 🎬 [Discovery Masterclass](https://youtube.com/watch?v=y0H6G7toc9s) — 30 Minutes to President's Club. SPIN implication questions in practice.
- 🎬 [Power Presenting in PreSales](https://youtube.com/watch?v=431K33x7mQ4) — PreSales Collective. The demo-as-storytelling craft.

---

**Next:** [5 · AEO / GEO / SEO for growth →](05-aeo-geo-seo-for-growth.md) — getting cited by ChatGPT, Perplexity, and Gemini.
