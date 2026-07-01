> **Stage 3 of 9 · Customer-facing AI prototypes** — build a convincing, grounded LLM demo in an afternoon; then make it *do* things with agents.
> [← 2 · AI automation](02-ai-automation-for-gtm.md) · [Back to roadmap](../README.md) · Next: [4 · Solution design & demo →](04-solution-design-and-demo-selling.md)

# 🧪 Customer-facing AI prototypes

**The demo is the audition, not the trial.** In an AI sale, buyer belief is manufactured in a live demo — and it's judged on one axis above all: *does it look like it can be trusted with real work?* A polished demo is no longer a differentiator (every vendor has one). The win comes from a demo that is **grounded, honest about its limits, and reliable under questioning.** This stage is the afternoon build: from an API key to a credible chat demo, with the reliability scaffolding that separates a $100K pilot from a "thanks but no thanks."

## Why an LLM demo breaks differently

A normal software demo fails obviously (a button 404s). An LLM demo fails **silently and credibly**: a fluent, confident, *wrong* answer a domain expert in the room can falsify on the spot. The canonical case: a logistics-SaaS SE demoed Q&A over a 600-page manual with a prompt-only bot; it hallucinated **3 of 10** questions and lost the deal. The rebuild — grounded retrieval plus an explicit "I could not find an answer" fallback — answered **8 correctly and refused 1**, and the customer closed. Same model, same docs.

> [!TIP]
> **The buying signal is not fluency — it's *visible reliability*.** A bot that cites a source or cleanly refuses reads as an *audit tool*; the same bot answering confidently with no citation reads as a *party trick*. Engineer the refusal and the citation first — they are the product.

## Three properties of a trustworthy demo

1. **Structured output** — it parses every time (no stray-token crash on stage).
2. **It can say "I don't know"** — refusal is a first-class *designed* behavior.
3. **It was measured before the meeting** — a smoke test, not a vibe check.

## Lock the output: strict-mode tool calls

Make the model *do things* (look up an account, draft an email) via **tool calling**. The reliability knob is `strict: true` — it guarantees the model's arguments adhere to your JSON schema instead of being best-effort:

```python
tools = [{
    "type": "function",
    "function": {
        "name": "lookup_account",
        "strict": True,                          # <-- the reliability knob
        "parameters": {
            "type": "object",
            "properties": {"domain": {"type": "string"}},
            "required": ["domain"],
            "additionalProperties": False,       # strict mode requires this
        },
    },
}]
```

For rendered data (a summary card, a lead score), use **structured outputs** (schema-constrained decoding). The pairing: **strict tool calls for actions, structured outputs for rendered data, free-form text only for the prose a human reads.** Once outputs are constrained, the "parser crashed on a weird response" class of bug — the one that makes a buyer wonder what *else* is flaky — disappears.

## Ground the demo in the customer's docs: Search-Ask

The beat that closes AI evaluations: drop the customer's *own* documents in and answer correctly, with citations, in front of the people who wrote them. **RAG** wins here — retrieve relevant passages at query time and make the model answer from them, with a citation and a refusal path. The smallest defensible pattern is the cookbook **Search-Ask**:

```python
SYS = ('Answer using ONLY the sources below. Cite the source id [n] after each claim. '
       'If the answer is not in the sources, reply exactly: '
       '"I could not find an answer in the documents."')
# SEARCH: cosine-rank chunks, fill UP TO a token budget (~1500). ASK: ground + refuse.
```

RAG buys three things a buyer cares about that fine-tuning can't: **freshness** (re-index when a doc changes, don't re-train), **attribution** (cite the exact chunk), and **access control** (filter by who may see what). For a customer-facing demo, **attribution is the buying signal** — a cited answer is auditable.

> [!WARNING]
> **Most "RAG hallucinations" are retrieval misses wearing a costume.** Before blaming the model, *print the retrieved chunks* — nine times out of ten the answer-bearing chunk never made top-k. The fix is upstream: a layout-aware parser (tables → not word soup), structure-aware chunking (~256–512 tokens with overlap), or **hybrid search** (add BM25 for exact SKUs/error codes dense search misses, fuse with RRF). A bigger model fabricates just as fluently over the same missing context.

### The citation panel + four grounding layers

Render cited source passages under every answer — and **verify the cited ids actually exist before displaying them** (a panel citing a nonexistent source breaks trust on inspection). Grounding is four stacked defenses, not one trick:

| Layer | Defense | What it catches |
|---|---|---|
| 1 | Prompt + refusal template | Confident answers when evidence is missing |
| 2 | Strict schema / structured outputs | Invented arg names, unparseable responses |
| 3 | Chain-of-Note filtering (tag each chunk relevant/partial/noise) | Noisy chunks the model embellishes |
| 4 | Offline answer-doc smoke test | Everything else, before the customer sees it |

## Ship the eval first: the 20-question smoke test

The highest-leverage habit most SEs skip: **before any customer-facing demo, run a 20-question offline smoke test.** Hand-curate 20 real questions with known-good answers, run each through the full pipeline, and grade every answer **faithful / partial / hallucinated.** Fix the hallucinations before the call. A demo that scores 18 faithful / 2 refused beats one that "felt great" once — and the same set becomes your morning-of regression gate and an artifact you hand the buyer to re-run on their data.

```
The 60-minute flagship build (allocate by LEVERAGE, not polish)
0-10   ingest: chunk + embed + index; 3 sanity-query checks
10-25  Search-Ask: token budget + "I could not find an answer"; strict tool
25-40  one output guardrail: LLM-judge "every claim in the chunks?" -> refuse
40-50  chat shell + citation panel (the trust signal)
50-60  20-question smoke test -> fix every hallucination
```

The UI is a wrapper — pick the shell by **delivery mode**: **Streamlit** for a rehearsal/screen-share, **Gradio** for a shareable Space, the **Vercel AI SDK** (`useChat`) for a hosted, branded, streaming URL. Brand the demo for the customer (their logo, vocabulary, a problem-summary slide one) — ten minutes that changes "generic AI thing" into "a tool built for us."

## When the demo has to *do* things: agents

An **agent** runs a loop of **Thought → Action (tool call) → Observation**, repeating until the task is done. Every framework is scaffolding around that loop. Four sales/support agent roles recur — name the role first and you've scoped 80% of the build:

| Role | What it does | Key primitive |
|---|---|---|
| Lead qualifier | Score + route inbound | tool call + schema (enrichment waterfall → **idempotent** CRM upsert) |
| Knowledge Q&A | Answer from a corpus | retriever-as-tool |
| Triage / router | Classify intent → hand off to a specialist | **handoff** |
| Proposal / composer | Draft customer-specific reply | compose retrieve + write |

Pick the runtime by control need, not brand: **smolagents** for the fastest notebook demo → **LangGraph** when you need persistence + human-in-the-loop → **OpenAI Agents SDK** when the customer demands *visible* guardrails.

> [!WARNING]
> **An agent demo's wow is the action; its credibility is the gate around the action.** Every tool the agent can call expands the blast radius — an over-autonomous agent that issues a refund or emails a customer *on stage* is a catastrophe, not a wow. Ship it **scoped**: least-privilege tools, a **human-in-the-loop approval on anything irreversible** (the agent *proposes*, a human *approves*), a tripwire ceiling, and a visible reasoning trace. Grade the **trajectory**, not just the outcome — a correct final answer that called the refund tool twice and retried five times is a production incident wearing a green checkmark.

> [!NOTE]
> **Privacy & tenancy carry into the demo.** Don't paste a customer's real contact export into a personal ChatGPT account (the Samsung scenario) — build on **synthetic, customer-shaped data**, and only use real data later in an isolated environment behind a signed data-handling addendum. For multi-tenant demos, tag every chunk with a `tenant_id` and **filter-then-retrieve** at query time — a prompt instruction to "only use Account A's data" leaks, because the chunks were still retrievable.

## 📚 Resources

- 💻 [OpenAI Cookbook](https://github.com/openai/openai-cookbook) — **repo · MIT.** 400+ runnable recipes (Search-Ask, tool calling, structured outputs). The parts bin — adapt, don't build from a blank file.
- 📘 [OpenAI Structured Outputs & Function Calling](https://platform.openai.com/docs/guides/function-calling) — `strict:true`, `additionalProperties:false` — the on-stage-crash fix.
- 🎬 [Why Your RAG System Is Broken, and How to Fix It](https://youtube.com/watch?v=wexpoR1R03A) — TWIML AI Podcast (Jason Liu). Retrieval, not the model, caps quality.
- 🎬 [How We Build Effective Agents](https://youtube.com/watch?v=D7_ipDqhtwk) — Barry Zhang, Anthropic (AI Engineer). The Thought-Action-Observation loop, mechanistically.
- 🎬 [How To Prepare for a Customer or Interview Demo](https://youtube.com/watch?v=BU50hcY3FH8) — We The Sales Engineers. The polish that wins the room.
- 🛠️ [Streamlit `chat` elements](https://docs.streamlit.io/develop/api-reference/chat) — a credible chat shell in ~20 lines of Python for a rehearsal.
- 🛠️ [Vercel AI SDK (`useChat`)](https://ai-sdk.dev/docs) — the hosted, branded, token-streaming URL a buyer can click and share.
- 💻 [onvoyage-ai/gtm-engineer-skills](https://github.com/onvoyage-ai/gtm-engineer-skills) — **repo · 1.2k★ · MIT.** Executable Claude/Codex skills (audit-website-aeo, build-resource-pages) you can wrap into a demo.

---

**Next:** [4 · Solution design & demo selling →](04-solution-design-and-demo-selling.md) — enterprise architecture, evals, observability, MCP, and the discovery/demo rounds.
