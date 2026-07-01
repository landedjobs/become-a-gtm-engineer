<div align="center">

<img src="https://static.b100x.ai/email/landed-wordmark.png" alt="Landed" width="300" />

# Become a GTM Engineer

**The annotated 2026 roadmap to the highest-leverage new revenue role — code + AI applied to go-to-market, built the way senior teams actually build it.**

[![Stars](https://img.shields.io/github/stars/landedjobs/become-a-gtm-engineer?style=social)](https://github.com/landedjobs/become-a-gtm-engineer)
[![License: MIT](https://img.shields.io/badge/License-MIT-6C2BD9.svg)](LICENSE)
[![Updated](https://img.shields.io/badge/updated-2026--07-00A86B)](#whats-new)
[![Stages](https://img.shields.io/badge/stages-9-6C2BD9)](#the-roadmap)
[![Resources](https://img.shields.io/badge/annotated%20resources-70+-6C2BD9)](#the-roadmap)
[![Questions](https://img.shields.io/badge/self--check-86%20Qs-6C2BD9)](skills-check.md)
[![Visit Landed](https://img.shields.io/badge/Visit-Landed-6C2BD9?logo=rocket&logoColor=white)](https://landed.jobs)

*Maintained by [Landed](https://landed.jobs) — daily AI-native job matches, agent help with every application, and mock-interview prep.*

</div>

---

A **GTM Engineer** is what a marketer, SDR, or RevOps operator becomes when the job turns technical. Skaled (Nov 2025) calls the role **"the revenue org's AI operator"** — someone who *"actively builds AI-powered systems that automate, augment, and accelerate go-to-market performance."* Tabula (2026) sharpens it against the neighbours: the GTM Engineer is the **"builder"** who *"connects systems, automates workflows, and creates technical scaffolding for Sales, Marketing, and CS,"* while **RevOps is the "conductor"** (governance, forecasts) and the **Sales Engineer is the "translator"** (de-risking technical objections). Clay coined the title in 2023; it now sees roughly **100 job listings a month**, with Anthropic, Notion, Canva, Intercom, Cursor, and ElevenLabs among the named adopters. Base comp lands around **$180K–$240K** with **$230K–$310K OTE**.

This repo is the roadmap: **9 stages**, each a one-concept-per-file lecture pulled from senior practice, with typed, annotated, capped resource links and an 86-question self-assessment. It is an *index* — the depth lives in [`roadmap/`](roadmap/).

> ⭐ **Star this repo** — it's a living, dated-2026 roadmap refreshed as the stack and the role evolve.

```mermaid
flowchart LR
    S0["🧭 0 · What it is"] --> S1["🏗️ 1 · The GTM stack"]
    S1 --> S2["🤖 2 · AI automation"]
    S2 --> S3["🧪 3 · AI prototypes"]
    S3 --> S4["🎯 4 · Solution design & demo"]
    S4 --> S5["🔎 5 · AEO / GEO / SEO"]
    S5 --> S6["🛠️ 6 · Tools & stack"]
    S6 --> S7["📦 7 · Portfolio projects"]
    S7 --> S8["📚 8 · Repos & academies"]
    style S0 fill:#6C2BD9,color:#fff
    style S2 fill:#6C2BD9,color:#fff
    style S4 fill:#6C2BD9,color:#fff
    style S7 fill:#00A86B,color:#fff
```

## Contents

- [The 2026 GTM engineering stack](#the-2026-gtm-engineering-stack) — the signature layer map
- [The roadmap](#the-roadmap) — 9 stages, each deep-linking into [`roadmap/`](roadmap/)
- [Tools every GTM engineer should know (2026)](#tools-every-gtm-engineer-should-know-2026)
- [Portfolio projects](#portfolio-projects) → [`projects/`](projects/)
- [Skills check (86 questions)](skills-check.md)
- [What's new](#whats-new)
- [FAQ](#faq)
- [Contributing](#contributing)

---

## The 2026 GTM engineering stack

The canonical modern stack is a **layer cake**: CRM → enrichment → warehouse → reverse-ETL → iPaaS → sequencing → AI-automation. The slow-changing bottom layers (schema, ICP, lifecycle) set the ceiling for every faster layer above; **sequence bottom-up — schema-first, plumbing-second, AI-third.**

| Layer | What it does | Named tools (2026) | Learn it |
|---|---|---|---|
| **CRM** (system of record) | Objects, lifecycle stages, the join graph everything reports off | HubSpot · Salesforce | [1 · The GTM stack](roadmap/01-the-gtm-stack.md) |
| **Enrichment** | Fill missing emails/firmographics via a provider *waterfall* | Clay · Apollo · ZoomInfo | [1 · The GTM stack](roadmap/01-the-gtm-stack.md) |
| **Warehouse** | The analytical source of truth for scoring & modeling | Snowflake · BigQuery · Postgres | [6 · Tools & stack](roadmap/06-tools-and-stack.md) |
| **Reverse-ETL** | Push warehouse-scored rows back into the CRM / tools | Hightouch · Census | [6 · Tools & stack](roadmap/06-tools-and-stack.md) |
| **iPaaS / automation** | The glue: webhooks, branching, retries, dead-letter | n8n · Zapier · Make · Workato | [1](roadmap/01-the-gtm-stack.md) · [2](roadmap/02-ai-automation-for-gtm.md) |
| **Sequencing** | Multi-touch outbound + deliverability | Outreach · Salesloft | [1 · The GTM stack](roadmap/01-the-gtm-stack.md) |
| **AI-automation** | LLM enrichment, personalization, agents, evals | OpenAI · Anthropic · Claygent · LangGraph | [2](roadmap/02-ai-automation-for-gtm.md) · [3](roadmap/03-customer-facing-ai-prototypes.md) |

> [!TIP]
> In an interview, the strong answer to *"connect Clay, Salesforce, and HubSpot into one source of truth"* is not "turn on the native sync." It's: draw the join graph (**Company/Account → Contact → Opportunity**), place Clay **upstream**, and specify **one-way writes with dedup-before-write and provenance fields** (source, confidence, enrichment status). Provenance over raw value is the rubric signal.

---

## The roadmap

Nine stages. Each links into a full lecture in [`roadmap/`](roadmap/) with concepts, tables, senior traps, and a capped block of typed, annotated resources.

### [0 · What "GTM Engineer" means in 2026](roadmap/00-what-is-a-gtm-engineer.md)
The role, the money, and the three-way distinction interviewers test hard: **GTM Engineer (builder) vs RevOps (conductor) vs Sales Engineer (translator).** How named companies (Notion, Canva, Anthropic, Intercom) actually structure the team — and why every one of them separates *pilot* from *production*. → [read](roadmap/00-what-is-a-gtm-engineer.md)

### [1 · The GTM stack, built right](roadmap/01-the-gtm-stack.md)
RevOps as an operating model, not a tool. The funnel as a **state machine on a record**, CRM data modeling (Salesforce Account-centric vs HubSpot Contact-centric), the **four-layer dedup cascade** (normalize → hash → fuzzy → semantic), and the API/webhook spine: **HMAC + timestamp, idempotency keys, distributed rate limits, backoff + dead-letter.** → [read](roadmap/01-the-gtm-stack.md)

### [2 · AI automation for GTM](roadmap/02-ai-automation-for-gtm.md)
Where AI actually adds value in the funnel (usually **segmentation**, not the first email line). The enrichment **waterfall** as a cost lever, verification before send, **gating AI columns** so Claygent never hallucinates on a signal-less row, additive-scoring footguns, and the **low-code-front-door / custom-code-second-floor** rule. → [read](roadmap/02-ai-automation-for-gtm.md)

### [3 · Customer-facing AI prototypes](roadmap/03-customer-facing-ai-prototypes.md)
Build a convincing LLM demo in an afternoon: start from the cookbook, lock output with **strict-mode tool calls**, ground answers in the customer's docs (**Search-Ask + citation panel + enforced refusal**), and gate it with a **20-question smoke test** before you ever click "share screen." Plus agents: the Thought-Action-Observation loop and the human-in-the-loop gate. → [read](roadmap/03-customer-facing-ai-prototypes.md)

### [4 · Solution design & demo selling](roadmap/04-solution-design-and-demo-selling.md)
The enterprise **seven-layer reference architecture**, evals as the differentiator (**the grader is production code**; the 42%→95% trap), observability (**TTFT is the new p95**), MCP connectors (**N×M → N+M**), and the discovery/demo rounds (**SPIN implication questions, Challenger reframe, 200–600% ROI ranges**). → [read](roadmap/04-solution-design-and-demo-selling.md)

### [5 · AEO / GEO / SEO for growth](roadmap/05-aeo-geo-seo-for-growth.md)
The new organic frontier: getting *cited by ChatGPT, Perplexity, and Gemini*, not just ranked by Google. GEO tactics (Princeton reports **up to +40% visibility**), the `llms.txt` standard, structured answer content, and running an executable AEO audit with the onvoyage-ai skill. → [read](roadmap/05-aeo-geo-seo-for-growth.md)

### [6 · Tools & the stack in depth](roadmap/06-tools-and-stack.md)
The warehouse + reverse-ETL layer (Snowflake/BigQuery + Hightouch/Census), the 2026 tools ranking, and how to choose: velocity-vs-leverage, change-management budget, and the build-vs-buy axis per layer. → [read](roadmap/06-tools-and-stack.md)

### [7 · Portfolio projects](roadmap/07-portfolio-projects.md)
Ship **3–5 public repos, not one big resume.** The six canonical project briefs (waterfall enrichment, AI personalization demo, AEO/GEO audit, reverse-ETL routing, n8n inbound-to-CRM, Claygent research agent) — full briefs in [`projects/`](projects/). → [read](roadmap/07-portfolio-projects.md)

### [8 · Learning repos & academies to mine](roadmap/08-learning-repos-and-academies.md)
The MIT-licensed repos worth cloning (**onvoyage-ai/gtm-engineer-skills**, **awesome-gtm-engineering**, **awesome-n8n-templates**), the free vendor academies (Clay University, HubSpot, Make), and the communities. → [read](roadmap/08-learning-repos-and-academies.md)

---

## Tools every GTM engineer should know (2026)

> SyncGTM's June 2026 ranking, annotated with what to actually learn each tool *for*. You do not need all of them — you need one per layer, deep.

| # | Tool | Layer | Why it's on the list |
|---|---|---|---|
| 1 | **Clay** | Enrichment / AI | The category-definer: waterfall enrichment + Claygent AI research. Learn the credit economy and conditional gating. |
| 2 | **Apollo** | Enrichment / sequencing | Data + outbound in one; API + MCP server + CLI. |
| 3 | **ZoomInfo** | Enrichment | Deep firmographic/intent data; the waterfall's premium tier. |
| 4 | **n8n** | iPaaS | Fair-code, source-control-friendly automation; 280+ community templates. |
| 5 | **Outreach / Salesloft** | Sequencing | Multi-touch outbound + deliverability guardrails. |
| 6 | **HubSpot Sales Hub** | CRM | Contact-centric, shared-DB CRM; Operations Hub custom code. |
| 7 | **Salesforce** | CRM | Account-centric, Apex/Flow customization; enterprise default. |
| 8 | **Snowflake** | Warehouse | The analytical source of truth for scoring & modeling. |
| 9 | **Hightouch / Census** | Reverse-ETL | Push warehouse-scored rows back into the CRM. |
| 10 | **OpenAI / Anthropic** | AI-automation | Structured outputs, tool calls, agents; the LLM layer of every 2026 play. |

Full annotations, docs links, and licenses in [6 · Tools & stack](roadmap/06-tools-and-stack.md).

---

## Portfolio projects

**The hiring signal is 3–5 shipped, documented, public repos — not one monolithic "resume project."** Each brief has a Problem, a Stack, Milestones, *What it proves*, and Stretch goals.

- 📦 [**Waterfall Enrichment Pipeline**](projects/README.md#1--waterfall-enrichment-pipeline) — Clay + Apollo + ZoomInfo + n8n; document the cost-per-lead drop.
- 🤖 [**AI Personalisation Demo**](projects/README.md#2--ai-personalisation-demo) — Lovable/Bolt + OpenAI; firmographic-driven landing copy.
- 🔎 [**AEO/GEO Audit**](projects/README.md#3--aeogeo-audit) — run the onvoyage-ai skill on 3 competitor sites; publish the diff.
- 🔁 [**Reverse-ETL Lead Routing**](projects/README.md#4--reverse-etl-lead-routing) — Snowflake + dbt + Hightouch → HubSpot.
- ⚡ [**n8n Inbound-to-CRM Flow**](projects/README.md#5--n8n-inbound-to-crm-flow) — webhook → verify → dedup → idempotent upsert.
- 🕵️ [**Claygent Research Agent**](projects/README.md#6--claygent-research-agent) — per-lead research, gated, pushed to CRM notes.

→ Full briefs in [`projects/README.md`](projects/README.md).

---

## What's new

> Most recent first.

- **2026-07** — Initial release. 9 stages, the signature stack table, the 86-question [skills check](skills-check.md), and 6 portfolio briefs. Dated for 2026: AI GTM Engineer as "the revenue org's AI operator," MCP connectors, agentic evals, AEO/GEO, and the low-code/custom-code seam.
- **2026-07** — Added the "builder vs conductor vs translator" role map (Tabula) and named-company team-shape patterns (Notion, Canva, Anthropic, Intercom).

---

## FAQ

**GTM Engineer vs RevOps vs Sales Engineer — what's the difference?**
Three lenses on the revenue org. **RevOps is the conductor** — owns the foundation: funnel taxonomy, lifecycle stages, dedup policy, SLAs, forecasts; graded on governance. **The GTM Engineer is the builder** — the technical "wingman to RevOps" who ships enrichment waterfalls, scoring services, CRM write-back, and AI workflows *on top of* that foundation. **The Sales Engineer is the translator** — customer-facing, de-risks technical objections, wins the technical evaluation with demos and architecture. Conflating GTM-E with RevOps is a documented hiring mistake (you get a Zapier power-user with no governance, or a software engineer with no GTM context). See [Stage 0](roadmap/00-what-is-a-gtm-engineer.md).

**Do I need to code?**
Yes — but not like a backend engineer. You live at the seam between **low-code velocity and engineering rigor**. Most workflows are low-code (Clay, n8n, HubSpot workflows); you drop into real code (Python, JavaScript, SQL, LLM APIs) for the specific slices that cross a threshold — **observability, deep branching, sub-second latency, or a typed ML step** like structured-output lead classification. HyperGrowth calls it a **T-shaped skillset**: broad across GTM + a spike in automation/APIs. You need APIs, webhooks, SQL, and LLM structured outputs — not a CS degree.

**Which tools should I learn first?**
In order: **(1) a CRM** (HubSpot is the fastest to learn; Salesforce is the enterprise default), **(2) Clay** (waterfall enrichment + Claygent — the category-definer), **(3) an iPaaS** (n8n if you want source control; Zapier for speed), then **(4) the LLM APIs** (OpenAI/Anthropic structured outputs and tool calls). Learn one tool *per layer*, deeply, rather than a shallow pass across ten. See [Stage 6](roadmap/06-tools-and-stack.md).

**Is GTM Engineering a real career in 2026?**
Yes. The title Clay coined in 2023 now sees ~**100 listings a month** and is a named function at Anthropic, Notion, Canva, Intercom, Cursor, Lovable, Webflow, and ElevenLabs. It's the technical evolution of the marketer/SDR role and appears on the [Landed AI-native jobs map](https://github.com/landedjobs/awesome-ai-native-jobs) as one of the fastest-growing new roles. It is not a fad title — it's a response to a real shift: revenue teams now build software, and someone has to be the builder.

**How do I build a GTM portfolio?**
Ship **3–5 small, public, documented repos — not one giant project.** Pick from the six canonical briefs (waterfall enrichment, AI personalization, AEO/GEO audit, reverse-ETL routing, n8n inbound-to-CRM, Claygent agent). For each, write the README as if it's a case study: the problem, the stack, *and the number you moved* (cost-per-lead drop, coverage lift, reply-rate delta). A repo with a clear revenue narrative beats a clever pipeline with no story. See [`projects/`](projects/README.md).

**GTM Engineer salary?**
Roughly **$180K–$240K base** with **$230K–$310K OTE** (25–30% variable), per aggregated 2026 US ranges; the broader band runs **$132K–$241K** depending on seniority, equity, and company stage. Ranges are approximate and skew higher at frontier labs and fast-growing B2B SaaS. See the live [GTM Engineer job list](https://github.com/landedjobs/gtm-engineer-jobs).

**Why do most candidates fail the interview?**
Clay's rubric scores **Commercial Bias** — *"automation should drive revenue outcomes, not just efficiency"* — and it's a stated reason only **~27%** of engineers pass. Candidates who say "I'd wire up Clay and Outreach to save the team time" without a revenue link read as posturing. Lead every answer with the pipeline number, name the funnel stage and unit economic, and *only then* reach for the tool. See [skills-check.md](skills-check.md).

---

## Contributing

PRs and issues welcome — add a resource, propose a tool, sharpen a stage, or expand the skills check. Every external link must be **typed, annotated, and capped** (~8 per section); no bare dumps, no promotional links. See [CONTRIBUTING.md](CONTRIBUTING.md). Content is MIT-licensed.

---

## ⭐ Star history

<a href="https://star-history.com/#landedjobs/become-a-gtm-engineer&Date">
  <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=landedjobs/become-a-gtm-engineer&type=Date" width="600" />
</a>

---

### Part of the Landed AI-native jobs family

This roadmap is one node in a cross-linked set of curated job lists, interview guides, and roadmaps:

- 🗺️ [**awesome-ai-native-jobs**](https://github.com/landedjobs/awesome-ai-native-jobs) — the umbrella map of every new AI-native role, with salaries and skills.
- 🚀 [**gtm-engineer-roles**](https://github.com/landedjobs/gtm-engineer-jobs) — the live, auto-updated GTM Engineer job list.
- 🧩 [**ai-product-engineer-roadmap**](https://github.com/landedjobs/ai-product-engineer-roadmap) — the sibling roadmap for the "PM who ships."
- 🤝 [**forward-deployed-engineer-jobs**](https://github.com/landedjobs/forward-deployed-engineer-jobs) — the customer-embedded builder role.
- 🧠 [**awesome-ai-engineer-interview**](https://github.com/landedjobs/awesome-ai-engineer-interview) — interview prep for the adjacent AI Engineer track.

---

<div align="center">

### Stop spraying. Get **matched**, get **prepped**, get **Landed**.

[![Get Started](https://img.shields.io/badge/Get%20Started%20Free-→-6C2BD9?style=for-the-badge)](https://landed.jobs)

<sub>Maintained by [Landed](https://landed.jobs) · No affiliation with the companies or tools named. Comp figures aggregated from public 2026 reports; ranges are approximate. Content MIT-licensed.</sub>

</div>
