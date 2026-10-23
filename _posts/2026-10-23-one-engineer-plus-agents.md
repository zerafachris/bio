---
title: "One Senior Engineer Plus Agents Beats a Team of Four. AI Is a Rounding Error Against One Salary."
tags:
   - AI
   - Data Engineering
   - Agentic Coding
   - Data Platform
   - Governance
   - Technology Strategy
   - Future of Work
toc: true
header:
   og_image: https://zerafachris.github.io/bio/assets/images/zero-cost-code-2-infographic.png
excerpt: "One senior engineer and a set of agents built what the industry staffs with a team of four to six. The AI bill was $200 a month per seat. The thing that made it work was the gate."
---

<figure>
	<a href="/bio/assets/images/zero-cost-code-2-infographic.png"><img src="/bio/assets/images/zero-cost-code-2-infographic.png"></a>
	<figcaption>Bad code fails loudly. Bad data completes on schedule.</figcaption>
</figure>

*Zero-Cost Code, part 2 of 8. The cost of writing software has gone to near zero. Everything around it just got more expensive. [Part 1](https://zerafachris.github.io/bio/ai-saas-moat-open-source/) covered ownership. This part covers judgment.*

One senior data engineer plus AI agents can build what used to take a platform team.

Six months ago I would have filed that sentence under vendor marketing. Then I spent 90 days testing it on a live build: the data platform for a multi-brand, crypto-first iGaming group. Real-money transactions across more than 15 chains. Regulated reporting on the roadmap. A treasury the platform is being built to watch in near real time.

## The Playbook Says a Team

The industry estimate for this scope is 6 to 12 engineers over 8 to 14 months, at a loaded cost past $1M a year.[^1] Benchmarks for a do-it-yourself CDC streaming layer alone assume 1.5 to 2 permanent engineers.[^2] I'll take the low end of that range as the comparison: a team of four to six.

I ran the first 90 days as one senior engineer paired with agents across the whole delivery lifecycle, with governance encoded in CI instead of headcount. I had one advantage a senior engineer on a team rarely has: I own the architecture decisions, so there was no coordination tax to pay. Part of the saving is that, not the agents.

## Context Before Code

The most valuable thing I built in those 90 days wasn't a pipeline.

It was context: an AGENTS.md in every repository, two dozen agent skills, a set of specialist agent definitions and a handful of house rules. Between them they encode conventions, ClickHouse patterns, money-precision rules and the domain language of casino, rewards and on-chain treasury. The agents read them before they generate a line of SQL.

The reason sits in one benchmark. When Spider 2.0 launched, the best model of the day went from 86.6% on the classic text-to-SQL benchmark to 10.1% on real enterprise warehouses with thousand-column schemas and tribal naming.[^3] Scores have risen since. The gap hasn't closed. The distance between those two numbers is your company's context. The model was never the asset.

## The Ledger

With that context in place, agents wrote most of the code. The 90-day ledger is the build; the production cutover at month five is the proof. Ninety days in:

1.  8 repositories, CI-gated from week six, promoted to production at month five
2.  160+ versioned schema migrations; every one since the gates landed has cleared them
3.  CDC streaming from operational databases through Kafka and Spark into ClickHouse
4.  20+ dimensional models and three fact chains: gameplay, rewards and KPIs
5.  An infrastructure bill of roughly $6K a month, and an AI bill of $200 a month per engineer seat: one flat-rate coding-agent subscription

## Bad Data Completes on Schedule

Software engineers underestimate one thing about data. Bad code fails loudly. Bad data completes on schedule.

Monte Carlo reviewed 1,000 pipeline incidents and found that AI has nearly killed the syntax error.[^4] What remains is worse: silent schema drift, fan-out joins that double revenue, merges that "completed as expected" and were wrong. In dbt Labs' 2026 survey, 71% of data teams named incorrect outputs reaching stakeholders as a top concern.[^5]

The wider industry pays for this in the review queue. Under heavy AI adoption, Faros AI measured PR review time up 441% and 31% more pull requests merging with no review at all.[^6] DORA's 2025 report shows the same thing from the other side: throughput up, delivery stability down.[^7] AI moved the bottleneck from writing to verification.

## The Gate

So green checks alone merge nothing here.

Every migration clears deterministic gates first: an idempotency lint, a destructive-DDL guard, schema compatibility enforced at the registry, contract tests against those schemas, and every migration applied to a throwaway ClickHouse before it touches a real one. Those gates arrived in that order over four months; the destructive-DDL guard was the last, added days before cutover. Then comes the human gate. Before merge, I reconcile the output to source, state the grain of every join, and explain the model with the agent switched off.

If I can't do all three, the change doesn't ship. That gate is the entire system. Everything upstream of it is volume.

## What It Does to the Cost Base

A CFO reads this differently from an engineer, and the CFO's reading matters more.

In the old model, a platform function's cost grows with scope. Each new source, product or tenant pulls in headcount, and headcount brings management layers, hiring cycles and attrition risk. In this model, cost grows with the number of verification surfaces: the places where someone has to decide that a number is true. Infrastructure scales with usage. The AI bill doesn't, yet: it's a flat $200-a-month subscription per engineer, a rounding error against one loaded salary and the cheapest line in the system. At list token prices the same work would cost many times that, which is a pricing risk to forecast, not a reason to doubt the economics (part 5 covers it).

The expensive line is the person at the gate. Senior data engineers now take 8 to 16 weeks to hire; streaming specialists, up to 20.[^8] AI didn't lower the demand for that person. One of them now carries what a team used to, and nothing in the market data says they got cheaper. Headcount still grows, but with the number of gates rather than the number of pipelines: the second engineer joined for the second gate, not for throughput.

That changes the planning question. You stop asking how many engineers a roadmap needs and start asking how many gates it creates, and who is qualified to stand at each one.

## Where I Might Be Wrong

Four objections I take seriously.

**The productivity evidence is mixed.** METR's randomised trial found experienced open-source developers 19% slower with early-2025 tools.[^9] I think the answer is harness quality: context, skills and gates. That is an argument, not a proof, and my build is one case.

**Agentic projects fail.** Gartner expects more than 40% of agentic AI projects to be cancelled by the end of 2027.[^10] Most of those failures, I suspect, skipped the context work.

**One gate is one point of failure.** If the system depends on one person's judgement, the company has swapped a staffing risk for a key-person risk. The mitigation is to keep encoding the gate (skills, lints, contract tests, written runbooks) so the next engineer inherits it on day one rather than learning it over a year. That work never finishes.

**The gate catches wrong numbers, not silence.** It works at merge. It does not catch a feed that stops. In September a production source went quiet for over a week and an audit found it, not an alarm. Pre-merge reconciliation is necessary and insufficient; the next gate is continuous reconciliation and freshness alerting in production, which is what I'm building now.

## The Question

Agents handle volume. The senior engineer decides what's true. Put that person at the gate and one plus agents beats a team of four.

So for your own platform: who is your gate, what does it cost you to lose them, and how much of their judgement lives anywhere other than their head?

*Next in Zero-Cost Code, part 3: what happens when you turn this gate into a pipeline, and the one file in a software factory the board should own.*

[^1]: [Dataforest, Data Platform Development Cost 2026](https://dataforest.ai/blog/data-platform-development-cost).
[^2]: [Streamkap, DIY CDC infrastructure costs](https://streamkap.com/resources-and-guides/diy-cdc-infrastructure-costs) (vendor content).
[^3]: [Spider 2.0 enterprise text-to-SQL benchmark](https://spider2-sql.github.io/): GPT-4o 86.6% → 10.1%. [Paper](https://arxiv.org/abs/2411.07763).
[^4]: Lior Gavish (Monte Carlo), [DZone](https://dzone.com/articles/ai-sql-quality-issues), May 2026.
[^5]: [dbt Labs, State of Analytics Engineering 2026](https://www.prnewswire.com/news-releases/new-dbt-labs-report-finds-ai-driven-acceleration-is-outpacing-trust-and-governance-302741246.html).
[^6]: [Faros AI, AI Code Quality: The Hidden Cost Senior Engineers Pay](https://www.faros.ai/blog/ai-code-quality-senior-engineer-review-burden), May 2026, drawing on the *AI Engineering Report 2026: The Acceleration Whiplash*. Figures compare high- with low-adoption teams; review time is the median.
[^7]: [DORA, State of AI-assisted Software Development 2025](https://dora.dev/dora-report-2025/).
[^8]: [KORE1, time-to-fill benchmarks for data engineers](https://www.kore1.com/time-to-fill-data-engineer/).
[^9]: [METR, early-2025 AI and experienced open-source developer productivity](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/).
[^10]: [Gartner, June 2025](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027).
