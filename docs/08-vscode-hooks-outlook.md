# 08 — VS Code Agent Hooks: Outlook & Einführungsempfehlung

## Aktueller Status

- Nach aktuellem Stand sind Agent Hooks in VS Code **Preview**.
- Referenzstand: **VS Code 1.109.3** (laut offizieller Dokumentation/Release-Stand im Kontext).
- Es gibt **kein verbindliches Datum** für General Availability (GA/stable).

---

## Einordnung (realistische Prognose)

Da kein offizieller GA-Termin vorliegt, ist nur eine bandbreitenbasierte Prognose sinnvoll.

Typisches Reifungsmuster bei VS-Code-Features:
1. Preview mit schnellen Iterationen und API-Änderungen,
2. Stabilisierung durch Telemetrie + Feedback aus Early Adopters,
3. graduelle Härtung (Dokumentation, Sicherheits- und Governance-Aspekte),
4. erst dann breiter Enterprise-Rollout.

**Reasoned Forecast:**
- Konservativ: 2–4 Minor-Releases bis „enterprise-tauglich“ für unkritische Use Cases.
- Für streng regulierte Umfelder eher später, abhängig von API-Stabilität und Auditierbarkeit.

(Kein hartes Datum; nur Entscheidungsrahmen.)

---

## Risikoanalyse für Enterprise

## Hauptrisiken

1. **API-/Verhaltensänderungen** in Preview-Phase.
2. **Unklare Governance** (wer darf welche Hooks ausführen).
3. **Sicherheits- und Compliance-Fragen** (Audit Trail, Datenpfade, Rechte).
4. **Vendor/Feature Drift**: Dokumentation und Implementierung ändern sich schnell.

## Mögliche Auswirkungen

- Pipeline-Instabilität, wenn Hooks kritisch verkettet sind.
- Zusätzlicher Betriebsaufwand für Pflege von Workarounds.
- Unsicherheit bei Security-Reviews.

---

## Risikoarme Einführungsstrategie

## Phase 1 — Controlled Pilot (jetzt)

- Nur nicht-kritische Aufgaben (z. B. Doku-Checks, Lint-Hinweise, PR-Assistenz).
- Klarer Nutzerkreis (Power User Team).
- Feature-Flag bzw. optionaler Einsatz, kein Produktionszwang.

## Phase 2 — Guarded Expansion

- Standardisierte Hook-Templates im Repo.
- Logging/Auditierbarkeit herstellen.
- Fallback-Prozesse definieren (wenn Hook fehlschlägt, geht Arbeit normal weiter).

## Phase 3 — Selective Standardization

- Erst nach Stabilitätsnachweis in mehreren Sprints.
- Kritische Workflows nur übernehmen, wenn:
  - API stabil,
  - Security-Abnahme dokumentiert,
  - Betriebsteam Ownership bestätigt.

---

## Konkrete Empfehlung

- **Nicht** als harte Enterprise-Baseline in der Preview-Phase einführen.
- **Ja** zu kontrollierten Piloten mit klaren Leitplanken und Messpunkten.
- Alle 4–6 Wochen Re-Evaluierung:
  - Breaking Changes,
  - Nutzen im Team,
  - Betriebsaufwand,
  - Security-/Compliance-Freigaben.

So wird Innovationsgeschwindigkeit genutzt, ohne unnötiges Betriebsrisiko.