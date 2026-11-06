# AURA sequence diagrams for Codex

This repository packages the AURA Shore Store UC sequence-diagram skill for another Codex user. It includes the approved AURA diagram profile (version 2.3.0). The profile is a project convention, not a general UML standard.

## Install

Copy the `skills/aura-sequence-diagrams` folder to one of these locations:

- Personal: `~/.agents/skills/aura-sequence-diagrams` (Windows PowerShell: `$HOME\.agents\skills\aura-sequence-diagrams`)
- One repository: `<repo>/.agents/skills/aura-sequence-diagrams`

Then start a new Codex chat and invoke `$aura-sequence-diagrams`, or ask for an AURA UC sequence diagram. Codex may detect the skill automatically from its description.

For GitHub-based installation, ask Codex's `$skill-installer` to install `skills/aura-sequence-diagrams` from this private repository. The installer must have access to the repository. Manual copying works without the installer.

## Scope

The bundled profile contains AURA-specific choices such as DTO lifelines, MySQL, numbering, A3 layout, `ref` naming, and V9 SVG output. Creating or auditing diagrams against the actual AURA application also requires access to the AURA workspace, its `AGENTS.md`, code, build scripts, and UC material. In another project, supply its code or UC specification and explicitly request the AURA diagram style; project-specific paths and outputs then apply only where available.

The source AURA workspace and this distribution repository are separate. Changes here are published to GitHub only when the owner explicitly requests an update.
