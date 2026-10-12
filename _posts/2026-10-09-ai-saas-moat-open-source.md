---
title: "AI Isn't Killing SaaS. It's Killing the Moat."
tags:
   - AI
   - SaaS
   - Open Source
   - Build vs Buy
   - Platform
   - Technology Strategy
   - Future of Work
toc: true
excerpt: "The moat was never the software. It was the cost of owning it, and AI has compressed exactly that. What it means for every line on your software bill."
header:
   og_image: https://i.ibb.co/hFBvXFm0/saas-moat-hero.png
---

<figure>
	<a href="https://i.ibb.co/hFBvXFm0/saas-moat-hero.png"><img src="https://i.ibb.co/hFBvXFm0/saas-moat-hero.png"></a>
	<figcaption>The castle is still standing. The water that kept everyone out is draining.</figcaption>
</figure>

## Seven Apps, No Subscription

This week ArtCraft released seven open-source creative applications written in Rust: clean-room answers to Photoshop, Illustrator, Premiere, Lightroom, Acrobat, After Effects and InDesign.[^1] MIT and Apache licensed, no telemetry, six of them runnable in a browser.

One developer, Brandon Thomas, with Claude Opus 5.5 as his coding assistant.[^2] The image editor round-tripped 134 of 135 real-world PSD files byte for byte. Most of it is alpha, and it was on Linus Tech Tips within days.[^3]

So take the hot take seriously for a moment, because this is its strongest available case: one person and a model produced credible alternatives to seven Adobe applications.

It still will not kill Adobe. My narrower claim: AI is not killing SaaS. It is killing what made SaaS defensible. If you sign software contracts, only the second is your problem.

## SaaS Was Never Selling You Features

Every category you pay for has had a credible free alternative for a decade. Metabase against Looker. Airbyte against Fivetran. GIMP against Photoshop. You bought the paid one anyway.

Not for the feature gap. You bought someone else's on-call rota, an upgrade path that doesn't break on a Tuesday, a SOC 2 report you can hand a regulator, one budget line instead of three headcount, and somebody outside the building to blame.

The moat was never the software. It was the cost of owning it. GIMP was free and cost a designer a week. Self-hosted Metabase was free and cost an engineer permanently. Every tooling decision I have signed off has turned on that number rather than on a feature matrix.

## AI Didn't Make Software Cheap to Write. It Made It Cheap to Own.

Version one was never the expensive part. Two engineers, two weeks. Keeping it alive for three years was expensive.

What has compressed is the long tail that made ownership irrational:

*   Integration glue nobody volunteered to write
*   Migrations, upgrades, dependency churn, security patching
*   Documentation, so the tool outlives its author
*   Reading unfamiliar code at 2am in year three

Each was a recurring, uncapped, unbudgeted tax, and none of it had a line in any budget I have seen, which is why it stayed invisible until something broke. SaaS vendors priced it, absorbed it, and sold it back at a markup you were right to pay.

So the question was never whether you could build it. It is whether you can still afford to own it in year three, and that answer has changed.

<figure>
	<a href="https://i.ibb.co/rf2x6gRR/saas-moat-cost.png"><img src="https://i.ibb.co/rf2x6gRR/saas-moat-cost.png"></a>
	<figcaption>Illustrative, not measured. Version one was always cheap; the slope after it was what you paid SaaS to avoid.</figcaption>
</figure>

## What Dies, What Survives

Your portfolio splits into three tiers.

<figure>
	<a href="https://i.ibb.co/0VsbXcnD/saas-moat-tiers.png"><img src="https://i.ibb.co/0VsbXcnD/saas-moat-tiers.png"></a>
	<figcaption>Replaced, repriced, or strengthened. The tier decides it, not the invoice.</figcaption>
</figure>

**The thin wrapper.** Form builders, dashboard layers, status pages, scheduling, light CRM, internal admin panels. No proprietary data, no network effect, no regulatory burden. Paying €15 per user per month for something an engineer now assembles in an afternoon does not survive two renewal cycles.

**The workflow layer.** Ticketing, onboarding, procurement, incident management. The value is the encoded process and the switching cost is organisational, so these survive. They get repriced instead, because per-seat billing breaks the moment an agent does the work of six seats.

**The system of record.** The ledger, the wallet, the payment rails, the regulated stores. Their value is being authoritative, audited, and liability-bearing. AI may strengthen them. Every new agent needs somewhere trustworthy to read from, and nobody wants to have self-hosted the thing a regulator later asks about.

## From the Inside

When architecting an internal AI ecosystem for a 200-plus developer organisation, every vendor evaluation collapsed into one comparison: licence cost against the fully loaded cost of owning the equivalent. Buying won, and it won without much argument.

It no longer wins by default. The platform I run now is ClickHouse, Kafka, and Metabase: mostly open source, with a commercial operator where that matters. Pay where somebody else's uptime guarantee is worth more than your engineers' time, own it where it isn't. That line has moved faster than most procurement cycles can track.

Take that with the caveat it earns. The cost of owning software has fallen. The discipline it demands has not, and nothing in a model supplies it.

So the question I ask before owning anything is no longer whether we can build it. It is who, by name, owns its upgrade in year three.

## If You Are the One Signing the Contracts

Retool's 2026 build-vs-buy report found 35% of teams had already replaced a SaaS tool with a custom build.[^4] Hold it loosely: 817 of Retool's own customers, surveyed by a company that sells build tooling. But the categories they named are the thin wrapper tier, item for item: internal admin tools, BI, CRM and form builders, project management.

Three things for your agenda rather than your feed:

1.  **Audit by defensibility, not invoice size.** Your biggest contracts are systems of record and they are fine. Your exposure is the long tail of €2k–€20k tools nobody owns and everybody renews.
2.  **Price the seat risk before your vendors do.** Every per-seat contract bets that headcount tracks workload. You should not meet the replacement pricing model for the first time in a renewal quote.
3.  **Say out loud that cost moves rather than disappears.** Ownership converts a predictable opex line into engineering capacity and risk you now carry. In a regulated business that is sometimes a bad trade at any licence price. I tie AI strategy to EBITDA for this reason: a saving that reappears as unbudgeted engineering time is not a saving, it is a transfer.

## Where I Might Be Wrong

Three objections I cannot dismiss.

**Distribution beats product.** Every incumbent is shipping AI into software your staff already has open and already has a contract for. "Good enough and already installed" has won for forty years.

**AI makes incumbents stickier.** A vendor's agent that reads across your CRM, tickets, and mail because it already sits in all three has a context advantage no self-hosted tool replicates.

**The maintenance claim is unproven.** Two years of evidence, much of it from people paid to say so. A production analytics database I was accountable for in a previous role sat more than six years without a major upgrade. Nobody decided that. It was never the quarter's priority, and every quarter it sat made the upgrade more expensive and more frightening. AI shortens the upgrade. It does not supply the will to run it.

If I am wrong it is on the third, and the third takes the whole argument with it.

## The Question for Your Next Renewal

Seven alpha-quality Rust apps will not displace Adobe. The pattern is the point: releases like it land weekly now, adopting one costs less every quarter, and the moat around your software portfolio was built out of maintenance work rather than features.

So, for every line on your software bill: what are you paying to avoid, and is it still expensive?

I'd rather hear the disagreements.

[^1]: ArtCraft's seven open-source creative apps, [covered by Techaeris](https://techaeris.com/2026/10/07/artcraft-launches-7-open-source-creative/), 7 October 2026.
[^2]: Brandon Thomas built the suite with Claude Opus 5.5 as his coding assistant, as a clean-room reimplementation: [Notebookcheck](https://www.notebookcheck.net/Photoshop-Premiere-more-Experienced-Rust-developer-recreates-Adobe-suite-with-AI-assistance-as-open-source.1419230.0.html), 8 October 2026.
[^3]: [Linus Tech Tips coverage](https://youtu.be/fr0WIIZxvx0).
[^4]: [Retool 2026 Build vs. Buy Report](https://retool.com/blog/ai-build-vs-buy-report-2026) — 817 respondents, surveyed late 2025, published 17 February 2026.
