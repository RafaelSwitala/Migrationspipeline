# Reference Rules

## REF-001 Evidence Required

Jede fachliche Aussage braucht eine Quelle. Phase 1 verwendet Legacy-Referenzen mit Datei, Symbol und Zeile. Spaetere Phasen verwenden die IDs aus Phase 1 und Phase 2.

## REF-002 Reference Format

Legacy-Code:

```text
[ios: Source/Path/File.swift:42 symbol=methodName]
[android: app/src/main/.../File.kt:88 symbol=methodName]
```

Artefakte:

```text
[P1-A12: EP-001]
[P2-A23: LT-004]
[P4-A42: RT-004]
```

## REF-003 Later-Phase Restriction

Phase 3 bis 5 duerfen keine neuen Legacy-Referenzen erzeugen. Wenn ein Detail fehlt, stoppt die Phase mit `ERR-REF-01` und fordert eine Phase-1-Ergaenzung.

## REF-004 No Floating Claims

Verboten sind Formulierungen wie `vermutlich`, `wahrscheinlich`, `typischerweise`, `sollte wohl`, `siehe Code` oder `in der Datei`.

## REF-005 Traceability

Jede implementierte RN-Funktion und jeder Testfall muss auf mindestens eine Phase-1-ID oder Phase-2-Test-ID zurueckfuehrbar sein.
