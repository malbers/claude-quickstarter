# Token Discipline — A Practical Operating Posture for Claude Max

A short guide to working with Claude (and similar agentic AI tools) in a way that produces leverage without burning your weekly token cap by Wednesday. Written for Max-plan users running Claude Code, the Claude Agent SDK, or similar.

This is field-tested, not theoretical. The author hit the weekly cap repeatedly in early 2026, then iterated on a posture that produced *more* output with substantially fewer tokens by getting the architecture right. Anthropic later raised the caps; the discipline stays useful regardless.

---

## The two levers people misuse

Most usage waste comes from conflating two orthogonal choices:

- **Model choice** = capability ceiling (Haiku → Sonnet → Opus, in order of cost)
- **Effort choice** = thinking budget (low / medium / high, where supported)

These compound. `Opus + high effort` is the most expensive combination available. `Haiku + low effort` is the cheapest. Most work belongs somewhere in the middle.

The trap: **defaulting to the high-spend combination on anything that feels important.** Importance and complexity are different things. A high-stakes message to a CEO can be obvious to write. A low-stakes architectural sketch can have five reasonable paths worth deliberating between.

---

## The complexity ≠ scale rule

The single biggest waste pattern: mistaking volume for complexity.

- **Volume** = how many files / how much content / how long the output
- **Complexity** = how much judgment is required at each decision point

A 5,000-line code review against established conventions is **scale-heavy, complexity-light**. Sonnet at low effort handles it.

A 200-word strategic decision about which feature to kill is **scale-trivial, complexity-heavy**. Opus at high effort earns its keep.

When you find yourself reaching for Opus because the task "feels big," check whether the bigness is volume or judgment. Volume is Sonnet's job. Judgment is Opus's job.

---

## The intuition test for effort

When deciding between low / medium / high effort, ask:

> *How many genuinely different reasonable answers could a careful person produce here?*

- **1** → low effort. The answer is determined by the inputs; just produce it.
- **2-3** → medium (default). Some judgment, but a clear best path will surface.
- **4+ with real tradeoffs** → high effort. Worth deliberating; there's no obviously-right answer.

Note what this excludes: "this is important" is not a reason for high effort. "This is irreversible" is not a reason. "I want to be thorough" is not a reason. The only reason for high effort is genuine ambiguity in the task itself.

---

## The architectural pattern: subagent for fetch+synth, main thread for judgment

This is the operating split that produces the most leverage.

**Dispatch to subagents (background or foreground, usually Sonnet):**
- Multi-source content gathering (web, files, search, MCP queries)
- Bulk extraction with mechanical structure (per-item summaries, batch reviews)
- Cross-reference passes against known criteria
- Anything where the output shape is well-defined and the subagent can fill the template

**Keep on main thread (where you're talking to Claude, usually Opus):**
- Judgment calls and decisions
- Voice work in your register (drafts, replies, articles)
- Strategic conversation ("the thinking-together surface")
- Decision points after subagent returns ("what to elevate, what to skip")

**Subagent return discipline:**
- Subagent saves its output to a file (not just chat)
- Returns a tight summary to main thread (under 1-2K words)
- Main thread reads the summary, decides next moves, doesn't re-derive

**Why this works:**
- Sonnet has a separate weekly bucket from Opus on Max plans; using Sonnet aggressively doesn't touch the Opus ceiling
- Subagent context is isolated; heavy fetches don't crowd the main conversation
- File-persisted output survives context window clears
- You can monitor stats in real time and adjust pace

---

## The model × effort compound matrix

| Combo | When to reach for it |
|---|---|
| Haiku + low | Lookups, mechanical edits, file reads |
| Sonnet + low | Bulk file ops, simple extractions |
| Sonnet + medium | Most subagent dispatches |
| Sonnet + high | Synthesis where the framework is established but the read is hard |
| Opus + low | Fast voice work where register is locked in |
| Opus + medium | Voice plus light judgment (typical writing in your register) |
| Opus + high | Genuinely hard judgment with real ambiguity — rare, expensive, save it for those |

**Practical discipline:** when scoping a subagent or a heavy task, name model + effort explicitly. ("Sonnet + medium." "Opus + high.") This forces conscious choice over defaulting.

---

## What "smart on usage" actually looks like in a session

Real example from one session (compressed):

- 5 lookups + status pulls → 5 Haiku-low subagents in parallel
- 2 multi-file synthesis passes → 2 Sonnet-medium subagents in parallel
- 1 strategic decision conversation → main thread, Opus, deliberation
- 1 voice rewrite of an important piece → main thread, Opus, medium effort
- 1 mechanical fix-up of that voice rewrite → Sonnet-low

That's a productive session. Total spend: a fraction of what running everything on Opus-default would have cost. Output quality: equal or better, because the right tool went to the right job.

---

## The disciplines that compound

1. **Save synthesis to disk immediately.** Don't hold strategic output in conversation context — the next compaction loses it. Subagents should write to a file and return a summary, not paste 3000 words into chat.

2. **Watch the usage meter.** Most tools surface a session % and weekly %. Flag yourself proactively at 60-70% session burn so you can adjust pace before you're stuck.

3. **Don't do speculative work.** If a draft / research / cleanup wasn't asked for, don't volunteer the cycles. Ambient helpfulness is a token leak.

4. **Pick model + effort consciously, every dispatch.** Defaulting to "whatever's loaded" is how usage compounds badly. Naming the choice forces calibration.

5. **Match the architecture to the work.** Fetch + synth = subagent. Judgment + voice = main thread. Keep them separate and the leverage emerges.

---

## What this isn't

- Not a budget restriction. It's an architectural posture. Headroom is for *more of the right work*, not permission for sloppy work.
- Not a quality compromise. Done right, you produce *more* high-quality output, not less.
- Not a one-size rule. Voice work, strategic deliberation, and mechanical bulk work each have their right combination. The discipline is matching them, not minimizing across the board.

---

## Credit + caveat

This was developed working with Claude Code on a Max plan, but the core ideas — separating model from effort, separating volume from complexity, splitting fetch+synth from judgment — apply to any agentic AI workflow where you're paying for capacity and want to maximize leverage.

If this saves you time or money, great. If it doesn't fit your workflow, ignore it. The rules are descriptive, not prescriptive — they describe a posture that earned its keep, not a thing you must do.

Last updated: 2026-05-06.
