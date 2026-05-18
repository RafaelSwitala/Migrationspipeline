# Validation Rules

## VAL-GEN-01 Artifact Completeness

Alle fuer eine Phase geforderten Artefakte existieren, besitzen den Header aus `OUT-001` und enthalten keine leeren Pflichtfelder.

## VAL-GEN-02 Traceability

Jede fachliche Aussage, jeder Test und jede Implementierungsentscheidung referenziert eine gueltige ID oder Quelle nach `REF-002`.

## VAL-GEN-03 No Placeholder Completion

Ein Artefakt mit `TODO`, `TBD`, `...`, leeren Tabellenzellen oder nicht erklaerten `UNKNOWN`-Werten darf nicht `COMPLETE` sein.

## VAL-P1-01 Discovery Coverage

Phase 1 hat iOS und Android durchsucht oder eine Plattform mit Quelle als `NOT_PRESENT` dokumentiert.

## VAL-P1-02 Code Facts Complete

`12_code_facts.md` enthaelt alle fuer das Feature relevanten Fakten-IDs: Entry Points, Verhalten, State, Storage, API, Navigation, Error Paths und Dependencies oder jeweils `N/A` mit Begruendung.

## VAL-P1-03 Later-Phase Readiness

Phase 1 enthaelt genug Informationen, damit Phase 2 bis 5 kein neues fachliches Legacy-Discovery brauchen.

## VAL-P1-04 Traceability Matrix Complete

Jede ID aus `12_code_facts.md` erscheint in `16_traceability_matrix.md`.

## VAL-P2-01 Test Derivation

Jeder Legacy-Testfall referenziert mindestens eine Phase-1-ID und prueft Verhalten, nicht nur Implementierungsstruktur.

## VAL-P2-02 Platform Coverage

iOS und Android besitzen Tests oder eine belegte `N/A`-Begruendung.

## VAL-P2-03 Execution Evidence

Alle validen Legacy-Tests wurden ausgefuehrt oder mit reproduzierbarem Ausfuehrungsfehler dokumentiert.

## VAL-P2-04 Coverage Recorded

Coverage ist je Plattform erfasst oder als `N/A` mit Tool-/Projektgrund dokumentiert.

## VAL-P3-01 Mapping Implementation

Jedes `MAP-*` aus `14_migration_mapping.md` ist implementiert, bewusst ausgeschlossen oder blockiert dokumentiert.

## VAL-P3-02 RN Static Health

RN-Code hat keine TypeScript-, Import- oder offensichtlichen Dependency-Fehler, soweit lokale Commands verfuegbar sind.

## VAL-P3-03 Architecture Compliance

RN-Code folgt `base/architecture.md`; kein Runtime-Code liegt im `ai-context`-Featureordner.

## VAL-P4-01 Test Mapping Complete

Jeder valide Legacy-Test aus Phase 2 hat einen RN-Test, einen Skip-Grund oder eine blockierende Mapping-Notiz.

## VAL-P4-02 RN Test Readiness

RN-Tests sind syntaktisch gueltig, importierbar und fuer Jest/React Native Testing Library vorbereitet.

## VAL-P4-03 No New Behavior

RN-Tests pruefen kein Verhalten, das nicht aus Phase 1 oder Phase 2 ableitbar ist.

## VAL-P5-01 Final Test Execution

Phase 5 fuehrt die RN-Tests aus Phase 4 gegen den RN-Code aus Phase 3 aus und speichert Ergebnis sowie Coverage.

## VAL-P5-02 Parity Comparison

Phase 5 vergleicht Legacy-Ergebnisse aus Phase 2 mit RN-Ergebnissen aus Phase 5 pro Test-ID.

## VAL-P5-03 Research Metrics Complete

`54_research_metrics.md` enthaelt alle messbaren Daten fuer den KI-Vergleich oder erklaerte `N/A`-Werte.
