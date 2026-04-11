<!-- GOLDEN_REFERENCE_START -->
# Testfälle – Login

| ID  | Beschreibung              | Input                        | Erwartung |
|-----|--------------------------|------------------------------|----------|
| TC1 | Erfolgreicher Login      | valid email + password       | Success + Token gespeichert |
| TC2 | Falsches Passwort        | valid email + wrong password | Error: Invalid credentials |
| TC3 | Ungültige E-Mail         | invalid email                | Validation Error |
| TC4 | Netzwerkfehler           | valid input                  | Error: Network error |
| TC5 | Leere Eingaben           | "" / ""                      | Validation Error |
<!-- GOLDEN_REFERENCE_END -->