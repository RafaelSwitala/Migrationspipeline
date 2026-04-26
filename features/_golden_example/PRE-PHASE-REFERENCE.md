# PRE-PHASE – CODE DISCOVERY REFERENCE (storage-config)

Dieses Dokument zeigt, wie PRE-PHASE für das Feature `storage-config` aussieht.

## AUSGANGSPUNKT

```
FEATURE_NAME = storage-config
```

## DURCHSUCHUNG: ios-mobilebrowser/Source

**Relevante Dateien:**

| Datei | Grund | Zeilenbereiche |
|-------|-------|------|
| PreferencesUtils.swift | Storage Abstraktionslayer via UserDefaults | L1-180 |
| LoginViewController.swift | Login UI + Preferences R/W | L1-280 |
| UrlUtils.swift | URL Building | L1-80 |
| AppSettings.swift | Config Constants | L1-20 |

## DURCHSUCHUNG: android-mobilebrowser/app/src

**Relevante Dateien:**

| Datei | Grund | Zeilenbereiche |
|-------|-------|------|
| PreferencesUtils.java | Storage Abstraktionslayer via SharedPreferences | L1-150 |
| ConfigFileLoader.java | Config File laden + Mapping | L1-70 |
| LoginActivity.java | Login UI + Preferences R/W | L1-380 |
| App.java | App Lifecycle + Preferences Init | L1-150 (referenced) |

## ERGEBNIS PRE-PHASE

✅ Code gefunden  
✅ Keine Scope-Violations  
✅ Ready für Phase 0 (Consistency Check)

---

## NÄCHSTER SCHRITT: intake.md

Nach erfolgreichem PRE-PHASE wird aus diesem Code **intake.md** erstellt.

**Beispiel (vollständig gefüllt):**

```
# Intake – storage-config

## STATUS
- [x] COMPLETE

## FILES
### iOS
| Datei | Zweck | Verwendet | Referenzen |
| PreferencesUtils.swift | Storage Abstraktionslayer via UserDefaults | UserDefaults.standard Properties | L1-180 |
| LoginViewController.swift | Login UI + Entry Point | Preferences lesen/schreiben | L1-280 |
| UrlUtils.swift | URL Building | buildLoginUrl() | L1-80 |
| AppSettings.swift | Config Constants | Protokoll Enum | L1-20 |

### Android
| Datei | Zweck | Verwendet | Referenzen |
| PreferencesUtils.java | Storage Abstraktionslayer via SharedPreferences | SharedPreferences.Editor | L1-150 |
| ConfigFileLoader.java | Config File aus assets laden | Gson Mapping | L1-70 |
| LoginActivity.java | Login UI + Entry Point | Preferences lesen/schreiben | L1-380 |
| App.java | App Lifecycle + Config Init | SharedPreferences Setup | L1-150 (referenced) |

## ENTRY POINTS
| Plattform | Datei | Methode | Zeile | Trigger |
| Android | LoginActivity.java | onCreate() | 115-125 | App Start |
| Android | App.java | onCreate() | (referenced) | Before LoginActivity |
| Android | ConfigFileLoader.java | loadConfigFileSettings() | 13-26 | App Init |
| iOS | LoginViewController.swift | viewDidLoad() | 77-85 | ViewController Init |
| iOS | LoginViewController.swift | viewWillAppear() | 41-70 | Screen Display |

... (weitere Sections: API CALLS, STORAGE, NAVIGATION, SCOPE)
```

Diese intake.md wird dann INPUT für alle weiteren Phasen (1-10).
