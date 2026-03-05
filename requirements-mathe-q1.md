# Anforderungen: Diagnose-Tool Mathematik Q1 GK

**Datei:** `index.html`
**Architektur-Basis:** siehe `ARCHITECTURE.md`

---

## 1. Zielgruppe & Lehrplan

| Merkmal | Wert |
|---|---|
| Klassenstufe | Q1 (Jahrgangsstufe 11) |
| Kurstyp | Grundkurs (GK) |
| Lehrplan | NRW Kernlehrplan Mathematik |
| Themenbereich | Exponentialfunktionen, e-Funktionen, Integrale |
| Fokus | Nur abiturrelevante GK-Kompetenzen (keine Quotientenregel-Kombinationen, keine komplexe Substitution) |

---

## 2. Kategorien

| categoryId | Anzeigename | Fragen (regulär) | Fallback |
|---|---|---|---|
| `ableitung` | Ableitungsregeln | 4 | 1 |
| `stamm` | Stammfunktionen | 4 | 1 |
| `integral` | Bestimmte Integrale | 3 | 1 |
| `sach` | Sachzusammenhänge | 4 | 1 |
| `graph` | Graphenanalyse | 3 | 1 |
| `beschraenkt` | Beschränktes Wachstum | 3 | 1 |
| **Gesamt** | | **21 regulär + 6 Fallback + 2 Level2 = 29** | |

---

## 3. Fragetypen

| Typ | Anteil | Beschreibung |
|---|---|---|
| `mc` | Mehrheit | 3–4 Antwortmöglichkeiten, 1 richtig |
| `VisualGraph` | ~5 Fragen | SVG-Grafik + MC-Antworten (z. B. Graph ablesen, Fläche schätzen) |
| `text` | ~5 Fragen | Term oder Wort eingeben (z. B. `(x+1)*e^x`, `zerfall`) |

---

## 4. XP & Gamification

| Parameter | Wert |
|---|---|
| Basis-XP pro richtiger Antwort | 100 |
| Streak-Bonus | +20 XP pro Streak-Stufe |
| Speed-Bonus | +50 XP wenn Antwort ≤ 10 s, kein Joker, keine Fallback-Frage |
| Joker-Kosten | −50 XP |
| Level-Up | alle 250 XP |
| Streak-Fire-Animation | ab Streak ≥ 3 |

---

## 5. Level-2-System

- Ab **Level 2** werden nach Abschluss der regulären Queue 2 schwerere Fragen freigeschaltet:

| categoryId | Inhalt |
|---|---|
| `ableitung` | Kombination Produkt- + Kettenregel: `f(x) = x·e^(2x)` |
| `integral` | Flächeninhalt mit Vorzeichenwechsel: `f(x) = e^x − 2` |

- Level-2-Fragen **zählen nicht** in `scores.total` (werden aber bei `correct++` berücksichtigt, daher `Math.min` in Ratio-Berechnung)

---

## 6. Adaptive Difficulty – Fallback-Fragen

Jede Kategorie hat genau eine Fallback-Frage (`isFallback: true`):

| Kategorie | Fallback-Inhalt |
|---|---|
| Ableitungsregeln | Ableitung von `f(x) = e^x` (Basis-Merksatz) |
| Stammfunktionen | Stammfunktion von `f(x) = 5` (Konstante) |
| Bestimmte Integrale | Was beschreiben die Grenzen a und b? |
| Sachzusammenhänge | Allgemeine Form `f(t) = c·e^(kt)` erkennen |
| Graphenanalyse | Was ist ein Hochpunkt? |
| Beschränktes Wachstum | Was ist die Sättigungsgrenze S? |

---

## 7. Auswertungs-Tipps (specificHint pro Kategorie)

| categoryId | Tipp-Inhalt (Klausur-Tipp / Lernplan) |
|---|---|
| `ableitung` | Kettenregel (Innere × Äußere), Produktregel, Ausklammern von e^x |
| `stamm` | Aufleiten e^(kx): durch k teilen; Konstante bleibt stehen |
| `integral` | Vorzeichenwechsel am Nullpunkt beachten (Betragsstriche) |
| `sach` | f(t) = c·e^(kt): c = Startwert, k-Vorzeichen = Wachstum/Zerfall |
| `graph` | f'(x) > 0 → steigt; Vorzeichenwechsel + → − bei f' = Hochpunkt |
| `beschraenkt` | S = Grenzwert für t → ∞; f(t) = S − (S − f₀)·e^(−kt) |

---

## 8. Lernressourcen (Links in der Auswertung)

Pro Kategorie werden bei `ratio < 1` YouTube-Suche-Links und Weblinks eingeblendet:

| categoryId | Ressourcen |
|---|---|
| `ableitung` | Kettenregel + Produktregel bei e-Funktionen (YouTube), mathebibel.de, mathe-im-abi.de |
| `stamm` | Stammfunktion von e-Funktionen, Aufleiten-Grundregeln (YouTube), mathebibel.de |
| `integral` | Bestimmtes Integral, Flächeninhalt mit Nullstelle (YouTube), mathebibel.de, GeoGebra |
| `sach` | Wachstum & Zerfall mit e-Funktion (YouTube), mathebibel.de |
| `graph` | Kurvendiskussion, Grenzverhalten (YouTube), mathebibel.de |
| `beschraenkt` | Beschränktes Wachstum, Sättigungsgrenze (YouTube), mathebibel.de, mathe-im-abi.de |

---

## 9. Design & Farben

| Element | Wert |
|---|---|
| Stil | Dark Mode / Neon / Gamer |
| Hintergrund | `#0f172a` |
| Primary-Glow | `#38bdf8` (Blau) |
| Secondary-Glow | `#c084fc` (Lila) |
| Joker-Farbe | `#fbbf24` (Gold) |
| Erfolg | `#34d399` (Grün) |
| Fehler | `#f87171` (Rot) |

---

## 10. localStorage

| Key | Inhalt |
|---|---|
| `diagnose-name` | Letzter eingegebener Schülername |
| `diagnose-best-xp` | Bisher höchste XP-Zahl |

---

## 11. Power Automate – Payload-Felder

```json
{
  "Datum":               "TT.MM.JJJJ",
  "Name":                "Schülername",
  "XP":                  1340,
  "Level":               6,
  "Ableitungsregeln":    "3/4",
  "Stammfunktionen":     "4/4",
  "Integrale":           "2/3",
  "Sachaufgaben":        "3/4",
  "Graphenanalyse":      "3/3",
  "BeschraenktesWachstum": "2/3"
}
```

---

## 12. Print-Zertifikat Footer

```
Offizielles Q1 Diagnose-Dokument -- NRW Grundkurs Mathematik -- Erfolg muss man sich erarbeiten!
```
