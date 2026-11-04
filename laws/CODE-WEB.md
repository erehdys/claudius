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

## Properties in groups (ruled 2026-10, suited_rewrite)
A rule lists its declarations in one order, so any property is found in
the same place in every rule:

```css
.fbet {
  /* layout */
    /* position */
    position: absolute;
    z-index: 888;

    /* dimensions */
    height: 3.5vh;
    min-width: calc(12 * var(--vhf));

  /* content */
    display: flex;
    justify-content: center;
    gap: 9px;
    padding: .2vh .7ch;
    white-space: nowrap;

  /* text */
    font-size: calc(3 * var(--vhf));
    letter-spacing: .14em;
    color: rgb(234, 230, 220);

  /* styling */
    border-radius: .5vh;
    background: var(--ink);
    box-shadow: 0 5px 14px rgba(0, 0, 0, .38);

  /* motion */
    transition: opacity .2s;
}
```

Custom properties come first. A rule of a few declarations keeps the order
on one line, without the labels. Within a group, a shorthand stays before
the longhands that refine it.

## What makes a box outgrow its parent (ruled 2026-11-04, suited)
These size a box past what its `width` and `height` say, or past its
parent, outside the arithmetic one expects. Each has cost a clipped or
overflowing box here:

- **padding** and **border** with a set `width` or `height`: the default
  `content-box` adds them on top (a `width: 100%` row with 18px of padding
  is the parent plus 36px). `box-sizing: border-box`, or no set width.
- **margin** on a `width: 100%` box: it adds outside.
- **min-width** / **min-height**: they beat `width`, `max-width` and
  `flex-shrink`. A flex item's default `min-width: auto` is its content's
  width, so a long name or a `nowrap` line pushes the row wider: give the
  item `min-width: 0`.
- **white-space: nowrap**, long unbroken words, and **letter-spacing**
  (it adds after the last letter too): the content sets the width.
- **1fr** grid tracks: `1fr` is `minmax(auto, 1fr)`, never narrower than
  its content. `minmax(0, 1fr)`.
- **gap** between fixed-size children: the sum is the children plus every
  gap.
- **vw** / **vh**: measured on the window, not the parent, scrollbars
  included.
- **transform**, **translate**, **box-shadow** and **outline** take no
  layout room but paint outside the box, where an `overflow: hidden`
  ancestor clips them.
