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

## What to Do Next

- **Use it daily.** The value compounds. Claude gets more useful the more context it has about your work.
- **Start with one project.** Pick one real thing you're working on and use Claude as your thinking partner for a week. Meeting prep, strategy docs, email drafts, whatever.
- **Add to your CLAUDE.md as you go.** When Claude does something you like, note it. When it does something you don't want, add a rule.
- **Try Claude Code** if you started with the desktop app. The CLI version can read and edit files, run commands, and work directly in your project folders. It's where the real power is.
- **Explore Projects** in the desktop app. Projects let you organize conversations by topic with persistent instructions.
- **Set up memory** (see "Build a Memory System" above). This is what separates "I use Claude sometimes" from "Claude is my operating partner."

## Resources

- [Claude documentation](https://docs.anthropic.com)
- [Claude desktop app](https://claude.ai/download)
- [Claude Code overview](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Memory system repo](https://github.com/malbers/claude-memory-context)
- [Trust framework repo](https://github.com/malbers/progressive-trust)

---

Built by Michael Albers. Questions? michael AT albersadvisory.biz
