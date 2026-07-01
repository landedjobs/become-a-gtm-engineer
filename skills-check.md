# 🧪 GTM Engineering Skills Check

**Test your GTM engineering readiness.** 86 scenario questions drawn from real interview loops — take-homes, architecture rounds, and discovery/demo mocks. Each is multiple-choice with a **per-option "why"** so a wrong answer teaches you the rubric, not just the key. This isn't trivia: every question is a *judgment* call a senior GTM engineer makes on the job.

> [!TIP]
> Don't just find the ✅. Read *why each ▫️ is wrong* — the distractors are the exact junior mistakes interviewers listen for. The rubric being tested is **Commercial Bias** (automation must drive revenue, not just efficiency), **reliability over the happy path**, and **judgment over tool recall.**

## How to use this

- **Grouped by topic**, tiered **🟢 Beginner · 🟡 Intermediate · 🔴 Advanced.**
- Answer before expanding — each answer is behind a `<details>` toggle.
- Map weak spots back to the roadmap stage and re-read it.

| Topic | Questions | Roadmap stages |
|---|---|---|
| [1 · GTM stack & automation](#1--gtm-stack--automation) | 30 | [1](roadmap/01-the-gtm-stack.md) · [2](roadmap/02-ai-automation-for-gtm.md) · [6](roadmap/06-tools-and-stack.md) |
| [2 · Customer-facing AI prototypes](#2--customer-facing-ai-prototypes) | 22 | [3](roadmap/03-customer-facing-ai-prototypes.md) |
| [3 · Solution design & demo selling](#3--solution-design--demo-selling) | 34 | [4](roadmap/04-solution-design-and-demo-selling.md) · [5](roadmap/05-aeo-geo-seo-for-growth.md) |

Legend: ✅ correct · ▫️ incorrect (with the reason it fails).

---

## 1 · GTM stack & automation

The funnel state machine, CRM data modeling, dedup at scale, the integration spine, the enrichment waterfall, AI-column gating, scoring, and the low-code/custom-code seam.

### 🟢 Beginner

<details>
<summary><b>Q1.</b> A new VP buys Clay, Outreach, and an LLM seat in week one and asks you to "start generating pipeline." Nothing is agreed on lifecycle stages or dedup. Senior first move?</summary>

- ▫️ Start building the enrichment waterfall immediately so you show pipeline fast — *Enriching on a contested schema burns credits on duplicates and routes leads into undefined stages — the classic tooling-first failure that lands flat on dirty data.*
- ✅ Lock down the funnel taxonomy, ICP, lifecycle stages, and dedup keys first — then plumb enrichment on top — *Schema-first, plumbing-second: the slow layers (taxonomy, lifecycle) cap every faster layer, so they must be agreed before any automation — exactly Valcat's "cleanup before enrichment" pattern.*
- ▫️ Turn on AI personalization since it has the highest reply-rate lift — *A 5× reply lift is wasted if leads route to an unstaffed queue on an undefined lifecycle — AI is layer 4 and capped by the weak layers below it.*
</details>

<details>
<summary><b>Q2.</b> An interviewer asks you to distinguish RevOps from GTM engineering. Strongest framing?</summary>

- ▫️ RevOps is strategy and GTM engineering is just running the same tools day-to-day — *This collapses the roles; "running tools" understates GTM engineering, which builds enrichment, scoring, and CRM write-back — it's technical execution, not administration.*
- ▫️ They're the same role with two titles depending on company size — *Conflating them is the documented hiring mistake — it produces either a Zapier power-user with no governance or a software engineer with no GTM context.*
- ✅ RevOps owns the foundation — taxonomy, lifecycle, dedup, SLAs; GTM engineering is the technical wingman that builds workflows on top of it — *This is the Hypergrowth "wingman to RevOps" framing: RevOps is graded on governance/foundation, GTM-E on shipping AI-powered execution — complementary, not interchangeable.*
</details>

<details>
<summary><b>Q3.</b> You're asked to double pipeline in six months without adding headcount. Which opening best fits the Commercial-Bias rubric?</summary>

- ✅ Identify the worst-converting funnel stage, fix the unit economic there (coverage, scoring, or routing), and tie it to a pipeline number — *This leads with revenue and the funnel mechanism — exactly what Clay's Commercial-Bias rubric rewards; it diagnoses before prescribing a tool.*
- ▫️ Roll out a new sequencing tool across the whole team to improve efficiency — *"Efficiency" with no revenue link is the red-flag answer the rubric penalizes; a tool rollout isn't a diagnosis of where pipeline is leaking.*
- ▫️ Increase outbound volume by 2× since pipeline scales with activity — *More volume on a leaky funnel amplifies the leak; without fixing the worst conversion stage you scale waste, not pipeline.*
</details>

<details>
<summary><b>Q4.</b> Marketing reports MQL volume is up 40% but SQLs and pipeline are flat. Where do you start the investigation?</summary>

- ▫️ Ask for more budget to drive even more top-of-funnel volume — *More MQLs into a stalled MQL→SQL transition just widens the gap — volume isn't the constraint when the conversion step is broken.*
- ▫️ Conclude the leads are low quality and pause the campaigns — *Pausing skips the diagnosis; the break could be dedup, lifecycle-stage drift, routing, or scoring — you isolate the transition before blaming lead quality.*
- ✅ Trace the MQL→SQL transition: check dedup, lifecycle-stage drift, routing to a dead queue, and scoring calibration one variable at a time — *A flat downstream with a rising upstream is a transition problem; the senior move is to isolate the single broken step in the funnel's state machine, not add volume.*
</details>

<details>
<summary><b>Q5.</b> Your single-provider email enrichment is matching ~65% of leads and the team wants higher coverage without blowing the budget. Best move?</summary>

- ✅ Build a 3–5 provider waterfall with conditional "Run only if…" gates so tier-2/3 fire only when tier-1 misses — *A waterfall lifts coverage from ~60–70% to >90% and, with conditional gates plus pay-per-match pricing, you only pay for hits and only run later tiers on rows the earlier tier missed.*
- ▫️ Switch to whichever single provider has the highest published match rate — *Any single provider caps around 60–70%; swapping one for another doesn't close the coverage gap that a cascade does.*
- ▫️ Run all available providers on every row to maximize matches — *Running every provider on every row burns 4×+ the credits on rows tier-1 already solved — coverage is the goal, but ungated fan-out blows the budget.*
</details>

<details>
<summary><b>Q6.</b> A Clay table found emails for 92% of rows, but your first send had a 22% bounce rate and your domain reputation dropped. What did the pipeline skip?</summary>

- ▫️ It needed more enrichment providers to raise coverage past 92% — *Coverage wasn't the problem — the emails were found but invalid; adding providers finds more addresses, not more deliverable ones.*
- ✅ An email-verification step (ZeroBounce/NeverBounce) before the address counts — a found-but-invalid email is worse than none — *Verification is the mandatory last step in the email waterfall; skipping it ships invalid addresses that bounce, tank deliverability, and poison the domain reputation every later send depends on.*
- ▫️ A higher sending volume to warm up the domain faster — *Sending more invalid emails accelerates the reputation damage; the fix is to verify and remove undeliverable addresses, not to send harder.*
</details>

### 🟡 Intermediate

<details>
<summary><b>Q7.</b> You have one GTM engineer and a small RevOps team at a Series A startup. What team shape do the named-company patterns suggest?</summary>

- ▫️ Immediately stand up three separate teams (RevOps, GTM AI, innovation pod) like Notion — *Notion's three-team split is a scale pattern for an org with accumulated pilot plays; imposing it at Series A creates coordination overhead with nothing to coordinate.*
- ✅ Embed the GTM engineer inside RevOps now, and split into pods only once pilot plays accumulate — *This is Anthropic's documented pattern — start embedded for shared context and a single data product, federate later; there is no single right org chart, so you scale the structure with the work.*
- ▫️ Hire a pure software engineer to own all GTM automation independently — *A software engineer with no GTM context builds pipelines the sales floor rejects — the documented anti-pattern; GTM-E needs to sit close to the revenue motion.*
</details>

<details>
<summary><b>Q8.</b> You're asked to connect Clay, Salesforce, and HubSpot into "one source of truth." What should your answer establish first?</summary>

- ▫️ Enable native bi-directional sync between all three so data is always consistent everywhere — *Two-way-everywhere creates write loops and silently overwrites clean CRM fields with lower-confidence enrichment — the risky pattern; you want one-way writes with confidence gating.*
- ✅ Draw the join graph (Company/Account → Contact → Opp), place Clay upstream, and specify one-way writes with dedup-before-write and provenance fields — *The single-source-of-truth prompt is really "which side hosts the join and where does provenance live" — the strong answer is the join graph plus conditional, provenance-tagged one-way writes.*
- ▫️ Pick whichever CRM has more integrations and route everything through it — *Integration count isn't the modeling decision; without a join graph and provenance you still get duplicate, conflicting records across systems.*
</details>

<details>
<summary><b>Q9.</b> Your Clay table is burning enrichment credits faster than expected, and you notice "Acme Inc." and "ACME, Inc." both got enriched. Root cause and fix?</summary>

- ✅ Normalize and dedup company names before the enrichment columns run, so one company consumes one credit — *Un-normalized duplicates each trigger a paid lookup; dedup-before-enrich (strip suffixes, collapse case/punctuation) is the credit-economy fix and prevents mismatched joins downstream.*
- ▫️ Switch to a cheaper enrichment provider to lower the per-credit cost — *A cheaper provider still pays twice for the same company; the waste is the duplicate lookups, not the unit price.*
- ▫️ Increase the credit budget so the table stops stalling — *Raising the budget funds the waste instead of fixing it — the duplicates remain and the joins stay mismatched.*
</details>

<details>
<summary><b>Q10.</b> A teammate proposes storing enrichment source and confidence as free-text in the contact's Notes field. Why push back?</summary>

- ▫️ Notes fields have a character limit that enrichment data will exceed — *Length isn't the real problem — even if it fit, free-text notes aren't queryable by workflows, lists, or scoring, so the provenance is useless to automation.*
- ✅ Provenance (source, confidence, match score, enrichment status) belongs in typed custom properties/objects so workflows and conditional writes can read it — *The rubric rewards provenance-over-raw-value: typed properties let you gate writes on confidence and route on enrichment status; free-text in Notes can't drive any conditional logic.*
- ▫️ Notes are visible to the whole team and that's a privacy issue — *Visibility isn't the core issue; the problem is that unstructured provenance can't be consumed by workflows, dedup, or scoring.*
</details>

<details>
<summary><b>Q11.</b> A partner's webhook intermittently creates duplicate contacts in your CRM. Your handler does heavy work, sometimes takes 8s, and returns 200 only at the end. Most likely cause?</summary>

- ▫️ The CRM's API is buggy and inserting twice — *The duplication originates upstream of the CRM: a slow handler that hasn't acked yet triggers vendor retries — blaming the CRM skips the real cause.*
- ✅ The slow handler exceeds the vendor's delivery timeout, so it retries — and a non-idempotent insert re-creates the contact each time — *Vendors retry on non-2xx or timeout; if the handler isn't idempotent, each retry re-inserts. Fix: ack 2xx fast, do work async, and key the write on an idempotency/external ID.*
- ▫️ You need to raise the CRM's rate limit so writes don't fail — *Rate limits aren't the issue here; the writes are succeeding multiple times. The problem is retry-without-idempotency, not throughput.*
</details>

<details>
<summary><b>Q12.</b> You verify inbound webhooks by recomputing the HMAC signature and comparing. A captured payload still gets accepted when replayed hours later. What's missing?</summary>

- ✅ A timestamp freshness check — reject events whose X-Timestamp has drifted beyond a ~5-minute window — *A valid signature proves authenticity but not freshness; without a timestamp/nonce window a correctly-signed payload can be replayed. The fix is the clock-skew window (plus constant-time compare).*
- ▫️ A stronger hash algorithm than SHA-256 — *SHA-256 is fine; the algorithm isn't the gap. Replay protection is about freshness (timestamp/nonce), not signature strength.*
- ▫️ Rotate the shared secret after every request — *Per-request rotation is impractical and doesn't address replay within the validity window; the standard defense is a timestamp drift check.*
</details>

<details>
<summary><b>Q13.</b> Your pipeline retries every failed CRM write up to 8 times. A batch returns 400 ("contact owned by another rep") and your retries hammer the API for an hour. What's wrong?</summary>

- ▫️ Eight retries is too few — raise the cap so they eventually succeed — *A 400 is a permanent client error; no number of retries will make it succeed — more retries just amplify the waste HubSpot explicitly warns about.*
- ✅ You're retrying a 4xx — short-circuit client errors to a "needs human fix" alert and only back off on 429/5xx — *The retry-vs-alert boundary: 429/5xx are transient (retry with backoff), 4xx are client errors that retries amplify — log, alert, and drop from the active queue.*
- ▫️ Switch CRMs because this one rejects valid writes — *The write isn't valid — the contact is owned by someone else; the bug is in your retry policy treating a 4xx like a transient error.*
</details>

<details>
<summary><b>Q14.</b> A Clay table found emails but a Claygent column researches each company and, on rows with thin or missing signal, writes confident but fabricated details. Best fix?</summary>

- ▫️ Lower the model temperature so it stops making things up — *Temperature reduces variance but won't stop fabrication on signal-less input — an LLM pointed at an empty row still invents; the fix is to not run it there.*
- ▫️ Switch to a larger model that hallucinates less — *Even strong models hallucinate on input unrelated to the task; gating the step beats hoping a bigger model behaves on empty rows.*
- ✅ Gate the Claygent column behind a "Run only if…" condition (e.g. verified email + matched firmographic) so it never fires on a signal-less row — *Conditional gating does double duty — credit economy and hallucination control: the AI step only runs when there's genuine signal, exactly like gating a structured-output call on relevant input.*
</details>

<details>
<summary><b>Q15.</b> A whole column of rows in a 30k-row table is suddenly returning empty downstream. What's the senior debugging sequence?</summary>

- ▫️ Add two more enrichment providers to the waterfall to compensate — *Adding providers is a reflex, not a diagnosis — you haven't isolated whether the cause is a dead provider, exhausted credits, a rate limit, or a formula bug.*
- ✅ Isolate one known-failing row, step column-by-column, simplify formulas, then check credits / rate limits / provider status — *This is Octave's canonical triage: isolate the breaking point on a single row and step through it before changing anything — interviewers grade the systematic isolation, not tool recall.*
- ▫️ Re-run the entire table from the top to see if it resolves itself — *A full re-run wastes credits and hides the cause; if it's a dead provider or exhausted credits, it fails identically — you must isolate first.*
</details>

<details>
<summary><b>Q16.</b> For a known, high-value segment of ~2,000 accounts where match accuracy matters far more than volume, what enrichment strategy fits best?</summary>

- ▫️ Maximize the waterfall to 10+ providers to guarantee a match on every account — *A sprawling waterfall optimizes coverage/volume and adds cost and maintenance; on a small known segment, accuracy beats breadth and diminishing returns set in past 3–5 providers.*
- ✅ Keep one trusted primary vendor for the segment and add a different secondary only for edge cases — *The decision rule: volume → pay-per-match waterfall; known-segment match quality → a trusted primary plus a targeted secondary for the long tail, which maximizes accuracy without over-engineering.*
- ▫️ Skip enrichment and have reps manually research all 2,000 accounts — *Manual research on 2,000 accounts is exactly the junior-SDR bottleneck GTM engineering automates; a focused primary+secondary enrichment is both faster and more consistent.*
</details>

<details>
<summary><b>Q17.</b> A teammate wants to rewrite your entire Clay + HubSpot stack as a custom Python service because "it'll be more robust." Volume is ~20K records/month and most workflows are simple. Senior response?</summary>

- ▫️ Agree — custom code is always more robust and maintainable long-term — *"Always custom" over-engineers the 80% of the surface that never hits a threshold and throws away fast iteration and citizen-developer authoring — robustness isn't free.*
- ✅ Push back: keep low-code for the simple, low-volume 80% and only carve out the specific slices that cross a threshold into a custom service — *Low-code and custom code are complements; at 20K records with simple branching nothing has crossed a threshold yet — you rebuild only the vertical slice that hits volume/branching/latency/observability/ML.*
- ▫️ Refuse any custom code — low-code can handle everything if configured well — *"Always low-code" ignores the real ceilings (observability, branching depth, sub-second latency, ML steps) that bite at scale; absolutism in either direction fails.*
</details>

<details>
<summary><b>Q18.</b> Your scoring step adds fit and engagement: fit 30 / engagement 60 = 90 routes to sales, while fit 80 / engagement 5 = 85 routes to nurture. The AE complains about tire-kickers. Root cause and fix?</summary>

- ▫️ The thresholds are too low — raise the sales cutoff above 90 — *Raising the cutoff doesn't fix the ordering: a poor-fit, high-engagement lead can still outscore an ideal-fit one under pure addition — the bug is the additive model, not the threshold.*
- ✅ Additive scoring is the footgun — gate on fit first, then let engagement rank within a fit tier (engagement is a tiebreaker, not a substitute for fit) — *Exactly Octave's flagged footgun: pure addition lets engagement promote a poor-fit lead over an ideal one; gating fit before summing engagement keeps tire-kickers out of the sales tier.*
- ▫️ Remove engagement from the score entirely and rank on fit only — *Dropping engagement loses a useful tiebreaker among qualified leads; the fix is to gate fit first, not to discard the behavioral signal.*
</details>

### 🔴 Advanced

<details>
<summary><b>Q19.</b> A 50k-record list scraped from event badges has wildly inconsistent free-text company names. Your normalize+hash+fuzzy cascade still leaves obvious duplicates. Best next layer?</summary>

- ▫️ Lower the Jaro-Winkler fuzzy threshold until everything matches — *Loosening the fuzzy threshold trades false negatives for false positives — it starts merging genuinely different companies and corrupts the join.*
- ▫️ Give up on dedup for this list and let the CRM matching rules handle it post-import — *CRM matching rules won't catch free-text noise their rules aren't configured for; the dupes just accumulate and get double-touched.*
- ✅ Add semantic dedup — embed the records (1536-d), cluster, and merge above a tuned cosine threshold — *Semantic dedup is exactly the layer reserved for noisy free-text upstreams; you embed and cluster, but only with a distance cutoff tuned on a labeled set so unrelated accounts don't merge.*
</details>

<details>
<summary><b>Q20.</b> You built a great dedup rule for the Q3 outbound campaign by configuring columns inside that one Clay table. What's the senior critique?</summary>

- ▫️ The rule should live in the CRM instead of Clay — *Location in CRM vs Clay isn't the issue; dedup often must run upstream in Clay before write-back — the problem is reusability, not which tool hosts it.*
- ✅ Dedup buried in one table's columns is debt — expose it as a named, versioned shared recipe every pipeline inherits (Notion's pattern) — *A dedup rule only one campaign benefits from is technical debt the moment a second motion ships; treating hygiene as a shared data product with SLAs is exactly how Notion keeps it from rotting.*
- ▫️ It's fine as long as the campaign hits its numbers — *Hitting one campaign's numbers ignores that the next motion re-implements (or skips) dedup, reintroducing the silent-duplicate failure mode across the org.*
</details>

<details>
<summary><b>Q21.</b> Three worker processes each enrich leads against a vendor whose basic plan allows ~1 req/s on a key shared across your whole account. Each worker throttles itself to 1 req/s, yet you keep getting 429s. Fix?</summary>

- ▫️ Add exponential backoff so the 429s eventually clear — *Backoff helps absorb spikes but doesn't fix the root cause: three independent buckets still emit ~3 req/s combined against a 1 req/s key.*
- ▫️ Upgrade to a faster machine so each worker sends faster — *Faster workers make the problem worse — the constraint is the shared 1 req/s key, not local compute.*
- ✅ Replace per-process counters with a distributed rate limiter (e.g. Redis sliding window) so the 1 req/s limit is enforced across all workers — *A shared key needs a shared limiter; per-process token buckets can't coordinate, so only a distributed limiter enforces the global ceiling across processes.*
</details>

<details>
<summary><b>Q22.</b> A Salesforce Bulk ingestion job that ran fine for months suddenly stops loading records, with no error surfaced in your pipeline. Most likely cause to check first?</summary>

- ▫️ The OAuth token expired and wasn't refreshed — *An expired token surfaces as a 401, not a silent stop; you'd see auth errors. A silent halt points elsewhere.*
- ▫️ Your HMAC verification started failing — *HMAC verification is for inbound webhooks, not outbound Bulk ingestion — it wouldn't silently block an ingestion job.*
- ✅ The daily Bulk API call quota was exceeded — Salesforce silently blocks ingestion, so quota must be monitored as a metric — *Salesforce's Bulk API publishes a daily ceiling that, when hit, silently blocks the queue with no loud error — the senior move is to track quota consumption as a first-class metric and alert before the cap.*
</details>

<details>
<summary><b>Q23.</b> A revenue-critical enrichment workflow runs at modest volume but goes completely dark whenever a provider returns 429 — no logs, no alert, leads just stop flowing. What's the strongest justification to put a custom service behind it?</summary>

- ✅ Observability — low-code hides failures (no logs/retries/dead-letter); a custom service surfaces the 429, retries with backoff, and alerts — *The real threshold here is observability, not throughput: a silent failure on a revenue-carrying slice is a latent incident, and instrumentation (logs, retries, dead-letter, metrics) is exactly what low-code compresses away.*
- ▫️ Throughput — the workflow obviously can't handle the record volume — *Volume is modest and isn't the problem; the slice fails on error handling and visibility, not on scale.*
- ▫️ Cost — custom code is cheaper than low-code per record — *Per-record cost isn't the driver here; the failure is silent error propagation, which is an observability gap, not a pricing one.*
</details>

<details>
<summary><b>Q24.</b> Your pipeline needs to classify each lead's intent into typed CRM fields with high reliability. Which part of the stack is the clearest case for custom code?</summary>

- ▫️ The CRM write-back step, which should always be hand-coded — *Write-back is well served by native integrations/Ops Hub custom code; it isn't the step that uniquely demands a custom ML service.*
- ▫️ The Slack alerting step, which low-code can't do — *Slack alerts are a core low-code capability; this isn't where the low-code ceiling hits.*
- ✅ A custom ML step — a Pydantic structured-output classification call (strict:true) that returns schema-conforming fields with no regex cleanup — *Typed, reliable classification is the canonical "custom code" slice the research names; structured outputs with strict:true guarantee schema adherence so the result drops straight into CRM fields.*
</details>

<details>
<summary><b>Q25.</b> You're asked: "Describe a time you balanced short-term sales needs with long-term system scalability." Which answer best fits the rubric?</summary>

- ✅ Shipped the workflow fast in low-code to unblock sales, then hardened the one revenue-carrying, threshold-crossing slice into an observable service — *This shows both build velocity and engineering judgment — ship now in low-code, then draw the seam and harden the specific slice that scale demands, tied to revenue.*
- ▫️ Refused to ship anything until the full custom architecture was designed — *Blocking sales for a perfect architecture fails the short-term-needs half of the balance; the rubric rewards shipping fast and iterating, not gold-plating up front.*
- ▫️ Built everything in Zapier and never revisited it — *Never revisiting ignores the long-term-scalability half — it leaves brittle, unobservable sprawl that fails silently as volume and complexity grow.*
</details>

<details>
<summary><b>Q26.</b> A startup hires a brilliant backend engineer with zero GTM background to "own all automation." Six months in, the pipelines are elegant but reps refuse to use them. What does this illustrate?</summary>

- ▫️ The engineer needed a bigger budget for better tools — *Tooling budget isn't the issue; the pipelines are technically sound but disconnected from how the sales floor actually works.*
- ▫️ The team should have gone fully low-code instead — *Fully low-code swaps one failure mode (rejected custom pipelines) for another (unobservable sprawl); the real gap is GTM context, not the build medium.*
- ✅ The documented anti-pattern of a pure SWE with no GTM context — the GTM engineer must sit between low-code velocity and engineering rigor, fluent in the revenue motion — *A pure SWE builds pipelines the sales floor rejects, just as a Zapier power-user builds ungoverned sprawl — the GTM engineer bridges both.*
</details>

<details>
<summary><b>Q27.</b> Mid-pipeline, your structured-output scoring call returns a populated refusal field for a particular lead. How should the pipeline handle it?</summary>

- ▫️ Retry the call a few times until it returns a valid score — *A refusal isn't a transient error; retrying won't coax a score and may just burn tokens — refusal is a distinct path, not a 5xx.*
- ▫️ Treat the refusal as a low score of 0 and route to awareness — *Coercing a refusal into a score fabricates data the model explicitly declined to produce; refusal, parse-failure, and low-score are three different paths that must not be conflated.*
- ✅ Treat the refusal as an alert (not a 200), skip writing the score schema, and route it for human handling — *The cookbook surfaces refusal as its own field precisely so you handle it distinctly — alert, don't deserialize into the score, never a silent 200.*
</details>

<details>
<summary><b>Q28.</b> A high-intent signal fires for a strategic enterprise account that's mid-negotiation. What should stage-4 alerting do?</summary>

- ▫️ Auto-enroll the account into the standard high-intent outbound sequence — *Auto-sequencing a strategic, mid-negotiation account can burn the relationship the pipeline exists to build — the guidance is to alert for human judgment, not auto-sequence.*
- ✅ Escalate up the graduated ladder — alert the owner (and pause any automation) so a human handles the strategic account directly — *The graduated ladder reserves auto-pause/human-handling for signals that need judgment; "if a signal requires human judgment and personalized outreach, alert your team" rather than firing another sequence.*
- ▫️ Do nothing — the sequence will reach them eventually — *Ignoring a high-intent signal on a strategic account wastes the moment; the point of alerting is timely human action, not silence.*
</details>

<details>
<summary><b>Q29.</b> In the live walkthrough, the interviewer asks "what would break in production?" Which answer best fits the passing rubric?</summary>

- ✅ Name concrete failure modes with their boundary guardrails: shared-key rate limits (distributed limiter), silent Bulk quota (monitor as metric), 4xx retry loops (short-circuit + alert), LLM refusals (distinct path), unverified emails (verify step) — *A per-stage pre-mortem with named failure modes and their guardrails is exactly what the take-home rubric rewards — it shows you grade the pipeline on reliability, not the happy path.*
- ▫️ "Nothing should break — I tested it end-to-end and it worked" — *"It worked in the demo" is the marked-down answer; a single clean run proves nothing about load, and the interviewer is grading the pre-mortem.*
- ▫️ "If something breaks I'll add more providers and retries" — *Reflexively adding providers/retries without naming the specific failure and its guardrail is the junior tell — blind retries amplify 4xx and double-write without idempotency.*
</details>

<details>
<summary><b>Q30.</b> You have one day left on a 3-day take-home and the core pipeline works on clean data. What's the highest-value use of the remaining time?</summary>

- ▫️ Add five more enrichment providers to push coverage higher — *More providers is diminishing returns past 3–5 and doesn't address what the rubric grades — tradeoffs, reliability, and a clear revenue narrative.*
- ✅ Tighten scope and over-invest in the defense: a per-column pre-mortem, a 5-failure-mode debug checklist, and a one-page revenue link — *The take-home grades the deliverable AND the narration equally; a "good enough" build with a crisp scope and a strong defense beats a "perfect" build that misses the deadline.*
- ▫️ Rebuild the whole thing as a custom Python service to look more rigorous — *A full rewrite risks missing the deadline and signals poor scoping; you harden only the threshold-crossing slice, not the entire pipeline.*
</details>

---

## 2 · Customer-facing AI prototypes

Grounded Q&A demos, strict-mode tool calls, retrieval debugging, agent trajectories, tenant isolation, PII handling, and demo-day safety gates.

### 🟢 Beginner

<details>
<summary><b>Q31.</b> It's the night before a flagship demo. You have a working Q&A bot over the customer's docs. What's the single highest-leverage thing to do next?</summary>

- ✅ Run a 20-question smoke test on the real questions the buyer will ask, graded faithful/partial/hallucinated, and fix every hallucination — *The smoke test catches the grounding bugs that lose deals while you can still fix them — it's the most valuable ten minutes of the build.*
- ▫️ Upgrade to the most advanced model so it makes fewer mistakes — *A frontier model still hallucinates fluently; without measuring, you don't know what it does on the buyer's actual questions.*
- ▫️ Polish the UI styling and animations so it looks impressive — *The UI is a wrapper; a beautiful shell on an unmeasured bot is the most common GTM-prototype failure mode.*
</details>

<details>
<summary><b>Q32.</b> A buyer wants to click the prototype themselves over the next week and share it with two colleagues, with their branding. Which shell fits best?</summary>

- ▫️ A local Streamlit app you run on your laptop during calls — *Great for a screen-share rehearsal, but it isn't a hosted, shareable, branded URL the buyer and colleagues can use async.*
- ✅ A hosted, branded URL built with the Vercel AI SDK (useChat) that streams tokens and manages chat state — *A hosted streaming URL is the right delivery mode when the buyer needs to use and share it themselves with their branding.*
- ▫️ A Jupyter notebook you send them to run — *A notebook isn't a usable product surface for a non-technical buyer or their colleagues, and it doesn't read as a real demo.*
</details>

<details>
<summary><b>Q33.</b> Mid-demo, the prospect asks a detailed question about a feature you haven't verified. The bot would happily generate an answer. What's the strongest move?</summary>

- ▫️ Let the bot answer — it's usually right and confidence sells — *Guessing is the deal-killer: a single fabricated claim the expert catches collapses trust in the whole demo.*
- ▫️ Change the subject quickly so no one notices the gap — *Evasion reads as worse than honesty to a technical panel and leaves the real concern unaddressed.*
- ✅ Say you want to give them a precise answer and will follow up with the product team by end of day, then continue — *Committing to precision over guessing is itself a strong signal — interviewers and buyers both test whether you hallucinate or stay honest.*
</details>

<details>
<summary><b>Q34.</b> You're starting a brand-new grounded-Q&A demo for tomorrow. What's the best first step?</summary>

- ▫️ Design a custom retrieval and prompt architecture from scratch to show depth — *The night before a demo is the worst time to re-discover failure modes a known recipe already solved; you pay for the deviation in debugging time.*
- ✅ Adapt the closest OpenAI Cookbook recipe (e.g. Search-Ask) as your starting point, then customize — *Starting from a vetted recipe removes a day of undifferentiated setup and inherits the failure modes it already handles.*
- ▫️ Pick the trendiest agent framework and learn it tonight — *Learning a new framework under deadline adds risk without buying reliability; match the tool to the task, not the hype.*
</details>

<details>
<summary><b>Q35.</b> A buyer asks during the demo: "How is this different from just fine-tuning a model on our documents?" Best answer?</summary>

- ▫️ Fine-tuning is always better because the knowledge is baked into the model — *Baking facts in makes them stale the moment a doc changes, gives no citation, and can't filter by who may see what — the buyer's real concerns.*
- ▫️ They're equivalent; RAG is just a cheaper way to fine-tune — *They're mechanistically different — RAG conditions on retrieved text at query time; conflating them misses the freshness/attribution/access-control advantages.*
- ✅ RAG retrieves your docs at query time, so it stays fresh on updates, cites the exact source, and can filter by user permissions — *Freshness, attribution, and access control are exactly what a customer-facing deployment needs and what fine-tuning can't provide.*
</details>

### 🟡 Intermediate

<details>
<summary><b>Q36.</b> Your demo bot calls a lookup_account tool, but ~1 in 20 times it returns a malformed arguments object and your UI throws a parse error on screen. Best fix?</summary>

- ▫️ Wrap the parse in a try/except and show a generic error — *Hides the symptom but the demo still visibly fails sometimes — and a swallowed error reads as flakiness to the buyer.*
- ▫️ Lower the temperature to 0 so the output is deterministic — *Temperature 0 is greedy, not a schema guarantee; the model can still emit arguments that don't match your shape.*
- ✅ Set strict: true on the tool (with additionalProperties:false) so arguments are guaranteed to adhere to the JSON schema — *Strict mode forces schema adherence on every call, eliminating the malformed-arguments class of on-stage crash.*
</details>

<details>
<summary><b>Q37.</b> Your docs demo confidently states an enterprise SLA of 99.99% — but that figure appears nowhere in the customer's documents. Most likely root cause and right first fix?</summary>

- ▫️ The model is outdated — upgrade to the newest model — *A newer model fabricates just as fluently when the supporting text was never retrieved; this isn't a model-capability problem.*
- ✅ The answer-bearing chunk never made the top-k (or the table parsed to noise) — debug retrieval and add an enforced refusal — *Most RAG "hallucinations" are retrieval misses; print the retrieved chunks, fix ingestion/search upstream, and make a miss return 'I don't know.'*
- ▫️ Raise the temperature so the model is more careful — *Temperature controls randomness, not whether the right passage was retrieved; it won't address a grounding failure.*
</details>

<details>
<summary><b>Q38.</b> You're building the minimum viable grounded Q&A demo over the customer's handbook for tomorrow. Which approach is the right default?</summary>

- ▫️ A multi-agent system with a planner, several retriever agents, and a critic — *That's over-engineering for a single-corpus demo — more latency and failure surface than the questions require, and far harder to debug the night before.*
- ✅ Cookbook Search-Ask: cosine-rank chunks into a token budget, then answer from them with an explicit "I could not find an answer" fallback — *The smallest defensible grounded-QA pattern — conditions on real chunks and refuses when evidence is missing; graduate to agentic only if needed.*
- ▫️ Stuff the entire handbook into one large-context prompt and ask — *Stuffing hits Lost-in-the-Middle, costs more, and drops citations — it isn't selective retrieval and tends to miss buried facts.*
</details>

<details>
<summary><b>Q39.</b> The customer's users frequently search by exact SKU and error codes. Your dense-embedding retrieval keeps missing them in the demo. Best fix?</summary>

- ▫️ Increase top-k to 50 and hope the right chunk appears — *Flooding the prompt with more dense-retrieved chunks adds noise and cost without fixing dense search's weakness on exact tokens.*
- ▫️ Switch entirely to keyword search and drop embeddings — *Pure lexical loses semantic matches (synonyms, paraphrases); you want both signals, not a trade of one weakness for another.*
- ✅ Add lexical BM25 alongside dense retrieval and fuse with RRF (hybrid search) so exact codes are matched as strings — *Exact SKUs/codes are string matches BM25 nails; hybrid + RRF keeps semantic recall while catching the exact tokens dense search misses.*
</details>

<details>
<summary><b>Q40.</b> Your demo renders a citation panel. During a dry run you notice it sometimes cites "[12]" when only sources [1]–[6] were retrieved. What does a production-quality demo do here?</summary>

- ▫️ Hide the citation panel so the discrepancy isn't visible — *Removing the panel removes the trust signal entirely — the citation panel is the buying signal you most want to keep.*
- ✅ Verify cited ids against the retrieved set before rendering; if a citation is invalid, refuse or retry instead of showing it — *A panel that cites a nonexistent source breaks trust on inspection; validating citations keeps the audit story honest.*
- ▫️ Trust the model — it usually cites correctly, so display whatever it returns — *A single fabricated citation an evaluator catches collapses the credibility of the whole panel; "usually right" isn't the bar for an audit tool.*
</details>

<details>
<summary><b>Q41.</b> A support buyer wants a demo where inbound tickets are routed to the right specialist (billing vs. product), each answering from its own knowledge base. What's the cleanest design?</summary>

- ▫️ One giant prompt that contains all billing and product docs and tries to answer everything — *A mega-prompt mixes corpora and tools, isn't least-privileged, and hides the routing decision — exactly what the triage pattern avoids.*
- ✅ A triage agent that classifies intent and hands off to a least-privileged billing or product specialist, each with its own corpus — *The handoff mirrors a real support org, keeps each specialist small/testable, and makes the routing decision visible to the buyer.*
- ▫️ A fully autonomous agent with access to every internal tool, left to decide on its own — *Maximal tool access expands the blast radius and provides no scoping or visible routing — a security review would reject it.*
</details>

<details>
<summary><b>Q42.</b> You want to demo an agent that can issue refunds, but you can't risk it actually refunding real money on stage. Best approach?</summary>

- ✅ Human-in-the-loop approval on the refund action plus a tripwire ceiling, so the agent proposes and a human approves before execution — *Gating irreversible actions behind approval (and capping the amount) lets you demo the capability safely — the gate is the feature the risk team wants.*
- ▫️ Trust the agent and lower the temperature so it behaves predictably — *Temperature doesn't make an irreversible action safe; the risk is the action itself, not output randomness.*
- ▫️ Remove the refund tool entirely and just say it would work — *Telling instead of showing kills the wow; the point is to demo the capability with a credible control, not to omit it.*
</details>

<details>
<summary><b>Q43.</b> For the fastest possible notebook demo of a lead-qualifier agent tomorrow, which runtime is the right default — and why not the others yet?</summary>

- ▫️ The OpenAI Agents SDK, because it has the most guardrail features — *Visible guardrails matter once a customer asks for them; reaching for the heaviest safety surface first slows the fastest demo without a stated need.*
- ▫️ LangGraph, because persistence and human-in-the-loop are always required — *Persistence/approval are escalation triggers, not day-one requirements for a single-pass qualifier demo; it's more machinery than the task needs.*
- ✅ smolagents (a few lines of Python), then escalate to LangGraph/Agents SDK only when persistence or visible guardrails are demanded — *The lightweight runtime is the fastest path to a working demo; you climb the framework ladder only when a real requirement appears.*
</details>

<details>
<summary><b>Q44.</b> The customer's task is "answer FAQ questions from our help center." The SE proposes a multi-agent system with a planner and three worker agents. What's the issue?</summary>

- ▫️ Nothing — more agents always means a more capable, more impressive demo — *Added agents add latency, cost, and failure surface; "more agents" is not "better," and it's a documented failure pattern to pick an agent design a simpler one beats.*
- ▫️ It needs even more agents to be robust — *Scaling up the architecture compounds the over-engineering; the task doesn't call for orchestration at all.*
- ✅ It's over-engineered — a single-pass RAG (or one tool-calling agent) solves FAQ retrieval; pick the simplest pattern that meets the use case — *FAQ answering is retrieve-and-ground; a swarm adds cost and brittleness with no benefit, and simpler patterns are cheaper to demo and operate.*
</details>

### 🔴 Advanced

<details>
<summary><b>Q45.</b> In testing, your agent returns the correct final answer to a ticket, but the logs show it called the refund tool twice and retried a failed lookup five times. How should you treat this?</summary>

- ▫️ Ship it — the final answer was correct, which is what matters — *A correct outcome can hide an unsafe or wasteful trajectory; a double refund call is exactly the kind of behavior that becomes an incident.*
- ✅ Grade the trajectory too (right tools, no unsafe/duplicate calls, clean termination), and add guardrails plus a max-steps cap before shipping — *Agents must be evaluated on trajectory as well as outcome; the duplicate refund call and retry storm are real defects regardless of the final answer.*
- ▫️ Raise the temperature so the agent explores fewer redundant paths — *Temperature won't prevent duplicate tool calls or retry loops; you need guardrails, idempotency, and a step cap.*
</details>

<details>
<summary><b>Q46.</b> Your lead-qualifier agent enriches an inbound lead and writes it to the buyer's HubSpot. The same lead is delivered twice by the form webhook. What design keeps the demo clean — both for the write and for the enrichment?</summary>

- ▫️ Call your single best enrichment provider, then create a new Contact each time — dedupe later with a nightly job — *Creating on every event puts duplicate Contacts in the buyer's CRM on stage; a one-provider call also misses coverage the waterfall would catch and overpays when the cheap source had the answer.*
- ✅ Run an enrichment waterfall (cheapest provider first, stop at first match) and upsert by a unique property (email/domain), so the second delivery is a no-op update — *The waterfall maximizes hit-rate at the lowest blended cost-per-match; an idempotent upsert keyed on a unique value makes the duplicate webhook update-in-place instead of creating a second record.*
- ▫️ Lower the model temperature so the agent produces the same record both times — *Idempotency is a property of the CRM write (upsert on a unique key), not of model determinism; temperature does nothing to prevent a duplicate record.*
</details>

<details>
<summary><b>Q47.</b> To make tomorrow's demo realistic, a teammate suggests pasting a real export of the customer's contacts into your personal ChatGPT account. What's the right call?</summary>

- ▫️ Do it — the data makes the demo land, and OpenAI doesn't train on API data anyway — *This is the Samsung scenario: an unmanaged surface plus real PII is a data-leak incident, and "no training" still means a 30-day retention blast radius.*
- ✅ Use synthetic, customer-shaped data for the build; only use real data later in an isolated environment behind a signed data-handling addendum — *Synthetic-first keeps real PII off unmanaged surfaces; the real-data step is earned with isolation and a contract, which is what procurement requires.*
- ▫️ Paste it but delete the chat afterward to remove the data — *Deleting the chat doesn't undo retention or the policy violation; the data already left the customer's control onto an unmanaged surface.*
</details>

<details>
<summary><b>Q48.</b> A buyer's security reviewer asks how you handle PII. Which answer is strongest?</summary>

- ✅ "We run Presidio on both input and output via an AI gateway, redact logs, and calibrate it with confidence scoring plus a human-review queue for low-confidence spans (recall is ~70–90%)." — *Both-sides scrubbing, log redaction, and a calibrated pipeline with numbers and a human fallback is the specific, defensible story a CISO wants.*
- ▫️ "We anonymize the customer data before it reaches the model." — *Vague and input-only; it ignores output leakage and treats a probabilistic scrubber as a black box — exactly the answer that loses a security review.*
- ▫️ "The model provider is SOC 2 compliant, so PII is their responsibility." — *Vendor compliance doesn't absolve your application of input/output sanitization; it's a shared-responsibility model, and the buyer is auditing your layer.*
</details>

<details>
<summary><b>Q49.</b> You're building a multi-customer demo where each customer's documents are searchable. What must be true to avoid cross-tenant leakage?</summary>

- ▫️ A single shared vector index is fine as long as the prompt tells the model to only use the current customer's docs — *Prompt-level instructions leak: the chunks were still retrievable, and an injection can override the instruction — the channel is structural.*
- ▫️ Retrieve across all tenants and redact the other customers' data from the final answer — *Too late — the model already saw forbidden context and may use it; post-hoc redaction can't guarantee isolation.*
- ✅ Tag every chunk with a tenant_id and enforce an ACL/tenant filter at retrieval time (filter-then-retrieve), with per-tenant isolation across the four layers — *If a chunk is never retrieved it can never leak; query-time tenant filtering plus layered isolation is what stops the leakage.*
</details>

<details>
<summary><b>Q50.</b> Your RAG demo retrieves from a customer-uploaded document store. A security reviewer asks about your biggest risk. Best answer?</summary>

- ▫️ Latency — large documents slow down retrieval — *A real operational concern, but not the security risk the reviewer is probing; it isn't an attack surface.*
- ✅ Indirect prompt injection via retrieved docs — so we tag retrieved content as untrusted, validate output with a privileged LLM, and gate risky actions with a human — *RAG is the primary indirect-injection vector (OWASP LLM01); treating retrieved content as adversarial and adding a validation + human gate is the expected mitigation.*
- ▫️ The model might use slightly outdated training data — *Training-data staleness isn't the injection threat introduced by reading untrusted retrieved content; RAG already addresses freshness.*
</details>

<details>
<summary><b>Q51.</b> A regulated buyer says "our data cannot leave our cloud, and we need to control the encryption keys." What do you commit to in the demo-to-POC plan?</summary>

- ▫️ Assure them the vendor is secure and the standard API is fine for everyone — *It ignores their explicit data-residency and key-control requirements; the standard API path doesn't satisfy a "data can't leave our cloud" constraint.*
- ▫️ Promise whatever closes the deal and figure out the architecture during the POC — *Over-promising on controls you haven't proven is exactly what a security review catches; the matrix should list only what you've tested.*
- ✅ A per-customer VPC / single-tenant deployment with CMEK/BYOK in the customer's own project (or a ZDR endpoint), documented in a promised/proven/out-of-scope control matrix — *Customer-managed keys plus deployment in their environment directly answers residency and key-control, and the matrix commits only to what you've verified.*
</details>

<details>
<summary><b>Q52.</b> An interviewer says: "Build us a demo that researches an account and drafts outreach." What's the strongest first move?</summary>

- ▫️ Immediately start coding the agent and retrieval to show technical speed — *Jumping to code skips the scoping that determines the whole architecture and reads as memorized, not designed — and risks building the wrong thing.*
- ▫️ Pick the trendiest multi-agent framework and start wiring it up — *Leading with a tool choice answers none of the requirements and signals you skip the actual design reasoning.*
- ✅ Scope it out loud first — sources, truth bar, data (synthetic vs real), draft-vs-send, tenancy/stakes — then design to those constraints — *Clarifying sources, grounding bar, data handling, action scope, and tenancy is what lets you pick retrieval, the agent, and the safety gate deliberately.*
</details>

<details>
<summary><b>Q53.</b> During the demo, the drafted email praises the prospect for "your recent Series C" — but that funding round isn't in any retrieved source. What does a production-quality build do?</summary>

- ✅ Drop claims that have no source_id, cite each remaining claim, and enforce refusal so unsourced "facts" never reach the draft — *Grounding the composer in cited findings only — and dropping ungrounded claims — is exactly what prevents the fabricated-flattery failure mode.*
- ▫️ Leave it in — confident, specific flattery improves reply rates — *A fabricated claim the prospect (or panel) catches destroys trust; reply-rate is irrelevant if the email is wrong.*
- ▫️ Lower the temperature so the model invents fewer details — *Temperature won't stop the model from using an unsupported claim; you need a grounding contract that drops unsourced findings.*
</details>

<details>
<summary><b>Q54.</b> A buyer asks whether the system can just send the outreach automatically to save reps time. What's the strongest design stance for the demo?</summary>

- ▫️ Yes — full autonomy is the most impressive version, so enable auto-send — *Auto-sending outreach is an irreversible action with real blast radius (spam, wrong recipient); a security review rejects unscoped send, and it can damage the prospect relationship.*
- ✅ Keep it draft-only with a human-in-the-loop approval (and idempotent send), and frame the gate as the feature that prevents spam and errors — *Gating the irreversible send behind human approval is what makes the capability safe to demo and deploy; the gate is a selling point, not a limitation.*
- ▫️ Enable auto-send but add a high temperature so emails feel more human — *Temperature doesn't address the risk of an irreversible action going to the wrong person; the issue is the unsupervised send itself.*
</details>

<details>
<summary><b>Q55.</b> You're demoing for two prospects in one session on a shared environment. While researching Account A, a finding about Account B appears. What should already be in place?</summary>

- ✅ A tenant_id on every chunk and an ACL/tenant filter applied at retrieval time, with per-tenant isolation across the stack — *Filter-then-retrieve by tenant is what stops cross-account bleed; if B's chunks are never retrieved for A, they can't surface.*
- ▫️ A post-processing step that removes other accounts' names from the final email — *Too late — the model already saw B's context and may have used it; post-hoc redaction can't guarantee isolation.*
- ▫️ A prompt instruction telling the agent to only consider Account A — *Prompt-level rules leak and can be overridden by injection; permission must be enforced in the query, not requested in the prompt.*
</details>

<details>
<summary><b>Q56.</b> Your account-research demo works on a few hand-picked accounts. How do you know it's ready to present to a flagship prospect?</summary>

- ▫️ The emails read well and your manager liked them — *That's the demo, not the bar — a few good drafts don't cover the accounts where it fabricates, leaks, or bleeds across tenants.*
- ▫️ It uses the newest model and a managed vector database — *Tooling choices don't prove faithfulness, isolation, or that send is gated; they're not evidence of readiness.*
- ✅ It passes a 20-question smoke test on real accounts (zero ungrounded claims), scrubs PII both sides, isolates tenants at retrieval, and gates send behind a human — *Readiness is a measurable bar across grounding, privacy, isolation, and safety — the smoke test plus the L4 controls — not a vibe check.*
</details>

<details>
<summary><b>Q57.</b> You're building a brand-new grounded-Q&A demo and the customer's users search by exact part numbers. Which retrieval baseline do you reach for first?</summary>

- ✅ Hybrid retrieval — dense embeddings for semantic recall fused with BM25 for exact-token matches — *Exact part numbers are string matches BM25 nails; combining them with dense recall via RRF is the robust default when queries mix natural language and exact codes.*
- ▫️ Dense-only retrieval with a very large top-k — *Dense embeddings systematically miss exact codes; enlarging top-k adds noise without fixing the failure mode.*
- ▫️ A fine-tuned model that memorizes the part catalog — *Baking the catalog into weights makes it stale on the next SKU change and gives no citation — the wrong tool for a lookup problem.*
</details>

<details>
<summary><b>Q58.</b> A demo Q&A bot over the customer's handbook is asked a question the handbook doesn't answer. What's the production-quality behavior?</summary>

- ✅ Return an explicit "I could not find an answer in the provided documents" refusal rather than generating from parametric knowledge — *Enforced refusal on a retrieval miss is the grounding contract that keeps a demo honest; a fabricated answer on a missing fact is the failure mode that loses the deal.*
- ▫️ Answer from the model's general knowledge so it never looks stuck — *General-knowledge answers aren't grounded in the customer's docs and can contradict their policy — confident-but-unsourced is exactly what an evaluator catches.*
- ▫️ Silently return an empty response — *An empty response reads as broken; the honest, trust-building behavior is an explicit refusal, not a blank.*
</details>

---

## 3 · Solution design & demo selling

Enterprise reference architecture, tenant isolation, evals as production code, observability (TTFT/latency/cost spans), MCP connectors, and the discovery/demo loop (SPIN, Challenger, ROI ranges).

### 🟢 Beginner

<details>
<summary><b>Q59.</b> In an architecture round you're given: "Design a customer-facing medical-billing AI that turns patient notes into insurer claims." What's the strongest opening move?</summary>

- ▫️ Pick the best foundation model and fine-tune it on a corpus of past claims — *Fine-tuning as the first move is a documented weak-answer tell — it treats the LLM as the system and skips retrieval, evals, governance, and the SLOs that make it enterprise-grade.*
- ✅ Lay out the walking skeleton (gateway → orchestrator → retrieval → tools → evals/guardrails → observability), then state the SLOs and turn layers on one at a time — *The skeleton-first move maps each layer to a rubric axis and surfaces the audit-bearing parts (RBAC retrieval, eval gate, audit log) that decide an enterprise build.*
- ▫️ Estimate the token cost per claim and optimize the prompt length first — *Cost matters but it's one axis inside one layer; leading with it skips problem decomposition, reliability, and the safety/eval design the panel is scoring.*
</details>

<details>
<summary><b>Q60.</b> A customer asks, "How will we know the AI is actually working in production?" You have 90 seconds. Strongest answer?</summary>

- ✅ A golden dataset gated in CI plus online sampling of >5% of traffic with a calibrated LLM-judge and a drift dashboard; deterministic graders where possible, judge where needed — *Names offline gates + online detection, the cheapest-sufficient grader per task, and judge calibration — the complete production-AI health stack.*
- ▫️ We collect thumbs-up / thumbs-down from users and review the negatives — *A thumbs button is a one-bit sentiment signal that correlates poorly with task success; it is not a measurement instrument and reads as a weak answer.*
- ▫️ We benchmark the model on MMLU and HumanEval before launch — *Public benchmarks measure a generic model, not the customer's task; they don't catch the customer-specific failure modes evals exist to find.*
</details>

<details>
<summary><b>Q61.</b> A customer asks why you'd standardize on MCP instead of writing direct API clients for each system. Best answer?</summary>

- ✅ It collapses integration from N×M bespoke glue to N+M standard endpoints — every connector is the same Resources/Prompts/Tools shape, so integrations stop exploding — *The value is uniformity: one protocol and one primitive set means each server is written once and every host speaks to all of them.*
- ▫️ MCP is faster at runtime than REST calls — *MCP is a protocol layer over JSON-RPC, not a performance optimization — speed isn't the argument and claiming it signals a shallow grasp.*
- ▫️ MCP removes the need for authentication to backend systems — *The opposite — MCP specifies auth (bearer/OAuth) and consent as first-class; it standardizes integration, it doesn't eliminate authn/authz.*
</details>

<details>
<summary><b>Q62.</b> You're explaining MCP's topology in an architecture round. Which description is correct?</summary>

- ✅ Host contains clients (one per server), each client connects to a server exposing Resources/Prompts/Tools, over JSON-RPC 2.0 via stdio or streamable HTTP — *That is the spec's host/client/server model, primitive vocabulary, and the two transports — the clean topology that signals hands-on familiarity.*
- ▫️ A single shared bus that all agents and tools publish to and subscribe from — *MCP is not a shared message bus; it's point-to-point host↔server connections, one client per server, over JSON-RPC.*
- ▫️ Servers run the LLM and call out to clients for data — *Backwards — the host runs/holds the model; servers expose data and tools, and clients (in the host) connect to them.*
</details>

<details>
<summary><b>Q63.</b> In a mock discovery the "VP of Product" says alerting is noisy and engineers waste time. What's the highest-value next question?</summary>

- ▫️ "Great — let me show you how our dashboard de-duplicates alerts." — *Jumping to a feature demo skips quantifying the pain in the customer's voice; you've pitched before earning the right and produced no defensible number.*
- ✅ An Implication question that quantifies the downstream cost: "If alerts are noisy, how many hours per engineer per week go to reconciling them, and what does that delay?" — *The SPIN Implication move turns a complaint into a customer-owned number that the demo and ROI story then answer — the SE's signature contribution.*
- ▫️ "Which competitors are you evaluating?" — *Competition matters for qualification, but here it abandons the open pain thread before quantifying it — you lose the chance to anchor the cost in their words.*
</details>

### 🟡 Intermediate

<details>
<summary><b>Q64.</b> A regulated customer asks how you guarantee tenant A can never retrieve tenant B's documents in a shared-model deployment. Best answer?</summary>

- ▫️ Instruct the model in the system prompt to only use the current tenant's data — *A natural-language instruction is advisory — the model can be talked out of it; it is not a control and will fail an audit.*
- ▫️ Give each tenant a dedicated fine-tuned model so the data never mixes — *That's the most expensive isolation tier (per-tenant replicas) and is overkill when a metadata filter at retrieval already enforces the boundary; you escalate to it only when a contract forces it.*
- ✅ Enforce RBAC at the retrieval layer: filter to tenant_id and the caller's ACL before similarity runs, so foreign documents are never candidates — *Zero-trust retrieval puts the boundary where code decides, not where probability decides — the filter-then-retrieve pattern.*
</details>

<details>
<summary><b>Q65.</b> A support assistant over a knowledge base that employees edit all day keeps citing policies that changed hours ago. Which architecture change actually fixes it?</summary>

- ▫️ Increase the nightly batch re-index to run twice a day — *Still batch — it shrinks but doesn't close the staleness window, and the customer experiences wrong answers between runs.*
- ✅ Move to CDC + streaming ingestion (e.g. Flink) with real-time upserts into the vector store, sized to the freshness SLA — *Change-data-capture keeps vectors synchronized with source edits in near real time, eliminating the "stale brain"; the freshness SLA is what justifies the heavier pipeline.*
- ▫️ Swap to a larger-context model so it can read more documents at once — *Context size has nothing to do with whether the index reflects today's edits — the wrong text is being retrieved, not too little.*
</details>

<details>
<summary><b>Q66.</b> Your AI feature's monthly bill 10×'d overnight with flat user traffic. Most likely cause and the right safeguard?</summary>

- ▫️ The provider raised prices; switch to a cheaper model — *A sudden 10× with flat traffic is almost never a price change — it's unbounded internal generation; swapping models without bounding the loop just makes a cheaper runaway.*
- ✅ An agent loop or retry storm with no token cap; bound it with gateway rate limits, max-tokens, a per-session cost budget, and back-pressure on the queue — *LLM endpoints are denial-of-wallet targets; the fix is the same back-pressure/rate-limiting primitives that govern any production system, applied per-token.*
- ▫️ Users discovered the feature; this is normal growth — *The premise is flat traffic — cost decoupled from usage points to runaway generation, not demand.*
</details>

<details>
<summary><b>Q67.</b> A customer wants the lowest-cost design for a high-volume support assistant where most questions repeat. Which lever should you reach for first?</summary>

- ▫️ Fine-tune a small model so each call is cheaper — *Fine-tuning is a fixed project cost that doesn't exploit the key fact here — repetition — and still pays full price for every duplicate question.*
- ▫️ Buy more GPU capacity to lower per-token cost — *Capacity changes unit economics marginally; it doesn't eliminate the redundant generations driving the bill.*
- ✅ Add semantic caching of similar prior queries (plus model routing and a token budget), cutting average $/request by an order of magnitude on repetitive traffic — *When the same fifty questions arrive a thousand ways, a semantic cache serves them without re-generating — the single biggest cost lever for repetitive traffic.*
</details>

<details>
<summary><b>Q68.</b> You need to grade whether the agent returned valid JSON with the right fields, and separately whether its written summary is high-quality. Which grading split is correct?</summary>

- ▫️ Use the LLM-as-judge for both, since it understands the task best — *Using a judge to check JSON validity is wasteful and less reliable than code — it ignores the "cheapest sufficient grader" rule and adds non-determinism to a deterministic check.*
- ✅ Deterministic grader (schema + field assertions) for the JSON; calibrated LLM-as-judge with a rubric for the summary quality — *Match the grader to the task: exact-match/schema validation is deterministic and free; open-ended quality needs a calibrated judge — composing classes is the senior move.*
- ▫️ Use exact string match for both against a reference answer — *Exact match can verify JSON structure but fails on open-ended summaries, where many different wordings are equally good — you'd reject correct answers.*
</details>

<details>
<summary><b>Q69.</b> A customer complains the assistant "feels slow." Your aggregate p95 looks fine. What's the right diagnostic move?</summary>

- ▫️ Tell them p95 is within SLO and the perception is subjective — *A healthy aggregate hides per-cohort tails; dismissing it without slicing the spans is exactly the anti-pattern observability exists to fix.*
- ✅ Split the response into TTFT / generation / post-processing spans and slice by prompt version, tenant, and retrieval slice to locate the tail — *Modeling the call as three spans and slicing by dimensions is how Intercom found and cut two seconds — it attributes user-perceived latency to its dominant cause.*
- ▫️ Upgrade everyone to a faster model to be safe — *Blindly swapping models is expensive and may miss the real cause (a big prompt's prefill, a slow tool call, or a long output) that the spans would reveal.*
</details>

<details>
<summary><b>Q70.</b> You can ship only ONE additional latency signal on every LLM span. Which buys the most diagnostic power for a customer-facing agent?</summary>

- ▫️ A single end-to-end total-latency number — *Total alone can't tell prefill from generation from tool time — it's the aggregate that hides the tail you're trying to find.*
- ▫️ CPU utilization of the inference host — *Host CPU rarely explains user-perceived LLM latency, which is dominated by prompt size and output length, not host load.*
- ✅ Time-to-first-token, recorded separately from total latency — *TTFT vs total is the split that localizes the tail to prefill vs generation and has different fixes — the single most valuable latency signal, per Intercom's win.*
</details>

<details>
<summary><b>Q71.</b> You're instrumenting a RAG assistant and must choose what to attach to each span for the most useful cost analysis. Best choice?</summary>

- ▫️ Only the total token count per request — *A single total can't separate cached from fresh tokens or attribute cost to a prompt variant or tenant — it's the aggregate that hides the leak.*
- ✅ Input / output / cached / total token counts plus prompt version, tenant, and retrieval slice as dimensions — *Granular per-span token breakdown with cohort dimensions is what lets you find which prompt variant and tenant drive the cost — the leak-finding pattern.*
- ▫️ A daily dollar total emailed to the team — *A daily aggregate tells you the bill rose but not which prompt, tenant, or slice caused it — you can't act on it without span-level breakdown.*
</details>

<details>
<summary><b>Q72.</b> An agent in production needs to call eight internal MCP servers across two teams. What's the right architecture for credentials and audit?</summary>

- ▫️ Give the agent the OAuth tokens for all eight servers directly — *Per-agent raw tokens to many servers is the N×M sprawl that fails compliance — no central policy point, fragmented audit, broad blast radius.*
- ✅ Route all traffic through one MCP gateway that holds credentials, enforces a per-agent allow-list, inherits the customer's IdP RBAC, and emits a unified audit log — *Past ~5 servers the gateway pattern collapses the OAuth/credential/audit sprawl into one broker — the control-plane model.*
- ▫️ Spin up a separate agent per server so each holds only one credential — *Fragmenting into many agents multiplies orchestration and still scatters audit; it doesn't give you the single policy and audit point a gateway does.*
</details>

<details>
<summary><b>Q73.</b> A security reviewer asks what stops an agent from taking a destructive action via a connected tool. Strongest containment story?</summary>

- ▫️ The model is instructed to be careful with destructive actions — *Tool execution is arbitrary code; a natural-language caution is advisory and not a control — it will not satisfy a security review.*
- ▫️ Run the agent with broad admin credentials but log everything — *Logging after the fact doesn't prevent the destructive call; broad credentials maximize blast radius — you want least-privilege allow-lists and consent before execution.*
- ✅ Explicit user consent for tool ops, a per-agent allow-list of servers, IdP-checked permissions, and an audit log of every call — consent and exec treated as boundaries — *These are MCP's named security principles plus enterprise zero-trust on top — boundaries enforced by code and identity, not by the prompt.*
</details>

### 🔴 Advanced

<details>
<summary><b>Q74.</b> After a refactor, your eval pass-rate jumps from 61% to 92% with no change to the model or prompt. What's the right reaction?</summary>

- ▫️ Celebrate and ship — the system clearly got better — *A leap with no model/prompt change is the 42%→95% signature of a grader or task-spec bug, not a real improvement; shipping on it means shipping a wrong conclusion.*
- ✅ Bisect the grader and task spec first — a pass-rate that jumps without a model change is a grader bug until proven otherwise — *The grader is production software; scores can move 42%→95% from grading bugs alone. Verify the meta-eval before trusting the number.*
- ▫️ Lower the threshold so the result is more conservative — *Changing the threshold hides the signal instead of diagnosing it; the question is whether the measurement is correct, not how strict it is.*
</details>

<details>
<summary><b>Q75.</b> Your offline golden-set eval has passed 100% for weeks, but users report new wrong answers. What's the gap and the fix?</summary>

- ▫️ The model degraded; swap to a newer model — *There's no evidence of model change, and swapping models doesn't address that your measurement never saw the new failure mode.*
- ▫️ Raise the sampling temperature so the eval is harder — *Temperature doesn't change which cases the offline set contains; the problem is coverage of real, drifting traffic, not difficulty.*
- ✅ The golden set saturated and went stale; add online evals that sample production traffic to surface new failure modes, then fold them back into the golden set — *Offline-only evals go stale — a 100% pass-rate signals saturation, not health. Online sampling catches drift and new modes the frozen set never imagined.*
</details>

<details>
<summary><b>Q76.</b> A capability eval you wrote to probe a hard multi-step task has climbed to a ~100% pass rate. What should you do with it?</summary>

- ▫️ Delete it — it no longer fails, so it's providing no value — *Deleting it loses regression protection; a task that now passes is exactly what you want to keep passing as the system evolves.*
- ✅ Promote it into the regression suite so it permanently guards against backsliding, and write a harder capability eval to find the new frontier — *The dual-suite pattern: saturated capability evals graduate into ~100%-pass regression evals; you then push the capability frontier with a harder probe.*
- ▫️ Lower its difficulty so it produces a spread of scores again — *Hand-nerfing a passing eval fabricates signal; the right move is to lock in the win as a regression and raise the bar elsewhere.*
</details>

<details>
<summary><b>Q77.</b> Your team keeps re-discovering the same failure (wrong citations) every quarter. What's missing from the system?</summary>

- ✅ A closed feedback loop: capture signals on traces → classify into failure modes → fix the top bucket → convert fixes into permanent eval cases — *Without feeding failures back into the eval harness, fixes don't become regressions and the same mode recurs; the loop is what compounds quality.*
- ▫️ A bigger model with better world knowledge — *Wrong citations are usually a retrieval/grounding or instrumentation gap, not a knowledge gap — a bigger model won't stop the recurrence.*
- ▫️ More thumbs-up / thumbs-down buttons in the UI — *Thumbs are one-bit signals; without classification into specific failure modes and feedback into evals, they don't prevent recurrence.*
</details>

<details>
<summary><b>Q78.</b> The customer says quality dropped this week, but your team shipped nothing. What do you check first?</summary>

- ▫️ Assume random LLM variance and wait to see if it recovers — *A sustained drop with no deploy is not noise — waiting lets a real regression keep hurting the customer.*
- ✅ Prompt-version and model-version telemetry plus a continuous-eval regression alert and the feedback cohort — a no-deploy drop is the provider-side or interacting-change signature — *Pinned-version telemetry + scheduled golden-set eval against live traffic is exactly what catches silent provider updates and interacting changes before the customer escalates.*
- ▫️ Roll back the most recent infrastructure change — *If nothing shipped, there's no app change to roll back; the cause is upstream (model/provider) or an interaction the eval and version telemetry will reveal.*
</details>

<details>
<summary><b>Q79.</b> A regulated bank needs audit logs and IdP integration for AI tool access on day one. Build the gateway in-house or buy a governance product?</summary>

- ▫️ Always build in-house for maximum control — *Building in-house delays auditability and IdP integration that the bank needs on day one — control isn't the binding constraint, time-to-compliance is.*
- ✅ Buy the governance layer for time-to-compliance (audit + Okta/Entra on day one); name the tradeoff that you give up some portability and new-feature adoption speed — *For a regulated buyer needing compliance immediately, the purpose-built gateway wins; the senior move is naming the optionality you trade for it.*
- ▫️ Avoid MCP entirely and use direct integrations to dodge the question — *Direct integrations bring back the N×M OAuth/audit sprawl and still need governance — abandoning MCP doesn't remove the compliance requirement.*
</details>

<details>
<summary><b>Q80.</b> A champion needs to defend the project to a steering committee you won't attend. How do you build the ROI story?</summary>

- ▫️ Present a polished 50% ROI in your own words so it feels conservative and credible — *A 50% ROI is high enough to require approval yet low enough to feel optimistic — the worst combination — and a story in your voice dies when you're not in the room.*
- ✅ Build From→To→Gap across the four value levers with the customer's numbers, anchor a 200–600% range, and hand it to the champion in their language so they can deliver it as their own — *A credible range plus customer-sourced levers, in the champion's vernacular, is what survives committee — the champion re-tells it because it's theirs.*
- ▫️ Send the champion your standard vendor case-study deck — *Vendor case studies aren't the customer's numbers and aren't in the champion's voice; executives discount them and the story doesn't transfer.*
</details>

<details>
<summary><b>Q81.</b> On an AI deal, the buyer says "we'll pull the data together for the PoC." What's the senior move?</summary>

- ▫️ Proceed to the full PoC quickly to keep momentum — *AI is gated by data; scoping the PoC on not-yet-ready inputs is exactly how it fails in week three, after the champion has spent political capital.*
- ✅ De-risk by scoping a fixed-scope data validation as the first milestone, surfacing readiness before the PoC depends on it — *Data readiness is the discovery filter; making validation the first milestone prevents a dead PoC and protects the champion's credibility.*
- ▫️ Switch the conversation to model selection since data can be sorted later — *Data can't be "sorted later" in an AI PoC — readiness is the gating constraint, and deferring it guarantees the failure mode you're trying to avoid.*
</details>

<details>
<summary><b>Q82.</b> You have 15 minutes for a mock discovery against a VP of Product and VP of Marketing. How do you spend it?</summary>

- ▫️ Open the product and walk through the main features so they see the value fast — *A feature tour with no scoping is the weak pattern panelists penalize; you haven't learned the workflow, the stakeholders, or the constraints.*
- ✅ Three beats — business outcome/stakeholders, today-workflow/pain (with Implication questions), then constraints/risk — and summarize the spec back at the end — *The three-beat structure translates a vague problem into a system spec while resisting an immediate solution — exactly what the discovery round scores.*
- ▫️ Invent plausible systems and APIs the case didn't mention so you can draw an architecture — *Fabricating systems is a documented trap — it signals you can't run discovery under ambiguity; ask scoping questions instead of inventing facts.*
</details>

<details>
<summary><b>Q83.</b> A buyer pattern-matches your LLM agent to "just another rules-based bot we tried and it failed." What does the SE do before demoing?</summary>

- ✅ Reframe the buyer's mental model first (Challenger), connecting their failed rules-engine experience to why a different approach is needed, then show the product — *Challenger's Reframe replaces the wrong mental model before the demo; otherwise the buyer maps the AI onto the legacy tool and discounts everything you show.*
- ▫️ Immediately demo every feature to prove it's different — *Demoing into a wrong mental model means the buyer reinterprets each feature as the old failed tool — you must change how they think first.*
- ▫️ Agree it's similar and compete on price — *Conceding the frame surrenders your differentiation and turns a value sale into a discount — the opposite of the reframe move.*
</details>

<details>
<summary><b>Q84.</b> You have a 30–45 minute panel demo for the logistics-rerouting scenario. How do you allocate the time?</summary>

- ▫️ Spend most of it walking every feature so they see the full product — *Filling the window with features is the most common failure — it buries the value and leaves no time for the Q&A and ROI re-anchoring that win the room.*
- ✅ 5–7 minutes of slides/context, ~10 minutes of a focused hero/problem/resolution demo on three capabilities, then live Q&A and re-anchor on the quarter-cost ROI — *The rubric caps slides at 5–7 minutes; a tight, interactive demo tied to the customer's number plus time for objections is what scores.*
- ▫️ Skip slides entirely and improvise the demo to seem confident — *A brief context frame is needed to set the pains in the customer's words; improvising with no structure forfeits the storyboard that anchors value.*
</details>

<details>
<summary><b>Q85.</b> In Act 2 you're tempted to showcase the agent's impressive multi-tool planning, which the customer never raised. What's the senior call?</summary>

- ✅ Cut it — the solution narrative must be answer-only, mapping each capability to a pain the customer quantified — *AI demos fail when you show capabilities the customer never named; if a layer doesn't map to a named pain, it doesn't belong in the demo.*
- ▫️ Show it — more demonstrated capability always strengthens the case — *Unrequested capability dilutes the story and invites tangents; the rubric rewards need-over-features, not breadth.*
- ▫️ Show it but only briefly at the end — *Even a brief unrequested tour breaks the answer-only discipline and spends scarce time that should re-anchor on the customer's number.*
</details>

<details>
<summary><b>Q86.</b> Across the loop (scenario → architecture/build → demo), what most distinguishes a strong candidate?</summary>

- ▫️ Maximum depth in the architecture round, treating the others as warm-ups — *Depth in one round doesn't carry the loop; weak handoffs (a spec the demo ignores) sink otherwise strong candidates.*
- ✅ A coherent handoff — discovery's quantified spec feeds an SLO-anchored architecture that the demo dramatizes and closes on the customer's number — *The unspoken bar is the seam between rounds; composing the five lessons into one defensible arc is the senior solutions-engineer signal.*
- ▫️ Using the most advanced AI techniques in every round to show expertise — *Reaching for advanced techniques (or fine-tuning) over fit is a weak tell; the loop rewards judgment and composition, not novelty for its own sake.*
</details>

---

## Scoring yourself

| You got… | Read as… |
|---|---|
| **< 60%** | Re-read the roadmap stages for your weak topic before interviewing — you're pattern-matching to tools, not rubrics. |
| **60–80%** | Solid. Drill the ✅→▫️ *reasons* on the ones you missed; the interview tests the reason, not the letter. |
| **> 80%** | Interview-ready. Now go [ship 3–5 portfolio repos](roadmap/07-portfolio-projects.md) so you can *show* it, not just answer it. |

> [!TIP]
> The single thread through all 86: **lead with the revenue mechanism, grade reliability over the happy path, and choose the simplest pattern that meets the need.** If your answer names a tool before it names a funnel stage or a failure mode, it's the junior answer.

---

<div align="center">

### Don't just apply. Get **referred**, get **prepped**, get **Landed**.

[![Get Started](https://img.shields.io/badge/Get%20Started%20Free-→-6C2BD9?style=for-the-badge)](https://landed.jobs)

<sub>Maintained by [Landed](https://landed.jobs) · Questions drawn from real 2026 GTM engineering loops. No affiliation with the companies or tools named. Content MIT-licensed.</sub>

</div>
