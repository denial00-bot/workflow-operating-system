# Conventional Commits (Teamstandard)

## Format

`<type>(<scope>): <beschreibung>`

Beispiele:

- `feat(api): neue Filteroption für /orders`
- `fix(auth): token refresh bei 401`
- `docs(readme): setup-schritte ergänzt`
- `refactor(db): migration runner vereinfacht`

## Erlaubte Typen

- `feat` — neues Feature
- `fix` — Fehlerbehebung
- `docs` — reine Dokuänderung
- `refactor` — Strukturänderung ohne Feature/Fix
- `perf` — Performanceverbesserung
- `test` — Tests
- `build` — Build-/Dependency-Themen
- `ci` — Pipeline-Themen
- `chore` — Sonstige Wartung

## Breaking Changes

- Entweder `!` im Typ: `feat(api)!: endpoint umgestellt`
- Oder Footer: `BREAKING CHANGE: ...`

## Teamregeln (opinionated)

1. Subject in Präsens, klar, ohne Punkt am Ende.
2. Ein Commit = eine fachliche Absicht.
3. WIP-Commits vor Merge squashen.
4. Bei DB-/API-Impact Scope verpflichtend (`api`, `db`, `auth`, ...).

## Nutzen

- Grundlage für automatische Patchnotes
- Bessere Reviewbarkeit
- Konsistente Historie für Releases/Audits
