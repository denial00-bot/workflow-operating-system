# 04 — Workflow: Branching, PR, Release

## Branching-Modell (trunk-orientiert)

- `main` ist immer releasbar
- Feature-Branches kurzlebig (`feat/<ticket>-<slug>`)
- Hotfix-Branches nur für produktive Störungen
- Lebensdauer eines Branches ideal < 3 Tage

## PR-Regeln

- PR-Größe: bevorzugt < 400 geänderte Zeilen
- Mindestens 1 Reviewer
- Pflichtinhalte gemäß [PR_TEMPLATE](../../templates/PR_TEMPLATE.md)
- Merge nur bei grünem CI-Status

## Merge-Strategie

- Squash Merge als Default für saubere Historie
- Commit-Title folgt Conventional Commits
- Merge-Commit nur bei bewusstem Bedarf (z. B. Release-Train)

## Release-Regeln

1. Merges auf `main` erzeugen versionierbares Artefakt.
2. Staging-Deployment automatisch.
3. Produktionsfreigabe über Gate (manuell/approver-basiert).
4. Rollback-Prozedur dokumentiert und testbar.

## OpenShift-Integration

- Immutable image tags (`sha` oder SemVer)
- Environment-Konfiguration getrennt von Build-Artefakt
- Smoke-Test nach Deployment obligatorisch

## Governance

- Wöchentliches PR-Retrofit (Bottlenecks, Review-Zeiten)
- Monatlicher Release-Postmortem-Block (auch ohne Incidents)

Cross-Link: [Patchnotes Automation](docs-and-patchnotes-automation.md), [Zielarchitektur](../02-target-architecture.md)
