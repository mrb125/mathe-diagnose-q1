# Anforderungen: Diagnose-Tool Physik – Struktur der Materie

**Datei:** `index-physik-atomkern.html`
**Architektur-Basis:** siehe `ARCHITECTURE.md`

---

## 1. Zielgruppe & Lehrplan

| Merkmal | Wert |
|---|---|
| Klassenstufe | Klasse 9 / 10 (je nach Schulform) |
| Fach | Physik |
| Themenbereich | Struktur der Materie – Kapitel 4.1–4.4 |
| Inhalte | Atomaufbau & Modelle, Isotope & Nuklidkarte, Strahlungsarten & Nachweis, Zerfallsprozesse, Halbwertszeit & Aktivität |
| Vorlage | Schulbuch „Natura Physik" (Klett), Kapitel „Struktur der Materie" |

---

## 2. Kategorien

| category (= categoryId) | Anzeigename | Fragen (regulär) | Fallback |
|---|---|---|---|
| `atomaufbau` | Atomaufbau & Modelle | 4 | 1 |
| `isotope` | Isotope & Nuklidkarte | 4 | 1 |
| `strahlung` | Strahlungsarten & Nachweis | 4 | 1 |
| `zerfall` | Zerfallsprozesse | 4 | 1 |
| `halbwertszeit` | Halbwertszeit & Aktivität | 4 | 1 |
| **Gesamt** | | **20 regulär + 5 Fallback = 25** | |

> **Hinweis:** Im Physik-Tool wird das Feld `category` gleichzeitig als Display-Name **und** als scores-Schlüssel verwendet (kein separates `categoryId`-Feld).

---

## 3. Fragetypen

| Typ | Beschreibung |
|---|---|
| `mc` | Alle Fragen sind Multiple-Choice mit 4 Antwortmöglichkeiten (1 richtig) |

> Kein `VisualGraph` und kein `text`-Typ im Physik-Tool (im Gegensatz zum Mathe-Tool).

---

## 4. Fragen-Datenstruktur (Physik-spezifisch)

```js
{
  category:   String,   // z. B. "atomaufbau" (= categoryId)
  options:    String[], // 4 Antwortmöglichkeiten
  correct:    Number,   // 0-basierter Index
  xpValue:    Number,   // Basis-XP: 60 (easy) | 80 (easy) | 100 (medium) | 120–140 (hard)
  difficulty: String,   // "easy" | "medium" | "hard"
  hint:       String,   // Tipp-Text für Joker
  fallback:   Boolean,  // true = Fallback-Frage (Feld heißt "fallback", nicht "isFallback"!)
}
```

---

## 5. XP & Gamification

| Parameter | Wert |
|---|---|
| XP pro Frage | Individuell per `q.xpValue` (60–140 XP) |
| Streak-Multiplikator | × 1.5 (gerundet) ab Streak ≥ 3 |
| Joker-Kosten | −50 XP |
| Level-Up | alle 250 XP |
| Streak-Fire-Animation | ab Streak ≥ 3 |
| Speed-Bonus | **nicht** vorhanden (nur im Mathe-Tool) |
| Level-2-System | **nicht** vorhanden (nur im Mathe-Tool) |

### XP-Werte nach Schwierigkeit

| difficulty | xpValue |
|---|---|
| `easy` | 60–80 XP |
| `medium` | 80–100 XP |
| `hard` | 120–140 XP |
| Fallback | 60–80 XP |

---

## 6. Adaptive Difficulty – Fallback-Fragen

Jede Kategorie hat genau eine Fallback-Frage (`fallback: true`):

| Kategorie | Fallback-Inhalt |
|---|---|
| Atomaufbau | Größenordnung Atomkern vs. Atomhülle (10⁻¹⁵ vs. 10⁻¹⁰ m) |
| Isotope | Bedeutung der Nukleonen-/Massenzahl |
| Strahlung | Strahlenart mit geringster Reichweite (α) |
| Zerfallsprozesse | Was verändert sich beim β⁻-Zerfall? |
| Halbwertszeit | Definition Halbwertszeit |

> **Technisch:** Die Fallback-Frage wird beim Inject als `{ ...fb, _isFallback: true }` kopiert. Das Feld `_isFallback` (mit Unterstrich) wird laufzeitig gesetzt, nicht im `allQuestions`-Array.

---

## 7. Auswertungs-Tipps (categoryHints)

| category | Tipp-Inhalt |
|---|---|
| `atomaufbau` | Atommodelle (Thomson/Rutherford), Streuversuch, Größenverhältnisse (Kern 10⁻¹⁵ m, Hülle 10⁻¹⁰ m) |
| `isotope` | Z, N, A aus Isotopenschreibweise ablesen; A = Z + N; Quark-Zusammensetzung Proton/Neutron |
| `strahlung` | Tabelle der 3 Strahlenarten: Zusammensetzung, Ladung, Reichweite, Abschirmmaterial, Ionisierung |
| `zerfall` | Zerfallsgleichungen: α (Z−2, A−4), β⁻ (Z+1), β⁺ (Z−1), γ (Z und A unverändert) |
| `halbwertszeit` | Diagramme ablesen, Formel n = n₀·(½)^(t/T½), Nullrate, C-14-Methode |

---

## 8. Lernressourcen

Pro Kategorie werden bei `ratio < 1` Links zu **leifi.de** eingeblendet (themenspezifische Physik-Ressource).

---

## 9. Design & Farben

| Element | Wert |
|---|---|
| Stil | Dark / Clean-Neon (heller als Mathe-Tool) |
| Hintergrund | `#020d1a` |
| Primary-Glow | `#38bdf8` (Sky-Blue) |
| Secondary-Glow | `#fb923c` (Orange) |
| Joker-Farbe | `#fbbf24` (Gold) |
| Erfolg | `#22c55e` (Grün) |
| Fehler | `#ef4444` (Rot) |

---

## 10. localStorage

| Key | Inhalt |
|---|---|
| `physik-atomkern-name` | Letzter eingegebener Schülername |
| `physik-atomkern-best-xp` | Bisher höchste XP-Zahl |

---

## 11. Power Automate – Payload-Felder

```json
{
  "Datum":           "TT.MM.JJJJ",
  "Name":            "Schülername",
  "XP":              980,
  "Level":           4,
  "Atomaufbau":      "3/4",
  "Isotope":         "4/4",
  "Strahlung":       "2/4",
  "Zerfallsprozesse":"3/4",
  "Halbwertszeit":   "4/4"
}
```

---

## 12. Bekannte Abweichungen vom Mathe-Tool

| Merkmal | Mathe-Tool | Physik-Tool |
|---|---|---|
| Fallback-Flag im Daten-Array | `isFallback: true` | `fallback: true` |
| Fallback-Flag zur Laufzeit | direkt `q.isFallback` | `q._isFallback` (wird beim Inject gesetzt) |
| categoryId-Feld | `categoryId` (separates Feld) | `category` (doppelt genutzt) |
| XP-Formel | dynamisch (100 + streak×20 + speed) | `q.xpValue` × Streak-Multiplikator |
| Speed-Bonus | ja | nein |
| Level-2-System | ja | nein |
| Fragetypen | mc, VisualGraph, text | nur mc |
| Next-Button onclick | festes HTML-Attribut | wird in `submitAnswer()` auf "Weiter" umgeschrieben → muss in `loadQuestion()` zurückgesetzt werden |
