<!-- GOLDEN_REFERENCE_START -->
# Analyse – Login

## iOS Implementation

- Datei: LoginViewController.swift
- Klasse: LoginViewController
- Framework: UIKit

### Ablauf

1. Button-Click → loginTapped()
2. Validierung (local)
3. URLSession POST Request
4. JSON Parsing
5. Speicherung via UserDefaults

### State

- isLoading: Bool
- errorMessage: String?

### Fehlerbehandlung

- HTTP Status Codes geprüft
- Fehler wird als Alert angezeigt

---

## Android Implementation

- Datei: LoginActivity.kt
- Klasse: LoginActivity
- Framework: Android SDK

### Ablauf

1. Button Click Listener
2. Validierung
3. Retrofit POST Request
4. Response Handling
5. Speicherung via SharedPreferences

### State

- LiveData<LoginState>

### Fehlerbehandlung

- Try/Catch
- Toast Messages

---

## Gemeinsame Logik

1. Eingaben validieren
2. API Request senden
3. Response auswerten
4. Token speichern
5. Navigation

---

## Unterschiede

| Aspekt        | iOS               | Android              |
|---------------|------------------|----------------------|
| Networking    | URLSession       | Retrofit             |
| Storage       | UserDefaults     | SharedPreferences    |
| UI Feedback   | Alert            | Toast                |

---

## Offene Fragen

- Token Ablaufzeit nicht klar
<!-- GOLDEN_REFERENCE_END -->