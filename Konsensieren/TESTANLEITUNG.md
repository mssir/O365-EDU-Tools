# Testanleitung Team-Konsensieren

Mit diesem Testbetrieb prüfen Sie vor dem echten Einsatz, ob Abstimmung, Sperren, Auswertung und Ergebnisabfrage funktionieren. Rechnen Sie mit etwa 30 Minuten. Am Ende wird alles gelöscht, damit die echte Abstimmung sauber beginnt.

Die App: https://claude.ai/artifact/8Jezf3vA37z7eXChUZkAHZ (oder `index.html` aus diesem Ordner)

Der Test hat drei Teile:

| Teil | Wer | Dauer | Was wird geprüft |
|---|---|---|---|
| 1 | Sie allein | 5 Min. | Rechenweg mit festen Testdaten |
| 2 | Sie allein | 15 Min. | Kompletter Ablauf der Live-Abstimmung |
| 3 | Sie und 2–3 Kolleg:innen | 10 Min. | Freigabe und Rechte aus Sicht der Teilnehmenden |

---

## Teil 1: Rechenweg mit festen Testdaten

Für diese Testdaten ist das richtige Ergebnis vorab bekannt.

1. Öffnen Sie den Reiter **„Auswertung aus Datei“**.
2. Kopieren Sie diese Tabelle in das Textfeld:

   ```
   Code;A. Rupprecht;Ch. Schön;J. Glaser;E. Ohland;Unbekannt
   TEST-0001;1;6;0;8;9
   TEST-0002;2;7;0;9;8
   TEST-0003;7;1;0;8;6
   TEST-0004;8;2;0;6;9
   TEST-0005;9;8;0;1;7
   TEST-0006;6;9;0;2;8
   TEST-0007;8;7;0;9;1
   TEST-0008;9;6;0;7;2
   TEST-0009;5;5;0;5;5
   TEST-0010;4;4;0;4;4
   ```

3. Klicken Sie auf **„Zuordnung berechnen“**.

**Erwartetes Ergebnis.** Alle zehn wollen am liebsten zu J. Glaser (Widerstand 0). Wegen der gleichmäßigen Verteilung bekommt aber jede Person genau 2:

| Person | Codes |
|---|---|
| A. Rupprecht | TEST-0001, TEST-0002 |
| Ch. Schön | TEST-0003, TEST-0004 |
| J. Glaser | TEST-0009, TEST-0010 |
| E. Ohland | TEST-0005, TEST-0006 |
| Unbekannt | TEST-0007, TEST-0008 |

J. Glaser bekommt die beiden, die bei allen anderen den höchsten Widerstand haben. Alle anderen landen bei ihrer zweitliebsten Person. Das Ergebnis muss in beiden Verfahren gleich sein: Ø Widerstand 1.20, höchster Wert 2.

- [ ] Ergebnis stimmt mit der Tabelle überein
- [ ] Unter „Verfahren“ auf „Klassisch“ umstellen und neu berechnen: gleiches Ergebnis
- [ ] Eine Zeile mit einem Wert von 11 ergänzen: Die App meldet die Zeile als fehlerhaft und rechnet ohne sie weiter
- [ ] „Ergebnis als CSV speichern“ erzeugt eine Datei, die sich in Excel öffnen lässt

---

## Teil 2: Live-Abstimmung allein durchspielen

Als Besitzer:in der Seite dürfen Sie auch selbst abstimmen. So können Sie den ganzen Ablauf allein testen.

### 2.1 Vorbereitung

1. Reiter **„Verwaltung“**: Der Status lautet *Vorbereitung*.
2. Bei „Anzahl neuer Codes“ **6** eintragen und **„Codes erzeugen“** klicken.
3. Notieren Sie die sechs Codes, zum Beispiel über „Codes kopieren“.
4. Klicken Sie auf **„Zettel zum Drucken speichern“**, öffnen Sie die Datei und sehen Sie sich die Druckvorschau an.

- [ ] Sechs Codes werden angezeigt, „Ausgegebene Codes: 6“
- [ ] Die Zettel-Datei zeigt die Codes als Schneidezettel

### 2.2 Abstimmung vor dem Start

1. Reiter **„Abstimmen“**.

- [ ] Hinweis „Die Abstimmung hat noch nicht begonnen.“, kein Formular

### 2.3 Abstimmen

1. **Verwaltung → „Abstimmung starten“**. Status: *Abstimmung läuft*.
2. Geben Sie im Reiter **„Abstimmen“** fünf Stimmen ab, je eine mit Code 1 bis 5. Bewerten Sie jede Person beliebig.

Prüfen Sie dabei diese Fälle:

| Eingabe | Erwartung |
|---|---|
| Code `ABCD-EFGH` (erfunden) | „Diesen Code gibt es nicht.“ |
| Gültiger Code, eine Person nicht bewertet | Hinweis, welche Person noch fehlt |
| Gültiger Code in Kleinbuchstaben oder ohne Bindestrich | wird akzeptiert |
| Prüfansicht → „Zurück“ | Angaben bleiben erhalten |
| Code 1 ein zweites Mal verwenden | „Mit diesem Code wurde bereits abgestimmt.“ |

- [ ] Alle Fälle verhalten sich wie erwartet
- [ ] Verwaltung zeigt „Abgegebene Stimmen: 5 von 6“

### 2.4 Abstimmung beenden

1. **Verwaltung → „Abstimmung beenden“**.
2. Versuchen Sie, mit Code 6 abzustimmen.

- [ ] Hinweis „Die Abstimmung ist beendet.“, kein Formular

### 2.5 Auswertung und Veröffentlichung

1. **Verwaltung → „Zuordnung berechnen“**.
2. Prüfen Sie die Tabelle: Bei 5 Stimmen bekommt jede Person genau 1.
3. **„Ergebnis veröffentlichen“**.

- [ ] Jede der fünf Personen hat genau eine Zuordnung
- [ ] Code 6 (ohne Stimme) taucht in der Tabelle nicht auf
- [ ] Status: *Ergebnis veröffentlicht*

### 2.6 Ergebnis abfragen

Reiter **„Mein Ergebnis“**:

| Eingabe | Erwartung |
|---|---|
| Code 1 | Name der zugeordneten Person und Ihr Widerstand |
| Code 6 (nicht abgestimmt) | „Zu diesem Code gibt es keine Zuordnung.“ |
| Erfundener Code | dieselbe Meldung |

- [ ] Alle Fälle verhalten sich wie erwartet
- [ ] Unter dem Eingabefeld erscheint die Verteilung (1/1/1/1/1)

---

## Teil 3: Test mit Kolleg:innen

Hier geht es darum, ob die Freigabe stimmt und Teilnehmende nur sehen, was sie sehen sollen.

### 3.1 Freigeben

1. Seite öffnen → **Teilen**.
2. Zwei oder drei Kolleg:innen aus Ihrer claude.ai-Organisation als **Mitwirkende** (Contributor) hinzufügen.
   Achtung: „Betrachter“ (Viewer) oder „Kommentierende“ können **nicht** abstimmen.
3. In der Verwaltung **„Veröffentlichung zurückziehen“**, dann **„Wieder öffnen“**.
4. Jeder Testperson einen noch ungenutzten Code geben. Erzeugen Sie bei Bedarf neue Codes.

### 3.2 Was die Testpersonen prüfen

- [ ] Sie sehen nur „Abstimmen“ und „Mein Ergebnis“, **nicht** „Verwaltung“
- [ ] Abstimmen mit dem eigenen Code klappt
- [ ] Ein zweiter Versuch mit demselben Code wird abgelehnt
- [ ] Auf dem Handy ist die 0–10-Skala gut bedienbar

Danach beenden Sie die Abstimmung, berechnen neu und veröffentlichen.

- [ ] Die Testpersonen sehen unter „Mein Ergebnis“ ihre Zuordnung

### Wenn etwas nicht klappt

| Problem | Ursache und Lösung |
|---|---|
| Testperson sieht „Die Abstimmung hat noch nicht begonnen“, obwohl sie läuft, oder „Sie haben keine Berechtigung zum Abstimmen“ | Person ist nur Betrachter:in oder Kommentierende:r → als Mitwirkende freigeben |
| „Die Abstimmung ist in dieser Ansicht nicht erreichbar“ | Person ist nicht bei claude.ai angemeldet oder nicht in Ihrer Organisation → anmelden lassen oder Variante B (Microsoft Forms) aus der README nutzen |
| Link öffnet sich nicht | Seite ist noch privat → Teilen-Menü prüfen |
| Code wird nicht erkannt | Verwechslung von Zeichen? Die Codes enthalten nie I, O, 0 oder 1 |

---

## Abschluss: Testdaten löschen

1. **Verwaltung → „Alles löschen …“ → „Ja, endgültig löschen“**.

- [ ] „Ausgegebene Codes: 0“, „Abgegebene Stimmen: 0“, Status *Vorbereitung*
- [ ] „Mein Ergebnis“ mit einem alten Testcode meldet „noch nicht veröffentlicht“

Danach kann die echte Abstimmung beginnen: echte Codes erzeugen, Zettel drucken und verlosen, Abstimmung starten.

### Tipps für den Echtbetrieb

- Lassen Sie alle **zur gleichen Zeit** abstimmen, etwa am Anfang einer Besprechung. Das stärkt die Anonymität, weil sich aus dem Zeitpunkt der Stimmabgabe nichts ableiten lässt.
- Erzeugen Sie 2–3 Codes mehr als nötig, für den Fall, dass ein Zettel verloren geht.
- Bitten Sie alle, ihren Zettel bis zur Veröffentlichung aufzuheben. Verlorene Codes lassen sich nicht wiederherstellen.
