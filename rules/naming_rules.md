# NAMING RULES

---

# CORE PRINCIPLE
- Alle Dateien müssen englische Namen verwenden
- Sprechende, selbsterklärende Namen verwenden
- Keine Abkürzungen außer allgemein etablierten Standards (API, URL, ID)
- Namen müssen Zweck und Verantwortung eindeutig beschreiben
- Konsistente Benennung im gesamten Projekt verwenden

- Klassen: PascalCase
- Klassenname muss immer dem Dateinamen entsprechen

- React Native Components: PascalCase
- Component-Dateiname muss immer dem Component-Namen entsprechen

- Funktionen/Methoden: camelCase
- Variablen: camelCase
- Konstanten: UPPER_SNAKE_CASE

- Interfaces mit klarer Rollenbeschreibung benennen

- Boolean-Variablen müssen wie Fragen lesbar sein:
  isEnabled
  hasPermission
  canNavigate

- Klassen sollen Substantive sein:
  BrowserSession
  NetworkClient
  UserRepository

- Dateinamen müssen den Hauptinhalt widerspiegeln

- Keine numerischen oder unsauberen Suffixe:
  LoginScreen2
  ApiHandlerFinal
  NewService
  TempHandler

- Kurze Namen bevorzugen, aber niemals auf Kosten der Verständlichkeit

- Singular für einzelne Objekte:
  user

- Plural für Collections:
  users

- Testdateien müssen Bezug zur getesteten Klasse oder Component haben:
  UserService.test.ts
  LoginScreen.test.tsx

- Hooks müssen mit "use" beginnen:
  useAuth
  useBrowserSession

- Screens müssen mit "Screen" enden:
  HomeScreen
  SettingsScreen

- Contexts müssen mit "Context" enden:
  AuthContext

- Providers müssen mit "Provider" enden:
  AuthProvider

- Types-Dateien mit "*.types.ts" benennen
- Constants-Dateien mit "*.constants.ts" benennen
- Hooks-Dateien mit "*.hook.ts" oder im hooks/ Ordner organisieren


---

# 1. ÜBERTITEL

## NR-0001 TITEL
text

---

# 2. ÜBERTITEL

## E-0101 TITEL
text

---

