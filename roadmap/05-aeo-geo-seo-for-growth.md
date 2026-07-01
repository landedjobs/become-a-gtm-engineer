> **Stage 5 of 9 · AEO / GEO / SEO for growth** — getting *cited* by ChatGPT, Perplexity, and Gemini, not just ranked by Google.
> [← 4 · Solution design](04-solution-design-and-demo-selling.md) · [Back to roadmap](../README.md) · Next: [6 · Tools & stack →](06-tools-and-stack.md)

# 🔎 AEO / GEO / SEO for growth

**The organic frontier moved.** A growing share of buyer research now happens *inside an answer engine* — ChatGPT, Perplexity, Gemini, Copilot — where the user reads one synthesized answer and rarely clicks a blue link. That reshapes growth work for a GTM engineer: the job is no longer only to *rank* a page, but to make your content the source an LLM **cites** when it answers a buyer's question. This is the highest-leverage growth skill on the 2026 roadmap that most teams still ignore.

## The three acronyms, disambiguated

| Term | Optimizes for | The bar |
|---|---|---|
| **SEO** | Search Engine Optimization | rank in Google/Bing blue links |
| **AEO** | Answer Engine Optimization | win the featured snippet / voice answer / direct answer |
| **GEO** | Generative Engine Optimization | get *cited* inside an LLM's synthesized response |

They stack: solid SEO fundamentals (crawlable, fast, structured) are still the floor; AEO structures content so it's *extractable as an answer*; GEO tunes for *citation inside generative engines.* The Aggarwal et al. GEO paper (Princeton, arXiv 2311.09735) is the load-bearing result: **"GEO can boost visibility by up to 40% in generative engine responses"** — with tactics like adding citations, statistics, and quotations to content.

> [!NOTE]
> **AI engines cite tables and structured, quotable content roughly 2.5× more than prose.** That's why every stage in this repo leans on tables and answer-first framing — it's not just readability, it's citation-optimization. Lead with the answer, back it with a statistic and a source, and structure it so an extractor can lift it cleanly.

## What actually moves GEO/AEO visibility

- **Answer-first structure** — put the direct answer in the first sentence under a question-shaped heading (`## What is X?`). Answer engines lift these directly.
- **Statistics, citations, quotations** — the Princeton paper's highest-impact additions; they make content look authoritative to an LLM synthesizer.
- **Schema markup** — `FAQPage`, `HowTo`, `Article` structured data helps both classic snippets and answer engines parse your content.
- **`llms.txt`** — the emerging standard: a plain-text file at your root that gives AI agents a curated, deep-understanding map of your site (the AI-era `robots.txt` + sitemap).
- **Comparison + listicle content** — "best X for Y" and "X vs Y" pages are disproportionately cited because they map to how buyers query LLMs.
- **Entity clarity** — be an unambiguous, well-described entity (consistent name, description, category) so the model resolves you correctly.

## The GTM-engineer angle: make it executable

This is where a GTM engineer beats a content marketer — **you can automate the audit and the fix.** The `onvoyage-ai/gtm-engineer-skills` repo (1.2k★, MIT) ships an executable Claude/Codex skill with **16 foundational AEO checks, 6 intelligence dimensions, and framework-specific fixes for Next.js and WordPress.** Run `audit-website-aeo`, then `improve-aeo-geo`, and publish the diff — that's both a growth play and [portfolio project #3](07-portfolio-projects.md).

> [!TIP]
> **Treat AEO/GEO like an eval loop, not a one-time audit.** Run the audit against your site *and* 3 competitor sites, publish the JSON diff, then re-run monthly to track whether your citation footprint in the target engines is rising. Answer engines drift; a scheduled audit is the drift monitor — the same discipline as [Stage 4's continuous eval](04-solution-design-and-demo-selling.md).

## 📚 Resources

- 📄 [GEO: Generative Engine Optimization (Aggarwal et al.)](https://arxiv.org/abs/2311.09735) — **paper.** The Princeton result: "GEO can boost visibility by up to 40%," with the ranked list of tactics. The primary source.
- 💻 [onvoyage-ai/gtm-engineer-skills](https://github.com/onvoyage-ai/gtm-engineer-skills) — **repo · 1.2k★ · MIT.** Executable AEO audit + improvement skills (16 checks, Next.js/WordPress fixes). The single best mineable asset for this stage.
- 📘 [HubSpot AEO Guide](https://www.hubspot.com/products/marketing/aeo-guide) — **guide.** The marketing-side AEO playbook: structuring content for answer engines.
- 📰 [LLM SEO: how to rank in ChatGPT & Perplexity](https://www.marketermilk.com/blog/llm-seo) — Marketer Milk. An 8-step, concrete ranking guide.
- 📰 [Answer Engine Optimization 2026](https://www.evergreen.media/en/guide/answer-engine-optimization/) — Evergreen Media. ChatGPT/Perplexity/Copilot visibility tactics.
- 📰 [Give your AI agents deep understanding with `llms.txt`](https://medium.com/google-cloud/give-your-ai-agents-deep-understanding-with-llms-txt-4f948590332b) — Google Cloud. The `llms.txt` standard, explained.
- 🌐 [generative-engines.com](https://generative-engines.com/) — a hub tracking GEO tactics, tools, and measurement.

---

**Next:** [6 · Tools & the stack in depth →](06-tools-and-stack.md) — the warehouse + reverse-ETL layer and how to choose per layer.
