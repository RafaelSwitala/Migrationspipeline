## ANTI-HALLUCINATION LAYER (HARD RULE)

Die KI darf ausschließlich arbeiten, wenn jede Aussage einen expliziten Beleg hat.

---

## REFERENZPFLICHT

Jede Aussage MUSS enthalten:

- Datei
- Methode
- Zeilennummer (wenn möglich)

Format:

[iOS: LoginViewController.swift: loginTapped():45-60]
[Android: LoginActivity.kt: onClick():30-50]

### VERBOTEN:

- Annahmen über UI Verhalten
- Ergänzen fehlender Logik
- Erfinden von API Responses
- „typisches Verhalten in Apps“

---

### ERLAUBT:

Nur Aussagen, die direkt aus folgenden Quellen stammen:

1. ios-mobilebrowser/Source
2. android-mobilebrowser/Source
3. intake.md Referenzen
4. explizit aufgerufene Methoden im Code

---

### VALIDATION RULE:

Jede Aussage in:

- legacy_analysis.md
- behavior_spec.md
- test-spec.md

muss referenzierbar sein auf:

→ konkrete Codezeile ODER
→ explizite Funktion ODER
→ API Call

Wenn nicht:

→ STOP IMMEDIATELY

## EXECUTION MODE

Du arbeitest als deterministische Migrations-Engine.

Du darfst NICHT:
- raten
- interpretieren ohne Codebasis
- Schritte überspringen

Wenn Informationen fehlen:
→ STOP
→ kein Output

# START HERE

## ZIEL

Migration des Features <FEATURE_NAME> basierend auf echtem Legacy-Verhalten.

---

# 1. SOURCE OF TRUTH

Arbeite in folgender Priorität:

1. features/<FEATURE_NAME>/
2. android-mobilebrowser/Source
3. ios-mobilebrowser/Source
4. ai-context/base/
5. features/_golden_example/ (nur Referenz)

WICHTIG:

- Legacy-Code (iOS + Android) MUSS aktiv analysiert werden
- Alle Aussagen müssen direkt aus Code ableitbar sein
- intake.md definiert die Einstiegspunkte in den Code

---

# 2. ARBEITSBEREICH

Du arbeitest AUSSCHLIESSLICH in:

features/<FEATURE_NAME>/

Alle Dateien müssen dort erstellt oder aktualisiert werden.

---

# 3. PHASE 1 – KONTEXT ERSTELLEN (PFLICHT)

## Ziel

Erstelle einen vollständigen, validen Feature-Kontext.

Reihenfolge ist VERBINDLICH:

1. intake.md
2. legacy_analysis.md
3. feature_description.md
4. behavior_spec.md
5. test-spec.md
6. context_status.md

---

## 3.1 Intake prüfen / erstellen

Datei:
features/<FEATURE_NAME>/intake.md

Diese Datei MUSS enthalten:

* relevante Dateien (iOS + Android)
* Entry Points
* API Calls
* Storage
* Navigation
* Scope (IN / OUT)

Wenn unklar:
→ STOP

---

## 3.2 Legacy-Analyse durchführen

Erstelle:
features/<FEATURE_NAME>/legacy_analysis.md

Regeln:

* Nur Beobachtung
* Keine Interpretation
* Alle Aussagen müssen aus Code ableitbar sein

---

## 3.3 Feature Description erstellen

Erstelle:
features/<FEATURE_NAME>/feature_description.md

Ziel:

* Beschreibung aus User-Sicht
* KEINE technische Details

---

## 3.4 Behavior Specification ableiten (KRITISCH)

Erstelle:
features/<FEATURE_NAME>/behavior_spec.md

Regeln:

* basiert auf legacy_analysis.md
* vollständig
* deterministisch
* keine Annahmen

---

## 3.5 Testfälle definieren

Erstelle:
features/<FEATURE_NAME>/test-spec.md

Regeln:

* basiert ausschließlich auf behavior_spec.md
* deckt ab:

  * Inputs
  * Outputs
  * Zustände
  * Fehlerfälle

---

## 3.6 Kontext validieren

Aktualisiere:
features/<FEATURE_NAME>/context_status.md

Alle Punkte müssen TRUE sein.

Wenn etwas fehlt:
→ STOP
→ KEINE TESTS
→ KEINE MIGRATION

---

# 4. PHASE 2 – TESTS ERSTELLEN (LEGACY)

## SOURCE OF TRUTH

* behavior_spec.md
* legacy_analysis.md
* intake.md

---

## Schritte

1. Mappe Testfälle auf echten Code (iOS + Android)
2. Implementiere Unit-Tests
3. Führe Tests aus

Wenn:

* Tests fehlschlagen
* Mapping nicht möglich

→ STOP

---

# 5. PHASE 3 – MIGRATION (RN)

Nur erlaubt wenn:

* Kontext vollständig
* Tests bestehen

---

## ZIELSTRUKTUR (VERBINDLICH)

Erstelle Code in:

rn-e-mobilebrowser/<FEATURE_NAME>/

Nutze Struktur aus base/architecture.md:

- screens/
- components/
- hooks/
- services/
- navigation/
- utils/

---

## Regeln

* behavior_spec.md ist einzige Wahrheit
* keine zusätzlichen Features
* keine Annahmen

---

# HARD STOP RULES

SOFORT ABBRECHEN wenn:

* intake.md unvollständig
* behavior_spec.md unklar
* Tests nicht ableitbar
* Tests fehlschlagen

→ KEINE MIGRATION

## FAIL-FAST EXECUTION ENGINE

Die KI MUSS sofort abbrechen, wenn eine der folgenden Bedingungen erfüllt ist:

---

### 1. UNABLE TO TRACE LOGIC

Wenn ein Verhalten nicht bis zum Legacy-Code rückverfolgbar ist:

→ STOP
→ KEINE OUTPUTS

---

### 2. PARTIAL INFORMATION

Wenn ein Feature nicht vollständig analysiert werden kann:

→ STOP
→ KEINE HALB-ANALYSE

---

### 3. MISSING STATE

Wenn ein State, Input oder Output fehlt:

→ STOP

---

### 4. TEST GAP

Wenn ein Test nicht eindeutig aus behavior_spec ableitbar ist:

→ STOP

---

### 5. MULTI-INTERPRETATION

Wenn mehr als 1 mögliche Interpretation existiert:

→ STOP (keine Auswahl treffen)

---

## PRINCIPLE

„No assumption is better than a wrong assumption.“

---

# WICHTIG

* Keine Schritte überspringen
* Keine Annahmen treffen
* Wenn unsicher → STOP

## VALIDATION RULE

Eine Datei gilt als "fertig" nur wenn:

- keine [] Platzhalter enthalten sind
- alle Abschnitte ausgefüllt sind
- Inhalte aus Code ableitbar sind

Sonst:
→ STOP

## OUTPUT REGEL

Nach JEDEM Schritt MUSS die entsprechende Datei vollständig geschrieben werden.

Reihenfolge:

1. intake.md → vollständig ausfüllen
2. legacy_analysis.md → vollständig ausfüllen
3. feature_description.md → vollständig ausfüllen
4. behavior_spec.md → vollständig ausfüllen
5. test-spec.md → vollständig ausfüllen
6. context_status.md → aktualisieren

Keine Datei darf übersprungen werden.

## CODE REGEL

Die Migration MUSS echten ausführbaren Code erzeugen.

Kein Pseudocode.
Keine Beschreibung.
Nur produktionsnaher Code.

## OUTPUT FORMAT (RN CODE)

Alle generierten Dateien müssen folgende Pfade enthalten:

rn-e-mobilebrowser/<FEATURE_NAME>/screens/...
rn-e-mobilebrowser/<FEATURE_NAME>/services/...
rn-e-mobilebrowser/<FEATURE_NAME>/hooks/...

Jede Datei muss mit vollständigem Pfad angegeben werden.

---

## Wenn STOP:

→ Erstelle Datei:
features/<FEATURE_NAME>/failure_report.md

Inhalt:
- Grund für STOP
- betroffene Phase
- fehlende Information