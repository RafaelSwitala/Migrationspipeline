# Phase 4: React Native Unit Test Migration

## Ziel

Migriere die validen Legacy-Unit-Tests aus Phase 2 nach Jest/React Native Tests in `../rn-e-mobilebrowser/`. Diese Phase erstellt und validiert Testcode, bewertet aber noch nicht final die RN-Implementierung. Die finale Ausführung und Interpretation passiert in Phase 5.

## Input

Runtime-Parameter:

| Parameter | Bedeutung |
|---|---|
| `FEATURE_NAME` | Feature-Bezeichnung aus dem Nutzerprompt |
| `FEATURE_SLUG` | identisch zum Phase-1-Run |
| `AGENT_ID` | identisch zum Phase-1-Run |
| `RUN_ID` | vorhandener Run; falls nicht genannt, den passenden reviewed Run wählen und dokumentieren |

Arbeitsquellen:

- Phase 1: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_1/`
- Phase 2: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_2/`
- RN-Projekt: `../rn-e-mobilebrowser/`
- Regeln: `rules/*.md`
- Base: `base/testing.md`, `base/validation_check.md`
- Templates: `templates/41_rn_test_plan.template.md` bis `templates/44_rn_test_readiness.template.md`

Phase 4 darf RN-Code lesen, um Imports und Testzugriffe korrekt zu setzen. Sie darf keine fachlichen Erwartungen neu erfinden.

## Output

Erzeuge folgende Dateien in `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_4/`:

| Artifact ID | Datei | Pflichtinhalt | Vollständig wenn |
|---|---|---|---|
| P4-A41 | `41_rn_test_plan.md` | `RT-*` Tests mit `LT-*` Quelle, Given/When/Then, Mocks, erwarteten Outputs | jeder valide `LT-*` hat Plan oder Skip-Grund |
| P4-A42 | `42_rn_test_mapping.md` | Legacy-Test zu RN-Test Mapping, Source IDs, RN-Ziel, Status | keine validen Legacy-Tests fehlen |
| P4-A43 | `43_rn_test_implementation.md` | erzeugte RN-Testdateien, Mocks, Test-IDs, geänderte Dateien | jede Testdatei ist dokumentiert |
| P4-A44 | `44_rn_test_readiness.md` | Jest-Konfiguration, Import-/Syntax-Check, bekannte Risiken für Phase 5 | RN-Tests sind ausführungsbereit oder Blocker dokumentiert |

Erzeuge oder aktualisiere RN-Testdateien in `../rn-e-mobilebrowser/`.

## Regelbindungen

- `PC-001` bis `PC-009`
- `MC-001`, `MC-003`, `MC-004`, `MC-006`
- `GR-001`, `GR-003`, `GR-006`, `GR-007`
- `REF-003`, `REF-005`
- `MIG-006`, `MIG-007`
- `TEST-004`, `TEST-005`, `TEST-006`
- `OUT-001`, `OUT-003`, `OUT-004`, `OUT-006`, `OUT-007`, `OUT-008`, `OUT-009`
- `VAL-P4-01` bis `VAL-P4-03`
- `ERR-P4-01`, `ERR-P4-02`

## Execution Steps

1. Pre-flight prüfen.
   - Stelle sicher, dass Phase-1- und Phase-2-Artefakte vorhanden sind.
   - Lies valide `LT-*` Tests und deren Ergebnisse.
   - Prüfe Jest/TypeScript-Konfiguration im RN-Projekt.
   - Lege `phase_4/` an.
   - Kopiere die Phase-4-Templates in `phase_4/` und entferne `.template` aus dem Dateinamen.

2. RN-Testplan erstellen.
   - Leite für jeden validen `LT-*` einen `RT-*` Test ab.
   - Dokumentiere Mocks, Inputs, erwartete Outputs und Quellen in `41_rn_test_plan.md`.

3. Testmapping erstellen.
   - Verknüpfe `LT-*` mit `RT-*`, Source IDs und RN-Dateien.
   - Markiere nicht migrierbare Tests als `SKIP` nur mit Grund.

4. RN-Tests implementieren.
   - Schreibe Jest-/React-Native-Testing-Library-Tests nach Projektkonvention.
   - Mocke Native/Expo APIs deterministisch.
   - Keine Tests für Verhalten ohne Phase-1- oder Phase-2-Quelle.

5. Readiness prüfen.
   - Prüfe Syntax, Imports und Test-Discovery, soweit lokale Commands verfügbar sind.
   - Führe keine interpretierende Erfolgsauswertung durch; diese gehört in Phase 5.

6. Reports erstellen.
   - Füll alle vier Phase-4-Artefakte.
   - Aktualisiere `run_metadata.md` mit Commands, Dauer, geänderten Dateien und Risiken.

## Validationsregeln

| ID | Check | Fehler |
|---|---|---|
| VAL-P4-01 | Jeder valide `LT-*` hat `RT-*`, `SKIP` oder Blocker | ERR-P4-01 |
| VAL-P4-02 | RN-Tests sind syntaktisch/importseitig bereit | ERR-P4-02 |
| VAL-P4-03 | Keine neuen fachlichen Erwartungen | ERR-P4-01 |
| VAL-GEN-02 | Jeder RN-Test referenziert Quelle | ERR-REF-01 |

## Fehlerfälle

| Fehler | Behandlung |
|---|---|
| ERR-P4-01 | STOP, fehlendes oder ungültiges Testmapping dokumentieren |
| ERR-P4-02 | STOP, Syntax-/Import-/Jest-Konfigurationsfehler dokumentieren |
