# ID Registry

Diese Datei ist die zentrale Orientierung fuer IDs. Andere Dateien duerfen IDs verwenden, sollen aber keine neuen Namespaces erfinden.

## Rule Namespaces

| Prefix | Datei | Bedeutung |
|---|---|---|
| GR | `rules/global_rules.md` | Globale Arbeitsregeln |
| REF | `rules/reference_rules.md` | Quellen und Traceability |
| NAM | `rules/naming_rules.md` | Benennung |
| OUT | `rules/output_rules.md` | Artefaktformate |
| MIG | `rules/migration_rules.md` | Migrationsverhalten |
| VAL | `rules/validation_rules.md` | Validierung |
| ERR | `rules/error_rules.md` | Fehlercodes |
| STOP | `rules/stop_rules.md` | Stop-Verhalten |
| ARCH | `base/architecture.md` | Zielarchitektur |
| TEST | `base/testing.md` | Testkonventionen |
| MET | `base/evaluation_framework.md` | Evaluationsmetriken |

## Phase Artifact IDs

Alle Artefakte werden unter `artifacts/<feature-slug>/<agent-id>/<run-id>/phase_<n>/` gespeichert. Templates liegen getrennt unter `templates/`.

| ID | Datei | Zweck |
|---|---|---|
| P1-A11 | `11_feature_analysis.md` | Feature-Scope und Discovery-Ergebnis |
| P1-A12 | `12_code_facts.md` | Belegte Legacy-Code-Fakten |
| P1-A13 | `13_test_definition.md` | Testbare Verhaltensdefinition |
| P1-A14 | `14_migration_mapping.md` | Mapping iOS/Android nach RN |
| P1-A15 | `15_execution_contract.md` | Ausfuehrungsvertrag fuer Phase 2 bis 5 |
| P1-A16 | `16_traceability_matrix.md` | Traceability von Fakten zu Tests und Migration |
| P2-A21 | `21_legacy_test_plan.md` | Legacy-Unit-Testplan |
| P2-A22 | `22_legacy_test_implementation.md` | Erzeugte Legacy-Testdateien |
| P2-A23 | `23_legacy_test_results.md` | Legacy-Test- und Coverage-Ergebnisse |
| P2-A24 | `24_legacy_test_quality.md` | Testqualitaet und Failure-Sensitivitaet |
| P3-A31 | `31_rn_implementation_plan.md` | RN-Implementierungsplan |
| P3-A32 | `32_rn_code_report.md` | Erzeugter RN-Code und Commands |
| P3-A33 | `33_rn_mapping_status.md` | Abdeckung des Phase-1-Mappings |
| P4-A41 | `41_rn_test_plan.md` | RN-Testmigrationsplan |
| P4-A42 | `42_rn_test_mapping.md` | Legacy-Test zu RN-Test Mapping |
| P4-A43 | `43_rn_test_implementation.md` | Erzeugte RN-Testdateien |
| P4-A44 | `44_rn_test_readiness.md` | Kompilierbarkeit und Ausfuehrungsbereitschaft |
| P5-A51 | `51_final_validation_report.md` | Finale Testausfuehrung und Gate |
| P5-A52 | `52_behavior_parity_report.md` | Verhalten RN vs Legacy |
| P5-A53 | `53_test_comparison_report.md` | Phase-2-Tests vs Phase-4/5-Tests |
| P5-A54 | `54_research_metrics.md` | Vergleichsmetriken fuer KI-Auswertung |
| P5-A55 | `55_interpretation_notes.md` | Interpretierbare Ergebnisse und Risiken |

## Run Artifact

| ID | Datei | Zweck |
|---|---|---|
| RUN-A00 | `run_metadata.md` | Agent, Modell, Feature, Run-ID, Zeitpunkte, Prompt-Text und globale Notizen |

## Fact IDs Produced In Phase 1

| Prefix | Bedeutung |
|---|---|
| IOS-FILE | iOS-Datei mit Relevanz fuer das Feature |
| AND-FILE | Android-Datei mit Relevanz fuer das Feature |
| EP | Entry Point |
| BEH | Verhalten / Business-Regel |
| STATE | Zustand oder State Transition |
| STOR | Storage-Key oder Persistenzoperation |
| API | Netzwerk/API-Aufruf |
| NAV | Navigation oder Routing |
| ERRPATH | Fehlerpfad |
| DEP | Dependency |
| UI | UI-relevantes Verhalten |
| SEC | Security- oder Datenschutzverhalten |
| MAP | Migration Mapping |
| LT | Legacy Unit Test |
| RT | React Native Unit Test |

IDs werden dreistellig vergeben, zum Beispiel `EP-001`, `STOR-002`, `LT-004`.

## Status Values

Erlaubte Statuswerte:

- `NOT_STARTED`
- `IN_PROGRESS`
- `READY_FOR_REVIEW`
- `BLOCKED`
- `FAILED`
- `COMPLETE`
