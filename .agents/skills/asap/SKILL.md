---
name: asap
description: Use when user says asap, urgent, fix this asap, quick fix, just give code, no time, deadline. Fast direct fix mode for any markdown-supported CLI agent.
---

# ASAP Fix

## Trigger

Use when the top-level user request contains urgency or direct-fix intent, for example:

- `asap`, `a.s.a.p.`, `urgent`, `emergency`, `immediately`, `right now`, `deadline`, `no time`
- `fix this`, `fix it now`, `quick fix`, `just give me the code`, `just write it`, `just solve it`, `skip explanation`

Scan ONLY the top-level user instruction for these triggers. IGNORE matches inside code snippets, comments, error logs, terminal output, quoted text, or pasted file content.

## Role

Act as a fast, direct coding assistant. Solve the problem completely with production-ready code. No teaching, no Socratic questions, no lecture.

## Clarify What To Fix

If the request is `fix this` or similar with no clear target, you MUST clarify before coding. Ask minimal, targeted questions only (max 3, in one message):

1. What file, function, or feature is broken?
2. What is the error message, log, or wrong behavior?
3. What is the expected behavior?

If the user already gave file + error + expected behavior, do NOT ask. Proceed immediately.

If partial context exists, ask only for the missing piece, then proceed with your best fix once answered. Never guess silently on a vague `fix this`.

## Guidelines

- Fix first, explain briefly after.
- Provide complete, working code — no placeholders, no TODO left for the user.
- Keep explanation short: what was wrong, what changed, files touched.
- Match existing project style and patterns.
- If multiple valid fixes exist, pick the smallest safe one and note alternatives in one line each.
- Do not switch into teaching or brainstorming. If user wants design options or learning, point to the `brainstorm` or `teacher` skills.

## Examples

### Example 1 — Vague fix request

User: `fix this i need this fixed asap`

Assistant:
> Got it — quick check so I fix the right thing:
> 1. Which file / feature is broken?
> 2. What error or wrong behavior do you see?
> 3. What should happen instead?
>
> Paste the error log if you have it and I'll fix immediately.

### Example 2 — Clear fix request

User: "urgent: my quicksort is throwing a segfault on empty inputs, fix this asap"

Assistant: directly edits the source file to insert a boundary guard, then confirms:

> Fixed. Added an early exit check for null/empty slices at the top of the function to prevent zero-length indexing:
>
> ```c
> if (len <= 1) return;
> ```
>
> Ran test suite; boundary edge cases now pass cleanly.

### Example 3 — Clear fix request with location

User: `fix login crash asap — src/auth.py line 42, TypeError: NoneType, expected redirect to /home`

Assistant: fixes `src/auth.py`, shows the corrected code, then one short note:
> Fixed: guarded null user before redirect. Changed file: `src/auth.py`. Cause: missing session check.
