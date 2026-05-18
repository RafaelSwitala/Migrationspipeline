# Phase 3: React Native Expo Feature Migration

## Ziel

Implementiere `<FEATURE_NAME>` in `../rn-e-mobilebrowser/` auf Basis von Phase 1. Diese Phase erzeugt RN-Produktionscode, aber keine RN-Tests.

## Input

Runtime-Parameter:

| Parameter | Bedeutung |
|---|---|
| `FEATURE_NAME` | Feature-Bezeichnung aus dem Nutzerprompt |
| `FEATURE_SLUG` | identisch zum Phase-1-Run |
| `AGENT_ID` | identisch zum Phase-1-Run |
| `RUN_ID` | vorhandener Run; falls nicht genannt, den passenden reviewed Run waehlen und dokumentieren |

Arbeitsquellen:

- Phase 1: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_1/`
- RN-Projekt: `../rn-e-mobilebrowser/`
- Base: `base/architecture.md`, `base/constraints.md`
- Regeln: `rules/*.md`
- Templates: `templates/31_rn_implementation_plan.template.md` bis `templates/33_rn_mapping_status.template.md`

Phase 2 ist fuer Phase 3 kein fachlicher Input.

## Output

Erzeuge folgende Dateien in `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_3/`:

| Artifact ID | Datei | Pflichtinhalt | Vollstaendig wenn |
|---|---|---|---|
| P3-A31 | `31_rn_implementation_plan.md` | `MAP-*` zu RN-Dateien/Symbolen, Reuse/Add/Adapt, Dependencies, Implementierungsreihenfolge | jedes `MAP-*` hat eine geplante Aktion |
| P3-A32 | `32_rn_code_report.md` | geaenderte RN-Dateien, erzeugte Symbole, Commands, Typecheck/Lint/Build-Ergebnisse, Fehler | jede Codeaenderung und jeder Command ist dokumentiert |
| P3-A33 | `33_rn_mapping_status.md` | Status pro `MAP-*`: `IMPLEMENTED`, `PARTIAL`, `EXCLUDED`, `BLOCKED`; Evidenz und Risiko | kein `MAP-*` fehlt |

Erzeuge oder aktualisiere Runtime-Code in `../rn-e-mobilebrowser/` gemaess Projektstruktur.

## Regelbindungen

- `PC-001` bis `PC-009`
- `MC-001` bis `MC-004`, `MC-006`
- `GR-001`, `GR-003`, `GR-004`, `GR-006`, `GR-007`
- `REF-003`, `REF-005`
- `MIG-001` bis `MIG-005`, `MIG-007`
- `ARCH-001` bis `ARCH-006`
- `CON-001`, `CON-003`, `CON-004`, `CON-005`
- `OUT-001`, `OUT-003`, `OUT-006`, `OUT-007`, `OUT-008`, `OUT-009`
- `VAL-P3-01` bis `VAL-P3-03`
- `ERR-P3-01`, `ERR-P3-02`, `ERR-P3-03`

## Execution Steps

1. Pre-flight pruefen.
   - Stelle sicher, dass RN-Projekt und Phase-1-Artefakte existieren.
   - Lies vorhandene RN-Struktur, `package.json`, TypeScript/Jest-Konfiguration und lokale Patterns.
   - Lege `phase_3/` an.
   - Kopiere die Phase-3-Templates in `phase_3/` und entferne `.template` aus dem Dateinamen.

2. Implementierungsplan erstellen.
   - Mappe `MAP-*` IDs auf konkrete RN-Dateien und Symbole.
   - Entscheide create/reuse/adapt nach `MIG-004`.
   - Dokumentiere Plan und Dependencies in `31_rn_implementation_plan.md`.

3. Code implementieren.
   - Implementiere Types, Services, Hooks, Components/Screens und Utils in passender Reihenfolge.
   - Keine Business-Logik in reinen Components.
   - Kein fachliches Verhalten ohne Phase-1-ID.

4. Dependencies behandeln.
   - Nutze vorhandene Libraries zuerst.
   - Neue Dependencies nur mit Begruendung und Installations-/Importnachweis.

5. Static Validation ausfuehren.
   - Fuehre verfuegbare TypeScript-, lint- oder buildnahe Commands aus.
   - Wenn Commands fehlen, dokumentiere `N/A` mit Grund.

6. Reports erstellen.
   - Fuell alle drei Phase-3-Artefakte.
   - Aktualisiere `run_metadata.md` mit Commands, Dauer, geaenderten Dateien und offenen Risiken.

## Validationsregeln

| ID | Check | Fehler |
|---|---|---|
| VAL-P3-01 | Jedes `MAP-*` hat Implementierungsstatus | ERR-P3-01 |
| VAL-P3-02 | RN-Code ist statisch pruefbar oder Fehler dokumentiert | ERR-P3-03 |
| VAL-P3-03 | Architekturregeln eingehalten | ERR-P3-01 |
| VAL-GEN-02 | Jede Entscheidung referenziert Phase 1 | ERR-REF-01 |

## Fehlerfaelle

| Fehler | Behandlung |
|---|---|
| ERR-P3-01 | STOP, Mapping-Luecke oder nicht umsetzbares Verhalten dokumentieren |
| ERR-P3-02 | STOP, fehlendes RN-Projekt oder Dependency dokumentieren |
| ERR-P3-03 | STOP, TypeScript/Import/Buildfehler im Report erfassen |
