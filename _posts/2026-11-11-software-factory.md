---
title: "Every Company Will Run a Software Factory. The Board Should Own One File in It."
tags:
   - AI
   - Agentic Coding
   - Governance
   - Technology Strategy
   - Software Engineering
   - Future of Work
toc: true
header:
   og_image: https://zerafachris.github.io/bio/assets/images/zero-cost-code-3-infographic.png
excerpt: "An open-source software factory builds a feature in an afternoon. The file that matters is the list of changes it may never merge alone: the company's risk appetite, written down, and the reason the build is no longer the slow part."
---

<figure>
	<a href="/bio/assets/images/zero-cost-code-3-infographic.png"><img src="/bio/assets/images/zero-cost-code-3-infographic.png"></a>
	<figcaption>The build used to hide the queue. Now the queue is all that's left.</figcaption>
</figure>

*Zero-Cost Code, part 3 of 7. The cost of writing software has gone to near zero. Everything around it just got more expensive. [Part 2](https://zerafachris.github.io/bio/one-engineer-plus-agents/) described the gate: one senior engineer deciding what's true. This part is what happens when you industrialise the gate, and why that turns speed into an executive problem.*

Here is a list of changes an AI agent may never merge on its own. The approver must hand the job to a human if the change:

- touches money, access or identity: payments, auth, permissions, database and storage security rules;
- changes deploy, CI or hosting config, or the build scripts it runs;
- migrates a schema, sends email, writes production data, or adds a dependency;
- rests on an assumption that is really a product or business decision, such as pricing or public copy.

It comes from an open-source software factory built on Anthropic's Claude Code and published on GitHub in October.[^1] Most people who find it will take it as a productivity trick. I think the list is a preview of how engineering organisations will be governed, and of where their speed will come from.

## What a factory is

The factory is small. One Claude Code skill acts as orchestrator. Seven subagents each own one step and write one file. A spec-writer turns a one-line request into a specification with acceptance criteria. A builder implements it on its own branch and writes a build report. Four reviewers (security, UX, UI, code) run in parallel, and each must open its file with `VERDICT: PASS` or `VERDICT: CHANGES`. If any asks for changes, the builder goes back in, twice at most. Then an approver reads everything, spot-checks a criterion itself, and writes `APPROVE` or `ESCALATE`. Approved jobs merge to main; the factory never pushes.

Dan Shapiro's five levels of AI coding put this at level 4: you act as the manager, writing specs while agents build.[^2] Level 5 he calls the dark factory, "a black box that turns specs into software".

The agents are generic by design; the README says they "carry nothing repo-specific". The organisation's judgment lives in one place, the escalation list. The repo ships two example jobs. One merged on its own. The other passed all four reviews and was still escalated, because it added one line to a prerender script, which counts as a deploy change. The approver's note to the human says what to check and which files to open. That is a better review request than most humans write.

Read the list again as an executive. It isn't an engineering checklist. It's a statement of risk appetite: the actions a company won't let a machine take without a named person agreeing. Most companies hold that appetite in people's heads and in whoever happens to review the pull request. A factory forces it into a file, and a file can be audited.

## The constraint moved

A factory changes one more thing, and it is the one boards will feel.

In February, Capgemini's Steve Jones argued that agentic delivery has "killed" the Agile Manifesto, because "agentic SDLCs are too fast for Agile."[^3] Sonya Siderova's reply is the one I'd frame on the wall: "Agile isn't dead. It's optimizing a constraint that moved." The constraint used to be how fast humans could build. It is now how fast humans decide what to build and confirm that it works.

Run the audit on your own last feature. Draw one bar per stage, from first signal to production: the signal (a competitor ships, a player complains, a metric drops); the decision to respond, with a named owner; the specification; the build; review and verification; legal, compliance and, in gaming, certification of anything that touches game outcomes; release sign-off.

In a regulated business today, the build is often the shortest bar. A typical shape I've seen across companies: a few days of build, weeks waiting for a decision and a spec, more weeks in approvals. The build used to hide the queue. A factory removes the build, and the queue is all that's left.

The pressure is coming from outside too. Open-source tools such as REA now let an agent reverse-engineer a feature from someone else's app, without its source, and build a version for yours.[^4] A competitor's new bonus mechanic can be a prototype by Monday. Most organisations still couldn't ship it by Christmas, and engineering won't be the reason.

## The list is the envelope

This is where the two ideas meet. The escalation list isn't only a safety control. It is the best instrument a company has for **decision latency**: the elapsed time from signal to a yes or no from a named owner.

The fastest organisations will decide in advance. Compliance blesses an envelope (parameter ranges, jurisdictions, payout bounds, data uses), and anything inside the envelope ships without a fresh committee. Anything outside escalates, fast, to a person who has reserved time to decide. AWS describes the same idea for agentic systems as zones of intent: specify the outcome, the intent and the guardrails, and let the agent work out the how.[^5] The factory's escalation list is that envelope written down, one line per risk.

So engineering can propose the list but shouldn't own it alone. Payments and wallets belong to finance. Access and identity belong to security. Player data and regulator reporting belong to compliance. Pricing and public copy belong to the commercial team. Each owner agrees which changes in their area a machine may merge, and the CTO keeps the list current and reports against it.

That turns a developer tool into a governance instrument. It gives the board something it has rarely had for software: a written, versioned answer to what the company lets machines do, and a lever on how fast it moves. The board, or its risk committee, should approve that file the way it approves any other statement of risk appetite.

## What the list looks like in a regulated business

In iGaming, finance or health the list grows fast. Anything touching game outcomes, wallet balances, bonus terms, KYC, responsible-gambling controls, player data or regulator reporting goes to a human. In my own world, every schema migration on a data platform would escalate under the default rules.

So a regulated factory will auto-merge the periphery and escalate the core. That's the right design. Its value isn't autonomy. Every change reaches a human with four completed reviews, a build report, a spot-checked acceptance criterion and a one-paragraph note on what to decide. The human gate from part 2 stays where it is, but the person at it spends their time on judgment, not on finding the obvious problems.

Four numbers then become worth tracking:

1. **Escalation rate**: the share of jobs that need a human. Too high and you've rebuilt the review queue with extra steps.
2. **Decision latency**: how long an escalated job waits for its owner. This is where the speed is.
3. **Rework rounds**: how often the builder needs a second or third attempt.
4. **Escape rate**: auto-merged changes that later cause an incident.

If the escape rate stays near zero, move items off the list deliberately, one at a time, with a record of why. That is how autonomy should grow: earned, measured and signed off.

## The dark end, and the bill

StrongDM's AI team runs at the far end. Their rules are short: "Code must not be written by humans" and "Code must not be reviewed by humans." They replace review with end-to-end scenarios held outside the codebase, like a holdout set.[^6] Their rule of thumb is that if you haven't spent "at least $1,000 on tokens today" per engineer, the factory has room to improve. Simon Willison works that out at about $20,000 a month per engineer, against his own $200 plan.

Two things follow for anyone running a budget. Factory economics depend on pricing you don't control; part 4 covers the gap between flat-rate and list-price costs. And a factory with no human review moves accountability somewhere uncomfortable. A Stanford Law School essay put it plainly: nobody reviewed the code that produced a given output, and the testing judges may share the builder's blind spots.[^7]

There is an IP point in the same place. In March the US Supreme Court declined to hear *Thaler v. Perlmutter*, leaving in place the rule that copyright needs human authorship.[^8] The record of which human decided what, which the escalation list produces as a side effect, is an IP asset as well as a governance one. Tools like REA also limit themselves to "software you own or are authorized to examine". I'm not a lawyer; ask one before anyone clones anything.

## Where I might be wrong

**Factories may stay toys.** Two example jobs on a marketing site prove the loop, not the economics. Most production systems are messier than a reading-time badge.

**Agent reviewers can agree with each other's mistakes.** Four reviewers from the same model family aren't four independent opinions. Stanford's point about shared blind spots applies here as much as to StrongDM.

**If everyone can build in a week, speed is worth nothing.** Fast-following becomes table stakes, and advantage moves to what can't be copied: distribution, data, licences, trust. Low decision latency keeps you in the game. It won't win it for you.

**Agile is fine, thank you.** Forrester's 2025 survey found 95% still call agile critically relevant.[^3] Fair. My argument is about where the constraint sits, not about the rituals.

## The question

If you ran a software factory tomorrow, who in your company would sign the list of things it may never do alone? And the last time a competitor shipped something you wanted, how many days passed before someone with authority said yes or no?

*Next in Zero-Cost Code, part 4: what a feature costs when a machine writes it, and the ledger I keep to answer that for a CFO.*

[^1]: [ZazenCodes, *Software Factory for Claude Code*, GitHub, October 2026](https://github.com/zazencodes/zazencodes-season-3/tree/main/src/software-factory-claude-code).
[^2]: [Simon Willison on Dan Shapiro, *The five levels: from spicy autocomplete to the dark factory*, January 2026](https://simonwillison.net/2026/Jan/28/the-five-levels/).
[^3]: [InfoQ, *AI and the Agile Manifesto debate*, February 2026 (Jones, Siderova, Forrester 2025)](https://www.infoq.com/news/2026/02/ai-agile-manifesto-debate).
[^4]: [REA (Reverse Engineer Anything)](https://github.com/morluto/rea).
[^5]: [AWS Prescriptive Guidance, *Evolving software delivery for agentic AI*](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-operationalizing-agentic-ai/software-delivery.html).
[^6]: [Simon Willison, *How StrongDM's AI team build serious software without even looking at the code*, February 2026](https://simonwillison.net/2026/feb/7/software-factory/).
[^7]: [Stanford Law School, *Built by Agents, Tested by Agents, Trusted by Whom?*, February 2026](https://law.stanford.edu/2026/02/08/built-by-agents-tested-by-agents-trusted-by-whom/).
[^8]: [Reed Smith, *Supreme Court denies certiorari in Thaler v. Perlmutter*, March 2026](https://www.reedsmith.com/our-insights/blogs/viewpoints/102mlpl/supreme-court-denies-certiorari-in-thaler-v-perlmutter-human-only-rule-for-ai/).
