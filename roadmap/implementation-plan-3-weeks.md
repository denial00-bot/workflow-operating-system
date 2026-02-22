# Implementierungsplan (3 Wochen)

## Ziel

In 3 Wochen einen stabilen, messbaren Workflow-Standard live bringen.

## Woche 1 — Standards setzen

### Outcomes

- Dokumente und Templates aktiviert
- Branching-/PR-Regeln verbindlich
- Conventional Commits eingeführt

### Tasks

1. Team-Kickoff (60 Min): Zielbild + Rollen
2. PR-Template im Repo aktivieren
3. Commit-Konvention kommunizieren + CI-Check hinzufügen
4. AGENTS/TOOLS je Teamkontext aus Templates ableiten

### Erfolgskriterien

- 100% neuer PRs nutzen Template
- Neue Commits folgen Standard

## Woche 2 — Automation aufbauen

### Outcomes

- Patchnotes automatisch generiert
- Doku-Gates für relevante Änderungen aktiv
- Staging-Releaseprozess vereinheitlicht

### Tasks

1. Release-Job für Notes/Changelog konfigurieren
2. Label- oder Dateipfad-basierte Doku-Pflicht einführen
3. Smoke-Tests nach Staging-Deploy etablieren

### Erfolgskriterien

- Jede Staging-Auslieferung erzeugt nachvollziehbare Notes
- Kein Merge ohne CI + Doku-Check (wenn relevant)

## Woche 3 — Stabilisieren & messen

### Outcomes

- KPI-Baseline erhoben
- Engpässe identifiziert
- Verbesserungszyklus aktiviert

### Tasks

1. KPI-Dashboard mit 4 Metriken (Lead Time, Deploy-Frequenz, CFR, MTTR)
2. PR-Retrofit + Release-Retrospektive
3. Top-2 Verbesserungen für nächsten Zyklus planen

### Erfolgskriterien

- Baseline liegt vor
- Konkrete Folge-Maßnahmen mit Owner + Termin existieren

## Risiken & Gegenmaßnahmen

- **Widerstand gegen neue Regeln** → klein starten, Nutzen sichtbar machen
- **Zu viel Paralleländerung** → Fokus auf 1–2 Hebel pro Woche
- **Tool-Lock-in** → Standards SCM-neutral halten

## Nächster Zyklus (Woche 4+)

- Wiederholen: messen → Engpass wählen → Standard anpassen → erneut messen.
Referenz: [Open Questions](../docs/05-open-questions.md)
