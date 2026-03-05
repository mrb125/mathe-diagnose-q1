# Planung: Diagnosetool Mathematik (Gymnasium)

## 1. Ziel und Einsatz
- Zielgruppe: Gymnasium, Q1 GK als Startversion; Architektur so anlegen, dass alle Klassenstufen (Sek. I + Sek. II) erweiterbar sind.
- Lehrplanbezug: NRW (Q1 GK) als feste Referenz.
- Zweck: Diagnose von Grundvorstellungen, Verfahren und Modellierung in ausgewählten Themenfeldern.
- Einsatzszenario: 30–45 Minuten, iPad/Tablet, offline, einzelne HTML-Datei.

## 2. Didaktisches Profil
- Kompetenzfokus: Argumentieren, Problemlösen, Modellieren, Darstellen, Kommunizieren.
- Diagnoseprinzip: Fehlervarianzen sichtbar machen, nicht nur Punkte zählen.
- Feedback: kategoriespezifisch (Ampel + Lernhinweis), keine Noten.

## 3. Inhaltlicher Zuschnitt (Version 1)
- Themenbereich: Exponentialfunktionen und Integrale (Q1 GK NRW).
- Erweiterbarkeit: Kategorien/Fragen modular, damit Themen je Klassenstufe ergänzt werden können.
- Kategorien (Q1 GK, V1):
  - Exponentialfunktion – Grundverständnis
  - Parameterwirkung und Graphen
  - Ableitung e-Funktionen (Produkt-/Kettenregel, einfache Zusammensetzung)
  - Integral als Fläche/Bestand (inkl. Einheiten/Deutung)
  - Zusammenhang f–f' (Steigung/Monotonie, grafische Deutung)
  - Modellierung: Wachstum/Zerfall/Sättigung
- Kategorien (Beispiele):
  - Funktionsverständnis (Wachstum/Abnahme, Parameterwirkung)
  - Ableitungen e-Funktionen (Produkt-/Kettenregel, einfache Zusammensetzung)
  - Integral als Bestandsfunktion / Fläche
  - Graphische Deutung (Steigung, Flächen, Änderungsrate)
  - Modellierungskontext (Sättigung, Zerfall, Wachstum)

## 4. Aufgabenformat-Mix
- Multiple Choice (Konzept-Checks)
- Freitext (Kurzantworten, normalisiert)
- Graphische Aufgaben (SVG, Ablesen/Interpretation)
- Mischung aus Verständnis- und Verfahrensaufgaben

## 4a. Kernaufgaben-Entwurf (Start: Integrale)
**Kategorie: Integral als Fläche/Bestand (inkl. Einheiten/Deutung)**
1. Aufgabe: Berechne \u222b_0^2 3x dx. | Typ: MC | Lösung: 6 | Erklärung: Stammfunktion 1.5x^2, eingesetzt 2 \u2192 6.
2. Aufgabe: Ein Zufluss r(t)=2t (L/min), Startbestand 5 L. Wie viel Wasser nach 3 min? | Typ: Freitext | Lösung: 14 | Erklärung: 5 + \u222b_0^3 2t dt = 5 + 9.
3. Aufgabe: Was bedeutet eine negative Integralfläche? | Typ: MC | Lösung: Nettoabnahme/negativer Saldo | Erklärung: Integral liefert orientierte Fläche.
4. Aufgabe: Einheitendeutung: v(t) in m/s, \u222b v(t) dt liefert ...? | Typ: MC | Lösung: m (Weg) | Erklärung: Integration von Geschwindigkeit ergibt Weg.
5. Aufgabe: Graph (SVG): y=x von 0 bis 2. Flächeninhalt unter dem Graphen? | Typ: VisualGraph | Lösung: 2 | Erklärung: Dreiecksfläche: 1/2 * 2 * 2.
6. Aufgabe: Gegeben f(x) \u2265 0. Welche Aussage stimmt? | Typ: MC | Lösung: \u222b_a^b f(x) dx ist Flächeninhalt | Erklärung: Bei nichtnegativer Funktion entspricht Integral der Fläche.

**Kategorie: Zusammenhang f\u2013f' (Steigung/Monotonie, grafische Deutung)**
1. Aufgabe: f'(x) > 0 auf (1,4). Aussage zu f? | Typ: MC | Lösung: f ist dort steigend | Erklärung: Positive Ableitung bedeutet Wachstum.
2. Aufgabe: f'(x)=0 bei x=2 und f' wechselt von + nach -. Was liegt bei f vor? | Typ: MC | Lösung: lokales Maximum | Erklärung: Vorzeichenwechsel +\u2192-.
3. Aufgabe: Graph (SVG): f'(x) ist konstant 3. Welche Aussage zu f stimmt? | Typ: MC | Lösung: f ist eine Gerade mit Steigung 3 | Erklärung: Konstante Ableitung \u2192 lineare Funktion.
4. Aufgabe: Wo ist f am steilsten? | Typ: VisualGraph | Lösung: dort wo f'(x) am groessten ist | Erklärung: Groesste Ableitung \u2192 groesste Steigung.
5. Aufgabe: f hat Extremstelle bei x=1. Was gilt fuer f'(1)? | Typ: Freitext | Lösung: 0 | Erklärung: Notwendige Bedingung: f'(1)=0.
6. Aufgabe: Graph (SVG): f'(x) < 0 fuer x<0, f'(x) > 0 fuer x>0. Aussage zu f? | Typ: MC | Lösung: f hat Minimum bei x=0 | Erklärung: Wechsel von - zu +.

## 4b. Kernaufgaben-Entwurf (Exponentialfunktionen)
**Kategorie: Exponentialfunktion – Grundverstaendnis**
1. Aufgabe: Welche Funktion beschreibt exponentielles Wachstum? | Typ: MC | Lösung: f(x)=2·1.3^x | Erklärung: Basis >1 bedeutet Wachstum.
2. Aufgabe: f(x)=3·0.5^x. Verhalten fuer x→∞? | Typ: MC | Lösung: f(x)→0 | Erklärung: Basis zwischen 0 und 1 → Abnahme gegen 0.
3. Aufgabe: Bestimme f(0) fuer f(x)=5·2^x. | Typ: Freitext | Lösung: 5 | Erklärung: 2^0=1, Vorfaktor bleibt.
4. Aufgabe: Verdopplungsfaktor: f(x)=4·2^x. Wie aendert sich f bei x+1? | Typ: MC | Lösung: verdoppelt sich | Erklärung: Faktor 2 pro Schritt.
5. Aufgabe: Graph (SVG): Zwei Kurven, welche ist f(x)=2^x? | Typ: VisualGraph | Lösung: die durch (0,1) und (1,2) | Erklärung: Charakteristische Punkte.
6. Aufgabe: Welche Aussage ist richtig? | Typ: MC | Lösung: Exponentialfunktionen schneiden die y-Achse bei f(0)=a | Erklärung: f(x)=a·b^x.

**Kategorie: Parameterwirkung und Graphen**
1. Aufgabe: f(x)=2·e^x. Wie wirkt der Faktor 2? | Typ: MC | Lösung: Streckung in y-Richtung | Erklärung: Vertikale Streckung.
2. Aufgabe: g(x)=e^{x-1}. Wie ist g gegenueber e^x verschoben? | Typ: MC | Lösung: um 1 nach rechts | Erklärung: x-1 → Rechtsverschiebung.
3. Aufgabe: h(x)=e^{x}+3. Was aendert sich? | Typ: MC | Lösung: Verschiebung um 3 nach oben | Erklärung: +3 addiert zur Funktion.
4. Aufgabe: k(x)=3·(0.8)^x. Monotonie? | Typ: MC | Lösung: streng fallend | Erklärung: Basis <1.
5. Aufgabe: Graph (SVG): Welche Kurve passt zu f(x)=e^{2x}? | Typ: VisualGraph | Lösung: die steilere wachsend | Erklärung: Groessere Steigung durch 2x.
6. Aufgabe: f(x)=a·e^x hat f(0)=10. Bestimme a. | Typ: Freitext | Lösung: 10 | Erklärung: e^0=1.

**Kategorie: Ableitung e-Funktionen (Produkt-/Kettenregel, einfache Zusammensetzung)**
1. Aufgabe: Leite f(x)=e^x ab. | Typ: Freitext | Lösung: e^x | Erklärung: e^x bleibt sich selbst.
2. Aufgabe: f(x)=3e^x. f'(x)=? | Typ: MC | Lösung: 3e^x | Erklärung: Faktor bleibt.
3. Aufgabe: f(x)=e^{2x}. f'(x)=? | Typ: MC | Lösung: 2e^{2x} | Erklärung: Kettenregel.
4. Aufgabe: f(x)=x·e^x. f'(x)=? | Typ: MC | Lösung: e^x + x·e^x | Erklärung: Produktregel.
5. Aufgabe: f(x)=(2x-1)e^x. f'(x)=? | Typ: MC | Lösung: 2e^x + (2x-1)e^x | Erklärung: Produktregel.
6. Aufgabe: f(x)=e^{x^2}. f'(x)=? | Typ: MC | Lösung: 2x·e^{x^2} | Erklärung: Kettenregel.

**Kategorie: Modellierung: Wachstum/Zerfall/Saettigung**
1. Aufgabe: Ein Bestand nimmt proportional zu sich selbst zu. Welche Funktion passt? | Typ: MC | Lösung: f(t)=a·e^{kt} | Erklärung: Exponentielles Wachstum.
2. Aufgabe: Halbwertszeit 10 Jahre. Modell mit f(0)=100. f(10)=? | Typ: Freitext | Lösung: 50 | Erklärung: Halbierung nach 10 Jahren.
3. Aufgabe: Zerfall mit 20% pro Zeiteinheit. Modell? | Typ: MC | Lösung: f(t)=a·0.8^t | Erklärung: Prozentfaktor.
4. Aufgabe: Saettigung: Annaeherung an Grenzwert. Welche Gleichung beschreibt das? | Typ: MC | Lösung: f(t)=L-(L-a)e^{-kt} | Erklärung: Exponentielle Annaeherung.
5. Aufgabe: Aus Text: Anfangsbestand 200, waechst 5% pro Jahr. f(3)=? | Typ: Freitext | Lösung: 200·1.05^3 | Erklärung: Exponentielles Wachstum.
6. Aufgabe: Graph (SVG): Erkenne Zerfallskurve. | Typ: VisualGraph | Lösung: fallend, asymptotisch gegen 0 | Erklärung: Typische Zerfallsgrafik.

## 4c. Fallback-Aufgaben (je Kategorie 2–3)
**Kategorie: Exponentialfunktion – Grundverstaendnis**
1. Aufgabe: Ist f(x)=2^x wachsend oder fallend? | Typ: MC | Lösung: wachsend | Erklärung: Basis >1.
2. Aufgabe: f(0) bei f(x)=3·2^x? | Typ: Freitext | Lösung: 3 | Erklärung: 2^0=1.

**Kategorie: Parameterwirkung und Graphen**
1. Aufgabe: f(x)=e^x+2 ist gegenueber e^x ... | Typ: MC | Lösung: nach oben verschoben | Erklärung: +2 verschiebt nach oben.
2. Aufgabe: f(x)=e^{x+1} ist gegenueber e^x ... | Typ: MC | Lösung: nach links verschoben | Erklärung: x+1 → Linksverschiebung.

**Kategorie: Ableitung e-Funktionen**
1. Aufgabe: f(x)=e^x. f'(x)=? | Typ: MC | Lösung: e^x | Erklärung: Ableitung bleibt gleich.
2. Aufgabe: f(x)=5e^x. f'(x)=? | Typ: MC | Lösung: 5e^x | Erklärung: Faktor bleibt.

**Kategorie: Integral als Fläche/Bestand**
1. Aufgabe: Berechne \u222b_0^1 x dx. | Typ: MC | Lösung: 0.5 | Erklärung: Stammfunktion 0.5x^2.
2. Aufgabe: v(t) in m/s, \u222b v(t) dt liefert ...? | Typ: MC | Lösung: Weg in m | Erklärung: Geschwindigkeit integriert → Weg.

**Kategorie: Zusammenhang f–f'**
1. Aufgabe: f'(x) > 0. Aussage? | Typ: MC | Lösung: f ist steigend | Erklärung: Positive Ableitung → steigend.
2. Aufgabe: f'(x) < 0. Aussage? | Typ: MC | Lösung: f ist fallend | Erklärung: Negative Ableitung → fallend.

**Kategorie: Modellierung: Wachstum/Zerfall/Saettigung**
1. Aufgabe: 10% Wachstum pro Jahr. Modell? | Typ: MC | Lösung: f(t)=a·1.1^t | Erklärung: Wachstumsfaktor 1.1.
2. Aufgabe: Halbwertszeit 8 Jahre. f(8) im Vergleich zu f(0)? | Typ: MC | Lösung: halb so gross | Erklärung: Definition Halbwertszeit.

## 4d. allQuestions-Entwurf (Q1 GK, V1)
```js
const allQuestions = [
  // ─── Exponentialfunktion – Grundverstaendnis ───
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Welche Funktion beschreibt exponentielles Wachstum?",
    options: ["f(x)=2·1.3^x", "f(x)=2·(1+x)", "f(x)=2·x^2", "f(x)=2·x"],
    correct: 0,
    hint: "Exponentielles Wachstum hat eine konstante Basis > 1.",
    explanation: "Bei f(x)=a·b^x mit b>1 waechst die Funktion exponentiell."
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f(x)=3·0.5^x. Verhalten fuer x→∞?",
    options: ["f(x)→0", "f(x)→∞", "f(x)→-∞", "f(x) bleibt konstant"],
    correct: 0,
    hint: "Basis zwischen 0 und 1 bedeutet Zerfall.",
    explanation: "Bei 0<b<1 faellt b^x gegen 0."
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "text", isFallback: false, difficulty: "easy",
    text: "Bestimme f(0) fuer f(x)=5·2^x.",
    correct: ["5"],
    hint: "2^0 = 1.",
    explanation: "f(0)=5·2^0=5."
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Verdopplungsfaktor: f(x)=4·2^x. Wie aendert sich f bei x+1?",
    options: ["verdoppelt sich", "halbiert sich", "bleibt gleich", "wird um 4 groesser"],
    correct: 0,
    hint: "Bei Basis 2 verdoppelt sich der Wert pro Schritt.",
    explanation: "f(x+1)=4·2^(x+1)=2·(4·2^x)."
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "VisualGraph", isFallback: false, difficulty: "easy",
    text: "Welche Kurve passt zu f(x)=2^x?",
    options: ["Kurve A", "Kurve B", "Kurve C"],
    correct: 0,
    hint: "Die Kurve geht durch (0,1) und (1,2).",
    explanation: "2^x hat charakteristische Punkte (0,1) und (1,2).",
    graphSVG: "TODO"
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis", categoryId: "exp_basic",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Welche Aussage ist richtig zu f(x)=a·b^x?",
    options: ["f(0)=a", "f(0)=b", "f(1)=a", "f(1)=b"],
    correct: 0,
    hint: "Setze x=0.",
    explanation: "b^0=1, daher f(0)=a."
  },

  // ─── Parameterwirkung und Graphen ───
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f(x)=2·e^x. Wie wirkt der Faktor 2?",
    options: ["Streckung in y-Richtung", "Stauchung in x-Richtung", "Verschiebung nach rechts", "Spiegelung an der x-Achse"],
    correct: 0,
    hint: "Vorfaktor multipliziert alle y-Werte.",
    explanation: "Der Vorfaktor skaliert den Graphen vertikal."
  },
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "g(x)=e^(x-1). Wie ist g gegenueber e^x verschoben?",
    options: ["um 1 nach rechts", "um 1 nach links", "um 1 nach oben", "um 1 nach unten"],
    correct: 0,
    hint: "x-1 bedeutet Rechtsverschiebung.",
    explanation: "f(x-a) verschiebt den Graphen um a nach rechts."
  },
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "h(x)=e^x+3. Was aendert sich?",
    options: ["Verschiebung um 3 nach oben", "Verschiebung um 3 nach rechts", "Streckung in y-Richtung", "Spiegelung an der y-Achse"],
    correct: 0,
    hint: "Additionen ausserhalb verschieben nach oben/unten.",
    explanation: "Das +3 addiert zu jedem Funktionswert."
  },
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "k(x)=3·(0.8)^x. Monotonie?",
    options: ["streng fallend", "streng wachsend", "konstant", "erst fallend, dann wachsend"],
    correct: 0,
    hint: "Basis < 1.",
    explanation: "Bei 0<b<1 faellt b^x streng."
  },
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "VisualGraph", isFallback: false, difficulty: "easy",
    text: "Welche Kurve passt zu f(x)=e^(2x)?",
    options: ["Kurve A", "Kurve B", "Kurve C"],
    correct: 0,
    hint: "e^(2x) waechst schneller als e^x.",
    explanation: "Der Faktor 2 im Exponenten macht den Graphen steiler.",
    graphSVG: "TODO"
  },
  {
    category: "Parameterwirkung und Graphen", categoryId: "exp_param",
    type: "text", isFallback: false, difficulty: "easy",
    text: "f(x)=a·e^x hat f(0)=10. Bestimme a.",
    correct: ["10"],
    hint: "Setze x=0.",
    explanation: "f(0)=a·e^0=a."
  },

  // ─── Ableitung e-Funktionen ───
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "text", isFallback: false, difficulty: "easy",
    text: "Leite f(x)=e^x ab.",
    correct: ["e^x"],
    hint: "Merksatz: e^x bleibt sich selbst.",
    explanation: "(e^x)'=e^x."
  },
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f(x)=3e^x. f'(x)=?",
    options: ["3e^x", "e^x+3", "e^(3x)", "3xe^x"],
    correct: 0,
    hint: "Konstanter Faktor bleibt.",
    explanation: "Faktorregel: (3e^x)'=3e^x."
  },
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "mc", isFallback: false, difficulty: "medium",
    text: "f(x)=e^(2x). f'(x)=?",
    options: ["e^(2x)", "2e^(2x)", "2xe^(2x)", "0.5e^(2x)"],
    correct: 1,
    hint: "Kettenregel mit u=2x.",
    explanation: "(e^u)'=u'·e^u, u'=2."
  },
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "mc", isFallback: false, difficulty: "medium",
    text: "f(x)=x·e^x. f'(x)=?",
    options: ["e^x+x·e^x", "x·e^x", "e^x", "x^2·e^x"],
    correct: 0,
    hint: "Produktregel.",
    explanation: "u=x, v=e^x → u'v+uv' = e^x + x·e^x."
  },
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "mc", isFallback: false, difficulty: "medium",
    text: "f(x)=(2x-1)e^x. f'(x)=?",
    options: ["2e^x+(2x-1)e^x", "2x·e^x", "e^x+(2x-1)e^x", "(2x-1)e^x"],
    correct: 0,
    hint: "Produktregel mit u=2x-1.",
    explanation: "u'=2, v=e^x → 2e^x+(2x-1)e^x."
  },
  {
    category: "Ableitung e-Funktionen", categoryId: "exp_derive",
    type: "mc", isFallback: false, difficulty: "hard",
    text: "f(x)=e^(x^2). f'(x)=?",
    options: ["e^(x^2)", "x·e^(x^2)", "2x·e^(x^2)", "e^(2x)"],
    correct: 2,
    hint: "Kettenregel mit u=x^2.",
    explanation: "u'=2x → f'(x)=2x·e^(x^2)."
  },

  // ─── Integral als Flaeche/Bestand ───
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Berechne ∫_0^2 3x dx.",
    options: ["3", "6", "9", "12"],
    correct: 1,
    hint: "Stammfunktion von 3x ist 1.5x^2.",
    explanation: "F(2)-F(0)=1.5·4=6."
  },
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "text", isFallback: false, difficulty: "medium",
    text: "Zufluss r(t)=2t (L/min), Startbestand 5 L. Wie viel Wasser nach 3 min?",
    correct: ["14"],
    hint: "Bestand = Start + ∫_0^3 2t dt.",
    explanation: "∫_0^3 2t dt = 9, plus 5 ergibt 14."
  },
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Was bedeutet eine negative Integralfläche?",
    options: ["Nettoabnahme/negativer Saldo", "Groessere Flaeche", "Positive Zunahme", "Keine Bedeutung"],
    correct: 0,
    hint: "Orientierte Flaeche kann negativ sein.",
    explanation: "Unterhalb der x-Achse liefert das Integral negative Werte."
  },
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "v(t) in m/s, ∫ v(t) dt liefert ...?",
    options: ["Weg in m", "Beschleunigung in m/s^2", "Zeit in s", "Kraft in N"],
    correct: 0,
    hint: "Geschwindigkeit integriert liefert Weg.",
    explanation: "Einheit: (m/s)·s = m."
  },
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "VisualGraph", isFallback: false, difficulty: "easy",
    text: "y=x von 0 bis 2. Flaecheninhalt unter dem Graphen?",
    options: ["1", "2", "3", "4"],
    correct: 1,
    hint: "Dreiecksfläche: 1/2 · Grundseite · Hoehe.",
    explanation: "0.5·2·2=2.",
    graphSVG: "TODO"
  },
  {
    category: "Integral als Flaeche/Bestand", categoryId: "int_area",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Gegeben f(x)≥0. Welche Aussage stimmt?",
    options: ["∫_a^b f(x) dx ist Flaecheninhalt", "Integral ist immer 0", "Integral kann negativ sein", "Integral ist Steigung"],
    correct: 0,
    hint: "Bei nichtnegativer Funktion ist die orientierte Flaeche positiv.",
    explanation: "Das Integral entspricht dem Flaecheninhalt unter dem Graphen."
  },

  // ─── Zusammenhang f–f' ───
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f'(x) > 0 auf (1,4). Aussage zu f?",
    options: ["f ist dort steigend", "f ist dort fallend", "f ist konstant", "f hat dort ein Maximum"],
    correct: 0,
    hint: "Positive Ableitung bedeutet Wachstum.",
    explanation: "f'(x)>0 → f waechst."
  },
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f'(x)=0 bei x=2 und f' wechselt von + nach -. Was liegt bei f vor?",
    options: ["lokales Maximum", "lokales Minimum", "Wendepunkt", "Sattelpunkt"],
    correct: 0,
    hint: "Vorzeichenwechsel +→-.",
    explanation: "Steigung geht von positiv zu negativ."
  },
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "VisualGraph", isFallback: false, difficulty: "easy",
    text: "f'(x) ist konstant 3. Welche Aussage zu f stimmt?",
    options: ["f ist eine Gerade mit Steigung 3", "f ist konstant", "f ist eine Parabel", "f ist eine Hyperbel"],
    correct: 0,
    hint: "Konstante Ableitung → lineare Funktion.",
    explanation: "f(x)=3x+c.",
    graphSVG: "TODO"
  },
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Wo ist f am steilsten?",
    options: ["Dort, wo f'(x) am groessten ist", "Dort, wo f'(x)=0", "Dort, wo f''(x)=0", "Dort, wo f negativ ist"],
    correct: 0,
    hint: "Groesste Ableitung bedeutet groesste Steigung.",
    explanation: "Steilheit entspricht dem Betrag der Ableitung."
  },
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "text", isFallback: false, difficulty: "easy",
    text: "f hat Extremstelle bei x=1. Was gilt fuer f'(1)?",
    correct: ["0"],
    hint: "Notwendige Bedingung.",
    explanation: "An Extremstellen gilt f'(1)=0."
  },
  {
    category: "Zusammenhang f–f'", categoryId: "rel_fdash",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "f'(x) < 0 fuer x<0, f'(x) > 0 fuer x>0. Aussage zu f?",
    options: ["f hat Minimum bei x=0", "f hat Maximum bei x=0", "f ist konstant", "f ist fallend fuer x>0"],
    correct: 0,
    hint: "Vorzeichenwechsel -→+.",
    explanation: "f faellt und steigt dann → Minimum."
  },

  // ─── Modellierung: Wachstum/Zerfall/Saettigung ───
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Ein Bestand nimmt proportional zu sich selbst zu. Welche Funktion passt?",
    options: ["f(t)=a·e^(kt)", "f(t)=a+kt", "f(t)=a·t^2", "f(t)=a/t"],
    correct: 0,
    hint: "Proportionalitaet zum Bestand → exponentiell.",
    explanation: "Differentialgleichung f' = kf fuehrt zu exponentieller Loesung."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "text", isFallback: false, difficulty: "easy",
    text: "Halbwertszeit 10 Jahre, f(0)=100. f(10)=?",
    correct: ["50"],
    hint: "Halbwertszeit bedeutet Halbierung.",
    explanation: "Nach 10 Jahren ist der Bestand halbiert."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "mc", isFallback: false, difficulty: "easy",
    text: "Zerfall mit 20% pro Zeiteinheit. Modell?",
    options: ["f(t)=a·0.8^t", "f(t)=a·1.2^t", "f(t)=a-0.2t", "f(t)=a+0.2t"],
    correct: 0,
    hint: "20% Zerfall bedeutet Faktor 0.8.",
    explanation: "Pro Schritt bleibt 80% uebrig."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "mc", isFallback: false, difficulty: "medium",
    text: "Saettigung: Annaeherung an Grenzwert. Welche Gleichung beschreibt das?",
    options: ["f(t)=L-(L-a)e^(-kt)", "f(t)=a·e^(kt)", "f(t)=a+kt", "f(t)=a·t^2"],
    correct: 0,
    hint: "Exponentielle Annaeherung an L.",
    explanation: "Mit e^(−kt) geht der Abstand zu L gegen 0."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "text", isFallback: false, difficulty: "medium",
    text: "Anfangsbestand 200, waechst 5% pro Jahr. f(3)=?",
    correct: ["200*1.05^3", "200·1.05^3"],
    hint: "Exponentielles Wachstum mit Faktor 1.05.",
    explanation: "f(3)=200·1.05^3."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung", categoryId: "model",
    type: "VisualGraph", isFallback: false, difficulty: "easy",
    text: "Erkenne die Zerfallskurve.",
    options: ["Kurve A", "Kurve B", "Kurve C"],
    correct: 0,
    hint: "Zerfall ist fallend und naehert sich 0 asymptotisch.",
    explanation: "Typische Zerfallsgrafik.",
    graphSVG: "TODO"
  },

  // ─── Fallbacks ───
  {
    category: "Exponentialfunktion – Grundverstaendnis (Basis)", categoryId: "exp_basic",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "Ist f(x)=2^x wachsend oder fallend?",
    options: ["wachsend", "fallend"],
    correct: 0,
    hint: "Basis >1.",
    explanation: "Exponentielles Wachstum."
  },
  {
    category: "Exponentialfunktion – Grundverstaendnis (Basis)", categoryId: "exp_basic",
    type: "text", isFallback: true, difficulty: "easy",
    text: "f(0) bei f(x)=3·2^x?",
    correct: ["3"],
    hint: "2^0=1.",
    explanation: "f(0)=3."
  },
  {
    category: "Parameterwirkung und Graphen (Basis)", categoryId: "exp_param",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f(x)=e^x+2 ist gegenueber e^x ...",
    options: ["nach oben verschoben", "nach rechts verschoben", "gestreckt", "gespiegelt"],
    correct: 0,
    hint: "+2 addiert zu y.",
    explanation: "Vertikale Verschiebung."
  },
  {
    category: "Parameterwirkung und Graphen (Basis)", categoryId: "exp_param",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f(x)=e^(x+1) ist gegenueber e^x ...",
    options: ["nach links verschoben", "nach rechts verschoben", "nach oben verschoben", "gespiegelt"],
    correct: 0,
    hint: "x+1 → links.",
    explanation: "Horizontale Verschiebung."
  },
  {
    category: "Ableitung e-Funktionen (Basis)", categoryId: "exp_derive",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f(x)=e^x. f'(x)=?",
    options: ["e^x", "x·e^x", "e^(2x)", "1"],
    correct: 0,
    hint: "Merksatz.",
    explanation: "Ableitung bleibt gleich."
  },
  {
    category: "Ableitung e-Funktionen (Basis)", categoryId: "exp_derive",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f(x)=5e^x. f'(x)=?",
    options: ["5e^x", "e^x+5", "e^(5x)", "5xe^x"],
    correct: 0,
    hint: "Faktor bleibt.",
    explanation: "Faktorregel."
  },
  {
    category: "Integral als Flaeche/Bestand (Basis)", categoryId: "int_area",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "Berechne ∫_0^1 x dx.",
    options: ["0.5", "1", "2", "0"],
    correct: 0,
    hint: "0.5x^2 einsetzen.",
    explanation: "0.5·1^2=0.5."
  },
  {
    category: "Integral als Flaeche/Bestand (Basis)", categoryId: "int_area",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "v(t) in m/s, ∫ v(t) dt liefert ...?",
    options: ["Weg in m", "Beschleunigung", "Zeit", "Kraft"],
    correct: 0,
    hint: "Einheiten pruefen.",
    explanation: "m/s mal s = m."
  },
  {
    category: "Zusammenhang f–f' (Basis)", categoryId: "rel_fdash",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f'(x) > 0. Aussage?",
    options: ["f ist steigend", "f ist fallend", "f ist konstant", "f hat Maximum"],
    correct: 0,
    hint: "Positive Ableitung.",
    explanation: "Steigend."
  },
  {
    category: "Zusammenhang f–f' (Basis)", categoryId: "rel_fdash",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "f'(x) < 0. Aussage?",
    options: ["f ist fallend", "f ist steigend", "f ist konstant", "f hat Minimum"],
    correct: 0,
    hint: "Negative Ableitung.",
    explanation: "Fallend."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung (Basis)", categoryId: "model",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "10% Wachstum pro Jahr. Modell?",
    options: ["f(t)=a·1.1^t", "f(t)=a·0.9^t", "f(t)=a+0.1t", "f(t)=a-0.1t"],
    correct: 0,
    hint: "Wachstumsfaktor 1.1.",
    explanation: "Exponentialfunktion mit b=1.1."
  },
  {
    category: "Modellierung: Wachstum/Zerfall/Saettigung (Basis)", categoryId: "model",
    type: "mc", isFallback: true, difficulty: "easy",
    text: "Halbwertszeit 8 Jahre. f(8) im Vergleich zu f(0)?",
    options: ["halb so gross", "doppelt so gross", "gleich gross", "viermal so gross"],
    correct: 0,
    hint: "Definition Halbwertszeit.",
    explanation: "Nach 8 Jahren ist der Bestand halbiert."
  }
];
```

## 5. Diagnoselogik
- Adaptive Schwierigkeit:
  - Nach 2 Fehlern in Folge in einer Kategorie: Fallback-Aufgabe einschieben.
- Joker-System:
  - XP opfern, um Hinweis zu erhalten.
- Streak/XP:
  - Motivationsmechanik, kein Einfluss auf Diagnoselogik.

## 6. Auswertung
- Pro Kategorie: Verhältnis richtig/gesamt, Ampel-Status.
- Lernhinweise:
  - Kurzer Tipp (1–2 Sätze)
  - Optional: Linkliste (wird nur angezeigt, wenn Hosting per HTTP)
- Zusatz-Erklärungen nach jeder Antwort (kurz, 1–3 Sätze)
- Zertifikat:
  - Druckansicht mit Name, Datum, Gesamtübersicht.

## 7. Datenhaltung & Datenschutz
- Lokal im Browser (localStorage):
  - Name, Best-XP (optional)
- Kein Backend erforderlich.
- Optional: Power Automate Flow (nur bei Hosting, nicht bei file://).

## 8. Qualitätskriterien
- Aufgabentexte:
  - Eindeutig, sprachlich kompakt, typische Fehlkonzepte adressiert.
- Mathematische Korrektheit:
  - Jede Aufgabe mit Musterlösung + Erklärung.
- Technische Robustheit:
  - Offline lauffähig, kein CDN, iPad-Safari kompatibel.

## 9. Projektstruktur (V1)
- `index.html` (Single-File-App)
- `manifest.json`, `sw.js` (PWA)
- `requirements.md` (Anforderungen)
- `PLANUNG.md` (diese Planung)

## 10. Nächste Schritte (konkret)
1. Themenrahmen finalisieren (Q1 GK NRW bestätigen oder anpassen).
2. Kategorien festlegen und pro Kategorie 6–8 Kernaufgaben definieren.
3. Fallback-Aufgaben je Kategorie erstellen.
4. Aufgaben in `allQuestions` einpflegen und UI testen.
5. Auswertungs- und Drucklayout finalisieren.
6. Zeitrahmen auf ca. 30 Minuten kalibrieren (Anzahl Fragen und Durchlaufzeit).

## 11. Offene Punkte zur Klärung
- Aufgabentypen: Verteilung MC/Graph/Freitext = 50/30/20.
- Bewertungsgewichtung: rein diagnostisch oder auch Leistungsrueckmeldung?
- Linkressourcen: erlaubte Quellen/Plattformen?
