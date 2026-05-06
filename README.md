# Claude Quickstarter

**How I set up Claude as my AI operating partner. A guide for operators and executives who want to do the same.**

## What This Is

Claude is an AI assistant built by Anthropic. Most people use it like ChatGPT: ask a question, get an answer. What makes it powerful is when you teach it who you are, what you're working on, and how you think. That's what this guide helps you do.

This covers both the Claude desktop/web app (easiest starting point) and Claude Code (the CLI tool for more technical users). Start wherever feels right.

## Pick Your Starting Point

### Option A: Claude Desktop App or claude.ai (Easiest)

1. Go to [claude.ai/download](https://claude.ai/download) or open [claude.ai](https://claude.ai) in your browser
2. Create an account. The Pro plan ($20/month) is worth it for longer conversations and better models.
3. You're ready. Open a new conversation and start talking to it.

That's it for step one. You can already ask it questions, paste in documents, brainstorm, draft emails, and think through problems.

### Option B: Claude Code (CLI, More Powerful)

This is the terminal-based version. It can read and edit files on your computer, run commands, and work directly in your project folders. More powerful, but requires some comfort with a terminal.

- Install instructions: [Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)
- Requires Node.js and a terminal (VS Code's built-in terminal works great)
- If this feels intimidating, start with Option A and come back here when you're ready

Claude also works inside code editors (called IDEs). If you use VS Code, Cursor, or JetBrains, you can install Claude as an extension and use it right where you write code or work on files. Cursor in particular has Claude built in as its default AI model.

## Your First Real Conversation

Don't start with "what's the weather." Start with something you actually need help with. The key is context. Instead of "help me with a presentation," try:

```
I'm [your name], [your role] at [company]. I need to prepare for a meeting 
with [person/group] about [topic]. Here's what I know so far: [paste your 
notes, context, background]. Help me think through my approach.
```

The more context you give, the better the output. Think of it like briefing a sharp colleague who just walked into the room. They're smart, but they don't know your situation yet.

A few tips:
- Paste in real documents, emails, or notes. Claude can read them and work with them.
- Say what you actually want. "Help me think through this" is different from "write me a draft" is different from "poke holes in this plan."
- If the response isn't what you wanted, say so. "That's too generic. I need something more specific to [my situation]." Claude adjusts.

## Make It Remember You (CLAUDE.md)

This is where it gets interesting. You can give Claude a file called CLAUDE.md that tells it who you are, how you work, and what you're focused on. Every conversation starts with that context already loaded.

**In the desktop app:** Create a Project (left sidebar), then add your CLAUDE.md content to the Project instructions. Every conversation in that Project will have your context.

**In Claude Code:** Claude Code can generate a starter CLAUDE.md for you automatically. Just type `/init` in your first session and it will scan your project and create one. Then open the file it created and add your personal context to it (who you are, how you work, your rules). Don't overwrite it with a blank template, build on top of what `/init` gives you.

We've included a starter template in this repo: **[starter-claude.md](starter-claude.md)**. Use it as a reference for what to add to your CLAUDE.md. For desktop app users, you can paste it directly into your Project instructions.

### What goes in a CLAUDE.md:
- **Who you are.** Role, background, what you're working on.
- **How you like to work.** "Be direct." "Push back on me." "Don't pad responses."
- **What you're focused on.** Current projects, priorities, key people.
- **Rules.** What Claude should and shouldn't do. Start simple, add more over time.

## Build a Memory System

After a few conversations, you'll notice Claude forgets everything between sessions. A memory system fixes that.

I built one and open-sourced it. The simplest way to use it: give Claude the repo link and tell it to set things up for you.

**The repo:** [github.com/malbers/claude-memory-context](https://github.com/malbers/claude-memory-context)

**How to use it:**

- **Desktop app:** Start a conversation and say: *"Read this repo and set up a memory system for me based on this approach: https://github.com/malbers/claude-memory-context"*. Claude will read the repo and walk you through it.
- **Claude Code:** You can clone the repo (`git clone https://github.com/malbers/claude-memory-context.git`) or just paste the URL in conversation and say *"Read this and set up my memory system based on this approach."*

**What it gives you:** Claude will remember who you are, what you're working on, key decisions you've made, and how you like to work. Across sessions. It builds up over time and gets more useful the longer you use it.

See **[sample-memory.md](sample-memory.md)** for an example of what a memory file looks like.

## Keep It Safe (Trust and Privacy)

Once Claude knows about you and your work, you want guardrails. What should it never share? What actions should it never take without asking? What's private?

Start simple. Add a section to your CLAUDE.md:

```
## Rules
- Never share my personal information in responses
- Always confirm before taking any action that can't be undone
- Don't make assumptions about what I want. Ask if unclear.
- Keep my company information confidential
```

I built a more comprehensive trust framework that covers data privacy, action permissions, and progressive access controls. It's what I use for my own setup:

**[github.com/malbers/progressive-trust](https://github.com/malbers/progressive-trust)**

You don't need all of that on day one. Start with basic rules in your CLAUDE.md and add sophistication as you learn what matters to you.

## How We Manage Token Usage

Claude Max gives you real capacity, but if you default to Opus + high effort on everything, you'll hit your weekly cap by Wednesday. Here's the operating posture that produces *more* output with substantially fewer tokens.

**Two levers, often confused:**
- **Model** = capability ceiling (Haiku → Sonnet → Opus, in cost order)
- **Effort** = thinking budget (low / medium / high)

These are orthogonal and compound. `Opus + high` is the most expensive combination available; `Haiku + low` is the cheapest. Most work belongs in the middle.

**The complexity ≠ scale rule.** A 5,000-line code review against established conventions is volume-heavy, judgment-light → Sonnet at low effort. A 200-word strategic decision can be five-paths-worth-deliberating → Opus at high effort. Don't reach for high-spend combinations because the task feels big. Check whether the bigness is volume or judgment.

**The intuition test for effort:** *How many genuinely different reasonable answers could a careful person produce here?*
- 1 → low
- 2-3 → medium (default)
- 4+ with real tradeoffs → high

Importance and irreversibility are not reasons for high effort. The only reason is genuine ambiguity in the task.

**The architectural pattern:** subagent for fetch + synthesis (Sonnet, usually), main thread for judgment + voice (Opus). Subagents save output to a file and return a tight summary; main thread reads, decides, doesn't re-derive. This separates volume from judgment cleanly and keeps Opus reserved for what it's actually good at.

**Practical discipline:** name model + effort explicitly when scoping a dispatch ("Sonnet + medium," "Opus + high"). Forces conscious choice over defaulting.

**Full guide with examples + matrix:** [operating-discipline/token-discipline.md](operating-discipline/token-discipline.md)

This was developed running into the cap repeatedly, then iterating. Anthropic later raised Max-plan caps; the discipline still earns its keep — headroom buys *more of the right work*, not permission for sloppy work.

## What to Do Next

- **Use it daily.** The value compounds. Claude gets more useful the more context it has about your work.
- **Start with one project.** Pick one real thing you're working on and use Claude as your thinking partner for a week. Meeting prep, strategy docs, email drafts, whatever.
- **Add to your CLAUDE.md as you go.** When Claude does something you like, note it. When it does something you don't want, add a rule.
- **Try Claude Code** if you started with the desktop app. The CLI version can read and edit files, run commands, and work directly in your project folders. It's where the real power is.
- **Explore Projects** in the desktop app. Projects let you organize conversations by topic with persistent instructions.
- **Set up memory** (see "Build a Memory System" above). This is what separates "I use Claude sometimes" from "Claude is my operating partner."

## The Next Layer

Once Claude is part of your daily workflow and your CLAUDE.md + memory system are dialed in, these are the features worth exploring next. Don't reach for them on day one — they're force multipliers, not starter equipment.

- **Skills** — reusable slash commands that bundle a workflow. You type `/<skillname>` and Claude runs the procedure. Anthropic ships some by default; the community has built many more. The one I reach for most: `/brainstorming` — it walks me through a structured exploration before any creative work (features, copy, decisions). If I'm about to start something open-ended, that's where I begin. Worth installing. [Anthropic Skills docs](https://docs.anthropic.com/en/docs/claude-code/skills)
- **MCP servers** — connect Claude to external systems. Read your Gmail, query your calendar, browse a SQL database, drive your browser. The protocol is open; both Anthropic and the community publish servers. This is what turns Claude from a chat tool into something that can actually do work in your stack. [Model Context Protocol overview](https://modelcontextprotocol.io)
- **Hooks** — Claude Code lets you run shell commands automatically at session events (start, stop, before tool use, etc.). Useful for state-file safety checks, automatic logging, periodic backups, or enforcing rules you don't trust yourself to remember.
- **Subagent dispatch** — fire off parallel agents to do bounded work (research, file edits, batch synthesis) while you keep talking to the main thread. The pattern in the "How We Manage Token Usage" section above explains when this earns its keep.
- **Plugins** — Anthropic's plugin system lets you bundle skills, hooks, and configuration into a single package. The community-built `superpowers` plugin is a good example: it ships a bundle of opinionated workflows (brainstorming, debugging, planning, code review) that compose well together. Worth a look once you've gotten value from individual skills.

The honest sequence: get comfortable with daily Claude → install a skill or two (start with `/brainstorming`) → connect one MCP server that fits your work → then think about hooks and plugins. Don't try to set all of this up at once.

## Resources

- [Claude documentation](https://docs.anthropic.com)
- [Claude desktop app](https://claude.ai/download)
- [Claude Code overview](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Memory system repo](https://github.com/malbers/claude-memory-context)
- [Trust framework repo](https://github.com/malbers/progressive-trust)

---

Built by Michael Albers. Questions? michael@albersadvisory.biz
