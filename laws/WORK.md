# Laws of work

How we work in every project. A project's PHILOSOPHY.md names the modules
it follows; it never copies them. A law ruled in one project and true for
all moves here in the same change set; the project keeps only its example.

## Provenance (ruled 2026-10-11)

Every file is one of:

- **HAND** — written by the user, by hand.
- **AGENT-REVIEWED** — written by an agent; the user read it and approved it
  with informed consent, knowing what it does and what it assumes.
- **AGENT** — written by an agent and not yet reviewed line by line by the
  user. Decisions it embodies are the agent's, not the project's, until
  ruled.

Orthogonal to authorship:

- **TESTED** — Only TESTED code is tried. HAND code that never ran is a draft.

`PROVENANCE.md` is the ledger. A change set that touches a file updates its
row. An agent never confuses "HAND" with "tested" and never confuses
"ran once in a scenario" with "ruled correct".

## Certainty and valence (ruled 2026-10-20, suited; general 2026-10-21) — a corollary to Provenance

Provenance says who made a thing. Certainty says how sure we are that it
stays. Every feature carries one of four, in `CERTAINTY.md`:

- **ETERNAL** — ruled by the owner and proven in real use (real play, a
  client's review). It changes only by a new ruling that names it.
- **FIRM** — ruled by the owner; not yet proven in real use.
- **UNCERTAIN** — built without a ruling, a placeholder, a test of an
  idea, doubted by the owner, or moved or rebuilt twice. Two moves make
  anything UNCERTAIN, whatever it was.
- **EXPERIMENTAL** — ruled by the owner as for testing or fun only, not
  expected to earn or ship. It is kept running and nothing more: no
  polish, nothing built on it, the first to go (the user, 2026-11-03).

And one of three **valences**, what rides on it: HIGH, MID, LOW. Each
project says in its `CERTAINTY.md` what its three mean.

WHY (the user, 2026-10-21): agents take what exists as more important than
it is. They keep a placeholder because it is there, and build on it, and
then it can never go. Provenance says who made a thing, not whether it is
wanted; certainty says that.

The rules that follow:

1. Nothing new is stacked on an UNCERTAIN feature. What would depend on it
   waits, or is built as a part that can be lifted off.
2. The second move is the moment to stop. A feature about to be moved a
   third time is asked about (Intent before change), not built again.
3. The work order is highest valence, lowest certainty, most dependents in
   the task graph first. The graph (`ROADMAP.dot`) shows certainty as a
   node's border colour and valence as its weight.
4. Content and container are rated apart. Keep the content in one place,
   so a move costs the container only.
5. An agent reads the register before building on a feature, and updates
   its row in the same change set. Values an agent sets are proposals,
   marked so, until the owner rules.
6. NEVER BE AFRAID OF DELETING CODE OR BREAKING THINGS (the user,
   2026-10-21). A working thing that can never be edited or maintained is
   much worse than a broken one: suited was that, until the owner rewrote
   it as a lean React app. An UNCERTAIN feature in the way is deleted, not
   worked around.

What happened (suited): the join's steps were modals, then rows in the
game tab, then rows in the table browser, then a sheet over it, then rows
again — each built in full, none marked as unsettled, so each move rebuilt
whatever had been stacked on the last.

## Intent before change

When a request leaves room for interpretation, ask for the exact intent.
Never resolve ambiguity by assumption. The same bar applies to adding
anything unasked: no features nobody has proven they need, no guards against
edge cases never seen or shown possible. When an assumption was unavoidable
to keep moving, it is written down as an OPEN RULING in RULINGS.md, with the
alternative readings, and the user rules on it. An unruled assumption is not
design.

This holds for the smallest user-facing choice: which button joins a
blackjack duel, where a link is offered, what a table is called. Such a
choice is asked before it is built, not built and offered as a default.

## Confidence sets the cost of a change (ruled 2026-10-14)

Weigh the cost of a change by how confident you are that it matches the
FINAL and ULTIMATE design vision and intent. Not confident at all: do not
write a single line. Very confident: it is fine to demolish the entire
project and build it back up again. Between the two, the size of the change
follows the confidence, never the convenience.

## Build what you know, now; never a placeholder (ruled 2026-10-15)

Once you know exactly what you want or need, build it immediately, in full.
A placeholder built to keep moving costs twice: the rework when the real
thing comes, and an architecture shaped around the placeholder that does
not support the real thing. What happened: the full rewrite was put off
and attempted in parallel with incremental changes, and that failed; the
blackjack demo got a "challenge" button, link-only rooms and its own
nameplate layout, all replaced within days by the table system they stood
in for. So: what is known is built properly now; what is not known is
asked (Intent before change), not stood in for.

## Determining intent
When performing low level tasks that involve design and user intent, like writing code or editing layouts,
give short updates, and ask questions when going from one task to the next, or from one
function or struct to the next, to prevent unnecessary work and avoid wasting time

**How to apply:** one or two lines of text between steps (what was done, what
is next). At a boundary where a real choice exists, stop and ask one focused
question before writing the next piece. Do not batch many functions into one
silent change.

## Demolition
When a replacement is finished and shown to work, the thing it replaced is
removed in the same change set — unless explicitly ruled otherwise. A
superseded mechanism left standing is not backup, it is a second writer
with a stale gate. Outdated code is deleted as soon as it is outdated.

No half measures (ruled 2026-10-21, suited). When a direction is chosen,
the old thing goes in the same change: no toggle kept just in case, no
backup code path, no parallel tree of pages, no dark copy of a replaced
design. Before building, ask whether the change leaves two ways to do one
thing; if it does, remove the old way or stop and say so. Say it plainly
when the user proposes one too. A feature switch is only for what a ruling
keeps off in production, never a fallback for a design. What happened: an
/alpha and /classic split made a demo feel half broken, and two look-alike
popups shipped for one feature.

## Scenarios, not tests
Tests are rapidly made outdated while developing new features,
can fail to catch unexpected behavior due to it being nominally correct,
are extremely slow and bloated and may influence codebases to change
themselves just to make sure a test written months ago passes. Instead, we should
use scenarios to develop mechanics/features in. A scenario may state a question and a
few expected results in plain words; running a script should say whether they
hold. Nothing stores a log of a run. Do not add checks that pin down how a
mechanic works today; add a scenario that shows what it is for.

## Verification is spelled out

Never a bare "verified". A report lists what ran and what it checked:
`✓ move: 3 steps at 360 ms · ✓ reach: impact tick 32 · ✓ twostrikes:
second waits on capacity`.

## Every feature has a spec (ruled 2026-11-04, suited)
`docs/specs/` holds one living document per feature: what it is for, how
it behaves, every state it has as a text layout (UI.md, "Draw the whole
screen"), its rules with who set each one (`owner` or `agent`) and when,
and where the code is. A dated design or plan written before building is
not a spec; it is history. A change set that changes how a feature works
changes its spec in the same change set; one that touches a feature with no
spec writes it. `docs/specs/README.md` is the index of every feature and
says which have a spec. The spec says what a feature must do; RULINGS.md
keeps the open questions, CHANGES.md what was done.

## Deploy what is committed (ruled 2026-10, suited)
A deploy runs from a commit that is pushed. A request to deploy is a
request to commit and push first. What happened: a deploy ran from
uncommitted work, and a redeploy from the last commit would have lost it.

## Talking to the user
- A change report opens with one line (what changed, live or not, checked
  or not), then one bullet per part, each led by a bold label naming the
  part ("**Plates:** …"). The user scans the labels and reads one line
  (ruled 2026-10-29, suited).
- When the user writes to someone else, give an outline: the points, the
  figures, the question to ask. Never a message ready to paste; it reads as
  not theirs (ruled 2026-10-27, suited). Tighten their own draft only when
  asked.
- A list for someone else names the things and stops. No selling and no
  description after the name; the reader asks about the one he wants
  (ruled 2026-11-09, suited). The feature list for the owner went from

      8. **Card faces.** Classic, corners, fanned; raised or peeking; one set of faces for every game.

  to

      8. **Card faces.**
