> **Stage 7 of 9 · Portfolio projects** — ship 3–5 public repos with a revenue narrative, not one monolithic resume project.
> [← 6 · Tools & stack](06-tools-and-stack.md) · [Back to roadmap](../README.md) · Next: [8 · Repos & academies →](08-learning-repos-and-academies.md)

# 📦 Portfolio projects

**The hiring signal is 3–5 shipped, documented, public repos — not one monolithic "resume project."** databar's June 2026 portfolio guide is explicit: focus on a small number of *high-quality, finished* builds, each with a README written like a case study — the problem, the stack, and **the number you moved** (cost-per-lead drop, coverage lift, reply-rate delta). A repo with a clear revenue narrative beats a clever pipeline with no story.

Each brief below has the same five parts: **Problem · Stack · Milestones · What it proves · Stretch.** Pick 3–5, ship them public, and write each README as if a hiring manager will grade it on the revenue link, not the line count.

> [!TIP]
> **Lead every README with the number, not the architecture.** "Cut blended cost-per-verified-lead 38% (Clay waterfall + gating)" is a hiring signal; "built a Clay pipeline with n8n" is a hobby. The full-brief format lives here; the presentation format (one public repo + a Reddit/LinkedIn writeup) lives in [`projects/`](../projects/README.md).

---

## 1 · Waterfall Enrichment Pipeline

- **Problem:** A single-provider enrichment process matches ~60–70% of leads and burns credits on duplicates. Prove you can lift coverage *and* lower blended cost-per-match.
- **Stack:** Clay (waterfall) + Apollo + ZoomInfo + n8n. Dedup-before-enrich; conditional "Run only if…" gates so tier-2/3 fire only on tier-1 misses.
- **Milestones:** (1) normalize + dedup a 500-domain CSV; (2) build the 3–5 provider waterfall with gates; (3) add an email-verification step (ZeroBounce/NeverBounce); (4) route matches to Apollo; (5) document cost-per-lead before/after.
- **What it proves:** The credit economy, dedup-before-enrich, conditional gating, and verification-before-send — the core Stage 1–2 rubric.
- **Stretch:** A distributed rate limiter (Redis) across workers so a shared provider key isn't exceeded; a dead-letter queue for un-enrichable rows.

## 2 · AI Personalisation Demo

- **Problem:** Generic landing copy converts worse than firmographic-tailored copy, but hand-writing per-segment variants doesn't scale.
- **Stack:** Lovable/Bolt (hosted, branded shell) + OpenAI structured outputs. Pull firmographic + public signals, rewrite the hero copy per visitor segment.
- **Milestones:** (1) scaffold a hosted, branded URL; (2) `strict:true` structured-output call that returns typed copy fields; (3) **gate** the AI on signal-present rows so it never fabricates on empty input; (4) a 20-question smoke test graded faithful/partial/hallucinated.
- **What it proves:** Customer-facing prototype discipline (Stage 3): strict-mode outputs, grounding, gating against hallucination, and a smoke test before "share screen."
- **Stretch:** A citation panel that shows which signal drove each copy variant; an enforced refusal when signal is missing.

## 3 · AEO/GEO Audit

- **Problem:** Buyers increasingly research inside answer engines; teams don't know whether ChatGPT/Perplexity cite them or a competitor.
- **Stack:** `onvoyage-ai/gtm-engineer-skills` (MIT). Run `audit-website-aeo` then `improve-aeo-geo` on your site *and* 3 competitor sites; publish the JSON diff.
- **Milestones:** (1) run the 16 foundational AEO checks; (2) capture the 6 intelligence dimensions per site; (3) apply framework-specific fixes (Next.js/WordPress); (4) publish the before/after diff and re-run monthly.
- **What it proves:** The GEO-as-eval-loop discipline (Stage 5) — the growth skill most teams still ignore, made executable.
- **Stretch:** Ship an `llms.txt` for the target site; schedule the audit as a monthly drift monitor and chart the citation-footprint trend.

## 4 · Reverse-ETL Lead Routing

- **Problem:** Fit scoring done with additive point rules inside the CRM can't express a real model; hot leads land in dead queues.
- **Stack:** Snowflake + dbt + Hightouch → HubSpot. Score accounts in the warehouse, reverse-ETL high-intent rows back into the CRM.
- **Milestones:** (1) load accounts into Snowflake; (2) build a dbt model that scores fit (gate fit *before* summing engagement — no additive footgun); (3) sync high-intent rows to HubSpot via Hightouch; (4) idempotent upsert on a unique key so re-syncs are no-ops.
- **What it proves:** The warehouse + reverse-ETL layer (Stage 6), gated (not additive) scoring, and idempotent write-back.
- **Stretch:** A drift dashboard on score distribution; a CDC/streaming refresh sized to a freshness SLA instead of a nightly batch.

## 5 · n8n Inbound-to-CRM Flow

- **Problem:** Inbound form leads arrive as raw webhooks — unverified, un-deduped, and sometimes delivered twice — and land as duplicate contacts.
- **Stack:** n8n. webhook → HMAC + timestamp verify → normalize → dedup → idempotent upsert into HubSpot/Salesforce.
- **Milestones:** (1) HMAC-SHA256 over the raw body + a ~5-min timestamp freshness window; (2) normalize + dedup keys; (3) idempotent upsert keyed on `email + tenant`; (4) a dead-letter path with a Slack alert; document the webhook chain.
- **What it proves:** The integration spine (Stage 1) end-to-end — the four contracts (throttle, backoff, idempotency, dead-letter) in a runnable flow.
- **Stretch:** Replay from the dead-letter queue; short-circuit 4xx to a "needs human fix" alert instead of retrying.

## 6 · Claygent Research Agent

- **Problem:** Per-lead research doesn't scale by hand, but an ungated AI research column fabricates confident details on signal-less rows.
- **Stack:** Clay (Claygent) + Anthropic/OpenAI. Research each account, gate the AI, push findings to CRM notes as typed provenance.
- **Milestones:** (1) a Claygent column gated behind "verified email + matched firmographic"; (2) structured output with a `refusal` path handled distinctly (alert, don't deserialize); (3) write source + confidence to **typed** custom properties, not free-text Notes; (4) push a research summary to CRM notes.
- **What it proves:** AI-column gating, refusal handling, and provenance-over-raw-value (Stage 2) — the Commercial-Bias rubric in code.
- **Stretch:** A per-lead cost budget; a trajectory grader that flags duplicate tool calls or retry storms.

---

## How to present them

Ship **one public repo per project** plus a short **Reddit (r/gtmengineering) or LinkedIn writeup** per build — the case-study framing that turns a repo into a hiring signal. The full presentation checklist lives in [`projects/README.md`](../projects/README.md).

## 📚 Resources

- 📰 [How to build a GTM engineering portfolio that gets you hired](https://databar.ai/blog/article/how-to-build-a-gtm-engineering-portfolio-that-gets-you-hired) — **article** (databar, 2026). The "3–5 high-quality builds" thesis and per-project case-study framing.
- 💻 [onvoyage-ai/gtm-engineer-skills](https://github.com/onvoyage-ai/gtm-engineer-skills) — **repo · ~1.2k★ · MIT.** The executable AEO/GEO audit skills behind project #3.
- 💻 [enescingoz/awesome-n8n-templates](https://github.com/enescingoz/awesome-n8n-templates) — **repo · 280+ templates · MIT.** Clone-and-adapt starting points for the n8n inbound-to-CRM flow (project #5).
- 📘 [Clay University](https://university.clay.com/docs) — **docs.** Waterfall + Claygent, the backbone of projects #1 and #6.
- 📘 [n8n Docs](https://docs.n8n.io/) — **docs.** The webhook → dedup → upsert spine for project #5.
- 🌐 [r/gtmengineering](https://www.reddit.com/r/gtmengineering/) — **community.** Where to publish the writeup and get feedback that surfaces in search.

---

**Next:** [8 · Learning repos & academies →](08-learning-repos-and-academies.md) — the MIT-licensed repos to clone and the free vendor academies to mine.
