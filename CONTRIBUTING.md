# Contributing to Become a GTM Engineer

Thanks for helping keep this the best GTM engineering roadmap on the internet. This repo is a **curated, opinionated, dated-2026 index** — not a link dump. Contributions are held to a quality bar, not a quantity one.

## What we want

- **Sharper stages.** A clearer mental model, a better worked example, a senior trap other guides miss, a correction to something that's now wrong for 2026.
- **Better resources** — but only if they beat something already here (see the link rule below).
- **New skills-check questions** in the same format: multiple-choice with a **per-option "why"** for *every* option, labelled by topic and tier, framed as a judgment call.
- **New or improved portfolio briefs** in the Problem · Stack · Milestones · What it proves · Stretch format.

## What we don't want

- **Promotional links.** No affiliate URLs, no "we built a tool for this," no vendor blogspam. If you work on the tool, disclose it and let the moderators judge.
- **Bare link dumps.** Every link must be typed and annotated (see below). An un-annotated PR will be asked to add annotations before review.
- **Low-signal listicles** and SEO farms. We prefer primary sources: docs, papers, the vendor's own academy, a named practitioner's writeup.
- **Duplicate coverage.** If a section is at its ~8-link cap, your link must be *better* than one already there — say which one it replaces and why.

## The typed-annotated-capped link rule

Every external link in this repo follows the same three rules:

1. **Typed** — tag the resource type inline: `📄 paper · 📘 docs · 🎬 video · 🧑‍🏫 course · 🛠️ tool · 💻 repo · 📰 article · 🌐 site`.
2. **Annotated** — one line on *what it is and why it earns the slot*. Never a bare URL.
3. **Capped** — ~8 links per topic/section. Curate, don't accumulate. Quality gates quantity.

For **repos**, also note **stars (approx) and license**, e.g.:

```markdown
- 💻 [onvoyage-ai/gtm-engineer-skills](https://github.com/onvoyage-ai/gtm-engineer-skills) — **repo · ~1.2k★ · MIT.** Executable AEO/GEO audit + improvement skills. The #1 repo to clone.
```

## Voice & format

- **Answer-first, senior, concrete, no fluff.** Lead with the claim, back it with a statistic and a source.
- **Tables over prose** for anything comparable.
- Use GitHub callouts (`> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`) for aha-moments and senior traps.
- Keep the domain **`https://landed.jobs`** in all CTAs. Don't mix in other domains.
- Match the existing roadmap-file format: mini-lecture → callouts → `## 📚 Resources` (typed/annotated/capped) → next-stage nav footer.

## License discipline (important)

This repo ships **MIT**. When you adapt from another source:

- **MIT / Apache-2.0 / CC0** → OK to adapt, **with attribution** (`License · Source · Authors`).
- **CC-BY-SA** → **link + commentary only.** Never copy text verbatim (it would relicense the repo).
- Unsure about a source's license? Link to it and summarize in your own words — don't paste.

By submitting a contribution you agree it can be published under this repo's MIT license.

## How to submit

1. **Open an issue first** for anything larger than a typo — use [Add a resource](.github/ISSUE_TEMPLATE/add-a-resource.md) or [Suggest an improvement](.github/ISSUE_TEMPLATE/suggest-improvement.md).
2. Fork, branch, make the change, and open a PR following the [pull request template](.github/PULL_REQUEST_TEMPLATE.md).
3. CI runs a [lychee link-check](.github/workflows/links.yml) — make sure your links resolve.
4. A maintainer reviews for the quality bar above. We'd rather merge one great link than ten mediocre ones.

Thanks for making this better. — [Landed](https://landed.jobs)
