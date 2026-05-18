# Stop Rules

## STOP-001 Hard Stop

Bei einem blockierenden Fehler wird die Phase beendet. Es werden keine weiteren Code- oder Artefaktaenderungen vorgenommen.

## STOP-002 Stop Artifact

Bei STOP darf genau ein Fehlerartefakt geschrieben werden:

```text
artifacts/<feature-slug>/<agent-id>/<run-id>/phase_<n>/<phase-number>_phase_error.md
```

Das Artefakt enthaelt Fehlercode, Ursache, betroffene Dateien, letzte erfolgreiche Aktion und notwendige Nutzerentscheidung.

## STOP-003 No Silent Recovery

Automatische Recovery ist nur erlaubt, wenn die Phase sie explizit nennt. Jede Recovery wird im Phasenreport dokumentiert.

## STOP-004 Warnings

Nicht-blockierende Abweichungen werden als `WARNING` dokumentiert und duerfen die Phase nur fortsetzen lassen, wenn alle Validierungsregeln erfuellt bleiben.
