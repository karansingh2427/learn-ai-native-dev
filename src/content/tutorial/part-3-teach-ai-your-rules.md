---
id: part-3
number: 3
title: Teach AI Your Rules
subtitle: 15 minutes - Make AI work the way you want
---

## step: why-rules-matter
### title: Why This Part Matters

Your prototype works, but here's a challenge you'll face as projects grow: AI can drift in unexpected directions.

**Try this experiment.** Ask the agent:

> "Add a user login system to my app"

Watch what happens — AI will happily try to add authentication, maybe install packages, possibly create a backend server. That's not what you want for a simple prototype!

**Without guardrails, AI does whatever seems helpful.** This part teaches you to set boundaries that AI follows automatically — no need to repeat yourself in every prompt.

---

## step: agentic-intro
### title: Step 12: The Rules You'll Create

As you add more features, AI can make decisions you didn't intend. Understanding these patterns helps you write better rules.

**Without rules, AI might:**
- Add a database when you just want sample data
- Install React or Vue when you want plain HTML
- Restructure your entire file while fixing one small bug
- Add login screens or backend servers you never asked for
- Use different coding styles each time, making the code messy

**Real example:** You ask AI to "add a summary section" and it installs three JavaScript libraries, creates a Node.js backend, and rewrites your entire file structure.

**The fix:** Create rule files that AI reads automatically. Set them once, and AI stays on track for every future prompt.

**Rule files you’ll create:**
• `.cursor/rules/project.mdc` — Rules Cursor applies to every Agent session in this project
• `AGENTS.md` — Project context both Cursor and Claude Code read (how to build, what not to do)
• `CLAUDE.md` — The same always-on rules, in the file Claude Code loads at the start of every session

Both tools read `AGENTS.md` automatically — you don't need to reference it in prompts.

**Click any file below to see what it does:**

:::diagram file-hierarchy
:::
💡 **Shared file:** `AGENTS.md` is an open standard. Cursor and Claude Code both read it. Tool-specific rule files (`.cursor/rules` and `CLAUDE.md`) hold the same constraints in the format each tool expects.

---

### Prompt Patterns That Get Better Results

Use these whenever you talk to the agent:

- **Start general → get specific** — Give the big picture first, then details. Example: "Create a filter feature. It should have a dropdown with Green/Yellow/Red options."
- **Give examples** — Show input/output samples. Example: "Format dates like: 05/02/2024"
- **Break complex tasks down** — One thing at a time. Instead of "build the whole app," ask for structure, then data, then styling
- **Avoid ambiguity** — Name things explicitly. Say "the `filterItems` function" not "this function"
- **Reference files** — Point to specific code. In Cursor, type `@` and pick the file. You can also write "look at app/index.html"

**Keep history clean:**
- Start a new chat for new tasks (old context can confuse AI)
- Delete failed attempts before trying again
- In Cursor, start a new Agent chat. In Claude Code, run `/clear`

💡 **Pro tip:** Ask the agent to draft the rules from the project you already built, then edit anything that is too strict or too vague.

---

## step: create-instructions
### title: Step 13: Create Rules AI Follows Automatically

Now you'll create a rules file that AI reads at the start of every conversation. This is powerful: set your constraints once, and AI respects them forever — no reminding needed.

After this prompt, you'll have a Cursor rule that keeps AI focused on your prototype approach, plus a `CLAUDE.md` with the same constraints.

Copy this into the Agent chat:

:::prompt
number: 9
title: Create project rules
---
Create two files with the same rules.

1. .cursor/rules/project.mdc — Cursor always-on rule. Start the file with this frontmatter, then the sections below:

---
description: Always-on rules for this prototype
alwaysApply: true
---

2. CLAUDE.md at the project root — Claude Code always-on memory. No frontmatter. Same four sections.

SECTION 1: Project Overview
- This is a {{projectName}} prototype
- The requirements are in specs/PRD.md
- The task list is in specs/Tasks.md
- The web app is in app/index.html

SECTION 2: How to Make Changes
- Always check specs/PRD.md before making changes
- Always update specs/Tasks.md when completing work
- Make small changes (one task at a time)
- Test changes by opening index.html in a browser

SECTION 3: Do NOT Do These Things
- Do not add a backend server or database
- Do not add login or user accounts
- Do not add external services or APIs
- Do not add secret keys or passwords
- Do not add frameworks like React or Vue
- Do not make changes that aren't in the requirements

SECTION 4: When Asked to Add New Features
- First, ask if it should be added to specs/PRD.md
- Then create a task in specs/Tasks.md
- Then implement following the normal process

Keep both files concise and easy to read.
:::

Check that `.cursor/rules/project.mdc` and `CLAUDE.md` were created. Open them — these rules now apply to every new Agent session in this project.

💡 **Rules persist across sessions**: Every time you open this project, Cursor loads rules with `alwaysApply: true`. Claude Code loads `CLAUDE.md`.

:::note
**Why two files?** Cursor's project rules are `.mdc` files in `.cursor/rules/` with `alwaysApply` or `globs`. Claude Code loads `CLAUDE.md` (and any `.claude/rules/` file that has no `paths` field) at the start of every session. The sentences inside are the same. The wrapper is what differs.
:::

## step: test-rules
### title: Step 14: Test That AI Follows Your Rules

Let's prove it works. Start a **new** Agent chat so it picks up the files you just created. Ask for features that would normally trigger AI to add complexity — and watch it refuse based on your rules.

After this prompt, AI should explain which features are blocked and suggest alternatives that follow your constraints.

Copy this into the Agent chat:

:::prompt
number: 10
title: Test the rules
---
I want to add these features:
- User login system
- Database to store data
- AI that predicts outcomes

Tell me:
1. Which of these features are you allowed to add?
2. Which are you NOT allowed to add, and why?
3. What could you add instead that would improve the prototype while following the rules?

Don't make any changes yet—just explain.
:::

AI should identify that login, database, and external AI are all blocked by your rules. It should suggest simpler alternatives that fit a prototype approach.

## step: reflect-on-rules
### title: See What Just Happened

🎯 **AI followed your rules without you reminding it.**

It knew what was allowed and what wasn't — because you wrote clear rules in a file it checks automatically.

This works for any project: set your rules once, and AI follows them every time. You're in control.

### ✅ Checkpoint

- [ ] `.cursor/rules/project.mdc` exists and has `alwaysApply: true`
- [ ] `CLAUDE.md` exists with the same constraints
- [ ] AI refused to add login/database when you tested it
- [ ] AI suggested alternatives that follow your rules

## step: create-guide
### title: Step 15: Create Shared Agent Instructions

`AGENTS.md` is onboarding for any coding agent that opens this repo — Cursor, Claude Code, and others. It says how to build, how to test, and what is out of scope. Your Cursor rule and `CLAUDE.md` hold the detailed do/don't list. `AGENTS.md` holds the project map.

After this prompt, you'll have an `AGENTS.md` file at the project root.

Copy this into the Agent chat:

:::prompt
number: 11
title: Create AGENTS.md
---
Create an AGENTS.md file in the root of the project.

This file is read by Cursor and by Claude Code. It is the shared project map.

Include:

1. PROJECT CONTEXT
   - This is a {{projectName}} prototype
   - Frontend-only, no backend or database
   - Requirements are in specs/PRD.md

2. BUILD AND TEST
   - No build step required — open app/index.html in browser
   - Test by checking all interactive features work
   - Use Reset button to restore sample data

3. CODING STANDARDS
   - Use vanilla JavaScript only (no frameworks)
   - Keep all code in a single HTML file
   - Follow the always-on rules in .cursor/rules/project.mdc and CLAUDE.md

4. WHAT NOT TO DO
   - Do not add backend services
   - Do not add authentication
   - Do not install packages

Keep it concise.
:::

Check that `AGENTS.md` was created at the project root.

💡 **Three files, different jobs**: `AGENTS.md` is the shared map (build, test, architecture). `.cursor/rules/project.mdc` is Cursor's always-on rule. `CLAUDE.md` is Claude Code's always-on memory. Keep the constraints in agreement — if you change a "do not", change it in all three.
