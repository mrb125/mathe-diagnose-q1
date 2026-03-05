# Diagnose-Tool – Gemeinsame Architektur

## Zweck

Interaktive, gamifizierte Diagnose-Tools als einzelne HTML-Datei für den Einsatz im Unterricht.
Schwerpunkt: iPad mit Safari. Kein Netz, kein Backend erforderlich.

---

## Technische Grundprinzipien

| Merkmal | Wert |
|---|---|
| Format | Eine einzige `.html`-Datei pro Tool |
| Abhängigkeiten | Keine (kein CDN, kein Framework, kein Build-Step) |
| Sprache | Vanilla HTML + CSS + JavaScript (ES2020+) |
| PWA | `<meta name="apple-mobile-web-app-capable" content="yes">` |
| Zielgeräte | iPad (Safari), iPhone, Desktop |
| Hosting | GitHub Pages oder lokaler HTTP-Server (nicht `file://` – sonst kein Power Automate) |

---

## 3-Screen-Struktur

Alle Tools folgen demselben Drei-Phasen-Aufbau:

```
Phase 1: #start-screen   → Name eingeben, Best-Score, Start-Button
Phase 2: #quiz-screen    → HUD + Frage + Antwortbereich + Joker + Fortschrittsbalken
Phase 3: #result-screen  → Zertifikat, Kategorie-Feedback (Ampel), Drucken, Neustart
```

Sichtbarkeit wird per CSS-Klasse `.screen` / `.screen.active` gesteuert.

---

## Fragen-Datenstruktur

Alle Fragen werden als JS-Array `allQuestions` definiert:

```js
{
  category:     String,   // Anzeigename der Kategorie (z. B. "Ableitungsregeln")
  categoryId:   String,   // Schlüssel im scores-Objekt (z. B. "ableitung")
                           // Im Physik-Tool heißt dieses Feld ebenfalls "category"
  type:         String,   // "mc" | "VisualGraph" | "text"
  isFallback:   Boolean,  // true = Fallback-Frage; zählt nicht in scores.total
                           // Im Physik-Tool: Feld heißt "fallback" statt "isFallback"
  isLevel2:     Boolean,  // optional: nur im Mathe-Tool; erscheint erst ab Level 2
  correct:      Number | String[],  // Index 0-N für mc/VisualGraph; Akzeptanzliste für text
  options:      String[], // nur bei mc / VisualGraph
  hint:         String,   // Tipp-Text für das Joker-System
  xpValue:      Number,   // Basis-XP (Physik-Tool); Mathe-Tool berechnet XP dynamisch
  difficulty:   String,   // "easy" | "medium" | "hard"
                           // Physik-Tool: bereits in allen Fragen vorhanden
                           // Mathe-Tool: geplant (Feature 10), noch nicht eingetragen
  numericInput: Boolean,  // optional: true → <input type="number"> statt text
  graphSVG:     String,   // optional: inline SVG-String für VisualGraph

  // --- Geplante Erweiterungen (siehe requirements-erweiterungen.md) ---
  explanation:  String,   // [Feature 1] Erklärung nach falscher Antwort (1–3 Sätze)
}
```

### Fragetypen

| Typ | Antwortmethode | `correct`-Typ |
|---|---|---|
| `mc` | Multiple-Choice-Div-Buttons (klickbar) | `Number` (0-basierter Index) |
| `VisualGraph` | SVG-Grafik + Multiple-Choice | `Number` |
| `text` | Freitexteingabe (`<input>`) | `String[]` (akzeptierte Formulierungen) |

---

## Kategorie-Scores-Objekt

```js
const scores = {
  "[categoryId]": { correct: 0, total: N, name: "Anzeigename" },
  // ...
};
```

- `total` = Anzahl der regulären Fragen (kein Fallback, kein Level2) in dieser Kategorie
- `correct` wird nur erhöht wenn `!isFallback` (bzw. `!fallback` im Physik-Tool)
- Verhältnis: `Math.min(correct / total, 1)` → Level-2-Fragen können Ratio nie über 1 treiben

---

## Gamification-Engine

### XP-Berechnung

**Mathe-Modell** (dynamisch):
```
xpGain = 100 + (streak × 20) + speedBonus
speedBonus = 50  falls: Antwortzeit ≤ 10 s  UND  kein Joker genutzt  UND  keine Fallback-Frage
```

**Physik-Modell** (frage-basiert):
```
gain = q.xpValue
gain = round(gain × 1.5)  falls: streak >= 3
```

### Level-Up (beide Tools)
```
level = floor(xp / 250) + 1
```

### Streak-Bonus
- Increment bei richtiger Antwort
- Reset auf 0 bei falscher Antwort
- CSS-Klasse `streak-fire` ab Streak ≥ 3 (Animation)

### Joker-System
- Kosten: **−50 XP**
- Zeigt `q.hint` als formatierte Box an
- Button wird nach Nutzung `disabled`
- Button ist **nicht sichtbar/nutzbar** wenn XP < 50

### Adaptive Difficulty
- Nach **2 aufeinanderfolgenden Fehlern** in derselben Kategorie:
  - Fallback-Frage der Kategorie wird **direkt nach der aktuellen** injiziert (`splice`)
  - Meldung: *"⚠️ Sicherheitsnetz aktiviert"*
  - `consecutiveMistakes` wird auf 0 zurückgesetzt
- Fallback-Fragen zählen **nicht** in die Kategorie-Auswertung (`scores.correct`)
- Zähler wird bei richtiger Antwort ebenfalls auf 0 gesetzt

---

## Auswertungs-Screen

### Ampelfarben pro Kategorie

| Ratio | Farbe | Bedeutung |
|---|---|---|
| 100 % | Grün (`--success`) | Exzellent – klausurbereit |
| 50–99 % | Gelb (`#f59e0b`) | Solide – konkreter Klausur-Tipp |
| < 50 % | Rot (`--error`) | Förderbedarf – Lernplan |

### Lernressourcen
- Werden nur eingeblendet wenn `ratio < 1`
- Pro Kategorie: Video-Links (YouTube-Suche) + Web-Links (mathebibel.de etc.)

---

## localStorage

| Tool | Name-Key | Best-XP-Key |
|---|---|---|
| Mathe Q1 | `diagnose-name` | `diagnose-best-xp` |
| Physik Atomkern | `physik-atomkern-name` | `physik-atomkern-best-xp` |

**Muster für neue Tools:** `[fach]-[thema]-name` / `[fach]-[thema]-best-xp`

---

## Power Automate Integration

```js
const FLOW_URL = "";  // leer lassen bis Flow-Setup abgeschlossen
```

- `reportToFlow()` wird **am Anfang von `showResults()`** aufgerufen
- Gibt sofort zurück (`return`) wenn `FLOW_URL` leer
- Payload-Schema:

```json
{
  "Datum":   "TT.MM.JJJJ",
  "Name":    "Schülername",
  "XP":      1340,
  "Level":   6,
  "[KategorieName]": "3/4"
}
```

- KategorieNamen im Payload entsprechen **Excel-Spaltennamen** → müssen beim Flow-Setup vorab definiert werden
- `fetch()` mit `Content-Type: application/json`, Fehler für Schüler unsichtbar (`.catch(() => {})`)

---

## Print / Zertifikat

- `window.print()` öffnet Browser-Druckdialog
- `@media print` blendet alles außer `#result-screen` aus (Buttons, HUD, Start-/Quiz-Screen)
- Saubere A4-Darstellung: weißer Hintergrund, schwarzer Text, keine Neon-Effekte
- `#result-screen::after` fügt Dokumenten-Footer per CSS ein

---

## Bekannte Einschränkungen

| Problem | Ursache | Lösung |
|---|---|---|
| Power Automate funktioniert nicht | `fetch()` von `file://` wird von iOS Safari blockiert | Tool via HTTP(S) hosten (GitHub Pages) |
| Antwort-Text-Fragen: Tippfehler werden als falsch gewertet | Nur exakte String-Übereinstimmung (normalisiert: lowercase, Whitespace entfernt) | Akzeptanzliste `correct[]` breit definieren |
| Adaptive Difficulty: Fallback kann mehrfach injiziert werden | Kein Duplikat-Check beim Inject | Aktuell kein Problem in der Praxis |
