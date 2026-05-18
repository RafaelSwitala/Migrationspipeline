# Validation Checklist

Diese Checkliste ist ein kompakter Gate-Check fuer Reviews nach jeder Phase.

## Phase 1

- [ ] `11_feature_analysis.md` bis `16_traceability_matrix.md` existieren.
- [ ] iOS und Android wurden durchsucht oder `NOT_PRESENT` ist belegt.
- [ ] Alle fachlichen Fakten haben IDs und Quellen.
- [ ] Jede Code-Fact-ID steht in der Traceability Matrix.
- [ ] Keine offenen `UNKNOWN`-Werte blockieren Phase 2 bis 5.

## Phase 2

- [ ] Legacy-Testplan referenziert Phase-1-Fakten.
- [ ] iOS- und Android-Tests existieren oder sind begruendet `N/A`.
- [ ] Tests wurden ausgefuehrt oder Ausfuehrungsfehler sind reproduzierbar dokumentiert.
- [ ] Coverage ist dokumentiert oder begruendet nicht verfuegbar.
- [ ] Testqualitaet wurde gegen `TEST-006` bewertet.

## Phase 3

- [ ] RN-Code liegt in `../rn-e-mobilebrowser/`.
- [ ] Jedes `MAP-*` ist implementiert, ausgeschlossen oder blockiert dokumentiert.
- [ ] TypeScript/Imports/Dependencies wurden geprueft.
- [ ] Keine fachliche Legacy-Neuableitung wurde vorgenommen.

## Phase 4

- [ ] Jeder valide Legacy-Test hat ein RN-Test-Mapping.
- [ ] RN-Tests sind syntaktisch/typisch ausfuehrbar vorbereitet.
- [ ] Tests fuehren kein neues Verhalten ein.
- [ ] Mocks sind dokumentiert und deterministisch.

## Phase 5

- [ ] RN-Tests aus Phase 4 wurden gegen RN-Code aus Phase 3 ausgefuehrt.
- [ ] Legacy-vs-RN-Ergebnisse sind pro Test-ID verglichen.
- [ ] Behavior-Parity und Coverage sind dokumentiert.
- [ ] Research-Metriken fuer KI-Vergleich sind vollstaendig oder `N/A` begruendet.
- [ ] Phase 5 hat keinen Code veraendert.
