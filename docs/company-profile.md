# Company Profile (Arbeitsstand)

> Strukturierte Faktensammlung für Entscheidungen im Workflow Operating System.
> Ziel: schnell aktualisierbar, klar, ohne Overhead.

## 1) Unternehmenskontext

- Fokus: Engineering-getriebene Produkt-/Plattformentwicklung.
- Zielbild: schnelleres, zuverlässigeres Delivery mit klaren Standards für Mensch + AI-Unterstützung.
- Arbeitsweise: iterativ, pragmatisch, mit hohem Automatisierungsanspruch.

## 2) Rolle & Verantwortungsrahmen (Danny)

- Treiber für Workflow-Modernisierung und technische Standardisierung.
- Verantwortlich für praktikable Leitplanken statt theoretischer Zielbilder.
- Schnittstelle zwischen Entwicklung, Betrieb und Stakeholder-Kommunikation.

## 3) Randbedingungen / Constraints

- Gewachsene Systemlandschaft mit historisch entstandenen Konventionen.
- Teilweise fehlende formale SWE-Prinzipien in Legacy-Bestand.
- Gleichzeitiger Druck auf Stabilität (laufender Betrieb) und Modernisierung.
- Teamkapazität begrenzt → inkrementelle Umsetzung notwendig.

## 4) Current Stack (Ist)

- IDE/Agent-Unterstützung: VS Code + GitHub Copilot
- Lokale Entwicklung: Docker
- Backend/API: PostgREST
- Plattform/Betrieb: OpenShift
- SCM-Ziellandschaft in Klärung: GitHub (aktuell), ggf. GitLab/Bitbucket/Azure DevOps
- Frontend-Landschaft: Aurelia v1 als Legacy-Basis

## 5) Target Stack (Soll)

- Modernisierte Frontend-Architektur mit schrittweiser Migration auf Aurelia v2.
- Entkoppelte Fachlogik mit klarer Schichtung (Domain/Application/Infrastructure/UI).
- Git-zentrierte Dokumentation als technische Source of Truth.
- Automatisierte Doku-/Patchnotes-Flows in CI/CD.
- Standardisierte, auditierbare Agent-Nutzung.

## 6) Tooling & Praktiken

- PR-basierte Änderungen mit kleinen Inkrementen.
- Versionierte Standards und Templates im Repository.
- KPI-orientierte Prozessverbesserung (Lead Time, PR-Durchlaufzeit, Rollback-Quote).
- Feature-Flags/gestufte Rollouts für risikominimierte Einführung.

## 7) Bekannte Entscheidungsfelder (offen)

- Ziel-SCM und Migrationskriterien.
- Doku-Betriebsmodell (Confluence vs Repo vs Hybrid) inkl. Ownership.
- Governance für Agent Hooks/Agent-Automation in Enterprise-Kontext.
- Priorisierung und Taktung der Aurelia-v1→v2-Migration.

## 8) Nächste Aktualisierung

- Dieser Profilstand sollte mindestens monatlich oder bei größeren Architektur-/Tooling-Entscheidungen aktualisiert werden.