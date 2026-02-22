# 03 — Standards: Agents

Ziel: AI-Agents beschleunigen Arbeit, ohne Qualität, Sicherheit oder Nachvollziehbarkeit zu opfern.

## Rollenmodell

- **Builder-Agent**: erstellt Entwürfe (Code, Doku, Refactorings)
- **Reviewer-Agent**: prüft gegen Checklisten, erzeugt Findings
- **Release-Agent**: erstellt Patchnotes, Release-Checks, Migrationshinweise
- **Human Owner**: finaler Entscheider, accountable für Merge/Release

## Verbindliche Regeln

1. Kein direkter Push auf `main` durch Agenten.
2. Jeder Agent-Output ist ein Artefakt im PR (Diff, Begründung, Tests).
3. Bei Unsicherheit: explizite Open Questions statt impliziter Annahmen.
4. Sicherheitskritische Änderungen benötigen menschliche Zweitprüfung.
5. Agenten sollen **kleine, reviewbare** Änderungen vorschlagen.

## Prompt-/Task-Contract (Mindestfelder)

- Kontext (Stack, Ziel, Einschränkungen)
- Scope (was ändern, was nicht)
- DoD (Tests, Doku, Rollback-Hinweis)
- Output-Format (Dateien, Checkliste, Risiken)

Template: [AGENTS.template.md](../../templates/AGENTS.template.md)

## Qualitätsgates für Agentenbeiträge

- Lint/Test erfolgreich
- Architektur-/Security-Risiken genannt
- Dokumentation aktualisiert (wenn Verhalten geändert)
- Commit-Messages nach Konvention

Siehe [conventional-commits](../../templates/conventional-commits.md) und [PR Template](../../templates/PR_TEMPLATE.md).

## Anti-Patterns

- „Big Bang“-PR aus Agentenlauf
- Kein Test, nur Behauptung
- Versteckte implizite Entscheidungen
- Prompt ohne Nicht-Ziele

## Empfehlung (opinionated)

- Max. 1 fachlicher Schwerpunkt pro Agenten-Task.
- Erst Doku-/Plan-PR, dann Implementierungs-PR bei größeren Änderungen.
- Agenten-Output wie Junior-Dev behandeln: hilfreich, aber reviewpflichtig.
