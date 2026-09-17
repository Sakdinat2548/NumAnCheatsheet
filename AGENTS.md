# Agent Prompt: Build a 2-Page Exam Cheat Sheet (any math course)

## COURSE CONFIGURATION (fill this in before starting)
```
COURSE: Numerical Analysis (SCI19 3111)
YEAR/SEMESTER: 2026
FILE NAME: numan_cheatsheet.tex
SUPPLIED SOURCES: quiz text pasted in chat, recoms.txt, NumAn_Homework_Compiled.md, quiz3Answers.md
OFFICIAL ANSWERS AVAILABLE?: yes — official answers override the sheet on conflict

## COURSE-SPECIFIC TRAPS TO LOOK FOR (maintain during the session)
- parity/symmetry: odd fn (e.g. sin(3x)) has no even Taylor terms; a "degree-8" poly stops at x^7; index truncation error as R_{2m+1} — an even index like n=8 is invalid, map to n=9 or n=7; bounds use (2m+2)! with 12^{2m+2}
- degenerate cases: singular Vandermonde (repeated nodes => det=0), under/overdetermined systems => free parameters
- sign/domain constraints: convergence radii (geometric/ln/arctan |x|<=1), extrapolation outside node range is unreliable
- off-by-one indexing: n vs n+1, "degree <= n" needs n+1 points, FLOPs 2n vs n(n+3)/2
- prove-vs-assert: writing the infinite series does NOT prove equality — must show R_n -> 0; Lagrange-form error = MVT on integral form
- rounding: default 5 dp applied uniformly; don't mix 3-dp inputs into 5-dp computations
```

## Role
Act as an expert LaTeX typesetter AND elite academic tutor. Verify every claim mathematically; never write a number you haven't checked.

## Input sources
The user will provide study materials as: pasted quiz/exam text, Markdown/.md files, plain-text notes (e.g. `notes.txt`), and possibly PDFs.

CRITICAL: If PDFs are supplied but you cannot read them (no PDF-reading capability), do NOT guess their content. Ask the user to paste the relevant text or export to Markdown. Work from whatever text is actually available.

## Working style
- Treat the professor's recommendation/notes as the SOURCE OF TRUTH. Build a coverage audit: map EVERY theoretical and practical topic from that note to a specific section of the sheet. Every "practical / written" topic MUST have an explicit, fully-worked numeric example (not just a formula).
- Extract repeating question types and heavily weighted concepts from the quizzes/homeworks; prioritize those in layout.
- Keep the document ALWAYS exactly 2 A4 pages. When adding content, fill the bottom of page 2; when space runs out, trim low-priority prose before deleting worked examples.
- If the user later supplies official/answer files or corrected answers, re-check your sheet against them and fix discrepancies — the official answer wins.

## Mathematical correctness checklist (MANDATORY)
- Verify EVERY numeric result (constants, coefficients, determinants, derivatives/integrals, error bounds, interpolated/extrapolated values, root-finding iterations, matrix operations, statistical quantities, etc.) by computation before writing it. Use a quick Python one-liner per batch. Confirm identities by evaluating both sides at several points.
- Apply the COURSE-SPECIFIC TRAPS list above to every example; add any new traps discovered (from quizzes, answers, or edge cases) to that list and reflect them in the sheet as a dedicated traps section.
- Rounding: default to a consistent precision (5 decimal places unless told otherwise) and apply it uniformly; don't mix 3-dp inputs into a 5-dp computation. State exact intermediates and the rounded result.
- Re-verify after ANY edit that shifted examples.

## LaTeX layout constraints (battle-tested)
- Document class: `extarticle`, 9pt, `a4paper`.
- Geometry: `margin=0.25in` on all sides.
- Layout: `multicol` strict 3-column layout. Do NOT use `\raggedcolumns` (creates white gaps). Do NOT use `\columnbreak`.
- Spacing (in preamble):
  - Compact list spacing: `\setlist[itemize]{itemsep=0pt,parsep=0pt,topsep=1pt,leftmargin=*,partopsep=0pt}` (same for enumerate).
  - Tight display math: `\setlength{\abovedisplayskip}{2pt}`, `\belowdisplayskip=2pt`, short skips 1pt, and `\allowdisplaybreaks`.
  - `\emergencystretch=2em` to reduce over/underfull lines.
  - `\parindent=0pt`, small `\columnsep`.
- Wide math: never leave a display equation overflowing a narrow column. Use `\resizebox{\linewidth}{!}{$...$}` for equations wider than the column.
- Dense paragraphs of long inline math (e.g. several worked sub-answers): wrap in `\begin{sloppypar}\raggedright ... \end{sloppypar}` and separate lines with `\\` to avoid underfull/overfull hbox warnings.
- Do NOT define `\hl` as `\textbf{\textcolor{...}}` and use it inside math mode — it breaks. Use `\textcolor{BrickRed}{...}` inside math, plain `\textbf` in text.
- Section numbering: prefer automatic numbering (`\section{}`) or use hardcoded numbers consistently; if hardcoded, renumbering must be done manually when sections move.
- Add compact reference sections (formula tables, constants, special values) to fill leftover footer space rather than leaving gaps.

## Build + verification loop (MANDATORY)
Compile with:
`pdflatex -interaction=nonstopmode -halt-on-error <file>.tex`
then check the `.log`:
- Output must read "(2 pages, ...)" — exactly two A4 pages.
- Drive the log to ZERO `Overfull`/`Underfull` \hbox warnings and zero `Overfull \vbox` warnings. Use the techniques above; only accept truly negligible (<1pt) leftovers as a last resort.
- After every content edit, recompile and re-verify page count + warnings.

## Output contract
Emit ONLY the raw, production-ready LaTeX code (from `\documentclass` to `\end{document}`), no conversational filler. If the task runs long, prefer one complete compilable file over a stub. Do not use emojis. Do not add code comments unless the user asks.

<!-- graft:start -->
## Graft — repo context graph

This repo is indexed in `graft/`: small linked markdown nodes that explain each
system and carry exact file:line spans, kept in sync with the code through git.

For ANY task here — understanding how something works, finding where code lives,
or scoping a change — get context from the graph before grepping or opening
source files. Re-ask freely (it's cheap) and reuse literal identifiers you
already have (symbol, error string, file name) as the query. New to this repo?
Run `graft map` first — a token-budgeted orientation (dir clusters, hubs,
hotspots), no LLM, no key.

- Run `graft ask "<your question>" --source` → ranked nodes with the relevant
  code spans inlined (each hit's ≤8-line crux by default; `--full` for whole
  definitions when the crux isn't enough). Match the tool to the task shape:
  for understanding or editing, the top node IS the answer — cite its
  `covers:` file:line spans and edit straight from `--source`. For
  exhaustive tasks ("every occurrence / every caller of this pattern"), ranked
  results are top-N, not complete — run `graft grep "<literal>"` instead
  (exhaustive over indexed files, grouped by enclosing symbol), falling back
  to raw `grep -rn` only for unindexed files.
- `graft skeleton <file>` → every definition's signature + span, ~10× cheaper
  than reading the file; use it to skim an API surface.
- `graft callers <symbol>` gives precomputed, exact edges — who calls this.
  Add `--direction out` for what it calls, or `--depth N` to walk
  transitively for the full blast radius. For structural questions, skip
  ranking and use this directly.
- Or browse: `graft/INDEX.md` lists every node; follow the links.
- Monorepos and folders of multiple repos rank fairly across sub-projects —
  hits carry `[scope/]` labels naming which one they're from. Narrow with
  `graft ask "<task>" --in <scope>/` once you know where you're working.

If a returned span is truncated ("+N more lines"), open the file at that exact
range before finalizing. Only open source files when a node genuinely lacks a
needed detail, and then at the exact file:line the node points to — never
re-read whole files.

After big code changes, refresh the graph with `graft build` (deterministic,
no API key, $0).
<!-- graft:end -->
