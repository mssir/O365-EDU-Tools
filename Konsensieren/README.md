# Team-Konsensieren

Anonyme Zuordnung von Mitarbeitenden zu fünf Personen (A. Rupprecht, Ch. Schön, J. Glaser, E. Ohland, Unbekannt) per **systemischem Konsensieren**.

Jede teilnehmende Person gibt für jede der fünf Personen ihren **Widerstand** von 0 (passt gut) bis 10 (auf keinen Fall) an. Die Auswertung ordnet anschließend alle automatisch so zu, dass möglichst wenig Widerstand entsteht und jede Person gleich viele Mitarbeitende bekommt (höchstens eine Person Unterschied).

`index.html` ist eine einzelne Datei ohne Abhängigkeiten.

## Variante A: Live-Abstimmung (claude.ai-Artefakt)

Die veröffentlichte Version nutzt eine gemeinsame Datenbank.

1. **Verwaltung → Codes erzeugen.** Etwas mehr Codes erzeugen, als Personen teilnehmen. „Zettel zum Drucken speichern“ liefert eine HTML-Datei mit Schneidezetteln.
2. Zettel ausdrucken, falten und in eine Box legen. Jede Person zieht einen. Damit weiß niemand, welcher Code zu wem gehört.
3. **Abstimmung starten** und die Seite für die Teilnehmenden als *Mitwirkende* freigeben.
4. Jede Person gibt Code und fünf Werte ein. Jeder Code gilt genau einmal.
5. **Abstimmung beenden → Zuordnung berechnen → Ergebnis veröffentlichen.**
6. Jede Person sieht unter **„Mein Ergebnis“** mit ihrem Code ihre Zuordnung.

## Variante B: Microsoft Forms und Datei-Auswertung

Wenn nicht alle Teilnehmenden Zugriff auf claude.ai haben:

1. In `index.html` unter „Code-Zettel ohne Datenbank“ Codes erzeugen und verlosen.
2. Ein Formular anlegen: Frage „Ihr Code“ und fünf Fragen 0–10, eine je Name. Einstellungen: *Nur Personen in meiner Organisation*, *Namen aufzeichnen* **aus**, *Eine Antwort pro Person* **an**.
3. Antworten nach Excel exportieren und die Spalten *Code* und die fünf Namen samt Kopfzeile in **„Auswertung aus Datei“** einfügen (oder als CSV laden).

Die Datei funktioniert auch lokal im Browser (Doppelklick auf `index.html`).

## Verfahren der Zuordnung

- Bei *n* Teilnehmenden bekommt jede Person ⌊n/5⌋ oder ⌈n/5⌉ Mitarbeitende.
- Unter dieser Bedingung wird die optimale Zuordnung mit der Ungarischen Methode berechnet (exakt, kein Näherungsverfahren).
- **Ausgewogen (Standard):** minimiert die Summe der *quadrierten* Widerstände. Große Einzelwiderstände werden so stärker vermieden. Ein Widerstand von 8 für eine Person zählt mehr als zweimal 4 für zwei Personen.
- **Klassisch:** minimiert die einfache Summe aller Widerstände.
- Bei exakt gleichem Ergebnis entscheidet ein fester, aus dem Code abgeleiteter Zufallswert. Die Reihenfolge der Stimmabgabe spielt keine Rolle.

## Anonymität und Grenzen

- Gespeichert werden nur ein gehashter Code (SHA-256 mit Salt) und die fünf Werte, aber keine Namen.
- Die Klartext-Codes sieht nur die Verwaltung. Anonym bleibt die Abstimmung, weil die Zettel verlost werden.
- Die Datenbank führt intern einen Änderungszeitpunkt je Stimme. Wer genau beobachtet, wann jemand abstimmt, könnte daraus Rückschlüsse ziehen. Deshalb sollten alle gleichzeitig abstimmen, etwa in einer Besprechung.
- Die Sperre „ein Code, eine Stimme“ prüft die Seite selbst. Wer technisch versiert ist und einen fremden Code kennt, könnte die Datenbank direkt ansprechen. Für einen internen Rahmen reicht dieser Schutz.
