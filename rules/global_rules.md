# GLOBAL RULES

## 1. STRICT SCOPE

Nur `<FEATURE_NAME>` verarbeiten.

Andere Features:
→ IGNORE  
→ Wenn notwendig → STOP

---

## 2. NO ASSUMPTIONS

Verboten:

* Raten
* Interpretieren
* Ergänzen

Fehlende Information:
→ STOP

---

## 3. SOURCE OF TRUTH

Erlaubte Quellen:

* ios-mobilebrowser/Source
* android-mobilebrowser/app/src
* features/<FEATURE_NAME>/

Andere Quellen:
→ VERBOTEN

---

## 4. DETERMINISM

Alle Outputs müssen:

* reproduzierbar sein
* eindeutig sein
* vollständig sein

---

## 5. NO IMPLICIT LOGIC

Erlaubt:

* explizite Ableitung

Verboten:

* implizite Annahmen
* „typisches Verhalten“