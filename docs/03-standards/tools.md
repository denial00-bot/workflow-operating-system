# 03 — Standards: Tools

## Ziel

Werkzeuge sollen Verhalten standardisieren: gleiche Befehle lokal, in CI und bei Onboarding.

## VS Code (Pflichtkonventionen)

- Workspace-Einstellungen versionieren (`.vscode/settings.json`)
- Tasks für Kernabläufe:
  - `task: up` (Docker stack starten)
  - `task: test`
  - `task: lint`
  - `task: build`
- Extensions als Empfehlungsliste dokumentieren

## Copilot-Nutzung (opinionated)

- Copilot für Boilerplate, Testskelette, Refactoringvorschläge
- Kein blindes Accept bei Security-/Migrationsthemen
- Bei DB/Policy-Änderungen immer manuelle Verifikation

## Docker-Standards

- `docker compose` als lokaler Default
- deterministische Images (fixe Base-Tags, nicht `latest`)
- Healthchecks verpflichtend für App/DB
- lokales `.env.example` pflegen, keine Secrets committen

## Testing & Quality

- Lint und Tests müssen lokal und in CI identisch aufrufbar sein
- Minimalstandard:
  - Format/Lint
  - Unit-/Integrationstests
  - SQL-Migrations-Check

## SCM-Portabilität

Workflowregeln müssen übertragbar sein:

- Branching/Commit/PR-Standards unabhängig vom Anbieter
- CI-Jobs möglichst neutral modellieren (Shell + klare Inputs/Outputs)
- Plattform-spezifische Features optional kapseln

Siehe [Branching/PR/Release Workflow](../04-workflows/branching-pr-release.md).

## Tooling-Template

Standardisierte Team-Metadaten in [TOOLS.template.md](../../templates/TOOLS.template.md).
