# Phase 5: Final Validation And Research Reporting

## Ziel

Fuehre die RN-Tests aus Phase 4 gegen den RN-Code aus Phase 3 aus, vergleiche die Ergebnisse mit Phase 2 und erstelle verwertbare Auswertungsartefakte fuer die Bachelorarbeit. Diese Phase veraendert keinen Code.

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
- Phase 2: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_2/`
- Phase 3: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_3/`
- Phase 4: `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_4/`
- RN-Projekt: `../rn-e-mobilebrowser/`
- Base: `base/evaluation_framework.md`, `base/testing.md`, `base/validation_check.md`
- Regeln: `rules/*.md`
- Templates: `templates/51_final_validation_report.template.md` bis `templates/55_interpretation_notes.template.md`

## Output

Erzeuge folgende Dateien in `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_5/`:

| Artifact ID | Datei | Pflichtinhalt | Vollstaendig wenn |
|---|---|---|---|
| P5-A51 | `51_final_validation_report.md` | RN-Testcommands, Resultate, Coverage, Ausfuehrungsumgebung, finaler Gate-Status | jeder RN-Test aus Phase 4 hat Ergebnis |
| P5-A52 | `52_behavior_parity_report.md` | Vergleich pro `BEH-*`, `STATE-*`, `STOR-*`, `API-*`, `ERRPATH-*`, `MAP-*` | jede relevante Phase-1-ID ist bewertet |
| P5-A53 | `53_test_comparison_report.md` | `LT-*` zu `RT-*`, Legacy Result, RN Result, Vergleichskategorie, Abweichungsgrund | jeder valide Legacy-Test ist verglichen |
| P5-A54 | `54_research_metrics.md` | Metriken aus `MET-001` bis `MET-004`, Fehleranzahl, Dauer, manuelle Eingriffe, Coverage | jede Metrik hat Wert oder `N/A` mit Grund |
| P5-A55 | `55_interpretation_notes.md` | Beobachtungen, Evidenz, Interpretation, Relevanz fuer KI-Vergleich | Beobachtung und Interpretation sind getrennt |

Keine Codeaenderungen in `../rn-e-mobilebrowser/`, `../ios-mobilebrowser/` oder `../android-mobilebrowser/`.

## Regelbindungen

- `PC-001` bis `PC-009`
- `MC-001` bis `MC-006`
- `GR-001`, `GR-004`, `GR-006`, `GR-007`
- `REF-003`, `REF-005`
- `MIG-001`, `MIG-006`
- `TEST-005`, `TEST-006`
- `MET-001` bis `MET-005`
- `OUT-001`, `OUT-004`, `OUT-005`, `OUT-007`, `OUT-008`, `OUT-009`
- `VAL-P5-01` bis `VAL-P5-03`
- `ERR-P5-01`, `ERR-P5-02`, `ERR-P5-03`

## Execution Steps

1. Pre-flight pruefen.
   - Pruefe, ob alle P1-P4-Artefakte vorhanden sind.
   - Pruefe, ob RN-Code und RN-Testdateien existieren.
   - Lege `phase_5/` an.
   - Kopiere die Phase-5-Templates in `phase_5/` und entferne `.template` aus dem Dateinamen.
   - Dokumentiere fehlende Inputs als Blocker.

2. RN-Testcommands bestimmen.
   - Nutze Commands aus `P1-A15`, `P4-A44` oder `package.json`.
   - Installiere keine neuen Dependencies ohne explizite Freigabe durch vorherige Phasen.

3. RN-Tests ausfuehren.
   - Fuehre Jest/Unit-Tests mit Coverage aus, wenn verfuegbar.
   - Erfasse Resultate nach `OUT-004` und Coverage nach `OUT-005`.

4. Testvergleich erstellen.
   - Vergleiche pro `LT-*`/`RT-*`: Legacy Result, RN Result, Coverage-Relevanz, Abweichung.
   - Dokumentiere `PASS_MATCH`, `FAIL_MATCH`, `RN_FAIL`, `LEGACY_FAIL`, `SKIPPED`, `MISSING`.

5. Behavior-Parity bewerten.
   - Vergleiche `BEH-*`, `STATE-*`, `STOR-*`, `API-*`, `ERRPATH-*` und `MAP-*` mit RN-Code- und Testergebnissen.
   - Markiere Abweichungen als bewusst, unbewusst oder ungeprueft.

6. Research Metrics berechnen.
   - Erfasse Metriken aus `base/evaluation_framework.md`.
   - Markiere nicht verfuegbare Daten als `N/A` mit Grund.

7. Interpretation schreiben.
   - Beschreibe kurz, was fuer den KI-Vergleich relevant ist.
   - Trenne Beobachtung, Messwert und Interpretation.
   - Keine nachtraeglichen Codefixes in dieser Phase.

8. Run abschliessen.
   - Aktualisiere `run_metadata.md`.
   - Setze finalen Status auf `COMPLETE`, `FAILED` oder `BLOCKED`.

## Validationsregeln

| ID | Check | Fehler |
|---|---|---|
| VAL-P5-01 | RN-Tests aus Phase 4 wurden gegen Phase-3-Code ausgefuehrt | ERR-P5-01 |
| VAL-P5-02 | Legacy-vs-RN-Vergleich pro Test-ID vorhanden | ERR-P5-02 |
| VAL-P5-03 | Research-Metriken vollstaendig oder `N/A` begruendet | ERR-P5-02 |
| VAL-GEN-01 | Alle Phase-5-Artefakte existieren | ERR-P5-02 |
| VAL-GEN-03 | Keine Platzhalter in finalen Reports | ERR-P5-02 |

## Fehlerfaelle

| Fehler | Behandlung |
|---|---|
| ERR-P5-01 | STOP, Testausfuehrung, Command, Output und Ursache dokumentieren |
| ERR-P5-02 | STOP, fehlende Vergleichsdaten oder Metriken dokumentieren |
| ERR-P5-03 | Als WARNING dokumentieren, wenn Divergenz bewusst und vollstaendig belegt ist |
