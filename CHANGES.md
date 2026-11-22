# Sync log

One entry per change set, NEWEST FIRST; prepend. Open rulings live in
RULINGS.md, not here.

## 2026-11-15 — a screen is sketched in Graphviz

UI.md, "Draw the whole screen before building it": a screen is sketched
as a `.dot` file (the text both edit), one HTML-like table with a cell
per region at its real size in pixels, rendered at 72 dpi and shown. It
replaces the box-drawing screen; a part, state by state, stays plain
text. From hvejs, the encounter screen (`__docs/gefecht.dot`). The
example in the law was rendered with Graphviz 12.2, no warning.

## 2026-11-15 — a control that cannot act is struck out, in its place

UI.md, "Controls are furniture": a control that cannot act now stays,
its words struck out and its border gone. The example is suited's lobby
bar, whose "watch" is struck out at a table with nothing to watch, as
the action bar's buttons are when it is not the player's turn.

## 2026-11-14 — a label displaces nothing

UI.md, new section "A label displaces nothing": a part that only says the
state keeps a place that is there with or without words; only a part the
user works with (a rail, a panel) may take room, and only from an edge of
the screen, never in the middle. From suited's blackjack table, where a
hint between hands moved the cards and the plates.

## 2026-11-14 — one worktree per session

WORK.md, "One worktree per session": a session that changes files works
in its own git worktree and branch; where sessions share a folder, each
commits its own files by path, and a file both changed waits for both.
From hvejs and hvejs_art, where two sessions changed the same docs.

## 2026-11-14 — pushed and deployed are two facts

WORK.md, "Deploy what is committed": a report says "pushed" for the git
remote and "deployed" for the site, each only when it happened. From a
suited report that said "pushed" where the site had been deployed.

## 2026-11-11 — agent text goes in a fold

WORK.md, new section "Agent text goes in a fold", from Simon Willison's
post of 2026-11-09: a short opener, the full agent text in
`<details><summary>model, effort</summary>`. The user chose where it applies
(PR and MR descriptions, issue and review comments, long chat reports,
CHANGES, FINDINGS, specs) and that the agent's opener is marked as the
agent's.

## 2026-11-09 — a list names the things and stops

WORK.md, "Talking to the user": a list written for someone else carries the
names and no description or selling; the card-faces line from suited's
PITCH.md is the example.

