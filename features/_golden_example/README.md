# GOLDEN EXAMPLES – REFERENCE IMPLEMENTATION

Dieses Verzeichnis enthält vollständig durchgearbeitete Beispiele für verschiedene Features.

## VERFÜGBARE EXAMPLES

### 1. Login (Feature: Login)

**Status:** ✅ Vollständig durchgearbeitet

**Dateien:**
- `behavior_spec.md` – Verhalten spezifiziert
- `legacy-analysis.md` – Legacy Code analysiert
- `test-spec.md` – Tests definiert
- `context_status.md` – Status validiert
- `migration_report_login.md` – Migrationsbericht
- `feature-description.md` – Feature beschrieben

**Verwendung:** 
Referenz für die erwartete Struktur und Detailgrad.

---

### 2. storage-config (Feature: Storage & Config Management)

**Status:** 📋 PRE-PHASE + Phase-Struktur dokumentiert

**Verfügbare Dokumentation:**
- `PRE-PHASE-REFERENCE.md` – Zeigt, wie PRE-PHASE funktioniert
  - Code Discovery im Workspace
  - Relevante Dateien aus iOS/Android
  - Beispiel-intake.md Ergebnis

**Verwendung:** 
1. Lese `PRE-PHASE-REFERENCE.md` um zu verstehen, wie PRE-PHASE läuft
2. Das ist die Vorlage für deinen eigenen Prozess mit FEATURE_NAME=storage-config oder ein anderes Feature

---

## WIE MAN EIN GOLDEN EXAMPLE NUTZT

### Szenario 1: Du startest einen neuen Prompt mit FEATURE_NAME=storage-config

1. **PRE-PHASE:**
   - KI durchsucht `ios-mobilebrowser/Source` und `android-mobilebrowser/app/src`
   - KI erstellt intake.md (wie in `PRE-PHASE-REFERENCE.md` dokumentiert)

2. **Phases 0-10:**
   - KI nutzt intake.md um alle anderen Dateien zu generieren
   - Nutze die Login-Beispiele als Struktur-Referenz

3. **Outputs:**
   - Alle neuen Dateien gehen nach `features/storage-config/`
   - (Nicht nach `features/_golden_example/`)

### Szenario 2: Du startest einen neuen Prompt mit FEATURE_NAME=xyz (andere Feature)

- Gleicher Prozess: PRE-PHASE → Phases 0-10
- Outputs gehen nach `features/xyz/`
- Nutze Login als Struktur-Referenz
- Nutze storage-config als PRE-PHASE Referenz

---

## QUALITÄTS-STANDARDS AUS GOLDEN EXAMPLES

### Aus Login-Feature:

- **Vollständigkeit:** Jeder Behavior ist dokumentiert
- **Referenzierung:** Alle Aussagen haben Datei + Methode + Zeile
- **Determinismus:** Keine "kann", "optional", "meistens"
- **Testabdeckung:** Jeder State hat Tests

### Aus storage-config PRE-PHASE:

- **Code Discovery:** Systematische Suche in Legacy-Codebases
- **Struktur:** Files → Entry Points → API Calls → Storage → Navigation (in intake.md)
- **Scope:** Klar defniert: IN + OUT
- **Details:** Zeilenangaben für jede Referenz

---

## WARNUNG

❌ Diese Verzeichnis ist NUR für Referenz.  
❌ Outputs von KI-Läufen gehen NICHT hierher.  
❌ Nutze dein Feature-Verzeichnis: `features/<FEATURE_NAME>/`
