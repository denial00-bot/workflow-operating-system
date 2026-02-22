# 06 — Framework-Modernisierung: Aurelia v1 → v2

## Ausgangslage (Danny-Kontext)

- Das aktuelle Framework wurde ursprünglich von einem Geoinformatiker aufgebaut.
- Hohe Domänenkompetenz, aber wenig formale SWE-Methodik im initialen Design.
- Ergebnis: fachlich wertvoll, technisch aber teilweise schwer wartbar (starre Konventionen, implizite Abhängigkeiten, hohe Einarbeitungszeit).
- Ziel ist **keine Big-Bang-Neuentwicklung**, sondern eine iterative Modernisierung mit maximaler Wiederverwendung der Business-Logik.

---

## Zielbild

1. **Business-Logik bleibt stabil**
   - Kernregeln werden nicht „neu erfunden“, sondern entkoppelt und testbar gemacht.
2. **Weniger starre Konventionen**
   - Konventionen, wo sie helfen; explizite Architekturregeln, wo sie Sicherheit geben.
3. **Klare Schichten**
   - `domain` (fachlich), `application` (Use Cases), `infrastructure` (API/DB/UI), `ui` (Aurelia).
4. **Aurelia v2 als Plattform für Wartbarkeit**
   - Bessere Typisierung, modernere Patterns, klarere Testbarkeit.

---

## Modernisierungsstrategie (Business-Logik zuerst schützen)

## 1) Stabilisieren vor Migrieren

- Bestehende v1-Funktionalität in kritischen Pfaden erfassen:
  - Top-10 User-Flows dokumentieren
  - Ist-Verhalten mit Characterization Tests absichern
- Minimaler Qualitätsrahmen:
  - Linting + TypeScript strictness schrittweise erhöhen
  - Smoke-Tests pro PR

## 2) Entkopplungsschicht einziehen

- Fachlogik aus UI/ViewModels in Services/Use-Case-Klassen verlagern.
- Harte Framework-Abhängigkeiten in Adaptern kapseln.
- Ziel: Logik ist migrationsfähig, egal ob v1 oder v2 UI.

## 3) Strangler-Migration

- Neue/überarbeitete Module direkt in v2-Style bauen.
- Bestehende v1-Module nur anfassen, wenn Business-Change oder technischer Schmerz hoch ist.
- Routen/Features schrittweise umziehen statt Komplettumschaltung.

## 4) Betriebsfähiger Parallelmodus

- v1 und v2 koexistieren zeitlich begrenzt.
- Feature Flags pro Modul, um Rollout und Rollback steuerbar zu halten.
- Monitoring auf Fehlerquote, Ladezeit, User-Support-Tickets.

---

## Phasenplan Aurelia v1 → v2

## Phase A — Discovery & Guardrails (1–2 Sprints)

- Architektur-Inventory: Module, Abhängigkeiten, kritische Flows.
- Definition „Migrations-ready“ pro Modul:
  - Tests vorhanden
  - klare Schnittstellen
  - keine direkten Framework-Leaks in Domain-Logik
- Technische Leitplanken festlegen (siehe Guardrails).

## Phase B — Foundation (2–3 Sprints)

- Gemeinsame Kernpakete aufbauen:
  - Design Tokens/UI-Basis
  - shared services (auth, config, logging, api-client)
  - Testharness + CI Gates
- Referenzmodul als Pilot in v2 umsetzen.

## Phase C — Inkrementelle Feature-Migration (laufend)

- Priorisierung nach Business-Nutzen × Migrationsaufwand.
- Pro Sprint 1–2 Module migrieren.
- Nach jedem Modul: Metriken und Lessons Learned ins Vorgehen zurückführen.

## Phase D — Konsolidierung & v1-Decommission

- Alte Adapter entfernen.
- Doppelte Komponenten/Funktionen abbauen.
- Abschluss-Review: Performance, Stabilität, Wartbarkeit.

---

## Guardrails (nicht verhandelbar)

1. **Kein Modul ohne Basistests** in die Migration.
2. **Keine Big-Bang-Cutovers** für geschäftskritische Bereiche.
3. **Jede Migration ist reversibel** (Rollback dokumentiert).
4. **PR-Größe kontrollieren** (Richtwert < 400 LoC Nettoänderung).
5. **Architekturentscheidungen als ADR** im Repo festhalten.

---

## Häufige Anti-Patterns

- „Rewrite-Euphorie“: Alles neu bauen, ohne Geschäftswert.
- UI-Refactoring ohne Testnetz.
- Vermischung von Fachlogik und Framework-spezifischem Code.
- Migration nach Entwicklerpräferenz statt nach Produktpriorität.
- Fehlende Definition, wann ein Modul als „fertig migriert“ gilt.

---

## Quick Wins (0–6 Wochen)

1. Top-5 kritische Flows als Characterization Tests sichern.
2. Gemeinsamen API-Client + Fehlerbehandlung standardisieren.
3. Ein Pilotmodul in v2 mit sauberer Schichtung liefern.
4. PR-Template um Migrations-Checkliste erweitern.
5. Migrations-Kanban mit Status je Modul (`legacy`, `in-progress`, `v2`, `retired`) einführen.

---

## Konkrete Empfehlung

- **Empfohlen**: Inkrementelle Strangler-Strategie mit klaren Guardrails.
- **Nicht empfohlen**: Vollständiger Rewrite ohne schrittweise Validierung.
- Erfolgskriterium: Nach 3 Monaten messbar weniger Change-Friction (Lead Time, Bug-Rate, Onboarding-Zeit).