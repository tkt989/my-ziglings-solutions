---
name: ziglings-progress-summary
description: Summarize how far someone has progressed in a Ziglings practice repository and what they learned by reading the current git status, diffs, and modified exercise files. Use this when the user asks for a progress recap, a learning summary, or a plain-language explanation of what the code changes mean in Ziglings.
---

# Ziglings Progress Summary

Use this skill when the user wants a concise report of progress from Ziglings edits.

## Goal

Turn repository changes into a short, human-readable summary that answers two questions:

1. How far has the user progressed?
2. What did the user learn from the fixes?

## What to inspect

Read the change set before writing the summary:

- `git status --short`
- `git diff --stat`
- `git diff --name-only`
- `git diff` for each modified Zig file

If an untracked file looks unrelated to the exercises, mention it separately and avoid folding it into the learning summary unless it clearly supports the workflow.

## How to interpret the changes

For each modified exercise file:

- Identify the exercise number or file name.
- State the concrete fix in plain language.
- Explain the Zig concept that was exercised.
- Keep inference explicit if the conclusion is based on the diff rather than an explicit note from the user.

Typical Ziglings themes include:

- `pub fn main` for executable entry points
- `@import("std")` for standard library access
- `var` versus `const`
- signed versus unsigned integer types
- choosing a type wide enough for the value

## Output style

Write the summary in the user's language unless they asked for another language. For this repository, Japanese is usually the right default.

Keep the tone factual and brief. Do not over-explain. Prefer a structure like this:

```markdown
## 進捗
- ...
- ...

## 学んだこと
- ...
- ...

## 補足
- ...
```

## Rules of thumb

- Focus on what changed, not on generic Zig trivia.
- Summarize by exercise or file, not by line-by-line diff.
- If you cannot tell the intent with confidence, say so instead of guessing.
- Make the summary useful for a weekly review or learning journal.
- If you mention a commit message, write the full text exactly as committed. Do not abbreviate or paraphrase it.

## Commit Flow

If the user asks for a progress summary, and especially if they ask to commit, do the following after writing the summary:

1. Confirm the current branch is `my-progress`.
2. Stage only solved exercise files under `exercises/`.
3. Commit those staged files with the summary text from `ziglings-progress-summary` as the commit message, using the full text verbatim rather than abbreviating it.
4. Report the commit hash and the exact commit message.

Do not stage unrelated files such as local helper scripts or skill files unless the user explicitly asks for them.
Treat the summary-and-commit flow as the default outcome for this skill: after generating the summary, commit the solved exercise files unless the user explicitly says not to commit.
