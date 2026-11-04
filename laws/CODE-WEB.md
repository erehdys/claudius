# Laws of web code (JavaScript, HTML, CSS)

With CODE.md.

## if / else in JSX
With "if / else, Kernighan & Ritchie" in CODE.md. Where a statement
cannot stand, compute the choice above the `return` with `if` / `else` and
render the variable. `cond && <X />` is not a choice and stays.

## State rides data
- A thing's IDENTITY is its class; its STATE is a `data-*` attribute (an
  enum as `data-x="name"`, a boolean as `data-x="1"`), styled by the sheet.
  Never a class variant per state: every applier grows its own gate, and one
  is always wrong.
- Logic ships what is true (data attributes, custom properties for
  continuous values); the stylesheet says what that looks like. A value
  carrying `property: value` with units or colours is a bug by definition.
- A name the stylesheet keys on exists AS WRITTEN in the markup or logic,
  never minted by string interpolation (`lf-${flag}`): grep must find both
  sides.
- Layout is placements, never mode names: a set of flags each placing one
  control; a named bundle is a preset over the flags. Who decides is its own
  variable (`decidedBy: aspect_ratio | override`), never an `auto` value
  inside the thing decided.
- If CSS can decide it, CSS decides it: no resize listeners, measurements or
  layout flags for what a container's own width can express. Measuring is
  fine only for paint that reflows nothing.

## No manual JavaScript testing (ruled 2026-10-14, suited)
No hand-written probes in
the browser console or through browser automation to measure or poke the
page. It is very inefficient, and nothing of it is kept. A behaviour worth
checking gets a scenario; a look is checked by the user's eye.

## In-browser testing is the user's (ruled 2026-10-15, suited)
The agent does not
open the browser pane, drive the page, or take screenshots to check its
own work. It compiles, runs the node scenarios and tests, and hands over
what to look at: the page, the steps, and what each step should show.

Layout invariant checks are allowed (ruled 2026-11-03, suited): a script
that forces a size and reports what overlaps, or the least height that
holds everything, measured at rest. Never snapshots of animation frames,
never a probe kept as a test.

## Name the stylesheets first (ruled 2026-10, suited)
Before CSS work, say which stylesheets will change, and keep to that list.
The user edits styles at the same time, often in DevTools; two writers on
one sheet clobber each other. A sheet the user is editing gets asked about,
or the rules go in another sheet.
