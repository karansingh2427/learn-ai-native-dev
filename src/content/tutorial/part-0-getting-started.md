---
id: getting-started
number: 0
title: Getting Started
subtitle: 5 minutes - Get ready to build
---

## step: what-youll-learn
### title: What You'll Learn

**Whether you've never built anything or you build every day** — AI-Native Development will change how you work.

This tutorial teaches you to **direct AI to create things** using structured techniques that work for any project. You describe what you want, AI handles the implementation.

**What changes:**
• Ideas → working results in hours, not weeks
• Complex tasks → described in plain English, AI handles the details
• Iteration → AI refines and improves based on your feedback
• Consistency → AI follows your rules automatically, every time

**In this tutorial,** you'll build a real, working web app — but the techniques apply to anything: documents, automation scripts, data analysis, and more. These skills scale from quick tasks to complex projects.

The lessons use **Cursor** as the main tool. Wherever Claude Code stores a file differently, or starts a session differently, a note shows the equivalent. The prompts you paste are the same in both.

## step: agent-setup
### title: Set Up Cursor (Agent)

Before you can direct AI to build things, you need an agent that can create and edit files. Chat that only suggests code is not enough.

**What you need:**
• [Cursor](https://cursor.com) installed and signed in

**Open Agent:**
1. Open Cursor
2. Open the Agent panel (`Cmd+I` on Mac, `Ctrl+I` on Windows) or the side chat (`Cmd+L` / `Ctrl+L`)
3. Set the mode to **Agent**

You should see **Agent** in the mode selector. The panel can now plan a task and edit files in the project.

💡 **What's the difference?** **Agent** plans and executes multi-step tasks, creating and editing files. **Ask** answers questions and leaves files alone. **Plan** writes the approach before it edits. Later in this tutorial, you'll create **subagents** — specialists the main agent can hand work to.

:::note
**Claude Code**

Install [Claude Code](https://code.claude.com/docs/en/setup), open a terminal in your project, and run `claude`. Claude Code edits files by default — there is no separate Agent switch. Paste the same prompts from this course into that session. When a lesson names a Cursor file (`.cursor/rules`, `.cursor/agents`, `.cursor/skills`), the note in that lesson names the Claude Code path (`.claude/rules`, `.claude/agents`, `.claude/skills`, or `CLAUDE.md`).
:::
