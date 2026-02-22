# Workflow Operating System (Danny)

Dieses Repository definiert ein **praktisches, versionierbares Betriebssystem für Engineering-Workflows** rund um:

- VS Code + GitHub Copilot
- Docker-basierte lokale Entwicklung
- PostgREST-Anwendung
- OpenShift als Produktionsplattform
- mögliche SCM-Zielplattformen: GitLab, Bitbucket oder Azure DevOps

Ziel: Weniger Reibung, schnellere Releases, klare Standards für Mensch + AI-Agents.

## Struktur

- [01 Executive Summary](docs/01-executive-summary.md)
- [02 Zielarchitektur](docs/02-target-architecture.md)
- [03 Standards: Agents](docs/03-standards/agents.md)
- [03 Standards: Tools](docs/03-standards/tools.md)
- [04 Workflow: Branching/PR/Release](docs/04-workflows/branching-pr-release.md)
- [04 Workflow: Docs & Patchnotes Automation](docs/04-workflows/docs-and-patchnotes-automation.md)
- [05 Offene Fragen](docs/05-open-questions.md)
- [Roadmap (3 Wochen)](roadmap/implementation-plan-3-weeks.md)
- Templates:
  - [AGENTS.template.md](templates/AGENTS.template.md)
  - [TOOLS.template.md](templates/TOOLS.template.md)
  - [PR_TEMPLATE.md](templates/PR_TEMPLATE.md)
  - [conventional-commits.md](templates/conventional-commits.md)

## Arbeitsprinzipien (opinionated)

1. **Automatisierung vor Disziplin**: Was wiederholt passiert, wird skriptbar gemacht.
2. **Single Source of Truth**: Entscheidungen und Standards sind in Git dokumentiert.
3. **Kleine Änderungen, schnelle Reviews**: PRs < 400 Zeilen, klare Ownership.
4. **Release-Sicherheit**: Reproduzierbare Builds + Trennung von Dev/Staging/Prod.
5. **AI ist Copilot, nicht Autopilot**: Agenten liefern Entwürfe, Menschen entscheiden.

## Iterationsmodus (monatlich)

1. KPIs prüfen (Lead Time, PR-Durchlaufzeit, Rollback-Quote).
2. 1-2 Engpässe aus [Open Questions](docs/05-open-questions.md) priorisieren.
3. Standard/Workflow in kleinem PR anpassen.
4. Im nächsten Sprint messen, ob Verbesserung messbar ist.

## Definition of Done für Prozessänderungen

- Änderung in Doku + Template reflektiert
- Impact auf Dev/CI/CD klar beschrieben
- Mindestens ein konkretes Beispiel im PR
- Rückfallplan vorhanden
