# Requirements: Ralph Wiggum Loop Refactor (Math Diagnostic Tool)

Dieses Dokument definiert die Anforderungen für die Überarbeitung des Diagnosetools für Exponentialfunktionen (Klasse 10) im **Ralph Wiggum Loop** Stil.

## 1. Design & Ästhetik (Ralph Wiggum Style)
- **Primary Color:** Simpsons-Gelb (`#FFD100`).
- **Secondary Color:** Simpsons-Blau (`#009DDF`).
- **Font:** Freundlich, abgerundet (z.B. Inter oder Comic-artige Serifenlose).
- **Vibe:** "Happy-go-lucky", motivierend, humorvoll, aber funktional.
- **Charakter-Integration:** Ralph Wiggum fungiert als Guide.

## 2. Pädagogischer Flow (The Loop)
- **🎯 Klare Mission:** Der Test ist nicht nur ein Test, sondern eine Mission (z.B. "Hilf Ralph, sein Sparbuch für 100 Jahre zu verstehen").
- **🔁 Scaffolding:** Abgestufte Hilfen (Tipps) müssen prominent sein und sich "lohnend" anfühlen.
- **✅ Sofort-Feedback:** Ralph gibt Feedback zu jeder Antwort (z.B. "Das ist ein Wort, das ich kenne!" bei Erfolg).
- **📈 Progress:** XP und Level bleiben, werden aber stärker visualisiert (z.B. "Ralph-Level").

## 3. Technische Anforderungen
- **Standalone HTML:** Das Projekt bleibt eine einzelne HTML-Datei.
- **KaTeX:** Beibehaltung der sauberen Formeldarstellung.
- **Interaktivität:** Beibehaltung der Fallback-Logik (wenn man 2x falsch liegt, kommt eine einfachere Aufgabe).
- **Barrierefreiheit:** Kontrastreiche Farben trotz des gelben Themes.

## 4. Struktur der Überarbeitung
- Anpassung des CSS an das "Ralph"-Farbschema.
- Implementierung von Ralph als Kommentar-Geber (Zufalls-Sprüche).
- Umformulierung der Einleitung und der Erfolgsmeldungen.
- Optimierung des Layouts für mobile Endgeräte (Responsive Design).
