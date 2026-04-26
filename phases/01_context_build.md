# PHASE 1 – CONTEXT BUILD

## ZIEL
Erzeuge eine vollständige, referenzierbare Feature-Analyse basierend auf allen relevanten Dateien für das Feature <FEATURE_NAME>.

---

## INPUT
Verwende folgende Pfade:

* iOS: ios-mobilebrowser/Source
* Android: android-mobilebrowser/app/src

Zusätzliche Regelwerke:
* base/output_rules.md
* base/validation_rules.md
* base/error_rules.md

---

## OUTPUT

Es müssen folgende Dateien vollständig erzeugt werden:

* features/<FEATURE_NAME>/11_feature_analysis.md
* features/<FEATURE_NAME>/12_code_facts.md
* features/<FEATURE_NAME>/13_test_definition.md
* features/<FEATURE_NAME>/14_migration_mapping.md
* features/<FEATURE_NAME>/15_execution_contract.md
* features/<FEATURE_NAME>/16_traceability_matrix.md

Alle Dateien sind verpflichtend.

### Regelbindung pro Datei:

* feature_analysis.md → O-0001 bis O-0010  
* code_facts.md → O-1301 bis O-1315  
* test_definition.md → O-1401 bis O-1406  
* migration_mapping.md → O-1501 bis O-1507  
* execution_contract.md → O-1601 bis O-1604  
* traceability_matrix.md → O-1701 

---

## EXECUTION STEPS

### STEP 1: DISCOVERY

Scanne alle Dateien und identifiziere relevante Dateien gemäß Relevanz-Regel:

**Dateitypen:**
* iOS: `.swift`
* Android: `.kt`, `.java`

**Eine Datei ist RELEVANT, wenn mindestens eine Bedingung erfüllt ist:**

* direkte Referenz zu `<FEATURE_NAME>`
* indirekte Nutzung durch das Feature (Helper, Utils, Storage, URL Builder)
* wird vom Feature aufgerufen oder ruft das Feature auf
* enthält Feature-spezifische Navigation
* enthält Feature-spezifische Storage- oder API-Nutzung

---

### STEP 2: STRUCTURED EXTRACTION

---

### 2A – FEATURE ANALYSIS

* Beantworte O-0001 bis O-0010  
* Ziel: Abstrakte, plattformunabhängige Feature-Beschreibung  

---

### 2B – CODE FACT EXTRACTION

* Beantworte O-1301 bis O-1310  
* Ziel: Vollständige, verlustfreie Extraktion aller technischen Details aus dem Code  

---

### 2C – TEST DEFINITION

**Ziel:**  
Erzeuge strikt ableitbare, atomare Testdefinitionen basierend ausschließlich auf CODE FACTS.

**REGELN:**

* Jede Zeile MUSS auf mindestens einen CODE FACT (O-130x) referenzieren
* KEINE neue Logik
* KEINE Interpretation außerhalb des Codes
* KEINE Zusammenfassung mehrerer Fakten ohne explizite Referenzen

**OUTPUT MAPPING:**

* O-1401 ← O-1302 (Entry Points)
* O-1402 ← O-1303 (Plattformpaare)
* O-1403 ← O-1305 (State Changes)
* O-1404 ← O-1306 (Storage Writes)
* O-1405 ← O-1308 (Error Branches)

**FORMAT ANFORDERUNG:**

Jeder Testfall MUSS enthalten:
* eindeutige ID
* referenzierte O-130x Quellen
* exakten Trigger (Entry Point)
* erwartetes Verhalten (nur aus Code ableitbar)

**VALIDATION (BLOCKING):**

* Kein Test ohne Source Mapping
* Kein Test ohne Entry Point Referenz
* Jeder Test ist vollständig tracebar zu O-130x

---

### 2D – MIGRATION MAPPING

**Ziel:**  
Transformiere CODE FACTS in eine plattformübergreifende Verhaltensbeschreibung für Migration.

**REGELN:**

* KEINE neue Funktionalität
* KEINE Interpretation
* KEINE Vereinheitlichung von Logik
* Jede Zeile MUSS exakt auf O-130x referenzieren

**OUTPUT MAPPING:**

* O-1501 COMPONENT MAPPING ← O-1301, O-1302  
* O-1502 STORAGE MAPPING ← O-1306  
* O-1503 API MAPPING ← O-1307  
* O-1504 UI MAPPING ← O-1302, O-1309  
* O-1505 STATE MAPPING ← O-1305, O-1308  

**FORMAT ANFORDERUNG:**

Jede Mapping-Zeile MUSS enthalten:
* Source (O-130x Referenz)
* exakte Beschreibung der bestehenden Implementierung
* Plattform-Zuordnung (iOS / Android)
* RN-Äquivalent ODER `NOT FOUND`

**VALIDATION (BLOCKING):**

* Kein Mapping ohne Code Fact
* Kein RN Target ohne vollständige Source Referenz
* Plattform-Divergenzen müssen explizit markiert werden

---

### 2E – EXECUTION CONTRACT

**Ziel:**  
Definiere ein strikt ausführbares Regelwerk für Testing und Migration.

**REGELN:**

* KEINE neue Logik
* KEINE Interpretation
* KEINE UI/UX Ableitung
* Nur Einschränkungen basierend auf bestehenden Fakten

**OUTPUT MAPPING:**

* O-1601 TEST EXECUTION RULES ← O-140x + O-130x  
* O-1602 RUN ORDER ← O-1401 + O-1302  
* O-1603 OUTPUT CONTRACT ← O-1403 + O-1404 + O-1305  
* O-1604 COMPARISON RULES ← O-1402 + O-1405  

**FORMAT ANFORDERUNG:**

Jede Regel MUSS enthalten:
* referenzierte O-130x / O-140x Quellen
* klare Einschränkung (was erlaubt / nicht erlaubt ist)
* keine impliziten Annahmen

**VALIDATION (BLOCKING):**

* Kein Contract ohne Source Mapping
* Keine Regel ohne O-130x Bezug
* Keine Ausführungsregel ohne Entry Point Bezug

### 2F – TRACEABILITY CONSOLIDATION

**Ziel:**  
Erzeuge eine zentrale, normalisierte Referenzstruktur aller Beziehungen zwischen Code Facts, Tests, Migration und Execution.

---

### REGELN:

* KEINE neue Logik
* KEINE Interpretation
* KEINE Ableitung neuer Beziehungen
* Nur bereits existierende Referenzen verwenden

---

### INPUT QUELLEN:

* O-130x (Code Facts)
* O-140x (Test Definition)
* O-150x (Migration Mapping)
* O-160x (Execution Contract)

---

### OUTPUT MAPPING:

* O-1701 TRACEABILITY MATRIX ← O-130x + O-140x + O-150x + O-160x

---

### NORMALISIERUNG:

Alle Referenzen müssen in folgende Typen überführt werden:

* EP → Entry Point (O-1302)
* SC → State Change (O-1305)
* ST → Storage (O-1306)
* API → API Calls (O-1307)
* PP → Plattformpaare (O-1303)
* EB → Error Branch (O-1308)

---

### FORMAT ANFORDERUNG:

Jede Zeile MUSS enthalten:

* Type (EP / SC / ST / API / PP / EB)
* ID (z. B. EP-1, SC-3)
* Referenziert von (z. B. T-EP-1, T-FLOW-1, O-1502, O-1601)
* Referenziert zu (z. B. SC-3, ST-1, API-2)

---

### HERLEITUNGSREGELN:

* EP ← O-1401 + O-1302
* SC ← O-1403 + O-1305
* ST ← O-1404 + O-1306
* API ← O-1503 + O-1307
* PP ← O-1402 + O-1303
* EB ← O-1405 + O-1308

---

### VALIDATION (BLOCKING):

* Keine Matrix-Zeile ohne existierende Source-ID
* Jede ID MUSS in mindestens einem anderen Artefakt referenziert sein
* Keine isolierten Knoten erlaubt
* Keine neuen IDs erlaubt
* Jede Beziehung muss bidirektional nachvollziehbar sein

---

## STEP 3: ABSTRACTION (FEATURE ANALYSIS)

Die Datei `feature_analysis.md` muss:

* plattformunabhängig sein
* keine Klassen- oder Methodennamen enthalten
* ausschließlich Verhalten, Datenflüsse und Logik beschreiben
* konsistente Terminologie verwenden
* alle Widersprüche auflösen

**INTERPRETATION ERLAUBT NUR WENN:**

* direkt aus Code ableitbar
* durch Referenzen belegbar

**REGELN:**

* Keine Annahmen
* Fehlende Informationen → `NOT FOUND`
* Jede Aussage MUSS referenzierbar sein

**FEHLER:**

* Aussage ohne Referenz → UNGÜLTIG
* Regelverletzung → VALIDATION FAIL + Abbruch

---

## CODE FACT RULES (BLOCKING)

* Alle Informationen müssen 1:1 aus Code stammen
* Keine Ableitung aus feature_analysis.md
* Keine Generalisierung
* Fehlende Werte → `NOT FOUND`

**Pflichtfelder pro Eintrag:**

* Datei
* Methode
* Zeile

**Zusätzlich:**

* Bedingungen im Original-Codeformat angeben

---

## VALIDATION (BLOCKING)

Angewendete Regeln:

* V-0301
* V-0302
* V-0303
* V-0304
* V-0305
* V-0306
* V-0307
* V-0308
* V-0309

---

## FEHLERFALL

Angewendete Regeln:

* E-0001