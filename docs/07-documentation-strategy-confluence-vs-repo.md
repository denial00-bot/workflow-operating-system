# 07 — Doku-Strategie: Confluence vs. Repo/App-Dokumentation

## Kurzempfehlung

**Empfohlenes Zielmodell: Hybrid.**

- **Repo/App-Doku** ist die operative Source of Truth für alles, was mit Code, Architektur, Runbooks, ADRs und Release-Artefakten zusammenhängt.
- **Confluence** bleibt für Management-übergreifende Kommunikation, Onboarding-Navigation, Entscheidungsprotokolle mit breiter Zielgruppe.

Damit wird technische Genauigkeit hoch gehalten, ohne Stakeholder außerhalb der Entwicklung auszuschließen.

---

## Entscheidungslogik

## Wann Repo-Doku?

Nutzen, wenn Inhalte:
- direkt am Code hängen,
- versioniert/reviewt werden müssen,
- automatisierbar aus CI/CD erzeugbar sind,
- in PRs gemeinsam gepflegt werden.

Beispiele:
- ADRs, API-Contracts, Architekturdiagramme (textuell/diagram-as-code),
- Betriebsrunbooks, Migrationsleitfäden,
- Patchnotes aus Commits/PR Labels.

## Wann Confluence?

Nutzen, wenn Inhalte:
- viele nicht-technische Leser brauchen,
- bereichsübergreifende Abstimmung im Vordergrund steht,
- strukturierte Meeting-/Programm-Kommunikation notwendig ist.

Beispiele:
- Entscheidungsübersichten für Leitung,
- Programm-Roadmaps,
- übergreifende Prozessseiten mit Links auf Repo-Details.

---

## Hybrid-Modell (praktisch)

## Schicht 1: „Truth in Git“

- Technische Primärdokumente liegen im Repo unter `docs/`.
- Änderungen nur via PR.
- Definition of Done: Codeänderung ohne passende Doku-Änderung ist unvollständig.

## Schicht 2: „Distribution in Confluence“

- Confluence-Seiten sind kuratiert und verlinken auf Repo-Quellen.
- Kein Copy-Paste langer technischer Inhalte.
- Stattdessen: Zusammenfassungen, Entscheidungsstatus, Verantwortlichkeiten.

---

## Automatisierung: Machbarkeit & Optionen

## Heute sofort machbar (niedriger Aufwand)

1. **Repo → Confluence Link-Index**
   - CI erzeugt/aktualisiert eine Übersichtsseite mit Links auf relevante Markdown-Dokumente.
2. **Release Notes Automation**
   - Changelog im Repo generieren, Kurzfassung nach Confluence spiegeln.
3. **ADR-Register**
   - ADR-Liste aus Repo-Dateinamen automatisch bauen und in Confluence verlinken.

## Mittelfristig machbar (mittlerer Aufwand)

1. Markdown-zu-Confluence-Konvertierung (selektiv, für definierte Seiten).
2. Qualitäts-Gates in CI:
   - fehlende Doku bei Codeänderung warnen/blockieren,
   - veraltete Links erkennen.
3. Label-basierte Synchronisation (z. B. nur `publish-confluence`).

## Grenzen / Risiken

- Vollsynchronisation in beide Richtungen erzeugt Konflikte und Ownership-Unklarheit.
- Empfehlung: **Einwegfluss bevorzugen** (Repo primär → Confluence sekundär).

---

## Praktischer Workflow (iterationstauglich)

1. Entwickler ändern Code + Repo-Doku im gleichen PR.
2. CI prüft Doku-Regeln (Datei vorhanden, Links gültig, optional Frontmatter).
3. Nach Merge:
   - Confluence-Übersicht wird automatisiert aktualisiert,
   - optional Kurz-Zusammenfassung per Template.
4. Monatlich: Doku-Review (Top 10 Seiten nach Zugriff / Incident-Relevanz).

---

## Betriebsregeln

- Jede Seite hat Owner + Review-Intervall.
- Veraltete Confluence-Seiten bekommen sichtbares Banner („nicht Source of Truth“).
- Keine kritischen Betriebsanweisungen ausschließlich in Confluence.

---

## Konkrete Empfehlung

- **Jetzt starten** mit Hybrid-Modell + Einweg-Automation von Repo nach Confluence.
- Nach 6–8 Wochen KPI-Review:
  - Zeit bis Doku-Update nach Codeänderung,
  - Anzahl Inkonsistenzen zwischen Plattformen,
  - Nutzungsfeedback von Tech- und Non-Tech-Teams.