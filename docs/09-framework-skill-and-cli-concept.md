# 09 — Framework Skill + CLI Concept (Service Lifecycle Automation)

## Goals

Dieses Konzept definiert einen **enterprise-tauglichen Framework-Skill + CLI-Ansatz** für den `workflow-operating-system`-Stack, damit Teams Service-Lifecycle-Aktivitäten standardisiert, sicher und reproduzierbar ausführen können.

Primäre Ziele:

1. **Service onboarding beschleunigen**
   - Neuen Service mit Basissetup in Minuten statt Tagen erstellen:
     - Reverse-Proxy-Route
     - Docker-Compose-Definition
     - Standardisierte Konfigurationsdateien
     - CI-Test-/Build-Template
2. **Service-Änderungen standardisieren**
   - Einstellungen pro Service (Ports, Env, Auth, Routing, Ressourcen) über deklarative Konfiguration statt ad-hoc Edits.
3. **Service-Landschaft transparent machen**
   - Alle Services inkl. Status, Versionen, Module/Funktionen und Schnittstellen auflisten.
4. **Projektänderungen über Service-Module orchestrieren**
   - Änderungen via
     - Framework-Module,
     - Funktions-Runner,
     - HTTP/REST-Operations
     automatisiert durchführen.
5. **Erweiterbarkeit sicherstellen**
   - Neue Module/Funktionen pro Service einfach ergänzen (Scaffold + Contract + Tests).
6. **Frontend-Änderungen integrieren**
   - Desktop/Mobile-Änderungen in Aurelia-Projekten mit klaren Migrations-/Kompatibilitätsregeln.
7. **Testqualität erhöhen**
   - Tests automatisch erzeugen/verbessern (Unit, API, Integration, Smoke) und in CI durchsetzen.

---

## Non-Goals

1. Keine vollständige Ablösung bestehender Betriebsplattformen (z. B. OpenShift-native Operatoren).
2. Kein „one size fits all“ Vollautomationsversprechen ohne manuelle Review-Gates.
3. Keine implizite Änderung produktiver Systeme ohne explizite Freigabe.
4. Keine Abhängigkeit von nur einem Frontend-Pattern; Aurelia v1/v2 Koexistenz bleibt möglich.
5. Kein Ersatz für Security/Compliance-Prozesse – das CLI ergänzt diese mit Audit-Trail.

---

## Architecture

## 1) High-Level Bausteine

- **wos CLI**
  - Entry point für Entwickler:innen, Architekt:innen, Ops.
  - Nutzt deklarative Manifeste + sichere Defaults.
- **Framework Skill (AgentSkill)**
  - Führt Benutzer durch standardisierte Workflows.
  - Übersetzt natürliche Sprache in valide CLI-Sequenzen.
- **Service Registry (Git-basiert + optional API)**
  - Single Source of Truth für Services, Module, Ownership, Versionen.
- **Template Engine**
  - Generiert neue Services/Module/Funktionen aus versionierten Templates.
- **Execution Layer**
  - Führt sichere Mutationen in Repos/Configs aus.
  - Optional HTTP-Actions gegen interne Service APIs.
- **Policy & Governance Layer**
  - Validiert Sicherheitsregeln, Naming, Auth, Netzgrenzen, Freigabeprozesse.

## 2) Service Architektur-Standards (verpflichtend)

### API-Standard
- Stil: **REST API** (ressourcenorientiert, konsistente Pfade, semantische HTTP-Methoden).
- Versionierung: `/api/v1/...` (später parallel v2 möglich).
- Fehlerformat: einheitliches JSON (`code`, `message`, `details`, `traceId`).
- Health/Readiness:
  - `/health/live`
  - `/health/ready`

### Security-Standard
- AuthN/AuthZ: **JWT** (kurzlebige Access Tokens, optional Refresh-Flows).
- Token-Prüfung als Middleware/Interceptor standardisieren.
- Rollen-/Scope-Konzept:
  - `service.read`, `service.write`, `admin` etc.
- Geheimnisse niemals in Git, nur über Secret Stores/CI-Injected Envs.

### Service-Struktur (Referenz)
```text
service-name/
  src/
    api/
    domain/
    infra/
    modules/
    functions/
  tests/
    unit/
    integration/
    contract/
  docker/
  compose/
  docs/
  service.yaml
```

## 3) Deployment-/Runtime-Layer

- **Docker Compose** für lokale/Integrationsumgebung.
- **OpenShift** für Enterprise Runtime (Dev/Test/Prod Projects).
- Proxy/Ingress-Regeln zentral und versioniert.

## 4) Frontend-Layer

- **Aurelia v1 (Bestand)** + **Aurelia v2 (Zielbild)**.
- Shared UI-Bausteine und API-Clients als versionierte Pakete.
- Desktop/Mobile-Konventionen in derselben Modul-Architektur (responsive + feature flags).

## 5) Version-Baseline (Startvorschlag)

- Node.js: **22 LTS**
- npm/pnpm: **pnpm 9+** (oder npm 10+ falls Standard vorgegeben)
- Docker Engine: **26+**
- Docker Compose Plugin: **2.29+**
- OpenShift CLI (`oc`): **4.16+**
- Aurelia:
  - v1: bestehende produktive Version je Projekt
  - v2: schrittweise Einführung für neue/modernisierte Module

---

## Command Surface

Vorgeschlagene Top-Level-Struktur:

```bash
wos service <subcommand>
wos module <subcommand>
wos function <subcommand>
wos project <subcommand>
wos frontend <subcommand>
wos test <subcommand>
wos governance <subcommand>
```

## 1) Service Lifecycle

```bash
wos service create <name> --template base-api --with-proxy --with-compose
wos service configure <name> --set key=value
wos service list [--json] [--env dev|test|prod]
wos service describe <name>
wos service validate <name>
```

- `create`: erzeugt Basissetup (proxy + compose + skeleton + tests).
- `configure`: ändert definierte Service-Settings (keine direkten Wild-West-Edits).
- `list/describe`: Transparenz über Portfolio.

## 2) Module & Functions

```bash
wos module add <service> <module-name> --type domain|integration|ui
wos module list <service>
wos function add <service> <function-name> --module <module-name>
wos function run <service> <function-name> --payload file.json
```

## 3) Projektänderungen via Module/Funktionen/HTTP

```bash
wos project apply <service> --module <module-name> --change-set changes.yaml
wos project call <service> --method POST --path /api/v1/tasks --body body.json
wos project sync <service> --from-registry
```

## 4) Frontend Desktop/Mobile

```bash
wos frontend change <service> --target desktop --spec ui-change.yaml
wos frontend change <service> --target mobile --spec ui-change.yaml
wos frontend migrate-aurelia <service> --from v1 --to v2 --scope module:<name>
```

## 5) Tests

```bash
wos test generate <service> --type unit|integration|api|smoke
wos test improve <service> --focus coverage|flaky|contract
wos test run <service> [--ci]
```

## 6) Governance

```bash
wos governance check <service>
wos governance diff <service> --against baseline
wos governance approve <change-id>
```

---

## Skill Design

## Ziel
Der Framework-Skill macht die CLI kontextsensitiv nutzbar und reduziert Fehlbedienung.

## Trigger-Szenarien
- „Neuen Service erstellen“
- „Service X konfigurieren“
- „Welche Services gibt es?“
- „Neues Modul/Funktion hinzufügen“
- „Desktop/Mobile UI anpassen“
- „Tests verbessern“

## Skill-Workflow (vereinfacht)

1. **Intent erkennen** (create/configure/list/change/test).
2. **Kontext laden** (Service Registry, `service.yaml`, Governance Rules).
3. **Plan erzeugen** (CLI-Kommandos + erwartete Dateiänderungen).
4. **Preflight checks**
   - Naming
   - JWT/REST-Konformität
   - Port-/Route-Konflikte
5. **Ausführung** in dry-run oder apply.
6. **Ergebnisbericht**
   - geänderte Dateien
   - betroffene Services/Module
   - Teststatus
   - nächste Schritte

## Skill-Ressourcenstruktur (Vorschlag)

```text
skills/framework-ops/
  SKILL.md
  references/
    architecture-standards.md
    jwt-rest-guidelines.md
    openshift-deployment.md
    aurelia-v1-v2-guidelines.md
  assets/
    templates/
      service-base/
      module-base/
      function-base/
  scripts/
    scaffold_service.sh
    scaffold_module.sh
    enforce_policies.js
```

---

## Templates/Resources

## 1) Service Template (`service-base`)
Enthält:
- REST Controller Skeleton (`/api/v1`)
- JWT Middleware/Guard
- Dockerfile + `docker-compose.yaml`
- Proxy Route/Ingress Template
- `service.yaml` Manifest (Owner, SLA, Dependencies, Ports)
- Test-Basis (Unit + API smoke)

## 2) Module Template (`module-base`)
Enthält:
- Modulvertrag (Inputs/Outputs)
- Error handling + Logging hooks
- Contract-Test-Skeleton

## 3) Function Template (`function-base`)
Enthält:
- idempotente Ausführungsstruktur
- Validierungs-/Policy-Hooks
- Beispiel-Payload + Test

## 4) Frontend Resource Kits
- Aurelia v1 Pattern Library (Bestand)
- Aurelia v2 Migration Recipes (neu)
- Responsive Tokens (Desktop/Mobile)

## 5) CI/CD Resource Sets
- Lint + Test + Coverage Gates
- Container Image Build
- OpenShift Deployment Manifeste
- Security Scan Hooks (SAST/Dependency Scan)

---

## Safety/Governance

1. **Default dry-run** für alle mutierenden Kommandos in Prod-Kontext.
2. **Role-based CLI permissions** (z. B. read vs write vs deploy).
3. **Policy as Code** (Pflichtprüfungen für REST/JWT/Secrets/Naming).
4. **Audit-Trail** je Kommando:
   - Wer
   - Wann
   - Was geändert
   - Ticket/Change-ID
5. **Approval Gates** für kritische Änderungen (Prod Routing/Auth/Schema).
6. **Rollback-Standard**: Jede Apply-Operation muss revertierbar sein.
7. **Environment Isolation**:
   - Dev/Test frei
   - Prod nur via freigegebenem Pipeline-Path.

---

## Rollout Phases

## Phase 1 — Foundation (2–4 Wochen)
- CLI-Grundgerüst
- `service create/configure/list`
- Basistemplates + Governance checks
- 2 Pilotservices onboarden

## Phase 2 — Modularization (4–6 Wochen)
- `module add`, `function add/run`
- Projektänderungen über change-sets + HTTP calls
- Erste OpenShift-Integration

## Phase 3 — Frontend & Migration (4–8 Wochen)
- Desktop/Mobile change commands
- Aurelia v1→v2 Migrationspfade für ausgewählte Module
- Shared UI/API-Paketierung

## Phase 4 — Quality & Scale (laufend)
- Test-Generation/-Verbesserung automatisieren
- Coverage-/Flaky-KPIs erzwingen
- Governance Reports für Management/Architekturboards

---

## KPIs

1. **Lead Time für neuen Service**
   - Ziel: von mehreren Tagen auf < 1 Tag
2. **Standardkonformität (REST/JWT/Struktur)**
   - Ziel: > 95% Services ohne Policy-Verletzung
3. **Automationsgrad bei Änderungen**
   - Anteil Changesets/CLI-basiert vs manuell
4. **Testabdeckung & Stabilität**
   - Coverage-Trend
   - Flaky-Test-Rate
5. **Incident-Rückgang durch Konfig-Fehler**
   - Ziel: signifikante Reduktion nach 2 Quartalen
6. **Migrationserfolg Aurelia**
   - Anteil v2-fähiger/modernisierter Module

---

## Risks

1. **Template Drift**
   - Unterschiedliche Teams weichen vom Standard ab.
   - Gegenmaßnahme: zentral versionierte Templates + Compatibility Matrix.
2. **Zu starre Governance**
   - Frust bei Teams, wenn Regeln unflexibel sind.
   - Gegenmaßnahme: policy tiers (strict/moderate/experimental).
3. **Legacy-Komplexität Aurelia v1**
   - Migration kann aufwändiger als geplant werden.
   - Gegenmaßnahme: strangler pattern + modulweise Migration.
4. **Tooling-Silo**
   - CLI ohne Skill-Nutzung oder umgekehrt.
   - Gegenmaßnahme: Skill als standardmäßiger Orchestrator über CLI.
5. **Security Debt bei HTTP-Automation**
   - Unsichere Tokens/Scopes.
   - Gegenmaßnahme: short-lived JWT + vault integration + scope minimization.

---

## Open Questions

1. Soll die Service Registry rein Git-basiert sein oder zusätzlich als API-Service laufen?
2. Welche Policy-Engine wird genutzt (OPA/Rego vs custom validator)?
3. Wie strikt ist der default Approval Flow für Test/Prod?
4. Welche Aurelia-v1-Module haben höchste Business-Priorität für v2-Migration?
5. Welche OpenShift-Standards sind bereits verbindlich (Namespaces, Quotas, NetworkPolicies)?
6. Wie wird Ownership modelliert (Team, on-call, cost center) im `service.yaml`?
7. Welche Mindest-Teststrategie gilt pro Service-Klasse (kritisch vs unkritisch)?
8. Soll das CLI Multi-Repo orchestration nativ unterstützen oder zunächst repo-lokal starten?

---

## Kurzfazit

Der vorgeschlagene Framework-Skill + CLI schafft einen pragmatischen, auditierbaren und skalierbaren Weg, um Services im Enterprise-Umfeld konsistent zu erstellen, zu ändern und zu betreiben. Durch klare Standards (REST/JWT/Struktur), standardisierte Templates (Docker/OpenShift/Aurelia) und Governance-by-default wird die Produktivität erhöht, ohne Sicherheit und Betriebsstabilität zu opfern.