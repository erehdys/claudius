# session guide for Claude

Every Claude Code session loads this file. It is pointers and imports only;
the substance lives in the canon documents below. Copy it into a project,
keep the imports of the law modules the project follows (PHILOSOPHY.md
names them), and fix the paths to where the project keeps its documents.

## The laws, loaded every session

@../claude_mds/laws/WORK.md
@../claude_mds/laws/CODE.md
@PHILOSOPHY.md

<!-- add the ones PHILOSOPHY.md names: @../claude_mds/laws/CODE-WEB.md,
     @../claude_mds/laws/CODE-C.md, @../claude_mds/laws/UI.md,
     @../claude_mds/ruhe_principles.md for a solo project -->

When a change and a law conflict, the law wins or the law is amended in the
same change set: a general law in its module in `../claude_mds/laws/`, a
project law in `PHILOSOPHY.md`.

## Read before working

- `docs/specs/` — how every feature is supposed to work, one document per
  feature; `docs/specs/README.md` is the index. Read a feature's spec before
  changing it; change the spec in the same change set.
- `PROVENANCE.md` — who wrote each file and what has actually RUN. Code that
  no scenario exercises is a draft, whoever wrote it.
- `RULINGS.md` — OPEN rulings, newest first. Prepend new assumptions.
- `CHANGES.md` — the sync log, newest first. Prepend an entry per change set.
- `FINDINGS.md` — what the work found: measurements, defects, surprises.
  Newest first. A RULINGS entry is ONE decision in a few lines, never a
  diary: what was found goes here, what was changed goes to CHANGES.md.
