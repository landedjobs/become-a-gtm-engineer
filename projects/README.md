# 📦 GTM Engineering Portfolio Projects

**Ship 3–5 public repos, not one monolithic resume project.** The hiring signal is a small set of *finished, documented* builds — each with a README written like a case study: the problem, the stack, and **the number you moved**. This folder is the index; the full briefs (Problem · Stack · Milestones · What it proves · Stretch) live in [`roadmap/07-portfolio-projects.md`](../roadmap/07-portfolio-projects.md).

## The six canonical briefs

Quick index — each links to the **full brief** (Problem · Stack · Milestones · What it proves · Stretch) in [`roadmap/07`](../roadmap/07-portfolio-projects.md).

### 1 · Waterfall Enrichment Pipeline
**Clay + Apollo + ZoomInfo + n8n** — proves the credit economy, dedup-before-enrich, conditional gating, and verification-before-send. → [full brief](../roadmap/07-portfolio-projects.md#1--waterfall-enrichment-pipeline)

### 2 · AI Personalisation Demo
**Lovable/Bolt + OpenAI** — proves strict-mode outputs, grounding, anti-hallucination gating, and the 20-question smoke test. → [full brief](../roadmap/07-portfolio-projects.md#2--ai-personalisation-demo)

### 3 · AEO/GEO Audit
**onvoyage-ai/gtm-engineer-skills** — proves the GEO-as-eval-loop discipline: an executable audit + fix, published as a diff. → [full brief](../roadmap/07-portfolio-projects.md#3--aeogeo-audit)

### 4 · Reverse-ETL Lead Routing
**Snowflake + dbt + Hightouch → HubSpot** — proves warehouse scoring, gated (not additive) scoring, and idempotent write-back. → [full brief](../roadmap/07-portfolio-projects.md#4--reverse-etl-lead-routing)

### 5 · n8n Inbound-to-CRM Flow
**n8n** — proves the integration spine end-to-end: verify → dedup → idempotent upsert → dead-letter. → [full brief](../roadmap/07-portfolio-projects.md#5--n8n-inbound-to-crm-flow)

### 6 · Claygent Research Agent
**Clay + Anthropic/OpenAI** — proves AI-column gating, refusal handling, and provenance-over-raw-value. → [full brief](../roadmap/07-portfolio-projects.md#6--claygent-research-agent)

## How to present a GTM project

The build is half the signal; the *framing* is the other half.

1. **One public repo per project.** A dedicated repo reads as a finished artifact; a folder buried in a mono-repo does not.
2. **A case-study README.** Open with the number you moved (cost-per-lead drop, coverage lift, reply-rate delta), *then* the problem, *then* the stack and the architecture. Lead with revenue, not the pipeline diagram.
3. **A public writeup.** A short post on [r/gtmengineering](https://www.reddit.com/r/gtmengineering/) or LinkedIn per build — the case study in prose. This is what surfaces in search and gets the repo seen.
4. **Synthetic data by default.** Use customer-shaped synthetic data in the public repo; never commit real PII or a customer export.
5. **Name the failure modes.** A `## What would break in production` section (rate limits, 4xx retry loops, refusals, unverified emails) signals you grade reliability, not the happy path — the take-home rubric's real bar.

> Test yourself on the concepts behind these projects with the [86-question skills check](../skills-check.md).

---

<sub>Part of [Become a GTM Engineer](../README.md) · Maintained by [Landed](https://landed.jobs) · MIT-licensed.</sub>
