# 04 — Workflow: Docs & Patchnotes Automation

## Warum das wichtig ist

Wenn Doku und Release Notes manuell bleiben, sinkt Konsistenz mit jeder Iteration. Deshalb: **Commit-Semantik + CI-Automation**.

## Konvention

- Conventional Commits als Pflichtstandard
- PR-Template erzwingt Impact-Dokumentation
- Changelog/Patchnotes aus Commits + PR-Metadaten generieren

Siehe [conventional-commits](../../templates/conventional-commits.md) und [PR Template](../../templates/PR_TEMPLATE.md).

## Minimal-Implementierung

1. Commitlint/Regex-Check in CI
2. Changelog-Generator im Release-Job
3. Automatisches Erstellen von:
   - Patchnotes pro Release
   - Liste von Breaking Changes
   - Migrationshinweisen (falls `db`, `migration`, `breaking` erkannt)

## Doku-Drift verhindern

- PR darf nicht mergen, wenn relevante Doku nicht angepasst ist
- Trigger via Label oder Dateipfad-Regeln (z. B. `docs-required`)
- Bei API/DB-Änderungen: verpflichtende „Impact“-Sektion im PR

## Empfohlener Release Output

- Version + Datum
- Zusammenfassung nach Typ (`feat`, `fix`, `perf`, `docs`, `chore`)
- Breaking Changes separat
- OpenShift Deployment-Hinweise
- Rollback-Hinweis

## Schneller Start

- Diese Woche: nur Commit-Standard + PR-Template erzwingen
- Nächste Woche: automatische Patchnotes einführen
- Danach: Doku-Gates verfeinern

Roadmap siehe [3-Wochen-Plan](../../roadmap/implementation-plan-3-weeks.md).
