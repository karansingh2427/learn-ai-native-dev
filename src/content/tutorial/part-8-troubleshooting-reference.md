---
id: part-8
number: 8
title: Troubleshooting & Reference
subtitle: 5 minutes - Quick fixes and what's next
---

## step: final-structure
### title: Step 44: Your Final Project Structure

You've built a complete AI-native development setup. Here's what your project should look like — use this as a reference to verify everything is in place.

```text
{{folderName}}/
├── .cursor/
│   ├── rules/                            ← Cursor rules
│   │   ├── project.mdc                   ← Always on
│   │   ├── app.mdc
│   │   ├── specs.mdc
│   │   └── tests.mdc
│   ├── agents/                           ← Cursor subagents
│   │   ├── test-agent.md
│   │   ├── docs-agent.md
│   │   └── review-agent.md
│   └── skills/                           ← Cursor skills
│       ├── verify-requirements/SKILL.md
│       ├── add-feature/SKILL.md
│       └── fix-bug/SKILL.md
├── .claude/
│   ├── rules/                            ← Claude Code folder rules
│   │   ├── app.md
│   │   ├── specs.md
│   │   └── tests.md
│   ├── agents/                           ← Same three subagents
│   └── skills/                           ← Same three skills
├── CLAUDE.md                             ← Claude Code always-on rules
├── AGENTS.md                             ← Shared project map
├── specs/
│   ├── PRD.md
│   └── Tasks.md
├── app/
│   └── index.html
├── tests/
│   └── test-plan.md
├── docs/
│   ├── USER-GUIDE.md
│   ├── CODE-REVIEW.md
│   └── VERIFICATION-REPORT.md
└── README.md
```

## step: when-to-use-what
### title: Step 45: Quick Reference (When to Use What)

With so many tools available, it helps to know when to use each one. Use this reference when you're unsure which approach fits your task.

### Instruction Files

| File | Location | Purpose |
|------|----------|--------|
| `project.mdc` | `.cursor/rules/` | Cursor rules for every session (`alwaysApply: true`) |
| `*.mdc` with `globs` | `.cursor/rules/` | Cursor rules for one folder |
| `CLAUDE.md` | Repository root | Claude Code rules for every session |
| `*.md` with `paths` | `.claude/rules/` | Claude Code rules for one folder |
| `AGENTS.md` | Repository root | Shared project context |

### Agent Modes

| Mode | When to Use |
|------|-------------|
| **Agent** | Edits files and runs commands |
| **Plan** | Writes the approach before editing |
| **Ask** | Questions only — no file changes |
| **Subagent** | A specialist the main agent delegates to |

### Prompt Patterns

| Pattern | Example |
|---------|--------|
| Start general → specific | "Add a filter. It should be a dropdown with 3 options..." |
| Give examples | "Format like: 2024-01-15" |
| Break down tasks | Ask for structure, then data, then styling |
| Name things explicitly | "The filterItems function" not "this" |
| Reference files | "Look at app/index.html" |

### Skills

| Skill Location | Purpose |
|----------------|--------|
| `.cursor/skills/*/SKILL.md` | Cursor project skills |
| `.claude/skills/*/SKILL.md` | Claude Code project skills |
| User profile skills | Personal workflows across projects |
| `SKILLS.md` at root | Quick reference for common tasks |

## step: troubleshooting-agents
### title: Step 46: Troubleshooting

When things don't work as expected, check these common issues and solutions. Most problems have simple fixes.

### Agent & Mode Issues

**"The agent isn't using my subagent"**
• Say it explicitly: "Use the test-agent subagent"
• Cursor reads `.cursor/agents/*.md`. Claude Code reads `.claude/agents/*.md`
• The file needs `name:` and a `description:` that says when to use it
• Start a new Agent chat so it picks up files you just added

**"Not sure which mode to use"**
• **Agent** → You want files created or edited
• **Plan** → You want to read the approach before anything changes
• **Ask** → You want an explanation and no edits

**"AI seems slow or gives shallow answers"**
• Try a different model in the model picker
• Fast models work for simple tasks; reasoning models handle complex logic better
• Start a new chat — long conversations slow down responses

### Instruction File Issues

**"My skill isn't being loaded automatically"**
• Cursor looks in `.cursor/skills/<name>/SKILL.md`. Claude Code looks in `.claude/skills/<name>/SKILL.md`
• The file must be named exactly `SKILL.md`
• The `description:` should say when to use the skill, in plain language
• Ask directly: "Use the verify-requirements skill"
• Start a new chat after you add a skill

**"Folder rules aren't working"**
• Cursor: `globs` matches the folder, and `alwaysApply` is `false`
• Claude Code: `paths` lists the same glob
• Cursor rules are `.mdc` files in `.cursor/rules/`. Claude Code rules are `.md` files in `.claude/rules/`
• Start a new chat so the new rules load

**"AGENTS.md isn't being read"**
• Ensure the file is at the repository root (or in a parent folder of where you're working)
• The file must be named exactly `AGENTS.md` (uppercase)
• AGENTS.md is read automatically — no setting required

**"Need help creating rule files?"**
• Ask the agent: "Read this project and draft `.cursor/rules/project.mdc` and `CLAUDE.md`"
• Then delete anything you do not actually want enforced

### Prompt & Response Issues

**"I'm getting inconsistent results"**
• Use `/clear` or start a new chat to reset context
• Be more specific in your prompts — avoid "this" and "it"
• Reference files explicitly: "Look at app/index.html"
• Delete failed attempts before trying again

**"AI keeps suggesting frameworks or complex solutions"**
• Check that `.cursor/rules/project.mdc` and `CLAUDE.md` exist and list your "Do NOT" rules
• Start a new chat — old context may be overriding your rules
• Be explicit: "Use plain HTML and JavaScript only, no frameworks"

**"AI suggestions don't match my coding style"**
• Add path-specific instructions for that file type (Part 4)
• Include an example of your preferred style in the instructions
• Keep a file open that shows your style — AI uses open tabs as context

**"AI keeps asking questions instead of just doing it"**
• Add "Don't ask me questions — just make your best decision" to your prompt
• Check your instruction files for conflicting rules that require clarification
• Be more specific about what you want in the original prompt

**"AI gives vague or incomplete answers"**
• Break your request into smaller steps
• Give examples of what you want
• Reference specific files with `@` in Cursor, or by path in either tool

### Validation Checklist

Before accepting AI-generated code:
- [ ] Does it compile/run without errors?
- [ ] Does it do what you asked?
- [ ] Did you test it in the browser?
- [ ] Does it follow your instruction files?
- [ ] Are there any obvious security issues (passwords, API keys)?

💡 **AI is powerful but not perfect.** Always review suggestions before accepting. You're the developer — AI is your assistant.

## step: whats-next
### title: Step 47: What's Next?

You've mastered the core techniques. Here's how to take your AI-native development skills further:

1. **Create more custom agents** for your specific needs (security-agent, performance-agent, etc.)

2. **Build more skills** for workflows you repeat often

3. **Share your setup** — All these files can be committed to git so your whole team benefits

4. **Explore MCP** (Model Context Protocol) — A standard for connecting AI assistants to external tools. With MCP, the agent can query databases, call APIs, or control other applications. This is an advanced topic for when you want AI to work with systems beyond your code files.

🎉 **Congratulations!** You now have a professional-grade setup for AI-assisted development.

💡 **Remember**: The techniques you learned work for any project — not just web apps. Use spec-driven development, custom agents, and skills for documents, automation scripts, data analysis, and more.

## step: learn-more
### title: Step 48: Learn More

Ready to go deeper? These official resources provide comprehensive documentation for everything you learned:

**Cursor**
- [Rules](https://cursor.com/docs/rules)
- [Subagents](https://cursor.com/docs/subagents)
- [Skills](https://cursor.com/docs/skills)

**Claude Code**
- [Memory and CLAUDE.md](https://code.claude.com/docs/en/memory)
- [Subagents](https://code.claude.com/docs/en/sub-agents)
- [Skills](https://code.claude.com/docs/en/skills)

**Shared**
- [Agent Skills standard](https://agentskills.io/)
