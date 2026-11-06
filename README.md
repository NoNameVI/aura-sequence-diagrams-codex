# AURA sequence diagrams for Codex

[Tiếng Việt](README.vi.md) | English

This repository contains a Codex skill for creating and reviewing use-case sequence diagrams with the AURA Shore Store conventions. The bundled profile is version 2.3.0. These conventions are project choices, not universal UML requirements.

## Before installing

1. Ask the repository owner for access. This repository is **private**; GitHub may show 404 until your account has access.
2. Install Git and sign in to GitHub when Git asks. The commands below clone the private repository and copy only the skill into your personal Codex skills directory. They stop if the skill is already installed, so they do not overwrite a local version.

## Install on Windows (PowerShell)

Open PowerShell, copy the entire block, and press Enter:

```powershell
$repoDir = Join-Path $env:TEMP ('aura-sequence-diagrams-codex-' + [guid]::NewGuid().ToString('N'))
$skillDir = Join-Path $HOME '.agents\skills\aura-sequence-diagrams'
if (Test-Path -LiteralPath $skillDir) { throw "Skill already exists at $skillDir" }
git clone --depth 1 https://github.com/NoNameVI/aura-sequence-diagrams-codex.git $repoDir
if ($LASTEXITCODE -ne 0) { throw 'Git clone failed. Check repository access and GitHub sign-in.' }
New-Item -ItemType Directory -Force -Path (Split-Path -Parent $skillDir) | Out-Null
Copy-Item -LiteralPath (Join-Path $repoDir 'skills\aura-sequence-diagrams') -Destination $skillDir -Recurse
if (-not (Test-Path -LiteralPath (Join-Path $skillDir 'SKILL.md'))) { throw 'Installation check failed.' }
Write-Host "Installed: $skillDir"
```

## Install on macOS or Linux (Terminal)

Open Terminal, copy the entire block, and press Enter:

```bash
(
  set -eu
  repo_dir=$(mktemp -d)
  skill_dir="$HOME/.agents/skills/aura-sequence-diagrams"
  if [ -e "$skill_dir" ]; then echo "Skill already exists at $skill_dir" >&2; exit 1; fi
  git clone --depth 1 https://github.com/NoNameVI/aura-sequence-diagrams-codex.git "$repo_dir/repo"
  mkdir -p "$HOME/.agents/skills"
  cp -R "$repo_dir/repo/skills/aura-sequence-diagrams" "$skill_dir"
  test -f "$skill_dir/SKILL.md"
  printf 'Installed: %s\n' "$skill_dir"
)
```

Git may open a GitHub sign-in prompt during cloning. If cloning reports 404 or permission denied, verify that the GitHub account used by Git has access to this private repository.

## Check and use

Start a **new Codex chat** and ask:

```text
Use $aura-sequence-diagrams to review this use-case sequence diagram against the AURA rules.
```

For the actual AURA application, the user also needs the AURA workspace, its `AGENTS.md`, current code, UC material, and release build scripts. In another project, provide its code or UC specification and explicitly ask for the AURA diagram style. The skill will use project-specific paths and outputs only when available.

The owner publishes changes to this repository only after an explicit update request. Installing the skill does not enable automatic GitHub updates.
