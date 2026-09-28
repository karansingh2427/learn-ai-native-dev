---
id: part-4
number: 4
title: Folder-Based Rules
subtitle: 15 minutes - Different rules for different folders
---

## step: why-folder-rules
### title: Why This Part Matters

Your global rules work great — but what if you want AI to behave differently in different folders? Real projects have distinct areas with distinct needs:

- Frontend code should use vanilla JavaScript
- Documentation should be written for beginners
- Test files need specific naming conventions

One rulebook can't handle all these contexts. This part teaches you to create **folder-aware AI** that adapts its behavior based on where it's working.

---

## step: path-problem
### title: Step 16: The Problem with One Rule File

Your always-on rule applies to the **entire project**. Different parts of a project have different needs — and a single rule file can't express context-specific guidance.

**Imagine your project grows:**

```text
{{folderName}}/
├── app/              ← Frontend code (HTML, CSS, JS)
├── specs/            ← Requirements documents
└── tests/            ← Test files
```

**You might want:**
• **Frontend code**: "Use vanilla JavaScript, no frameworks"
• **Test files**: "Always use descriptive test names"
• **Specs**: "Keep documents under 1 page"

Folder rules let you do exactly this.

:::note
**Same idea, two files**

| | Cursor | Claude Code |
|---|---|---|
| Always-on | `.cursor/rules/project.mdc` with `alwaysApply: true` | `CLAUDE.md` |
| One folder | `.cursor/rules/app.mdc` with `globs: app/**` and `alwaysApply: false` | `.claude/rules/app.md` with `paths: ["app/**"]` |

Cursor applies a glob rule when matching files are in context. Claude Code loads a `paths` rule when it works on a matching file.
:::

## step: create-instructions-folder
### title: Step 17: Create the Rules Folders

You'll create three rule files for each tool — one for each area of your project.

After this prompt, both folders exist and the files are empty.

Copy this into the Agent chat:

:::prompt
number: 12
title: Create rule folders
---
Create these empty files:

1. .cursor/rules/app.mdc
2. .cursor/rules/specs.mdc
3. .cursor/rules/tests.mdc
4. .claude/rules/app.md
5. .claude/rules/specs.md
6. .claude/rules/tests.md

Leave them empty for now. Just create the structure.
:::

Check the sidebar — you should see `.cursor/rules/` and `.claude/rules/`, each with three files.

## step: frontend-instructions
### title: Step 18: Add Frontend Instructions

Now you'll define rules that apply only when AI edits files in the `app/` folder. These rules enforce vanilla JavaScript, modern syntax, and accessibility standards.

Copy this into the Agent chat:

:::prompt
number: 13
title: Write frontend rules
---
Write the same frontend rules into two files, with the frontmatter each tool expects.

File 1: .cursor/rules/app.mdc

---
description: Frontend rules for the app folder
globs: app/**
alwaysApply: false
---

File 2: .claude/rules/app.md

---
paths:
  - "app/**"
---

After the frontmatter, both files get this body:

# Frontend Code Instructions

## Technology Rules
- Use vanilla JavaScript only (no React, Vue, or other frameworks)
- Use modern ES6+ syntax (const, let, arrow functions, template literals)
- Keep all code in single HTML files unless specifically asked to separate

## Styling Rules
- Use CSS variables for colors (define once like `--primary-color: #3B82F6`, use everywhere with `var(--primary-color)`)
- Mobile-first responsive design
- Minimum touch target size: 44x44 pixels

## Code Quality
- Add comments explaining "why", not "what"
- Use meaningful variable names (not x, y, temp)
- Handle errors gracefully with user-friendly messages

## Accessibility
- All interactive elements must be keyboard accessible
- Use semantic HTML (button, nav, main, etc.)
- Include ARIA labels where needed
:::

💡 **The frontmatter is the switch.** Cursor uses `globs` and `alwaysApply: false`. Claude Code uses `paths`. The rules under the heading are identical.

## step: specs-instructions
### title: Step 19: Add Specs Instructions

Different rules for your requirements documents. These ensure PRD and task files stay concise, numbered, and written in beginner-friendly language.

Copy this into the Agent chat:

:::prompt
number: 14
title: Write specs rules
---
Write the same specs rules into two files.

File 1: .cursor/rules/specs.mdc

---
description: Rules for requirement and task documents
globs: specs/**
alwaysApply: false
---

File 2: .claude/rules/specs.md

---
paths:
  - "specs/**"
---

Body for both:

# Specification Document Instructions

## Document Format
- Keep all documents under 1 page when possible
- Use simple, non-technical language
- Number all requirements (R1, R2, R3...)

## Required Sections for PRD
1. GOAL (2-3 sentences)
2. WHO USES IT
3. WHAT IT SHOWS
4. REQUIREMENTS (numbered, with verification steps)
5. DEMO SCRIPT

## Required Sections for Tasks
- Use checkbox format: [ ] or [x]
- Each task maps to requirement(s)
- Each task has "Done when:" verification

## Writing Style
- Write for someone who has never seen the project
- Avoid jargon and acronyms
- Include specific, testable criteria
:::

## step: test-instructions
### title: Step 20: Add Test Instructions

Finally, rules for test files you'll create later. These enforce consistent naming, test structure, and coverage requirements.

Copy this into the Agent chat:

:::prompt
number: 15
title: Write test rules
---
Write the same test rules into two files.

File 1: .cursor/rules/tests.mdc

---
description: Rules for test files
globs: tests/**
alwaysApply: false
---

File 2: .claude/rules/tests.md

---
paths:
  - "tests/**"
---

Body for both:

# Test File Instructions

## Naming Conventions
- Test files: [feature].test.html or [feature].test.js
- Test names: should_[expected behavior]_when_[condition]

## Test Structure
- Arrange: Set up the test conditions
- Act: Perform the action being tested
- Assert: Verify the expected outcome

## Coverage Requirements
- Every requirement in specs/PRD.md needs at least one test
- Test both success and failure cases
- Test edge cases (empty data, maximum values, etc.)

## Manual Test Format
If creating manual test checklists:
- [ ] Test name
  - Steps: numbered list of actions
  - Expected: what should happen
  - Actual: (filled in during testing)
:::

## step: test-path-instructions
### title: Step 21: Verify Folder Rules Work

Start a new Agent chat, then ask it to explain what rules apply to different folders. It should describe different rules for each.

Copy this into the Agent chat:

:::prompt
number: 16
title: Test folder rules
---
I want to add a new feature to my project. Before making any changes, tell me:

1. What rules apply when you edit files in the app/ folder?
2. What rules apply when you edit files in the specs/ folder?
3. Are these rules different from each other?

Don't make any changes yet—just explain what you found.
:::

AI should describe the different rules for each folder — vanilla JavaScript for `app/`, simple language for `specs/`, and naming conventions for `tests/`.

## step: path-instructions-work
### title: See What Just Happened

🎯 **AI now follows different rules for different folders.**

When you edit frontend code, AI knows to use vanilla JavaScript. When you edit specs, AI knows to keep documents short and numbered. Each folder has context-aware assistance — and this scales as your project grows.

### ✅ Checkpoint

- [ ] Three `.mdc` files exist in `.cursor/rules/` besides `project.mdc`, each with `globs` and `alwaysApply: false`
- [ ] Three matching files exist in `.claude/rules/` with `paths`
- [ ] AI correctly identifies different rules for `app/` vs `specs/`

💡 **Adding new folders**: Create another pair of files with the same body and a glob that matches the new folder.
