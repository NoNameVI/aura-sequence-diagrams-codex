---
name: aura-sequence-diagrams
description: Create, revise, and review UML use-case sequence diagrams using the AURA Shore Store diagram conventions. Use for AURA diagrams or when a user explicitly wants the AURA sequence style; do not apply these project conventions to unrelated diagrams by default.
---

# AURA sequence diagrams

Use the bundled [AURA UC sequence profile](references/AURA_UC_SEQUENCE_PROFILE.md) as the rule source. It is a project convention, not a claim that UML requires the same layout. Read only the sections relevant to the request. For UML semantics and attribution, see [sources](references/SOURCES.md).

## Determine the context

1. Identify the use case, source revision, desired release, and whether the AURA project is available. Ask for missing behavior only when the available code or UC material cannot establish it.
2. In the AURA workspace, obey its `AGENTS.md`. Read `Code/AURA Shore Store/AGENTS.md` and `docs/CODEBASE_MAP.md`; check Cartographer freshness before relying on the map, then verify the actual source. Use the current controller, service, validator, repository, mapper, DTO, and template interactions to establish the trace. Do not infer behavior from an old diagram.
3. Outside that workspace, use the supplied code or UC specification as the behavior source. Treat AURA-specific paths, MySQL naming, release V9, and its build scripts as conditional project details. Do not claim to have run project gates or produced formats that are unavailable.

## Draw and review

- Keep one overview diagram per UC. Use `alt`, `opt`, `loop`, and `ref` according to the profile. Make guards, returns, and interaction boundaries unambiguous.
- Show relevant Actor, Boundary, Controller, Service, Repository, Mapper, and request/response DTO lifelines. Under the AURA profile, do not show Entity lifelines; represent their work through actual service, repository, or mapper exchanges. Use the actual database name outside AURA.
- Give visible messages and `ref` captions concise business or data-operation meanings. A short method call may help code traceability. Keep code bodies, HTTP routes, SQL, exception class names, and status codes out of visible labels.
- Name AURA referenced children `UC-<UC>-Part-<n>_<Functional_Description>`. Keep the Part ID in filenames and metadata, not in the visible `ref` caption. Maintain a single source for shared interactions.
- In the AURA workspace, use the selected release's scripts to build editable sources and rendered outputs. For V9, SVG is the canonical rendered artifact. Elsewhere, create only the requested formats that the available tools can actually produce.
- Review every fragment edge, guard, participant, activation, return, `ref` target, and legibility in the rendered diagram. Report unresolved findings.

## Final numbering gate

As the final pre-handoff action, compare numbering in the final source and every rendered or editable artifact being handed off. Check uniqueness, parent and operand scope, branch prefixes, return to the outer scope after fragments, caller/child `ref` prefixes, and notes without messages. Any later message, fragment, `ref`, or ordering edit invalidates the result and requires this gate again. Do not hand off a diagram with a confirmed numbering defect.

## Changing conventions

Change the bundled profile only when the user explicitly approves a rule change. Record the change in `VERSION` and `CHANGELOG.md`; distinguish new conventions from diagram defects. Updating this local skill does not authorize publishing or pushing to a remote repository. Follow the user's explicit request for any GitHub update.
