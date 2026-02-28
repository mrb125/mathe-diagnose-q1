# Anforderungen: Diagnose-Tool Mathematik (Q1)

## 1. Übersicht
- **Zielgruppe/Klassenstufe:** Q1 **Grundkurs (GK) nach Kernlehrplan NRW**
- **Themenbereich:** Exponentialfunktionen, e-Funktionen und Integrale
- **Format:** HTML, CSS, Vanilla-JS in einer einzigen `index.html`-Datei. PWA-fähig (iPad).

## 2. Design & UX
- **Motto/Stil:** Modern Gamification (Dark Mode, Neon)
- **Elemente:** Erfahrungspunkte (XP), Level-System, Fortschrittsbalken, Streak-Bonus.

## 3. Neue pädagogische Features
1. **NRW GK-Fokus:** Nur abiturrelevante Fragen für den Grundkurs (z.B. keine komplexen Substitutionen oder Quotientenregel-Kombinationen, Fokus auf Produkt-/Kettenregel bei einfachen e-Funktionen und lineares Rückwärtsarbeiten).
2. **Joker-System:** Ein Schüler kann verdiente XP opfern (z.B. -50 XP), um sich einen Hint (Tipp) freizuschalten.
3. **Visuelle Graphen-Aufgaben:** Aufgaben, die das grafische Verständnis prüfen (z.B. Flächenabschätzung anhand einer SVG-Grafik).
4. **Adaptive Schwierigkeit:** Wenn ein Schüler zweimal in Folge etwas falsch macht, wird eine leichtere "Fallback-Aufgabe" (Basic) eingeschoben, um Frust zu vermeiden.
5. **Zertifikat (PDF-Export):** Auf der Auswertungsseite gibt es einen "Zertifikat erstellen"-Button, der das Drucker-Dialogfenster öffnet, um via `print` ein sauberes A4-Zertifikat mit Auswertung zu generieren (ideal für iPad -> GoodNotes).

## 4. Struktur (3 Phasen)
- Phase 1: Startbildschirm.
- Phase 2: Diagnosebogen (mit Joker-Button, Graphen, Adaptiven Quests).
- Phase 3: Diagnose-Auswertung (mit Druck-Funktion).
