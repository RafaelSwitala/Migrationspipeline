# Phase Contract

Jede Phase muss in der jeweiligen Datei unter `phases/` dieselbe Struktur verwenden:

1. Ziel
2. Input
3. Output
4. Regelbindungen
5. Execution Steps
6. Validationsregeln
7. Fehlerfälle

## Contract Rules

| ID | Regel |
|---|---|
| PC-001 | Eine Phase darf nur die in `Input` genannten Quellen verwenden. |
| PC-002 | Eine Phase darf nur die in `Output` genannten Artefakte erzeugen oder aktualisieren. |
| PC-003 | Jede Phase endet mit `READY_FOR_REVIEW`, `COMPLETE`, `FAILED` oder `BLOCKED`. |
| PC-004 | Jede Phase dokumentiert Commands, geänderte Dateien, Fehler und offene Risiken. |
| PC-005 | Ein STOP erzeugt nur das Fehlerartefakt aus `STOP-002`. |
| PC-006 | Wenn eine spätere Phase neue fachliche Legacy-Details benötigt, muss Phase 1 nachgezogen werden. |
| PC-007 | Die Chat-Eingabe löst die Phase aus; sie ist kein inhaltlicher Datei-Input. |
| PC-008 | Jede Output-Datei muss die in der Phase genannten Pflichtinhalte enthalten. |
| PC-009 | Templates werden nur gelesen/kopiert, nie direkt ausgefüllt. |

## Review Handoff

Nach jeder Phase werden die erzeugten Artefakte geprüft. Die nächste Phase startet erst nach Review oder bewusster Freigabe.
