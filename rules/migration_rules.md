## BEHAVIOR_SPEC VALIDATION ENGINE (STRICT)

Eine behavior_spec.md gilt nur als gültig, wenn ALLE Regeln erfüllt sind:

---

### 1. CODE-ABLEITBARKEIT

Jede Aussage MUSS direkt aus legacy_analysis.md ableitbar sein.

Wenn eine Aussage nicht direkt im Code vorkommt:
→ INVALID

---

### 2. KEINE FREIEN INTERPRETATIONEN

Verboten:

- „typischerweise“
- „wahrscheinlich“
- „wahrscheinlich bedeutet“
- „User erwartet vermutlich“

→ führt zu INVALID STATUS

---

### 3. VOLLSTÄNDIGKEIT DER STATES

Alle Zustände müssen enthalten:

- Idle
- Loading (falls API existiert)
- Success
- Error

Wenn ein State fehlt → INVALID

---

### 4. INPUT-OUTPUT KONSISTENZ

Jeder Input muss:

- im Intake existieren
- im Code vorkommen
- im Testfall abgedeckt sein

sonst → INVALID

---

### 5. SIDE EFFECT CHECK

Alle Side Effects müssen explizit sein:

- Navigation
- Storage
- API Calls

Wenn implizit → INVALID

---

### 6. DETERMINISMUS CHECK

Keine Formulierungen mit:

- „kann“
- „optional“
- „meistens“
- „in der Regel“

→ verboten

---

### FINAL RULE

Wenn auch nur 1 Regel verletzt ist:

→ STOP MIGRATION
→ KEINE TESTS
→ KEIN CODE