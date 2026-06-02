# Evaluation Framework

Diese Metriken dienen dem Vergleich mehrerer KI-Agenten.

## MET-001 Functional Result

| Metric | Beschreibung |
|---|---|
| Legacy test passrate | Anteil bestandener Phase-2-Tests |
| RN test passrate | Anteil bestandener Phase-5-Tests |
| Behavior parity | Anteil gemappter Verhalten ohne Abweichung |
| Blocking failures | Anzahl Fehler mit `BLOCKING` Severity |

## MET-002 Test Quality

| Metric | Beschreibung |
|---|---|
| Test count | Anzahl valider Tests |
| Coverage | Statements, Branches, Functions, Lines |
| Failure sensitivity | Ob Tests bei gebrochenem Verhalten plausibel fehlschlagen |
| Structural-only tests | Tests ohne echte Verhaltensassertion |

## MET-003 Implementation Quality

| Metric | Beschreibung |
|---|---|
| TypeScript errors | Anzahl Compile-/Typecheck-Fehler |
| Dependency additions | Anzahl neuer Dependencies |
| Mapping coverage | Anteil implementierter `MAP-*` IDs |
| Manual fixes | Anzahl manueller Korrekturen nach KI-Ausgabe |

## MET-004 Effort

| Metric | Beschreibung |
|---|---|
| Phase duration | Zeit pro Phase |
| Changed files | Anzahl gänderter Dateien |
| Commands run | Anzahl relevanter Commands |
| Re-runs | Anzahl Wiederholungen einer Phase |

## MET-005 Interpretation Notes

Bewertet wird nicht nur `PASS/FAIL`, sondern warum ein Agent besser oder schlechter abschneidet: fehlende Traceability, falsche Annahmen, unvollständige Tests, gute Mapping-Entscheidungen oder stabilere Fehlerdokumentation.
