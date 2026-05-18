# Phase 1: Context Build

## Ziel

Erstelle fuer `<FEATURE_NAME>` einen vollstaendigen, belegten Feature-Kontext aus iOS und Android, sodass Phase 2 bis 5 kein neues fachliches Legacy-Discovery mehr brauchen.

## Input

Runtime-Parameter aus der aktuellen Chat-Eingabe:

| Parameter | Bedeutung |
|---|---|
| `FEATURE_NAME` | Feature-Bezeichnung aus dem Nutzerprompt |
| `FEATURE_SLUG` | abgeleitet nach `NAM-001` |
| `AGENT_ID` | Agent/Tool, zum Beispiel `codex`, `cursor`, `claude`; falls unbekannt `unknown-agent` |
| `RUN_ID` | neuer Run nach `artifacts/README.md`; falls nicht genannt, neu erzeugen |

Arbeitsquellen:

- Legacy iOS: `../ios-mobilebrowser/`
- Legacy Android: `../android-mobilebrowser/`
- Regeln: `rules/*.md`
- Base: `base/*.md`
- Contracts: `contracts/*.md`
- Templates: `templates/run_metadata.template.md`, `templates/11_feature_analysis.template.md` bis `templates/16_traceability_matrix.template.md`

Die Chat-Eingabe selbst ist nur der Ausloeser, kein fachlicher Inhalt ausser `FEATURE_NAME`.

## Output

Artefaktwurzel:

```text
artifacts/<feature-slug>/<agent-id>/<run-id>/
```

Erzeuge `run_metadata.md` aus `templates/run_metadata.template.md` und folgende Dateien in `phase_1/`:

| Artifact ID | Datei | Pflichtinhalt | Vollstaendig wenn |
|---|---|---|---|
| P1-A11 | `11_feature_analysis.md` | Feature-Scope, Suchbegriffe, relevante iOS/Android-Dateien, Boundary, Cross-Platform Summary | beide Plattformen durchsucht oder `NOT_PRESENT` belegt |
| P1-A12 | `12_code_facts.md` | Entry Points, Behaviors, State, Storage, API, Navigation, Error Paths, Dependencies, UI, Security | jede fachliche Zeile hat Quelle nach `REF-002` |
| P1-A13 | `13_test_definition.md` | testbare Behaviors, geplante `LT-*` Tests, Edge Cases, Coverage-Ziele, nicht testbare Punkte | jeder wichtige `BEH-*`/`STATE-*`/`ERRPATH-*` ist getestet oder begruendet ausgeschlossen |
| P1-A14 | `14_migration_mapping.md` | `MAP-*` fuer RN-Ziele, Services, Storage, API, State, Divergenzen, Dependencies | jedes relevante Code Fact hat Mapping oder Ausschlussgrund |
| P1-A15 | `15_execution_contract.md` | Testframeworks, Mocks, Commands, spaetere Phasenregeln, bekannte Build-/Test-Hinweise | Phase 2 bis 5 koennen ohne neues fachliches Discovery starten |
| P1-A16 | `16_traceability_matrix.md` | Source-ID zu Test-ID, Mapping-ID, RN-Ziel und Status | keine Source-ID aus `12_code_facts.md` ist orphaned |

Keine Codeaenderungen in Legacy- oder RN-Repositories.

## Regelbindungen

- `PC-001` bis `PC-009`
- `MC-001`, `MC-002`, `MC-004`, `MC-006`
- `GR-001` bis `GR-007`
- `REF-001`, `REF-002`, `REF-004`, `REF-005`
- `OUT-001` bis `OUT-009`
- `NAM-001`, `NAM-002`, `NAM-005`
- `VAL-GEN-01` bis `VAL-GEN-03`
- `VAL-P1-01` bis `VAL-P1-04`
- `ERR-REF-01`, `ERR-P1-01`, `ERR-P1-02`, `ERR-P1-03`
- `STOP-001` bis `STOP-004`

## Execution Steps

1. Run initialisieren.
   - Leite `FEATURE_SLUG` ab.
   - Lege `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_1/` an.
   - Kopiere die Phase-1-Templates in `phase_1/` und entferne `.template` aus dem Dateinamen.
   - Fuell `run_metadata.md` mit Agent, Modell, Prompt, Zeit und Artefaktwurzel.

2. Discovery planen.
   - Sammle Suchbegriffe aus `FEATURE_NAME`, UI-Begriffen, Klassen-/Methodennamen und bekannten Synonymen.
   - Suche in iOS und Android nach Code, Strings, Storage Keys, API Clients, Navigation und vorhandenen Tests.
   - Dokumentiere Suchbegriffe, Treffer und irrelevante Treffer in `P1-A11`.

3. Relevanz entscheiden.
   - Markiere Dateien als relevant, indirekt relevant oder out of scope.
   - Jede relevante Datei erhaelt `IOS-FILE-*` oder `AND-FILE-*`.

4. Code Facts extrahieren.
   - Erfasse die Pflichtkategorien aus `P1-A12`.
   - Verwende `N/A` nur, wenn eine Kategorie belegbar nicht existiert.
   - Widersprueche zwischen iOS und Android nicht aufloesen, sondern als Divergenz dokumentieren.

5. Testdefinition ableiten.
   - Erzeuge `LT-*` Testideen aus den Code Facts.
   - Formuliere Given/When/Then und erwartete Outputs.
   - Priorisiere Behavior, Branches, Error Paths, State und Storage/API Side Effects.

6. Migration Mapping erstellen.
   - Erzeuge `MAP-*` fuer RN-Codeziele.
   - Dokumentiere Reuse/Add/Adapt-Entscheidungen und RN-Dependencies.
   - Lege Platform Divergences mit RN-Entscheidung fest.

7. Execution Contract erstellen.
   - Dokumentiere, welche Informationen Phase 2 bis 5 verwenden muessen.
   - Notiere bekannte Testcommands oder `UNKNOWN` mit Grund.

8. Traceability konsolidieren.
   - Verknuepfe jede Source-ID mit Tests, Mappings und RN-Zielen.
   - Markiere Gaps als `BLOCKED`, wenn sie spaetere Phasen verhindern.

9. Self-Validation.
   - Fuehre alle Validierungsregeln aus dieser Phase durch.
   - Setze Artefakte auf `READY_FOR_REVIEW`, `BLOCKED` oder `FAILED`.

## Validationsregeln

| ID | Check | Fehler |
|---|---|---|
| VAL-P1-01 | iOS und Android durchsucht oder `NOT_PRESENT` belegt | ERR-P1-01 |
| VAL-P1-02 | Code Facts vollstaendig oder `N/A` begruendet | ERR-P1-02 |
| VAL-P1-03 | Spaetere Phasen koennen ohne fachliches Rediscovery arbeiten | ERR-P1-02 |
| VAL-P1-04 | Jede Code-Fact-ID steht in der Traceability Matrix | ERR-P1-02 |
| VAL-GEN-02 | Jede fachliche Aussage hat Quelle | ERR-REF-01 |

## Fehlerfaelle

| Fehler | Behandlung |
|---|---|
| ERR-P1-01 | STOP, Feature-Scope oder Suchbegriffe klaeren |
| ERR-P1-02 | STOP, fehlendes Artefakt oder fehlende IDs ergaenzen |
| ERR-P1-03 | STOP, iOS/Android-Divergenz als Mapping-Entscheidung dokumentieren |
| ERR-REF-01 | STOP, Quelle nachtragen oder Aussage entfernen |
