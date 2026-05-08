---
name: reveal-assumptions
description: Surface hidden assumptions made during work. Use this skill whenever the user asks to "reveal assumptions", "what did you assume", "what choices did you make", or any variation of asking Claude to be transparent about implicit decisions. Also trigger when the user says "assumptions check", "decision log", or asks Claude to audit its own reasoning. This skill should be used mid-task or retrospectively after work is done — any time the user wants visibility into choices Claude made without explicitly being told to.
---

# Reveal Assumptions

When triggered, audit your own recent work and surface every implicit decision, default choice, or unstated assumption you made that the user did not explicitly specify. The goal is radical transparency: the user should never be surprised by a silent choice you made.

## What counts as an assumption

An assumption is any decision you made where a reasonable alternative existed and you picked one without asking. Examples include but are not limited to:

- Default parameter values (learning rate, batch size, threshold, timeout)
- Data subset selection (filtering criteria, date ranges, which columns to use)
- Interpretation of ambiguous requirements ("sorted" → ascending? by which field?)
- Library or tool choices when multiple options exist
- File naming, directory structure, output format
- Error handling strategy (fail silently, raise, log and continue)
- Scope decisions (what you included or excluded from the task)
- Ordering or priority when the user didn't specify
- Edge case handling (nulls, empty inputs, duplicates)
- Style or convention choices (naming, formatting, architecture patterns)

## What to produce

For each assumption, state:

1. **What** — The assumption, stated plainly
2. **Why** — Why you chose this over alternatives
3. **Alternatives** — What you could have done instead

Separate each numbered assumption with a blank line so the list is easy to scan.

## After listing assumptions

After the full list, add a **"Requires attention"** section. Pick the single assumption (or small handful) most likely to cause incorrect results, silent bugs, or wasted effort if left unexamined. Briefly explain *why* it is the highest-priority item and what the user should check or decide.

When ranking severity for "Requires attention," use this priority hierarchy:

1. **Fabricated or unverified external facts** — Any time you guessed, recalled from memory, or generated metadata that should have been looked up (paper authors, dataset names, catalog descriptions, URLs, version numbers, API field names). These are the most dangerous because they look authoritative, propagate silently, and the user has no reason to doubt them. Always flag these first, even if they seem minor compared to a technical parameter choice.

2. **Assumptions that silently change results** — Filtering, subsetting, or transforming data in ways that alter what the user sees without any visible signal (e.g., dropping rows, clipping ranges, sentinel value handling).

3. **Technical parameter choices** — Bin counts, thresholds, normalization, etc. These matter but are usually visible in the output and easier to catch.

## Rules

- **Be exhaustive.** Go back through everything you've done in the current task and surface *every* implicit decision. Err on the side of over-reporting. The user can dismiss entries that don't matter to them — but they can't act on assumptions they don't know about.
- **Be honest about uncertainty.** If you made a choice because you weren't sure and just picked something, say so. "I wasn't confident either way and defaulted to X" is a valid and useful entry.
- **No defensiveness.** Don't justify your choices — just state them. The point is to give the user the information they need to decide whether your choices were the right ones.
