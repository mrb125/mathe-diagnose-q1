# Anforderungen: Geplante Erweiterungen

**Status:** Backlog – noch nicht implementiert
**Architektur-Basis:** siehe `ARCHITECTURE.md`
**Betrifft:** `index.html` (Mathe Q1) und `index-physik-atomkern.html` (Physik Atomkern)

---

## Übersicht

| # | Feature | Priorität | Abhängigkeiten |
|---|---|---|---|
| 1 | Erklär-Feedback nach falschen Antworten | Hoch | – |
| 2 | Selbsteinschätzung vor dem Quiz | Hoch | – |
| 3 | Spaced Repetition / Wiederholungs-Modus | Mittel | Feature 1 |
| 4 | Doppel-Joker (Hinweis + 50:50) | Mittel | – |
| 5 | Kategorienauswahl vor dem Start | Mittel | – |
| 7 | Formelblatt / Merkkarten | Mittel | – |
| 9 | Fehleranalyse für Lehrperson (Power Automate) | Niedrig | Feature 1 |
| 10 | Adaptive Schwierigkeit vorwärts | Niedrig | difficulty-Feld in Mathe-Daten |

---

## Feature 1: Erklär-Feedback nach falschen Antworten

### Beschreibung

Nach einer falschen Antwort wird eine farbige Erklär-Box eingeblendet, die erklärt *warum* die richtige Antwort korrekt ist. Fördert nachhaltiges Verständnis statt bloßem Ausschlussprinzip.

### Datenstruktur-Änderung

```js
{
  // ... bestehende Felder ...
  explanation: String, // Erklärung, die nach falscher Antwort erscheint
}
```

> `explanation` ist optional – fehlt das Feld, erscheint keine Erklär-Box.

### UI-Verhalten

| Zustand | Verhalten |
|---|---|
| Richtige Antwort | Keine Erklärung (nur grünes Feedback) |
| Falsche Antwort | Erklär-Box erscheint unter den Antwort-Buttons |
| Design | Rote/gedämpfte Box, leicht abgesetzt, klarer Text |
| Timing | Erscheint gleichzeitig mit der Auswertung, vor dem Weiter-Button |

### Inhalt (Claude schreibt alle Erklärungen)

Die Erklärungstexte werden direkt ins `allQuestions`-Array geschrieben. Sie sollen:
- Die richtige Antwort begründen (nicht nur nennen)
- Auf häufige Fehlvorstellungen eingehen
- Kurz bleiben (1–3 Sätze)

---

## Feature 2: Selbsteinschätzung vor dem Quiz

### Beschreibung

Zwischen Start-Screen und Quiz erscheint ein neuer Screen, auf dem Schülerinnen und Schüler für jede Kategorie einschätzen, wie sicher sie sich fühlen. Am Ende wird die Einschätzung mit dem tatsächlichen Ergebnis verglichen.

Fördert Metakognition (Selbstwahrnehmung des eigenen Lernstands).

### Neuer Screen: `#selfcheck-screen`

```html
<div id="selfcheck-screen" class="screen">
  <!-- Überschrift: "Wie sicher bist du?" -->
  <!-- Pro Kategorie: Label + 3 Buttons (Sicher / Unsicher / Gar nicht) -->
  <!-- Start-Button → wechselt zu #quiz-screen -->
</div>
```

### Datenstruktur (Runtime)

```js
const selfRatings = {
  "ableitung": "sicher",    // "sicher" | "unsicher" | "garnicht"
  "stamm": "unsicher",
  // ...
};
```

### Result-Screen: Vergleichstabelle

Neue Sektion im `#result-screen`:

| Kategorie | Einschätzung | Ergebnis | Übereinstimmung |
|---|---|---|---|
| Ableitungsregeln | Sicher | 4/4 ✅ | ✓ |
| Stammfunktionen | Unsicher | 3/4 🟡 | ✓ |
| Integrale | Sicher | 1/3 🔴 | ✗ Überschätzt |

### Ampel-Logik für Übereinstimmung

| Einschätzung | Ergebnis | Bewertung |
|---|---|---|
| Sicher | ratio ≥ 0.75 | Passt ✓ |
| Sicher | ratio < 0.75 | Überschätzt ✗ |
| Unsicher | ratio ≥ 0.75 | Unterschätzt ✗ (positiv!) |
| Unsicher / Garnicht | ratio < 0.75 | Passt ✓ |
| Garnicht | ratio ≥ 0.75 | Unterschätzt ✗ (sehr positiv!) |

### localStorage (optional)

```js
localStorage.setItem("[tool]-self-ratings", JSON.stringify(selfRatings));
```

---

## Feature 3: Spaced Repetition / Wiederholungs-Modus

### Beschreibung

Falsch beantwortete Fragen werden in localStorage gespeichert. Beim nächsten Besuch kann der Schüler gezielt diese Fragen wiederholen.

### localStorage-Datenstruktur

```js
// Gespeichert nach jedem Quiz-Ende
localStorage.setItem("[tool]-review-queue", JSON.stringify([
  { text: "Was ist die Ableitung von f(x) = e^(3x)?", categoryId: "ableitung" },
  // ... weitere falsch beantwortete Fragen (max. 15 gespeichert)
]));
```

> Alternativ: Speicherung per Fragen-Index (stabiler, wenn Fragen nicht umbenannt werden)

### Start-Screen: Wiederholen-Button

- Erscheint nur, wenn `[tool]-review-queue` nicht leer ist
- Button-Text: "🔁 [N] Fragen wiederholen"
- Startet Quiz mit ausschließlich den gespeicherten Fragen

### Review-Modus Besonderheiten

| Merkmal | Verhalten |
|---|---|
| Queue | Nur falsch beantwortete Fragen aus letzter Session |
| Fallback-Inject | Deaktiviert (kein Sicherheitsnetz) |
| Level-2 | Deaktiviert |
| Scores | Eigene temporäre Auswertung (nicht in Power Automate) |
| Nach Review | Review-Queue wird geleert wenn alle richtig beantwortet |

---

## Feature 4: Doppel-Joker (Hinweis + 50:50)

### Beschreibung

Zusätzlich zum bestehenden Hinweis-Joker gibt es einen 50:50-Joker, der zwei falsche Antwortoptionen entfernt und so die Wahrscheinlichkeit erhöht, die richtige Antwort zu erraten.

### Joker-Übersicht (nach Erweiterung)

| Joker | Kosten | Effekt | Bedingung |
|---|---|---|---|
| 💡 Hinweis | −50 XP | Zeigt `q.hint` als Text-Box | XP ≥ 50, nur einmal pro Frage |
| 50:50 | −50 XP | Blendet 2 falsche Optionen aus | XP ≥ 50, nur mc-Fragen, mind. 4 Optionen |

### UI-Änderung

```html
<!-- Beide Buttons nebeneinander in #joker-area -->
<button id="btn-joker">💡 Hinweis</button>
<button id="btn-fifty">50:50</button>
```

### 50:50-Logik

1. Alle falschen Optionen ermitteln (alle außer `q.correct`)
2. 2 davon zufällig auswählen
3. Diese 2 Buttons: `display: none` oder `opacity: 0.2 + pointer-events: none`
4. `btn-fifty.disabled = true` nach Nutzung
5. Kann auch nach Hinweis-Joker genutzt werden (und umgekehrt)

### Einschränkungen

- Nicht verfügbar bei `type: "text"` (Mathe-Tool: Freitext-Fragen)
- Nicht verfügbar wenn weniger als 3 Optionen verbleiben

---

## Feature 5: Kategorienauswahl vor dem Start

### Beschreibung

Schülerinnen und Schüler können vor dem Quiz wählen, welche Kategorien sie üben möchten. Ermöglicht gezieltes Lernen einzelner Themenbereiche.

### UI-Platzierung

Option A: Zusätzliche Sektion auf dem `#start-screen` (einfacher)
Option B: Eigener Screen `#category-select-screen` (sauberer)

### UI-Mockup (Option A)

```
[Start-Screen]
Name eingeben: ___________

Kategorien wählen:
☑ Ableitungsregeln     ☑ Stammfunktionen
☑ Bestimmte Integrale  ☑ Sachzusammenhänge
☑ Graphenanalyse       ☑ Beschränktes Wachstum

[QUIZ STARTEN]
```

### Logik-Änderungen

| Bereich | Änderung |
|---|---|
| `buildQueue()` | Filtert `allQuestions` auf `selectedCategories` |
| `scores`-Objekt | Wird nur für gewählte Kategorien initialisiert |
| Fallback-Inject | Nur wenn Fallback-Frage zur gewählten Kategorie gehört |
| Mindestauswahl | Start-Button disabled wenn keine Kategorie ausgewählt |

### localStorage (optional)

```js
localStorage.setItem("[tool]-selected-categories", JSON.stringify(["ableitung", "stamm"]));
```

---

## Feature 7: Formelblatt / Merkkarten

### Beschreibung

Ein Formelblatt-Button im Quiz-HUD öffnet ein Modal mit den wichtigsten Formeln und Regeln des jeweiligen Themas. Konfigurierbar durch die Lehrkraft (immer sichtbar / nur erste N Fragen / nie).

### UI

```html
<!-- Im HUD, neben Joker-Buttons -->
<button id="btn-formulas" onclick="toggleFormulaSheet()">📋 Formelblatt</button>

<!-- Modal, außerhalb des HUD -->
<div id="formula-modal">
  <div id="formula-content"><!-- Tool-spezifischer Inhalt --></div>
  <button onclick="closeFormulaSheet()">✕ Schließen</button>
</div>
```

### Konfiguration (Konstante im JS)

```js
const FORMULA_SHEET_MODE = "always"; // "always" | "never" | "first5"
```

---

### Formelblatt-Inhalt: Mathe Q1

#### Ableitungsregeln

| Regel | Formel |
|---|---|
| Potenzregel | (xⁿ)' = n·xⁿ⁻¹ |
| Kettenregel | (f(g(x)))' = f'(g(x)) · g'(x) |
| Produktregel | (u·v)' = u'·v + u·v' |
| e-Funktion | (e^x)' = e^x |
| e-Funktion mit k | (e^(kx))' = k·e^(kx) |

#### Stammfunktionen / Aufleiten

| Funktion | Stammfunktion |
|---|---|
| f(x) = xⁿ (n ≠ −1) | F(x) = xⁿ⁺¹/(n+1) |
| f(x) = c (Konstante) | F(x) = c·x |
| f(x) = e^x | F(x) = e^x |
| f(x) = e^(kx) | F(x) = (1/k)·e^(kx) |

#### Bestimmtes Integral

```
∫[a→b] f(x) dx = F(b) − F(a)
```

> **Achtung Vorzeichenwechsel:** Hat f(x) eine Nullstelle zwischen a und b,
> muss das Integral in Teilbereiche aufgeteilt werden und die Fläche
> als Betragssumme berechnet werden!

#### Wachstum & Zerfall (Sachaufgaben)

```
f(t) = c · e^(k·t)
```

| Symbol | Bedeutung |
|---|---|
| c | Startwert: f(0) = c |
| k > 0 | Exponentielles Wachstum |
| k < 0 | Exponentieller Zerfall |
| t | Zeit |

#### Beschränktes Wachstum

```
f(t) = S − (S − f₀) · e^(−k·t)
```

| Symbol | Bedeutung |
|---|---|
| S | Sättigungsgrenze (Grenzwert für t → ∞) |
| f₀ | Anfangswert f(0) |
| k > 0 | Wachstumsrate |

---

### Formelblatt-Inhalt: Physik Atomkern

#### Strahlungsarten

| Strahlung | Zusammensetzung | Ladung | Reichweite | Abschirmung |
|---|---|---|---|---|
| α (Alpha) | 2 Protonen + 2 Neutronen (⁴He-Kern) | +2 | Wenige cm in Luft | Papier, Haut |
| β⁻ (Beta minus) | Elektron (e⁻) | −1 | Einige m in Luft | Aluminiumblech |
| β⁺ (Beta plus) | Positron (e⁺) | +1 | Einige m in Luft | Aluminiumblech |
| γ (Gamma) | Elektromagnetische Strahlung | 0 | Sehr groß | Blei, dickes Beton |

#### Zerfallsgleichungen

| Zerfallsart | Änderung Ordnungszahl Z | Änderung Massenzahl A |
|---|---|---|
| α-Zerfall | Z − 2 | A − 4 |
| β⁻-Zerfall | Z + 1 | A unverändert |
| β⁺-Zerfall | Z − 1 | A unverändert |
| γ-Strahlung | unverändert | unverändert |

#### Nuklidschreibweise

```
    A
    X    →  A = Massenzahl (Nukleonen = Protonen + Neutronen)
    Z        Z = Ordnungszahl (= Protonenzahl)
             N = A − Z  (Neutronenzahl)
```

#### Halbwertszeit

```
N(t) = N₀ · (½)^(t / T½)
```

| Symbol | Bedeutung |
|---|---|
| N(t) | Anzahl radioaktiver Kerne zum Zeitpunkt t |
| N₀ | Anfangsanzahl (t = 0) |
| T½ | Halbwertszeit |
| t | Zeit |

> **Merke:** Nach n Halbwertszeiten gilt: N = N₀ · (½)ⁿ
> Die Aktivität A ist proportional zu N: A ∝ N

---

## Feature 9: Fehleranalyse für Lehrperson (Power Automate)

### Beschreibung

Der Power-Automate-Payload wird um Fehleranalyse-Felder erweitert: Pro Kategorie wird gesendet, welche falschen Antworten die Schülerin / der Schüler gewählt hat. Ermöglicht der Lehrkraft, systematische Fehlvorstellungen der ganzen Klasse zu erkennen.

### Runtime-Datenstruktur

```js
const wrongChoices = {
  "ableitung": [
    { q: "Ableitung von f(x) = e^(3x)?", chosen: "3·e^x", correct: "3·e^(3x)" }
  ],
  // ... pro Kategorie, nur falsche Antworten
};
```

### Erweiterte Payload-Felder

```json
{
  "Datum": "TT.MM.JJJJ",
  "Name": "Schülername",
  "XP": 980,
  "Level": 4,

  "Ableitungsregeln": "3/4",
  "Ableitungsregeln_Fehler": "f(x)=e^(3x) → gewählt: 3·e^x | ...",

  "Stammfunktionen": "4/4",
  "Stammfunktionen_Fehler": "",

  "Strahlung": "2/4",
  "Strahlung_Fehler": "α-Zerfall → gewählt: β-Teilchen | ..."
}
```

### Datenschutz-Hinweis

- Keine zusätzlichen personenbezogenen Daten (nur Name wie bisher)
- Fehleranalyse ist inhaltsbezogen, nicht verhaltensbezogen
- Excel-Spalten für `_Fehler`-Felder müssen vorab im Flow angelegt werden

### Technische Änderungen

1. Tracking: In `submitAnswer()` bei falscher Antwort `wrongChoices[categoryId]` befüllen
2. Serialisierung: Kompaktes Stringformat (Pipe-getrennt) für Excel-Lesbarkeit
3. Payload: In `reportToFlow()` die `_Fehler`-Felder anhängen

---

## Feature 10: Adaptive Schwierigkeit vorwärts

### Beschreibung

Nach 3 aufeinanderfolgenden richtigen Antworten in **derselben Kategorie** wird eine schwerere "Herausforderungs-Frage" dieser Kategorie injiziert. Pendant zur Fallback-Logik (die rückwärts adaptiert).

### Trigger-Bedingung

```
consecutiveCorrect[categoryId] >= 3
→ Inject nächster "hard"-Frage derselben Kategorie
→ Meldung: "🔥 Herausforderung freigeschaltet!"
→ consecutiveCorrect[categoryId] = 0  (Reset)
```

### Runtime-Datenstruktur

```js
const consecutiveCorrect = {
  "ableitung": 0,
  "strahlung": 0,
  // ... pro Kategorie
};
```

### Herausforderungs-Fragen

| Tool | Quelle | Kennzeichnung |
|---|---|---|
| Physik | Bereits bestehende `difficulty: "hard"` Fragen | Bereits im Daten-Array |
| Mathe | Neue Fragen mit `difficulty: "hard"` (noch zu ergänzen) | Bisher kein `difficulty`-Feld |

> **Achtung Mathe-Tool:** Das `difficulty`-Feld muss in allen Mathe-Fragen nachgetragen werden (z. B. Level-2-Fragen = hard; normale Fragen = easy/medium). Datenstruktur-Änderung nötig.

### Scoring-Verhalten

| Merkmal | Verhalten |
|---|---|
| Zählt in `scores.correct` | **Ja** (im Gegensatz zu Fallback-Fragen) |
| Ratio-Cap | `Math.min(correct / total, 1)` weiterhin anwenden |
| Level-2-Fragen (Mathe) | Gelten nicht als Herausforderungs-Fragen |
| Doppelter Inject | Verhindern: Frage markieren mit `_challenged: true` |

### Inject-Logik

```js
function injectChallenge(categoryId) {
  const hardQ = allQuestions.find(q =>
    (q.categoryId || q.category) === categoryId &&
    q.difficulty === "hard" &&
    !q._challenged &&
    !currentQueue.includes(q)
  );
  if (!hardQ) return;
  hardQ._challenged = true;
  currentQueue.splice(currentIndex + 1, 0, { ...hardQ, _isChallenge: true });
}
```

---

## Abhängigkeiten & Implementierungsreihenfolge

```
Feature 1 (Explanation)          → unabhängig, zuerst umsetzen
Feature 2 (Selbsteinschätzung)   → unabhängig
Feature 5 (Kategorienauswahl)    → unabhängig, aber Queue-Logik ändert sich
Feature 4 (50:50-Joker)          → unabhängig
Feature 7 (Formelblatt)          → unabhängig (Inhalt ist oben vollständig)
Feature 3 (Spaced Repetition)    → benötigt Feature 1 (falsche Antworten tracken)
Feature 9 (Fehleranalyse PA)     → benötigt Feature 1 (wrongChoices-Tracking)
Feature 10 (Vorwärts-Adaptiv)    → benötigt difficulty-Feld in Mathe-Fragen
```
