# AURA sequence diagram skill changes

## 3.1.0 — 2026-11-06

- Required every displayed synchronous call to open an activation on the receiving lifeline, including nested and self calls.
- Required each return or operation endpoint to close the corresponding activation independently in every `alt`/`opt` operand.
- Deferred non-semantic layout polishing until a dedicated formatting pass; content, branch structure, numbering and activation correctness remain the current V9 migration priority.

## 3.0.0 — 2026-11-06

- Changed visible message and `ref` numbering to require one trailing period immediately before the label, including hierarchical numbers such as `1.1.`.
- Required every UC actor set to come directly from the current `AURA_Backlog.xlsx` `Authorization` sheet; actor names are displayed without spaces, separated by `/`, and wrapped by role at `/` when needed.
- Required a nested `ref` frame to remain strictly inside its parent operand with visible padding on all four sides.
- Marked V9 source, Draw.io and SVG artefacts for migration and final QA under the new breaking conventions.

## 2.3.0 — 2026-11-06

- Extended referenced-child filenames from `UC-<UC>-Part-<n>` to `UC-<UC>-Part-<n>_<Functional_Description>` so files remain traceable and distinguishable without opening them.
- Required the filename description to carry the same concise business meaning as the visible `ref` caption while continuing to omit UC/Part identifiers from the frame itself.
- Defined SVG as the canonical V9 rendered artefact and removed PNG/PNG 4K generation from the V9 workflow; PlantUML, Mermaid, Draw.io and supporting metadata remain when used by the build and QA process.
- Kept historical V8 and earlier artefacts unchanged; migration applies to the new V9 release.

## 2.2.0 — 2026-11-06

- Approved the AURA branch-prefix numbering algorithm for `alt` and `opt`.
- Required each operand to start with its own numbered first message (`P.1`, `P.2`...) and subsequent messages to inherit that operand prefix (`P.1.1`, `P.1.2`...).
- Required numbering to return to the parent scope after `end`, and defined recursive application for nested fragments.
- Updated the final numbering gate and recorded the affected UC-13.2 v8 defect as pending migration; diagrams were not redrawn in this rule-only update.

## 2.1.0 — 2026-11-06

- Made numbering QA the highest-priority and mandatory final gate before every sequence-diagram handoff.
- Required numbering checks across source and rendered artifacts, including fragment scope, `ref` prefixes, parent steps, duplicates and notes without messages.
- Required the numbering gate to be rerun after any later message, fragment, `ref` or ordering change.

## 2.0.0 — 2026-11-05

- Updated the approved profile to breaking rule version 2.0.0: Entity lifelines and `«entity»` stereotypes are no longer used in AURA sequence diagrams.
- Kept relevant request/response DTO lifelines with `«dto»`; entity work is represented through Service/Repository/Mapper interactions or DTO results.
- Recorded removal of existing v8 Entity participants as a pending migration; this rule-only update did not redraw v8.

## 1.3.1 — 2026-11-05

- Clarified approved profile 1.2.1: method names and short method calls are the explicit exception to the no-code rule.
- Continued to prohibit code bodies/expressions, long declarations, HTTP routes, SQL, implementation exception names and HTTP status codes.

## 1.3.0 — 2026-11-05

- Updated the approved profile to rule version 1.2.0: visible sequence labels must not contain code syntax, method signatures, HTTP routes, SQL, implementation exception names or status codes such as 404/500.
- Required concise business or data-operation wording while retaining implementation traceability outside the visible diagram.
- Recorded migration of existing v8 labels as pending; this rule update did not redraw v8.

## 1.2.0 — 2026-11-05

- Updated the approved profile to rule version 1.1.0 for concise visible `ref` captions.
- Removed UC/Part identifiers and detailed parameter/result contracts from the visible `ref` caption; retained them in filenames, metadata and mapping documents.
- Recorded the v8 caption migration as pending; no v8 diagram was silently redrawn by this rule-only update.

## 1.1.0 — 2026-11-05

- Added a feedback intake log for new suggestions, prior accepted decisions, and confirmed v8 defects.
- Kept the approved profile at rule version 1.0.0; no unapproved numbering rule or diagram change was introduced.

## 1.0.0 — 2026-11-04

- Created the project skill around the existing approved AURA sequence profile without copying its rule text.
- Established `UC-<UC>-Part-<n>` for referenced child interactions while retaining names of main UC diagrams.
- Recorded the current v8 build and QA workflow; existing v5/v6/v7 releases remain historical.
