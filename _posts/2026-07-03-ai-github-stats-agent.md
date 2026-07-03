---
title: "The Two-Prompt Profile: Delegating a Dev Chore to an Agent"
tags:
   - AI
   - Claude Code
   - AI-Assisted Coding
   - Developer Tools
   - GitHub
   - Developer Experience
toc: true
---

<figure>
	<a href=""><img src="https://streak-stats.demolab.com/?user=zerafachris&theme=github-dark&hide_border=true"></a>
	<figcaption>The end result — self-hosted, GitHub-dark, and counting work the public tools never see.</figcaption>
</figure>

## The Most Boring Task I Could Find

Every so often I like to test a thesis on something trivial. I have argued here more than once that the centre of gravity in software work is shifting from *authoring* code to *delegating and reviewing* it. That is an easy thing to assert about grand, greenfield systems. It is more honest to test it on a chore — the kind of fiddly, low-stakes job that is too dull to enjoy and too fussy to finish quickly.

So here is the chore. My GitHub profile was a wall of text. I wanted the little dynamic cards you see on the profiles of people who clearly enjoy this more than I do: a stats summary, a language breakdown, a contribution streak. I had seen a profile I liked[^1] and wanted something similar. What I did not want was to spend an evening reading the documentation for half a dozen image-generating micro-services to get it.

So I did not. I described the outcome to a coding agent — Claude Code[^2] — and reviewed what came back. Twice, really: two prompts of intent, and a series of small approvals in between.

## Prompt One: "Make My Profile Show My Work"

The first request was deliberately vague, the way a real request is: *look at this profile I like, find the equivalent widgets, and add them to mine so they showcase my contributions.*

What I did not do was any of the following, all of which the agent did instead. It read the reference profile and enumerated the exact services behind each badge. It wrote the embed markup. And — the part I would certainly have skipped — it actually *tested* every generated URL rather than trusting it, curling each endpoint to confirm it returned a real image.

That test caught the first snag immediately. The most popular stats service, the one behind a good half of the profiles on GitHub, was returning `503 — DEPLOYMENT_PAUSED`. The single most-used free instance had been throttled into dormancy. Left to my own devices I would have pasted the URL, seen a broken image on my profile a day later, and had no idea why. The agent saw it in seconds, found a maintained fork that was actually up, and re-pointed the cards at it.

Snag one, cleared before it ever reached my profile.

## Prompt Two: "Now Make It Count the Work Nobody Can See"

The public tools carry an honest limitation: they can only see public repositories. As someone whose day job lives almost entirely in private ones, the cards were quietly underselling me by an order of magnitude. The fix is to self-host the stats generator with a token that can read your private contributions.

This is exactly the sort of task that *sounds* like five minutes and turns into an afternoon of yak-shaving. It did not — and not because it was frictionless, but because the friction was handled.

The agent forked the generator to my account, and I deployed it to Vercel. The first thing my shiny new instance did was refuse to load: every request `302`-redirected to a Vercel login page. This is Vercel's Deployment Protection — sensible for a private app, fatal for a public image that GitHub's servers need to fetch anonymously. The agent diagnosed it from the redirect target alone, told me precisely which toggle to flip, and confirmed the fix the moment I did.

Then the payoff. With a personal access token wired in to read private repositories, the same card went from **661** commits to **2,572**; from **18** pull requests to **347**. Years of private work, suddenly visible. That gap — between what the public internet can measure about your output and what you have actually done — is the whole argument for self-hosting, rendered as a single number.

<figure>
	<a href=""><img src="https://github-readme-stats-fast-zerafachris.vercel.app/api/top-langs/?username=zerafachris&layout=compact&langs_count=8&theme=github_dark"></a>
	<figcaption>The language breakdown, served from my own Vercel instance rather than a shared one.</figcaption>
</figure>

## My Job Was the Pull Request, Not the Markup

Here is what I want to draw attention to, because it is the whole point.

At no stage did I write an image URL, read a service's README, or debug a redirect. I steered and I approved. The work arrived as a branch, then a commit, then a pull request I could review like any other[^3]. My interface to the entire task was the same one I use to review a colleague's work: a diff and a decision.

This is precisely the shape I keep describing when I write about where development is heading — the developer as reviewer and curator, not author. Here it is not a prediction. It is just what setting up a profile widget looked like on a Tuesday.

## If You Want to Do This Yourself

You do not need an agent for any of this. You just need to know where the landmines are. The short version:

- **The cards** come from `github-readme-stats`, a streak service, and a profile-view counter[^4] — free, drop-in image URLs you paste straight into your README.
- **To count private work**, fork the generator, deploy it to Vercel, and add a GitHub personal access token as an environment variable. Two things will bite you: the popular public instance is periodically **paused**, so self-hosting is the more reliable path anyway; and new Vercel projects ship with **Deployment Protection on**, which silently breaks every card until you disable it for production.
- **Embed your stable production domain**, never the per-deployment URL — the latter changes on every redeploy and will rot the moment you ship again.

That is the knowledge the whole exercise really consisted of: perhaps a dozen small facts, none of them hard, all of them tedious to discover.

## The Takeaway

The interesting thing about delegating a boring job is what it reveals about the job. The difficulty here was never conceptual. There was no algorithm, no architecture, nothing to *think* about. The entire cost was discovery and integration — knowing which services exist, which are up today, which flag unlocks private data, which setting quietly breaks everything.

That is the category of work agents are quietly absorbing: not the parts that require judgement, but the parts that require *knowing where things are*. I kept the judgement — which profile to emulate, whether the numbers were worth exposing, what to merge. I handed over the rummaging.

A better profile was the deliverable. The data point was the bonus.

[^1]: The reference profile that started it: [github.com/gustavoflw](https://github.com/gustavoflw).
[^2]: [Claude Code](https://claude.com/claude-code), Anthropic's command-line coding agent.
[^3]: The actual pull request: [zerafachris/zerafachris#1](https://github.com/zerafachris/zerafachris/pull/1).
[^4]: [github-readme-stats](https://github.com/anuraghazra/github-readme-stats), [github-readme-streak-stats](https://github.com/DenverCoder1/github-readme-streak-stats), and [komarev/ghpvc](https://github.com/antonkomarev/github-profile-views-counter).
