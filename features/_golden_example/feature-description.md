<!-- GOLDEN_REFERENCE_START -->
# Feature: Login

## Ziel
Der Nutzer kann sich mit E-Mail und Passwort authentifizieren, um Zugriff auf geschützte Inhalte zu erhalten.

## Inputs
- email: string (z. B. "user@example.com")
- password: string (mind. 6 Zeichen)

## Outputs
- Erfolgreich:
  - User-Objekt (id, email, token)
- Fehler:
  - Fehlermeldung (z. B. "Invalid credentials")

## Verhalten
- Nutzer gibt E-Mail und Passwort ein
- Klick auf "Login"
- Anfrage an Backend wird gesendet
- Bei Erfolg:
  - Token speichern
  - Navigation zur Startseite
- Bei Fehler:
  - Fehlermeldung anzeigen
<!-- GOLDEN_REFERENCE_END -->