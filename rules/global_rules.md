# Global Rules

## GR-001 Feature Scope

Bearbeite ausschliesslich das Feature aus dem aktuellen Prompt. Andere Features duerfen nur als Dependency benannt werden, wenn Phase 1 oder bestehende Artefakte sie belegen.

## GR-002 Repository Boundaries

Erlaubte Projektpfade:

- `../ios-mobilebrowser/`
- `../android-mobilebrowser/`
- `../rn-e-mobilebrowser/`
- `./artifacts/<feature-slug>/<agent-id>/<run-id>/`
- `./features/` fuer globale Uebersichten und altes Referenzmaterial
- `./rules/`, `./base/`, `./contracts/`, `./templates/`, `./phases/`

Runtime-Code der RN-App gehoert nach `../rn-e-mobilebrowser/`, nicht nach `ai-context/`.

## GR-003 No Assumptions

Keine fachliche Aussage darf geraten, aus typischem Verhalten abgeleitet oder frei ergaenzt werden. Unklare Punkte werden als `UNKNOWN` dokumentiert und koennen eine Phase blockieren.

## GR-004 Source Of Truth

Source-of-truth-Reihenfolge:

1. Phase-1-Artefakte im Feature-Ordner.
2. In Phase 1 belegte Legacy-Referenzen.
3. Phase-2-Testresultate fuer Testparitaet.
4. RN-Code und RN-Tests fuer Phase 5.

Nach Phase 1 duerfen neue fachliche Details nicht direkt aus Legacy-Code abgeleitet werden.

## GR-005 Determinism

Alle Artefakte muessen reproduzierbare Tabellen, IDs, Statuswerte und Quellen enthalten. Freitext ist erlaubt, darf Tabellen aber nicht ersetzen.

## GR-006 Research Comparability

Jede Phase dokumentiert Modell/Tool, Startzeit, Endzeit, geaenderte Dateien, ausgefuehrte Commands, Fehler und manuelle Eingriffe. Diese Daten sind Pflicht fuer den KI-Vergleich.

## GR-007 Template Immutability

Dateien in `templates/` werden nie ausgefuellt oder ueberschrieben. Sie werden als Vorlage in den passenden Artefaktordner kopiert und dort bearbeitet.
