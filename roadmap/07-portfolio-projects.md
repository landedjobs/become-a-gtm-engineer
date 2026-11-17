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

## Build for a real hiring need (Nov 2026)

*Last checked: 17 Nov 2026*

**Start from a revenue problem a real team has posted, then build the smallest system that solves it.** The six briefs above teach the parts. The two below aim at work that two named companies describe in live job postings. Read the posting first, then build for the problem it names: not for the tool list.

The two projects are practice builds we propose. They are not the companies' own assignments, and neither company has said it grades these exact demos. Each brief has the usual five parts plus two more: **the result to show** (a metric, how you measure it, and an honest baseline) and **how to present it**.

> [!TIP]
> **Use a baseline you can defend.** Run your system and a simple "before" version (round-robin routing, one enrichment provider, a script with no retries) on the same labeled test set. If you never ran it on live traffic, label the numbers **offline evaluation**. Don't report reply rates, meetings or pipeline you did not actually measure.

Templates for the README, the eval report and the write-up: [💻 landedjobs/ai-engineer-portfolio-projects/templates](https://github.com/landedjobs/ai-engineer-portfolio-projects/tree/main/templates) (MIT). They were written for AI engineering projects, but the results table, the eval report and the resume-line formula fit GTM builds as-is.

### 7 · Inbound Routing and SDR Handoff Loop

**Built for:** Clay's handoff problem. Clay's [GTM Engineer, Marketing posting](https://jobs.ashbyhq.com/claylabs/9f8067d1-61cf-42cd-aad7-0ac54de8b345) (official, New York, published 12 Oct 2026) asks this person to own handoff logic, routing and assignment rules, follow-up SLAs, and "the feedback loop that tells marketing which leads were actually worth working." It also asks them to measure the impact of what they build. Most routing demos stop at "lead assigned". This one shows what happens after.

- **Problem:** Inbound leads get scored and routed, but nobody can see whether the SDR followed up on time or whether the lead was worth working. So the qualification rules never improve.
- **Stack:** A webhook or form source → normalize and dedup → enrichment (Clay, or one provider plus a fallback) → a deterministic fit score → optional AI classification for ambiguous rows → CRM assignment (a Salesforce Developer Edition or HubSpot sandbox) → Slack alert to the owner → an SLA check → an outcome table that feeds back into the score.
- **Milestones:** (1) build a labeled fixture set of about 100 synthetic leads, including duplicates, missing fields, ambiguous territories and accounts you should reject; (2) the routing path with an exception queue for rows the system should not guess on; (3) an SLA timer that flags leads with no first touch inside the window; (4) an outcome field (worked, disqualified, meeting) that SDRs set, and a weekly report on which score bands converted; (5) one rule change driven by that report, re-run on the same fixtures.
- **What it proves:** You can own the space between Marketing and SDRs, not just the enrichment step. Routing, SLAs, the exception queue and a feedback loop that changes the rules.
- **Stretch:** Territory and capacity-aware assignment; a dashboard of where leads stall, by source.
- **Result to show:**

  | Metric | How to measure it | Honest baseline |
  |---|---|---|
  | Assignment accuracy | Share of fixture leads routed to the owner your label says is correct | Round-robin or a single territory rule, same fixtures |
  | Exception precision | Of rows sent to the exception queue, the share a human agrees were truly ambiguous | The baseline routes every row and never refuses |
  | Enrichment match rate | Share of leads with a verified company and contact after enrichment | One provider, no fallback |
  | Time to owner | Seconds from webhook received to CRM owner set, p50 and p95 over the fixture run | Your own estimate of the manual step, labeled as an estimate |
  | Duplicate rate | Duplicate CRM records created per 100 inbound rows, with duplicates seeded on purpose | No dedup step |

- **How to present it:** Open the README with the results table. Add a 2-minute walkthrough that shows one clean lead, one duplicate and one lead the system refuses to route. Show the feedback report and the rule it changed. Name it plainly: "inbound routing with an SDR feedback loop, offline evaluation on 100 labeled leads."

### 8 · GTM Agent Reliability Harness

**Built for:** Baseten's reliability standard. Baseten's [GTM Engineer posting](https://jobs.ashbyhq.com/baseten/5cd2f489-b9ee-428b-b252-94e83d55f107) (official, New York, published 25 Aug 2026) asks for production agents built "with durable workflows and sandboxed execution", so they run "reliably in production instead of as one-off scripts." It also names Clay, Salesforce, Claude Code, APIs and webhooks. The point: how the system behaves when something fails matters as much as the prompt.

- **Problem:** Most AI GTM demos only show the happy path. In production, a provider times out, a webhook arrives twice, the model returns broken JSON or the CRM write fails. A one-off script then double-writes, loses the record or stops with no alert.
- **Stack:** Take any project above (the inbound router or the Claygent research agent fit best) and wrap it in a durable workflow runner (Vercel Workflow, or Temporal or Inngest) with retries per step. Run model-generated code or tool calls in a sandbox. Validate structured output against a schema. Upsert to Salesforce or HubSpot keyed on a unique ID. Send failures to a dead-letter queue with a Slack alert.
- **Milestones:** (1) a failure-injection script that triggers four faults on demand: provider timeout, duplicate webhook, invalid model response, failed CRM write; (2) capped retries with backoff and an idempotency key on every write; (3) structured logs with one run ID across steps; (4) a replay command for the dead-letter queue; (5) a cost sheet per run.
- **What it proves:** You can ship an agent that a sales team can trust. It survives the failures that turn a demo into a support ticket.
- **Stretch:** A per-run cost ceiling that stops the workflow; an alert when the failure rate crosses a threshold.
- **Result to show:**

  | Metric | How to measure it | Honest baseline |
  |---|---|---|
  | Duplicate writes | CRM records created when each of N webhooks is replayed 2 to 3 times (target: 0) | The same flow as a plain script, no idempotency key |
  | Recovery rate | Share of injected faults that finish correctly after retry or replay | The plain script, same injected faults |
  | Invalid-output handling | Share of malformed model responses caught by the schema check, not written to the CRM | No validation step |
  | Time saved per task | Minutes a rep spends on the task by hand vs. with the agent, timed on 10 real or realistic tasks | Your own timed manual run, stated with its sample size |
  | Cost per successful run | Model, enrichment and compute cost divided by runs that finished correctly | Not applicable: just report it, with prices dated |

- **How to present it:** Put a fault table at the top of the README: each injected fault, what the baseline did, what your system did. Record a short video that triggers each fault live and shows the log and the recovered record. Add a `## What would break in production` section for the faults you did not cover.

---

## How to present them

Ship **one public repo per project** plus a short **Reddit (r/gtmengineering) or LinkedIn writeup** per build — the case-study framing that turns a repo into a hiring signal. The full presentation checklist lives in [`projects/README.md`](../projects/README.md).

## 📚 Resources

- 📰 [How to build a GTM engineering portfolio that gets you hired](https://databar.ai/blog/article/how-to-build-a-gtm-engineering-portfolio-that-gets-you-hired) — **article** (databar, 2026). The "3–5 high-quality builds" thesis and per-project case-study framing.
- 💻 [onvoyage-ai/gtm-engineer-skills](https://github.com/onvoyage-ai/gtm-engineer-skills) — **repo · ~1.4k★ · MIT.** The executable AEO/GEO audit skills behind project #3.
- 💻 [enescingoz/awesome-n8n-templates](https://github.com/enescingoz/awesome-n8n-templates) — **repo · 280+ templates · ⚠️ CC BY 4.0 (n8n itself uses the fair-code Sustainable Use License).** Clone-and-adapt starting points for the n8n inbound-to-CRM flow (project #5).
- 📘 [Clay University](https://university.clay.com/docs) — **docs.** Waterfall + Claygent, the backbone of projects #1 and #6.
- 📘 [n8n Docs](https://docs.n8n.io/) — **docs.** The webhook → dedup → upsert spine for project #5.

---

**Next:** [8 · Learning repos & academies →](08-learning-repos-and-academies.md) — the open repos to clone (licences noted) and the free vendor academies to mine.
