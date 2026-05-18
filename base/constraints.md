# Constraints

## CON-001 Functional Equivalence

Ziel ist funktionale Aequivalenz zum belegten Legacy-Verhalten, nicht Produktverbesserung.

## CON-002 Unit Tests Only

Der Scope umfasst Unit Tests. E2E-Tests, manuelle QA und visuelle Regressionstests werden nicht als Erfolgskriterium verwendet.

## CON-003 No Extra Features

Keine neuen Screens, Flows, API-Aufrufe, Storage Keys oder Fehlerbehandlungen ohne Phase-1-Quelle.

## CON-004 Existing Structure First

Bestehende Projektstruktur, Libraries und lokale Helper haben Vorrang vor neuen Abstraktionen.

## CON-005 Dependency Handling

Neue Dependencies muessen begruendet, installiert/importierbar und im Report dokumentiert sein. Fehlende Dependencies fuehren zu `ERR-P3-02` oder `ERR-P4-02`.

## CON-006 Bachelorarbeit Comparability

Phasen duerfen nicht durch nachtraegliche, undokumentierte Korrekturen geglaettet werden. Jeder manuelle Eingriff wird als Messwert erfasst.
