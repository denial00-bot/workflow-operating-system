# 05 — Offene Fragen

Diese Fragen sollten priorisiert und innerhalb der nächsten 2–4 Wochen entschieden werden.

## SCM-Ziellandschaft

1. Bleibt GitHub mittelfristig oder ist Migration geplant?
2. Falls Migration: GitLab vs Bitbucket vs Azure DevOps — nach welchen Kriterien?
3. Welche Compliance-/Audit-Anforderungen sind entscheidend?

## CI/CD Ownership

1. Wer besitzt Pipeline-Logik fachlich und technisch?
2. Gibt es eine verbindliche Freigabematrix für Prod?
3. Wie werden Secrets zentral verwaltet?

## PostgREST & Datenbankprozesse

1. Wie werden Migrationen versioniert und reviewed?
2. Gibt es eine klare Policy für Breaking API/Schema Changes?
3. Welche Testtiefe ist vor Prod verpflichtend?

## OpenShift-Betrieb

1. Welche Rollout-Strategie ist Standard (Blue/Green, Canary, Rolling)?
2. Gibt es ein dokumentiertes, getestetes Rollback je Service?
3. Welche Observability-Metriken sind release-blocking?

## Team & Arbeitsweise

1. Wie strikt sollen PR-Größen limitiert werden?
2. Welche Agentenaufgaben sind erlaubt, welche tabu?
3. Welche KPIs werden verbindlich monatlich reviewed?

## Entscheidungsvorlage (pro Frage)

- Kontext
- Optionen
- Empfehlung
- Risiko
- Entscheidung + Datum + Owner

Hinweis: Ergebnisse in Standards/Workflows rückführen, damit Entscheidungen operativ wirksam werden.
