# 02 — Zielarchitektur

## Architekturprinzipien

- **Code + Konfiguration versioniert** (Infra- und App-Änderungen nachvollziehbar)
- **Build once, deploy many** (gleiches Image durch Umgebungen promoten)
- **Explizite Qualitätsgates** (Lint, Test, Security-Checks)
- **Environment Trennung** (dev/staging/prod mit klaren Rechten)

## Sollfluss (End-to-End)

1. Entwickler arbeitet in VS Code + Docker lokal.
2. Branch erstellt (kurzlebig), Commits nach Konvention.
3. PR öffnet automatisierte Checks.
4. Nach Review/Merge: CI baut Container-Image + Signatur + SBOM.
5. CD deployed zuerst nach Staging (OpenShift), Smoke Tests laufen.
6. Promotion nach Prod über kontrollierten Gate (manuell/regelbasiert).
7. Release Notes und Patchnotes automatisch aus Git-Historie.

## Komponenten

### 1) Lokal: VS Code + Copilot + Docker

- Einheitliche Tasks für `lint`, `test`, `build`, `up`, `down`
- Optional Devcontainer für reproduzierbare Onboarding-Zeit
- Agenten erzeugen Code nur mit Test-/Dokupflicht

Siehe [Standards Tools](03-standards/tools.md) und [Standards Agents](03-standards/agents.md).

### 2) App-Layer: PostgREST

- API-Verhalten aus DB-Schema/Policies ableiten
- SQL-Migrationen als versionierte Artefakte
- Migrations-Reihenfolge in CI validieren

### 3) CI/CD & SCM

Unterstützt GitHub heute; migrationsoffen für:

- GitLab
- Bitbucket
- Azure DevOps

Anforderung: Workflow-Logik muss **SCM-portabel** bleiben (YAML/Jobs nicht zu plattformspezifisch schreiben).

### 4) OpenShift Runtime

- Image aus Registry deployen (keine lokalen Sonderbuilds in Prod)
- Secrets per Secret Management, keine Klartextwerte
- Rollout-Strategie mit schnellem Rollback

## Messgrößen

- Deployment-Frequenz / Woche
- Lead Time (Commit bis Prod)
- Change Failure Rate
- Mean Time to Recovery (MTTR)

Diese KPIs treiben Iterationen in [Roadmap](../roadmap/implementation-plan-3-weeks.md) und [Open Questions](05-open-questions.md).
