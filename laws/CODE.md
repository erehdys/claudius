# Laws of code

For code in any language. The language modules (CODE-C.md, CODE-WEB.md)
add to these.

Reference:
“The Exceptional Beauty of Doom 3's Source Code” — Shawn McGrath on id Software's C++ (http://web.archive.org/web/20130401084122/http://kotaku.com/5975610/the-exceptional-beauty-of-doom-3s-source-code).
"Clean" Code, Horrible Performance - Casey Muratori https://www.computerenhance.com/p/clean-code-horrible-performance
Data Oriented Design - https://en.wikipedia.org/wiki/Data-oriented_design
- **What code is**: 
All code is about accepting input data, mutating it and outputting other data.
To write performant, comprehensible and maintainable code, all possible inputs,
mutation paths and outputs need to be legible, finite and human-readable
- **Single source of truth**:
Every single system should have one place where a given data element is Mastered.
All other places don't write or edit that data element, and they explicitly
say their information is a flawed copy and specify when it was last reconciled
with the Master.
- **Hierarchy**
Strict hierarchy, the old HTML discipline: the ancestor determines
everything about its descendants. A descendant never decides something
about itself that its parent should own. Brutal, but a descendant deciding
silently in the wrong direction is how everyone dies. Corollary: empty files
are deleted on sight; if something breaks, that is the parent's fault for
relying on an empty file. Similarly, the ancestor determines all
interactions between its descendants. This means they don't have to
know anything about the rest of the world, they don't have to make calls
to other elements, they don't have to make calls to their Master, they 
just do what they were asked to do.
- **Separation of data and functions**
We don't do clown fiesta OOP like Animal:Dog>Bark(). A dog is a data struct
that stores information like bark_sfx and withers_height. It barks when 
its Master tells it to bark.
- **No null wearing a value's clothes.** Absent means absent: boundaries
check types explicitly (in JS `Array.isArray(flags)`, not truthiness), and an
unset override falls through to the decider — it never masquerades as a
configuration.
- **Minimize state and make it easily mutable**:
NO setters, NO getters, NO override layers. There is ONE state object per
concern; "setting" it MUTATES that object, and after an override there is
only the overridden state — never a shadow copy in the caller, never a
base-plus-patches stack a reader has to collapse in their head.
- **Don't try to fix bugs as they appear,  make them IMPOSSIBLE BY DEFINITION**
Weird machines suggest that every single state machine is going to be able to
create malformed abominations inside of itself, which will also have undesirable states of their own,
aka bugs, and so an infinite number of bugs is going to exist in a badly written
codebase by default. Instead of trying to reduce infinity to smaller infinity,
make sure your code has a finite number of clear states it can take, and 
each of those states is intentional and well-defined.
No test-driven development (ruled 2026-10-23). A test catches one malformed
state after the code can already reach it; the design removes the state.
We do not write the test first and grow code until it passes: we shape the
data so the wrong state cannot be written down. A test that remains is a
record of something that broke.
- **Fail very loudly: crash the whole program** (the user, 2026-10-31).
A broken invariant, an absent value read as present, an index out of
range: the program stops at once. Nothing logs and carries on, nothing
falls back to a guess. So a program that runs is a program in which
nothing went wrong. There are NO RUNTIME CHECKS: thousands of
re-simulations fit into 8.33 ms only without them (hvejs). The code is written so
that a bug crashes by itself, at no cost (absent is -1, never a valid index).
Drawing is the one exception (ruled 2026-11-02): a screen part that throws
while it draws crashes only itself. Its box turns into a red error panel
with the error text, the error goes to the server log, and the part draws
again on the next turn, street or hand. Drawing writes no state (the server
owns the hand, the seats and the money), so a broken part cannot make a
running program wrong. It can only end a demo. State, the engine, the
gateway and money still crash the whole program.
- **Code is self-documenting; comments are avoided whenever possible.**
A comment duplicates work at both write and read time; code that needs
one to be understandable should usually be rewritten instead.
The comments worth keeping are WHY-comments — decisions, repealed laws,
paid-for quirks — never WHAT-comments narrating the next line. When a
WHAT-comment appears necessary, that is the rewrite signal Doom 3 means.
While a codebase is iterating fast, new code carries no comments at all
but a one-line WHY for a quirk that already cost an outage or a bug
(ruled 2026-10-18, suited). Never a comment about what was removed,
replaced or used to be: that history is git's.
- **Locally coherent.** 
**Local code explains — or at least hints at — the overall system
design.** Reading any one place should teach you the shape of the whole.
This makes comments 
- **Legible control flow**
A tight loop in a highly performant application that runs every single frame
makes it obvious what data comes in, what happens to it and why, and what comes out.
Execution order is strict and deterministic, killing numerous classes of bugs before they spawn.
- **Reading code is MUCH harder than writing it**
Most of the work of a software engineer is READING and UNDERSTANDING code.
Make code EASY TO READ AND UNDERSTAND. Do NOT write 'clever' code.
You can confidently DELETE code, if it no longer runs and
has been made obsolete by something else. ADDING code is the thing that
potentially costs billions of manhours of extra work down the line,
multiplies bugs and unexpected behavior, and sometimes doesn't even provide any value.
So ADDING code is the decision you should be carefully debating, not REMOVING it.
LLMs spare humans thousands of hours of anguish and frustration by being able to
read giant bloated rotting codebases and turn them into streamlined and maintainable works of art.
- **Names say what a thing is** (the user, 2026-10-23). Lean towards
verbose, self-explanatory names: `carrier`, `wound_band`, `steps_left`,
never `w2`, `q`, `tmp`. A reader then holds no table from letters to
meanings in working memory, and an agent spends no tokens to work one
out again. A name is also a test: a variable that cannot be described
cleanly in human language is a sign of an antipattern, and it is
rewritten or deleted, not given a vague name. An index over a short,
obvious loop may stay `i`.
In suited's JavaScript: `walletBalanceMicroUsdg`, `seatsTakenAtThisTable`,
`handIdOfTheLastDeal`. A variable that cannot be described is a flag that
means two things, a half-built state, a value that is "this unless that":
it is replaced with data that can be named, not with a shorter name.
- **if / else, Kernighan & Ritchie (ruled 2026-10-30)**
A choice is written as `if` / `else`, braces on the same line:
```
if (condition1) {
  func1();
} else if (condition2) {
  func2();
} else {
  fallback();
}
```
It is easy to read, everyone knows it, and the whitespace carries the
structure: one condition per line, one branch per block, each editable
alone. Packing the same decisions into one line is goodharting a metric
(fewer lines) that benefits nobody. Clever code benefits only the person
screenshotting it. People who mock plain `if` / `else` are wrong.
  1. No ternary chains, ever: `a ? b : c ? d : e` becomes `if` / `else if`.
  2. No ternary with side effects, and none as a statement.
  3. A value picked by a condition is set by `if` / `else` (a `let`, or a
     small function that returns from each branch).
  4. A lookup object (`{ f: 'fold', c: 'call' }[w]`) is data, not a branch,
     and stays where it reads better.
  5. No body on the line of its head (the user, 2026-11-14): `if`, `for`,
     `while`, `else`, a `switch` case, a match arm, a function, a method and a lambda put
     their body on lines of their own. In GDScript, `a if c else b` is a
     ternary and becomes a block.
  6. WHITESPACE DRAWS THE GRAPH (the user, 2026-11-14). Written this way,
     a function is its own control-flow graph, drawn in text, the same
     graph a Graphviz file draws:
     - one `if` is one decision, a diamond. Its block is the "yes" edge;
       its `else`, or the next line, is the "no" edge.
     - The indentation is the depth in the graph: a line stands as far
       from the margin as the number of decisions it waits on.
     - An `else if` chain is a column of diamonds, each one asked only
       when every one above it said no.
     - A `return`, `continue` or `break` is an edge out of the graph, an
       oval. Guard clauses at the top cut the side branches off early, so
       the main path stays at the left margin and at the bottom: the
       spine of the graph.
     - Reading down the page is following the edges.
     A ternary hides a diamond inside an expression, and a body on the line
     of its head hides a node: the graph is still there, but the eye does
     not see it. Deep nesting is a wide graph; a guard clause or a function
     of its own makes it narrow again. THE TEST: draw the function as a
     `.dot` (a diamond per `if`, a box per statement, an oval per exit). A
     shape in the drawing that the text does not show is a reason to
     rewrite the text.
This supersedes "Ternaries: one choice, two values" (2026-10-27).
- **Document order beats DRY**
A layout written as a list, in the order things appear on screen, run on the
machine or sit in memory, is an invariant a reader can check. Deduplicate
VALUES (one template per card, one colour per name); never deduplicate
STRUCTURE at the cost of its order.

- **WE ALWAYS VENDOR OUR DEPENDENCIES.** Every font, library, runtime and
trace lives in this repo as the bytes we ship — no package managers in the
serving path, no registry fetch between us and a working page. A project
reopened after weeks must run EXACTLY as it was left; "urgent client work"
must never begin with debugging someone else's resolver (the Ruby lesson:
a gem graph and a libpq build error own your morning, not you). A new dependency is admitted by copying its
built artifact in, pinned, with its origin and version noted beside it.

Reference: “Always vendor your dependencies” — Valigo (Valentin
Ignatiev), https://youtu.be/s7uji5kJakI. The law above IS its thesis. The
cautionary line behind it: ecosystems that made the resolver the centre of
the workflow (Rails and its gem graph, Homebrew) rotted from exactly
there — a project's ability to RUN must never be custodied by
infrastructure that can drift while you sleep. Corollary for us: the
serving path contains only files in this repo, and a dependency is a FILE
we adopted, not a name we request.
