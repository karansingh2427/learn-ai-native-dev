# How to build an AI agent

From scratch. Spec, build, evals, rails.

Source: Basia Kubicka, "How to Build an AI Agent." Hands-on write-up: https://lnkd.in/ebckfuAx

Saved 2026-10-02 as a reference for this course. The Foundation path does not teach these nine steps yet.

Open question kept with the note: spec first, or evals first?

## 1. Define the job

One weekly task. Write what goes in, what comes out, what "good" means, and what it must never do.

Example: in = meeting notes; out = action items with owners. Good = every item has an owner and a date. Never = email anyone outside the team.

## 2. Write the instructions

Turn the spec into the prompt. Add 2 real examples of good output. Try it on 3 old inputs. Watch for made-up owners, missing dates, and other failures.

Shape: spec + 2 examples + one model = answer.

## 3. Give it tools

Every system you open to do the job becomes a tool. Nothing extra. Start in test mode.

Example: read the notes folder, write drafts, do not send. Reads might be Drive, Inbox, CRM, web search. Acts might be send email or book meetings — test mode first.

## 4. Control the loop

It picks a tool, reads the result, decides, and repeats until done. Cap the turns (for example 10), then it asks you. Save every run. You read these logs in step 9.

## 5. Add memory

Only for what changes between runs. Fixed facts stay in the instructions.

- A log of what it already did (for example: Mar 3 action items already emailed).
- Mistakes you corrected, as a lessons file, one page max.

## 6. Set the guardrails

Reads are lower risk. Anything that sends, deletes, pays, or posts waits for your yes.

Own login, fewest permissions, and a "never" list. Reads: search, open files, read inbox. Acts that stay blocked until you approve: send, delete, pay, post.

## 7. Check the result

Its "done" does not count. A check confirms the result exists (email in the sent folder, event on the calendar). If the check fails, it stops and tells you. Retries may search; they never send.

## 8. Build a golden dataset

20 real past examples with correct answers. Not the 2 examples from the prompt. It must pass a bar (for example 18 of 20) before it goes live. Run it with tools still in test mode.

## 9. Run continuous evals

After launch, every week. Evals do not stop at launch. Every failure becomes a new test.

- Weekly: read 10 saved runs.
- Each mistake: a new row in the golden dataset.
- Each change: rerun the full set first.
