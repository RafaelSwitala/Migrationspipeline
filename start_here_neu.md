# START HERE – EXECUTION ENTRYPOINT

## OVERVIEW

Diese Datei definiert die Ausführungsreihenfolge.

Alle Details sind in den jeweiligen Phase-Dateien definiert.

---

## EXECUTION ORDER

1 → /phases/01_code_discovery.md  
2 → /phases/02_intake_extraction.md  
2.5 → /phases/025_feature_dependency.md  
3 → /phases/03_context_derivation.md  
...

---

## GLOBAL RULES

→ /base/global_rules.md

---

## CONTRACT

- Reihenfolge ist strikt
- Jede Phase ist blocking
- Bei Fehler → STOP gemäß /base/stop_rules.md