> **Paths into GTM engineering** · how the role overlaps with its neighbours, and for each starting point: what carries over, the gap to close, a first project and a real person who made the move.
> [Back to the roadmap](README.md) · Related: [Interviews and take-homes](interviews.md) · [Skills check](skills-check.md)

# 🧗 Paths into GTM engineering

**Most GTM engineers did not start as engineers.** They came from sales, marketing, operations and data, then learned to build. Your starting point decides which half of the job you already have: the commercial half (who buys, why, where the funnel leaks) or the building half (code, data, systems that do not break). The work is to prove the half you are missing with one project someone can open and run.

Last checked: 17 Nov 2026

**Evidence labels used on this page:** **official** (a company writing about its own roles or team), **first-person** (the person's own post), **interview** (a podcast or newsletter summary of a conversation with the person), **second-hand** (an article, study or aggregator).

## Where the role overlaps

The title is not standard. The same words cover very different jobs, so read what the posting owns and how it is measured.

| Role | What it mainly owns | How it differs from GTM engineering | Source |
|---|---|---|---|
| **GTM engineer** | Systems that find, convert and grow customers: enrichment, scoring, routing, signals, agents | Builds and owns the system, and is measured on revenue outcomes. Clay's internal team was measured on pipeline created, stage-one-to-stage-two conversion and quota capacity per seller in Q3 2026. | Official: [Clay newsletter, 10 Nov 2026](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer) |
| **RevOps** | CRM data, territories, lifecycle and handoff rules, reporting | The closest neighbour. Clay says RevOps and GTM engineering are converging and it plans to merge them further; its GTM engineers sit in GTM Operations. | Official: [Clay newsletter, 10 Nov 2026](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer) |
| **Sales engineer** | Technical side of a specific sale: discovery, demos, solution proposals | Helps one customer buy, rather than building the internal revenue engine. Salesforce describes the role as a bridge between the customer's technical people and the sales team. | Official definition from a vendor: [Salesforce](https://www.salesforce.com/blog/sales/what-is-a-sales-engineer/) |
| **Solutions engineer** | Customer requirements, solution design, technical fit | Overlaps heavily with sales engineering; titles alone do not separate them. Clay lists solutions engineering as one of the backgrounds it pairs with RevOps when hiring GTM engineers. | Official: [Clay newsletter, 10 Nov 2026](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer) |
| **Growth engineer** | Product and website experiments: signup, pricing page, onboarding | Changes the product funnel more than the sales system. PostHog's examples include a pricing call-to-action change that lifted clickthroughs 27%. | Official (2023): [PostHog](https://posthog.com/blog/what-is-a-growth-engineer) |

Some GTM engineer postings bridge growth and RevOps. AgentMail's posting, for example, asks one person to own funnel instrumentation, enrichment, lookalike outbound, PLG experiments and the API glue between PostHog, the CRM and outbound tools ([AgentMail posting](https://jobs.ashbyhq.com/AgentMail/0f25ff04-0250-4c8c-b9a6-00b164f1f19a), official, live on 17 Nov 2026).

> [!TIP]
> **Ask one question of every posting:** am I building the company's own GTM system, helping customers implement the product, or changing the product's growth funnel? The answer tells you more than the title. [Stage 0](roadmap/00-what-is-a-gtm-engineer.md) covers the builder, conductor and translator split in more depth, and [Stage 4](roadmap/04-solution-design-and-demo-selling.md) covers the customer-facing side.

## Where GTM engineers actually come from

Kenso, a sales data company, looked at 1,028 people who have held a GTM engineer title in six English-speaking countries, using its own profile data up to April 2026 ([Kenso methodology PDF](https://ken.so/research/rise-of-the-gtm-engineer.pdf), second-hand vendor study). For the 999 with an earlier job, the role held just before was:

| Previous role family | Share |
|---|---|
| GTM sales (SDR/BDR, AE, account management, CS, presales) | 19.8% |
| Marketing (growth, demand gen and other) | 14.2% |
| Engineering, data and product | 11.0% |
| Founders, consultants and agencies | 9.9% |
| GTM operations (RevOps, sales ops, marketing ops, CRM) | 9.6% |
| Other GTM roles | 6.1% |
| Other | 29.3% |

Software and data engineering alone was 7.7%. These are shares of one sample built from public profiles, not your odds of getting hired from each background.

Clay says the same thing about its own team. Its GTM engineers have come from product design, RevOps and sales; one, Spencer, started as a product designer and learned SQL on the job with Claude ([Clay blog, 21 Apr 2026](https://www.clay.com/blog/gtm-engineering), official). For its functional GTM engineer roles, Clay wants a background that pairs at least two of: a commercial role, revenue or sales or marketing operations, solutions engineering, software engineering, product management, data science or GTM analytics ([Clay newsletter, 10 Nov 2026](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer), official).

## Path by path

### From SDR or AE

| | |
|---|---|
| **What carries over** | You know targeting, follow-up, objections and what wastes a rep's day. You know which signals actually lead to meetings. |
| **Gap to close** | Building things that run without you: data in a CRM, enrichment, APIs, basic SQL or Python, and handling bad data. |
| **First project** | A signal-to-meeting system: one buying signal, enrichment, a qualification step you can audit, a drafted email for human approval, and the outcome written back to the CRM. Start from [Waterfall Enrichment Pipeline](roadmap/07-portfolio-projects.md#1--waterfall-enrichment-pipeline) and [Claygent Research Agent](roadmap/07-portfolio-projects.md#6--claygent-research-agent). |
| **Read first** | [The GTM stack](roadmap/01-the-gtm-stack.md), [AI automation for GTM](roadmap/02-ai-automation-for-gtm.md) |

**Real example: Benyamin Holley** ([LinkedIn](https://www.linkedin.com/in/benyaminholley/)). Holley sold motorcycles, became an SDR at PandaDoc, then moved into growth and GTM engineering: Head of Growth at Cyft, then GTM engineer at AirOps, where he helped run cold email, built lead magnets and did CRM enrichment. He now leads GTM at Apero Advisors, a GTM engineering firm. In the interview he describes building guardrails before letting an AI agent touch the CRM, including a rollback script and keeping the write-access key separate from the read-only one ([The GTM Engineer podcast, 24 Sep 2026](https://thegtmengineer.substack.com/p/full-stack-gtm-engineering-with-benyamin), interview). He also stresses earning the SDRs' trust by first building what they asked for, which is where a former SDR has an edge.

### From RevOps or sales ops

| | |
|---|---|
| **What carries over** | The data model, lifecycle stages, routing rules, territories and the politics of changing them. This is the background Clay leans on most. |
| **Gap to close** | Moving from configuring tools to building systems: code or a coding agent, APIs and webhooks, tests, monitoring, and owning a revenue number rather than tickets. |
| **First project** | Take a CRM process you know and rebuild it as a monitored service with tests and an exception queue. [Reverse-ETL Lead Routing](roadmap/07-portfolio-projects.md#4--reverse-etl-lead-routing) or [n8n Inbound-to-CRM Flow](roadmap/07-portfolio-projects.md#5--n8n-inbound-to-crm-flow). |
| **Read first** | [The GTM stack](roadmap/01-the-gtm-stack.md), [Tools and stack](roadmap/06-tools-and-stack.md) |

**Real example: Greig Fields at Clay.** Clay describes Fields as a career Salesforce admin with about ten years of Apex flows and integrations, skills it says carried straight over to building Clay CLI flows. He now leads Clay's systems and infrastructure GTM engineering work, a track Clay frames as the next step for the Salesforce admin ([Clay newsletter, 10 Nov 2026](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer), official). The same post describes Sydney Bedient, who came from CX with experience building CRM applications and now works as RevOps plus GTM engineer for Clay's CX team.

### From marketing ops

| | |
|---|---|
| **What carries over** | Lifecycle stages, lead scoring, attribution, campaign tooling, and the handoff from marketing to sales. |
| **Gap to close** | Data work beyond the marketing automation platform: joins across CRM and product data, enrichment, APIs, and proving a change moved pipeline rather than clicks. |
| **First project** | Lead scoring plus routing with a feedback loop: score inbound leads, route them to SDRs with an SLA, and feed back which leads were worth working. Clay's Marketing GTM Engineer posting describes this exact handoff ([posting](https://jobs.ashbyhq.com/claylabs/9f8067d1-61cf-42cd-aad7-0ac54de8b345), official). For a growth angle, add [AEO/GEO Audit](roadmap/07-portfolio-projects.md#3--aeogeo-audit). |
| **Read first** | [AI automation for GTM](roadmap/02-ai-automation-for-gtm.md), [AEO / GEO / SEO for growth](roadmap/05-aeo-geo-seo-for-growth.md) |

**Real example: Petra Hajal** ([LinkedIn](https://www.linkedin.com/in/petra-hajal/)). Hajal started in digital marketing and growth, moved into demand generation, did partner operations at Superside, then marketing and GTM operations at Oyster. There she started using Clay to improve outbound, became a power user and joined Clay's expert program early. Companies asked her to implement Clay for them, so she went freelance and in 2024 co-founded RevenueHoop, a RevOps and GTM engineering agency. She argues experienced RevOps operators are well placed to build with AI, because they already orchestrate systems and do QA ([The GTM Engineer podcast, 6 Nov 2026](https://thegtmengineer.substack.com/p/the-modern-revops-gtme-skillset-with-6dd), interview).

### From software engineering

| | |
|---|---|
| **What carries over** | Code, APIs, data pipelines, testing, deploys, and the habit of designing for failure. |
| **Gap to close** | Commercial judgment: how a funnel works, what sellers need, which problem is worth solving. Leading with the revenue problem, not the architecture. |
| **First project** | An internal tool that sellers actually use, such as an account review that pulls context from calls, tickets and the CRM and proposes CRM updates for a human to approve. Show adoption and the decisions it changed. Pair [AI Personalisation Demo](roadmap/07-portfolio-projects.md#2--ai-personalisation-demo) with the CRM write-back in [Claygent Research Agent](roadmap/07-portfolio-projects.md#6--claygent-research-agent). |
| **Read first** | [Customer-facing AI prototypes](roadmap/03-customer-facing-ai-prototypes.md), [Solution design and demo selling](roadmap/04-solution-design-and-demo-selling.md) |

**Real example: Chris Prinz** ([LinkedIn](https://www.linkedin.com/in/chris-prinz/)). Prinz started as an IoT software engineer at Accenture, moved into product management at Plato, then spent six years at Pave as its first hire, building its compensation benchmarking product and later its product analytics, growth and AI work. He joined Modal in January 2026 as a GTM engineer, responsible for the data systems and workflows that take a lead from awareness to customer. He centralised enrichment in Snowflake, built an account score from custom company fields, and runs an internal MCP server that gives every rep's agent shared skills, such as a weekly account review that proposes CRM updates ([The GTM Engineer podcast, 4 Sep 2026](https://thegtmengineer.substack.com/p/a-unique-gtm-engineering-system-build), interview). Note the route: engineering, then product and analytics, then GTM. It was not a direct title jump.

### From data analysis or data science

| | |
|---|---|
| **What carries over** | SQL, modelling, warehouse work, and measuring whether something worked. |
| **Gap to close** | Turning analysis into action: a score that routes a lead, an alert a rep sees, a workflow that runs daily. Plus enough sales context to know which decision the model should change. |
| **First project** | Take a warehouse model and make it live: an account or lead score that drives routing or alerts, with a check on whether the decisions it drives are better. [Reverse-ETL Lead Routing](roadmap/07-portfolio-projects.md#4--reverse-etl-lead-routing) is the closest brief. |
| **Read first** | [The GTM stack](roadmap/01-the-gtm-stack.md), [Tools and stack](roadmap/06-tools-and-stack.md) |

**Real example: Mark Freeman** ([his post](https://scalingdataops.substack.com/p/approaching-go-to-market-as-a-data), first-person, 12 Sep 2023). Freeman writes that his data science roles taught him technical skill alone did not drive impact; domain knowledge combined with technology did. He joined Gable.ai as its first employee and led go-to-market as GTM engineering, using his and his co-founder's audience and engagement data to work out who to engage and when. This is a 2023 account of one move, not a statement about his current role.

## Other routes

- **Founders, consultants and agencies** are about one in ten in Kenso's sample (9.9%). Clay says former founders do well with it, because they combine marketing, sales, systems and technical skills ([Clay newsletter](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer), official).
- **Product design and other non-technical roles** are possible. Clay's Spencer example shows it, but specific postings still ask for code and production ownership. AgentMail, for example, wants real Python, TypeScript or SQL ([AgentMail posting](https://jobs.ashbyhq.com/AgentMail/0f25ff04-0250-4c8c-b9a6-00b164f1f19a), official).

> [!NOTE]
> **Every path needs the missing half shown, not claimed.** Sellers and operators need a build that runs and survives bad data. Engineers and analysts need a build tied to a revenue problem someone actually has. One finished project with a clear story beats several unfinished ones. See [Portfolio projects](roadmap/07-portfolio-projects.md), then prepare the walkthrough with [Interviews and take-homes](interviews.md).

## 📚 Resources

- 📘 [How to Hire a Go-to-Market Engineer for the Agentic GTM Era](https://thegtme.com/p/how-to-hire-a-go-to-market-engineer) · **official** (The GTM Engineer by Clay, 10 Nov 2026). Backgrounds Clay hires from, its two GTM engineer archetypes and real team members' routes in.
- 📄 [Who are GTM engineers, and where do they come from?](https://ken.so/research/rise-of-the-gtm-engineer.pdf) · **second-hand vendor study** (Kenso, data to April 2026). Previous-role shares for 999 GTM engineers, with methods and limits.
- 🎬 [Full-Stack GTM Engineering with Benyamin Holley](https://thegtmengineer.substack.com/p/full-stack-gtm-engineering-with-benyamin) · **interview** (24 Sep 2026). The SDR-to-GTM-engineer route and CRM guardrails for agents.
- 🎬 [The Modern RevOps and GTME Skillset with Petra Hajal](https://thegtmengineer.substack.com/p/the-modern-revops-gtme-skillset-with-6dd) · **interview** (6 Nov 2026). Marketing and GTM ops into a GTM engineering agency.
- 🎬 [A GTM Engineering System Build with Chris Prinz](https://thegtmengineer.substack.com/p/a-unique-gtm-engineering-system-build) · **interview** (4 Sep 2026). Software and product into GTM engineering at Modal.
- 📰 [Approaching Go-to-Market as a Data Engineer](https://scalingdataops.substack.com/p/approaching-go-to-market-as-a-data) · **first-person** (Mark Freeman, 2023). A data scientist's move into GTM engineering.
- 📰 [What is a growth engineer?](https://posthog.com/blog/what-is-a-growth-engineer) · **official** (PostHog, 2023). Useful for telling growth engineering apart from GTM engineering.

---

**Next:** [Interviews and take-homes →](interviews.md) · what companies ask and how to hand in a take-home.
