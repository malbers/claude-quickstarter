<!--
  EXAMPLES: What memory files look like

  These are samples. Your memory system (see README, "Build a Memory System")
  will create files like this automatically as Claude learns about you. You
  don't need to write these by hand.

  Memory files have a simple structure:
  - Frontmatter (the --- section) tells Claude what the memory is about
  - Body contains the actual information to remember

  The memory system supports a few different types — three of the most common
  are shown below. Each lives in its own file. Over time you'll build up a
  collection. Claude reads them at the start of each session so it knows your
  context without you having to repeat yourself.

  TYPES:
  - user      = facts about you (role, background, preferences, working style)
  - feedback  = how you want Claude to behave (corrections, validated approaches)
  - project   = ongoing work, decisions, deadlines, motivations
  - reference = pointers to external systems (where to find what)
-->

---
name: User profile
description: Background and working style preferences
type: user
---

Senior product leader with 15 years experience in B2B SaaS. Currently VP Product
at a 120-person company going through a growth transition. Reports to the CEO.

Prefers structured thinking (frameworks, pros/cons, clear recommendations) over
open-ended brainstorming. Values brevity. Gets frustrated when AI responses are
too long or repeat what was already said.

Working on: Q2 roadmap prioritization, hiring a senior PM, evaluating whether
to build or buy an analytics platform.

---

<!--
  Below: a "feedback" memory. These capture how you want Claude to behave —
  things you've corrected or specifically validated. Live in their own file.
-->

---
name: Push back on weak reasoning
description: Don't agree by default — name flaws and propose alternatives
type: feedback
---

When I'm thinking through a decision and the logic is shaky, name the flaw
directly instead of helping me build on it. I'd rather hear "this assumption
doesn't hold because..." than have you draft me a polished version of a bad
plan.

**Why:** I learned this the hard way after running with a positioning idea
Claude validated that I should have killed.

**How to apply:** when reviewing my thinking, lead with the weakest point.
If you can't find one, say so explicitly. Don't manufacture an objection
just to perform critique, but don't smooth over real issues either.

---

<!--
  Below: a "project" memory. These capture ongoing work — what's happening,
  why, with whom. Convert relative dates ("next Thursday") to absolute dates
  before saving so the memory stays interpretable later.
-->

---
name: Q2 platform decision (build vs. buy)
description: Analytics platform evaluation, decision target end of June
type: project
---

Evaluating Mixpanel, Amplitude, and a custom build for the Q2 analytics
rollout. CFO wants TCO under $200k year one. Decision target: 2026-06-30.

**Why:** Current self-hosted setup is brittle, eng team won't maintain it
past Q3. Sales asked for cohort analysis they can't get today.

**How to apply:** when I'm working on roadmap or vendor decisions, factor
this analytics decision in — it affects what's even possible to instrument.
Stakeholders: CFO (cost-sensitive), Sales VP (wants cohort+attribution),
Eng lead (wants out of self-host).
