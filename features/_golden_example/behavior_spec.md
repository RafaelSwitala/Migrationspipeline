<!-- GOLDEN_REFERENCE_START -->
# Behavior Specification – Login

## Status
- [x] Aus Legacy-Code abgeleitet
- [x] Verifiziert

## Quelle der Informationen
- iOS: LoginViewController.swift (Zeilen 45–120)
- Android: LoginActivity.kt (Zeilen 30–110)

---

## 1. Ziel des Features
Authentifizierung eines Nutzers über Backend-Service.

---

## 2. Inputs

| Name     | Typ    | Validierung                |
|----------|--------|----------------------------|
| email    | string | Muss gültige E-Mail sein   |
| password | string | Min. 6 Zeichen             |

---

## 3. Outputs

| Zustand  | Beschreibung |
|----------|-------------|
| Success  | User + Token |
| Error    | Fehlermeldung |

---

## 4. Hauptverhalten

1. Eingaben validieren
2. POST /login API aufrufen
3. Response verarbeiten:
   - 200 → Erfolg
   - 401 → falsche Credentials
4. Token speichern
5. Navigation auslösen

---

## 5. Zustände

- Idle
- Loading
- Success
- Error

---

## 6. Erfolgsfall

- Token wird gespeichert
- User wird weitergeleitet zur Home-Screen

---

## 7. Fehlerfälle

| Fall                  | Verhalten |
|-----------------------|----------|
| Ungültige E-Mail      | Validierungsfehler |
| Falsches Passwort     | "Invalid credentials" |
| Netzwerkfehler        | "Network error" |
| Timeout               | "Request timeout" |

---

## 8. Seiteneffekte

- API-Call
- Speicherung Token
- Navigation

---

## 9. Persistenz

- Key: "auth_token"
- Storage: SecureStore

---

## 10. Abhängigkeiten

- API: POST /login
- Storage: SecureStore
- Navigation: HomeScreen
<!-- GOLDEN_REFERENCE_END -->