# Feature Folders – React Native Migration

## Overview

Diese Verzeichnis enthält die Struktur für alle Features, die nacheinander mittels AI-gestützter Code-Generation in React Native (Expo) migriert werden.

## Reihenfolge der Migration

| # | Feature | Priority | Complexity | Dependencies |
|---|---------|----------|-----------|--------------|
| **0** | *Projektbasis* | - | - | - |
| **1** | storage-config | High | Low | - |
| **2** | login | High | Medium | storage-config |
| **3** | navigation | High | Medium | login + storage-config |
| **4** | webview | High | Medium | navigation |
| **5** | settings | Medium | Low | storage-config |
| **6** | qr-scanner | Medium | High | navigation |
| **7** | barcode-scanner | Medium | High | navigation |
| **8** | extended-features | Low | High | all above |
| **9** | platform-specific | Low | High | all above |
| **10** | optional | Low | Medium | optional |

## Folder Structure

Jeder Feature-Ordner (`01-storage-config/`, `02-login/`, etc.) enthält:

```
FEATURE_FOLDER/
├── intake.md                 # Legacy Code Analysis
├── legacy_analysis.md        # Verhaltensdokumentation
├── behavior_spec.md          # Feature Verhaltensspezifikation
├── feature_description.md    # Zusammenfassung
├── mapping.md                # iOS/Android → RN Mapping
├── test_spec.md              # Test Spezifikation
├── context_status.md         # Validierungsstatus
├── migration_report.md       # RN Migrationsbericht
├── execution_metrics.md      # Metriken & Perfor
mance
└── execution_log.md          # Ausführungsprotokoll
```

## Workflow Pro Feature

Für jedes Feature wird dieser Prompt eingegeben:

1. **User definiert:** `FEATURE_NAME = <feature_name>` im Prompt
2. **KI führt PRE-PHASE bis PHASE 10 durch:**
   - PRE-PHASE: Findet Legacy-Code in ios-mobilebrowser/Source + android-mobilebrowser/app/src
   - PHASE 1-5: Analysiert & dokumentiert Verhaltensweisen
   - **PHASE 6: GENERIERT VOLLSTÄNDIGEN RN CODE** (TypeScript/React)
   - PHASE 7-10: Validiert & dokumentiert

3. **Output in Feature-Ordner:**
   - Alle 10 Dokumentationsdateien gefüllt
   - `src/` Folder mit komplettem RN-Code
   - Tests geschrieben & ausführbar

## Start mit Feature 01-storage-config

```bash
# 1. Prompt aus prompt.md eingeben (mit FEATURE_NAME = storage-config)
# 2. KI generiert Code + Dokumentation
# 3. Ergebnis in features/01-storage-config/
# 4. npm install & npm start
# 5. Prüfen ob alles funktioniert
# 6. Commit & Next Feature
```

## Feature-Beschreibungen

### 01-storage-config
**Wofür:** Zentrale Storage-Verwaltung (Token, URLs, Config)  
**Complexity:** Low  
**Proviorities:** Wird von fast allen anderen Features genutzt

### 02-login
**Wofür:** Authentication UI + API Integration  
**Complexity:** Medium  
**Dependencies:** 01-storage-config

### 03-navigation
**Wofür:** App Navigation + Session Handling  
**Complexity:** Medium  
**Dependencies:** 01-storage-config, 02-login

### 04-webview
**Wofür:** WebView für URL-Laden mit Token-Injection  
**Complexity:** Medium  
**Dependencies:** 03-navigation

### 05-settings
**Wofür:** Settings-Screen (URLs, Sprache, Config ändern)  
**Complexity:** Low  
**Dependencies:** 01-storage-config

### 06-qr-scanner
**Wofür:** QR-Code Scanner  
**Complexity:** High  
**Dependencies:** 03-navigation

### 07-barcode-scanner
**Wofür:** Barcode Scanner  
**Complexity:** High  
**Dependencies:** 03-navigation

### 08-extended-features
**Wofür:** Mehrsprachigkeit, QR Config Import, etc.  
**Complexity:** High  
**Dependencies:** Alle obigen

### 09-platform-specific
**Wofür:** Multi-Flavor (Android), Build-Configs  
**Complexity:** High  
**Dependencies:** Alle obigen

### 10-optional
**Wofür:** License Screen, Edge Cases  
**Complexity:** Medium  
**Dependencies:** Optional

## Wichtige Regeln

### Für jeden Prompt-Durchlauf:
1. **FEATURE_NAME muss eindeutig sein** (01-storage-config, 02-login, etc.)
2. **iOS/Android Code muss im Workspace sein** (ios-mobilebrowser/Source + android-mobilebrowser/app/src)
3. **Dokumentation MUSS gefüllt werden** bevor KI Code generiert
4. **RN Code wird in src/ geschrieben** (nicht in Feature-Ordner)
5. **Alle Tests müssen lauffähig sein** (npm test)

### Nach Code-Generation:
```bash
# 1. In sein RN-Projekt kopieren
cp -r src/ /path/to/rn-project/

# 2. Dependencies installieren
npm install $(cat dependencies.json)

# 3. Tests laufen lassen
npm test

# 4. App starten
npm start
```

## Status Tracking

Jeder Feature-Ordner hat `context_status.md` + `execution_log.md` um Status zu tracken:

- ✅ COMPLETE – Feature ist fertig & getestet
- 🟡 IN_PROGRESS – Feature wird gerade migriert
- ❌ FAILED – Feature hat Fehler (siehe execution_log.md)

## Nächste Schritte

1. **Review prompt.md** – Der universelle Prompt für ALLE Features
2. **Start mit Feature 01-storage-config** – Einfach, niedrige Komplexität
3. **Evaluate resultat** – Hat KI korrekten Code generiert?
4. **Iterieren** – Bei Bedarf prompt.md anpassen
5. **Next Feature** – 02-login starten

---

**Ziel:** Mit diesem System kannst du systematisch Features migrieren, alle KI-Systeme mit dem gleichen Setup testen, und Ergebnisse vergleichen.
