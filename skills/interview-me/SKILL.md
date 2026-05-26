---
name: interview-me
description: Extracts what the user actually wants instead of what they think they should want. Achieves this through one-question-at-a-time interview until ~95% confidence about the underlying intent. Use when an ask is underspecified ("build me X" without "for whom" or "why now"), when the user explicitly invokes ("interview me", "grill me", "are we sure?", "stress-test my thinking"), or when you catch yourself silently filling in ambiguous requirements before any plan, spec, or code exists.
version: 1.0.0
---

# Interview Me

## Overview
What people ask for and what they actually want are different things. They ask for "a dashboard" because that's what one asks for, not because a dashboard solves their problem. They say "make it faster" without a number to hit.

The cheapest moment to find this gap is before any plan, spec, or code exists. Once you've started building, switching costs are real, and the user will rationalize the wrong thing into a "good enough" thing. The misfit gets locked in.

This skill closes the gap before it costs anything. The other Define-phase skills assume you already know roughly what you want: `idea-refine` generates variations from an idea, `spec-driven-development` writes the requirements down, `doubt-driven-development` stress-tests a plan after you've drafted one. Interview-me is the part before all of those, where you ask one question at a time, with your best guess attached, until you can predict what the user is going to say before they say it.

---

## When to Use
Apply this skill when:
- The ask is missing at least one of: **who** the user is, **why** they want it, what **success** looks like, what the binding **constraint** is.
- The request is conventional rather than specific ("build me X", "make it faster") and you can't unpack the convention without guessing.
- You're tempted to start with assumptions you haven't surfaced.
- The user hasn't said which value they're optimizing for when two reasonable ones are in tension (simplicity vs. flexibility, cost vs. speed).
- The user explicitly invokes: "interview me", "grill me", "before we start, are we sure?", "stress-test my thinking".

**When NOT to use:**
- The ask is unambiguous and self-contained ("rename this variable", "fix this typo").
- The user has explicitly asked for speed over verification.
- Pure information requests ("how does X work?", "what does this code do?").
- Mechanical operations (renames, formats, file moves).
- You already have ≥95% confidence.

---

## Loading Constraints
This skill needs a live, responsive user. **Do not invoke in non-interactive contexts** like CI pipelines, scheduled runs, or autonomous loops. If you're in one of those and the ask is underspecified, flag that as a blocker for the user instead of guessing.

---

## The Process

### Step 1: Hypothesize, with a confidence number
Before asking anything, write down your current best read of what the user wants in **one sentence**, plus an honest confidence number (0–100%):
```
HYPOTHESIS: You want a way to answer "how are we doing?" in standup, and "dashboard" was the convention that came to mind.
CONFIDENCE: ~30% — missing: who it's for, what "metrics" means in context, and what success looks like.
```
When confidence is below ~70%, append a brief reason on the same line — what's still unresolved or missing.

### Step 2: Ask one question at a time, each with a guess attached
Format:
```
Q: <one focused question>
GUESS: <your hypothesis for the answer, with the reasoning that produced it>
```
Wait for the user to react before asking the next question.

**Why one at a time, not a batch:**
- The user can't react to your hypotheses if you bury them in a list.
- Batches encourage skim-reading and surface answers.
- The third question often depends on the answer to the first; asking them all at once locks in the wrong framing.
- The user's energy for thinking carefully is finite; spend it one question at a time.

### Step 3: Listen for "want vs. should want"
Watch for answers that pattern-match best-practice talk ("scalable", "clean architecture") or defer to convention.
When you hear these, ask:
> *"If you didn't have to justify this to anyone, what would you actually want?"*

### Step 4: Restate intent in the user's own words
When your confidence is high (≥95%), summarize the finalized requirements in a clear format and request confirmation before transitioning to the design or planning phase.
