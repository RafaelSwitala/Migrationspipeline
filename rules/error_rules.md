# ERROR RULES

---

# CORE PRINCIPLE

Fehlerzustände sind:

* binär (OK / STOP)
* deterministisch
* nicht interpretativ

---

# 1. DISCOVERY ERRORS

## E-0001 CODE DISCOVERY FAILED

if code_discovery_failed:
    STOP

Aktion:
* Pfade prüfen  
* Feature Scope prüfen  

---

# 2. INTAKE ERRORS

## E-0101 INTAKE EXTRACTION FAILED

if intake_extraction_failed:
    STOP

Aktion:
* fehlende Referenzen ergänzen  
* Datei erneut analysieren  

---

## E-0102 CONTEXT INVALID

if context_invalid:
    STOP

Aktion:
* zurück zu PHASE 2  
* intake.md ergänzen  

---

# 3. TEST ERRORS

## E-0201 TEST INVALID

if test_invalid:
    STOP

Aktion:
* behavior_spec.md prüfen  
* intake.md ergänzen  

---

## E-0202 TEST IMPLEMENTATION FAILED

if test_implementation_failed:
    STOP

Aktion:
* zurück zu PHASE 4  

---

## E-0203 MISSING ANDROID TEST ENVIROMENT
- Erstelle fehlende Gradle-Dateien anhand eines minimalen Android-Test-Setups
- Ergänze automatisch:
  testImplementation 'junit:junit:4.13.2'
  androidTestImplementation 'androidx.test.ext:junit:1.1.5'
  androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
- Erstelle minimale Testordnerstruktur
- Erstelle einen Dummy-Test:
  ExampleUnitTest.kt

Stoppe NICHT bei fehlender Testumgebung.
Erzeuge stattdessen ein lauffähiges Minimal-Setup.

---

## E-0204 MISSING IOS TEST ENVIROMENT
- Erstelle automatisch eine minimale XCTest-Testumgebung
- Erstelle fehlendes Test Target
- Erstelle Podfile falls notwendig
- Füge XCTest hinzu
- Erstelle Dummy-Testdatei:
  ExampleTests.swift

Stoppe NICHT bei fehlender Testumgebung.
Erzeuge stattdessen ein lauffähiges Minimal-Setup.


---

# 4. MIGRATION ERRORS

## E-0301 RN MIGRATION FAILED

if rn_migration_failed:
    STOP

Aktion:
* behavior_spec.md prüfen  
* mapping.md prüfen  
* dependency rules prüfen  

---

## E-0302 RN TEST MIGRATION FAILED

if rn_test_migration_failed:
    STOP

Aktion:
* test_spec.md prüfen  
* RN Code prüfen  

---

# 5. DEPENDENCY ERRORS

## E-0401 DEPENDENCY ANALYSIS FAILED

if dependency_analysis_failed:
    STOP

Aktion:
* intake.md prüfen  
* bestehende Features erneut analysieren  

---

# 6. FINAL VALIDATION ERRORS

## E-0501 FINAL VALIDATION FAILED

if final_validation_failed:
    STOP

Dokumentiere:
* Fehler  
* betroffene Dateien  
* mögliche Ursachen  

---