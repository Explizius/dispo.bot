# dispo.bot

**Auto-Disponent für [leitstellenspiel.de](https://www.leitstellenspiel.de).**
Er fährt die Leitstelle, während du etwas anderes machst.

---

> ## 🚧 Noch in Entwicklung — Release folgt in Kürze!
>
> **Dieses Repository ist absichtlich noch leer.** Es gibt aktuell **keinen Download** und
> **keine Version** zum Herunterladen. Hier erscheint später ausschließlich die fertige
> `dispo.exe` unter *Releases* — der Quellcode bleibt privat.
>
> Wer Bescheid wissen will, wenn es losgeht: oben rechts auf **Watch → Custom → Releases**,
> dann gibt GitHub Bescheid, sobald die erste Version da ist.

---

## Inhalt

[Was er macht](#was-er-macht) ·
[Das Bedienpanel](#das-bedienpanel) ·
[Die Einstellungen](#die-einstellungen) ·
[Was ihn unterscheidet](#was-ihn-unterscheidet) ·
[Systemvoraussetzungen](#systemvoraussetzungen) ·
[Einrichten](#einrichten-in-fünf-schritten) ·
[Vom Handy aus](#vom-handy-aus) ·
[Aktualisieren](#aktualisieren) ·
[Lizenz](#lizenz) ·
[Häufige Fragen](#häufige-fragen)

---

## Was er macht

Der Bot beobachtet deine offenen Einsätze und beantwortet sie selbstständig — dauerhaft,
ohne dass jemand danebensitzt. Jede der folgenden Funktionen ist einzeln ein- und
ausschaltbar; **in der Auslieferung ist jede Zusatzfunktion aus**, es passiert also nichts,
was du nicht selbst eingeschaltet hast.

### Alarmieren

| | |
|---|---|
| **Erstalarm & Nachalarmierung** | Zwei verschiedene Entscheidungen, und sie werden getrennt getroffen: der erste Zug zu einem neuen Einsatz, und später genau das, was noch fehlt |
| **Echter Fehlbestand** | Was der Einsatz laut Spiel noch braucht, nicht die starre Vorlage des Einsatztyps — damit zählen auch Fahrzeuge von Verbandspartnern mit |
| **Patienten** | Je Patient RTW, NEF, LNA oder RTH, gelesen aus der Patientenliste des Einsatzes. Auch die Sammelform großer Einsätze („7 Patienten, davon 2 mit NEF-Bedarf") |
| **Gefangene** | Je Gefangenem ein Streifenwagen — das Spiel nennt in seinem Fehlbestand nie ein Fahrzeug dafür, dieser Einsatz bliebe sonst ewig offen |
| **Wasser, Schaum, Pumpenleistung** | Werden aus den Tankgrößen der Fahrzeuge gedeckt, große Tanks zuerst |
| **Personal** | „28 Feuerwehrleute" wird mit MTF vor LF beantwortet, „1 Polizist" mit einem Streifenwagen — der MTF ist die einzige Besatzung, die sonst nichts kann |
| **Doppelalarme ausgeschlossen** | Drei Ebenen: Sperrzeit nach dem Alarm, Abzug der bereits fahrenden eigenen Fahrzeuge, und ein Zähler gegen wirkungslose Wiederholungen |
| **Radius & Mindest-Credits** | Wie weit ein Fahrzeug fährt und ab welchem Wert ein Einsatz überhaupt angefasst wird |

### Transport

| | |
|---|---|
| **Patient → Krankenhaus** | Nach Entfernung, freien Betten, Gebühr — passende Fachabteilung wird bevorzugt, aber nie erzwungen, sonst säße der Patient bei vollen Häusern für immer im RTW |
| **Gefangener → Zelle** | Dasselbe für Streifenwagen und freie Zellen |
| **Übergabeort** | Boot und Hubschrauber können kein Krankenhaus anfahren — der Patient wird an einer Rettungswache übergeben, und der Folgeeinsatz, den das Spiel daraus macht, wird ebenfalls beantwortet |
| **Eigene Häuser zuerst** | Fremde Häuser sind der Rückfall, nicht der Konkurrent: die Gebühr bleibt bei 0 und die Credits im Haus |
| **Alles voll → freilassen** | Sonst blockiert das Fahrzeug für immer und der Einsatz schließt nie. Ist etwas frei und nur durch deine Grenzen ausgeschlossen, wird gewartet und gesagt, welche Grenze es ist |

### Verband

| | |
|---|---|
| **Verbandseinsätze mitfahren** | Eigener Radius, eigene Mindest-Credits, Obergrenze je Einsatz |
| **Fester Fahrzeugsatz** | „Zu jedem Verbandseinsatz genau einen FuStW" — wahlweise nach Anforderungsschlüssel oder nach exaktem Fahrzeugtyp |
| **Stehende Obergrenze** | Zusätzlich: wie viele Fahrzeuge eines Typs insgesamt gleichzeitig bei Partnern unterwegs sein dürfen. Wird jeden Durchlauf nachgezählt, nicht gemerkt — ein Neustart ändert nichts daran |
| **Eigene Einsätze teilen** | Mit Vorsprung für die Partner: zuerst fährt nur *ein* Fahrzeug los, danach bleibt der Einsatz für die eingestellte Zeit unberührt, damit Partner ankommen können |
| **Verbandsregeln abbildbar** | Mindestens N benötigte Fahrzeuge, und einzelne Einsatzarten (z. B. Rettungsdienst) grundsätzlich nie freigeben |

### Personal

| | |
|---|---|
| **Anwerben** | Unterbesetzte Wachen starten von selbst eine Werbekampagne. Kostet keine Credits; Wachen, die schon werben oder auf Premium-Automatik stehen, werden in Ruhe gelassen |
| **Lehrgänge** | Zielwerte je Wache oder je Wachentyp, mit Prioritätenliste. Eigene Schulen (kostenlos, belegt einen Klassenraum) und Verbandslehrgänge (kostet keinen Raum, kann Gebühren kosten) — der günstigere gewinnt |
| **Kurse werden gefüllt, nicht nur gestartet** | Ein Klassenraum ist für dieselben Tage belegt, ob drei oder zehn Leute drin sitzen: die Plätze werden aus dem Bedarf *aller* Wachen aufgefüllt |
| **Personalzuweisung** | 82 Fahrzeugtypen verlangen einen Lehrgang. Wer ihn hat und auf keinem Fahrzeug sitzt, wird gebunden — nie jemand, der schon zu einem anderen Fahrzeug gehört |
| **Wachen bleiben einsatzfähig** | Wer im Lehrgang sitzt, kann nicht ausrücken. Unter einer eingestellten Mindeststärke gibt eine Wache niemanden ab |

### Nebenbei

| | |
|---|---|
| **Funkrufnamen** | Neu gekaufte Fahrzeuge bekommen den Namen, den dein Schema vorgibt — `Fl. Langen HLF 3-10` statt `HLF 20`. Von Hand benannte Fahrzeuge bleiben unberührt |
| **Engpässe** | Zählt mit, woran deine Einsätze tatsächlich scheitern — die Antwort auf „welches Fahrzeug kaufe ich als nächstes" |
| **Täglicher Login** | Der Tagesbonus wird abgeholt. Kostet an 364 Tagen im Jahr keine einzige zusätzliche Anfrage |
| **Neue Einsätze** | Das Spiel erzeugt Einsätze nur, solange ein Client danach fragt — sonst füllt sich die Karte nicht. Der Bot fragt im selben Takt und unter derselben Obergrenze wie der Kartenreiter |
| **Dienstplan** | Feste Dienstzeiten, täglich leicht verschoben. Außerhalb passiert **gar nichts**, und das Konto wird ausgeloggt |
| **Mehrere Spielaccounts** | Jedes Konto mit eigenen Einstellungen, eigenem Cache, eigener Sitzung. Umschalten im laufenden Betrieb, wahlweise von Hand oder nach Dienstplan |

---

## Das Bedienpanel

Läuft lokal auf `http://127.0.0.1:8787`, komplett auf Deutsch. Kein Cloud-Dienst, kein
Account, keine externe Verbindung — die Seite lädt nichts nach und funktioniert auch
offline. Sechs Reiter.

### einsätze

![Einsatzübersicht](img/panel-einsaetze.jpg)

Der Startbildschirm: eine Zeile je Einsatz, älteste zuerst, mit Wertverfall, Alter, Status,
welche eigenen Fahrzeuge drauf sind und was noch fehlt. Eigene Einsätze und
Verbandseinsätze stehen als getrennte Blöcke untereinander — sie werden nach
unterschiedlichen Regeln beantwortet und lesen sich deshalb als unterschiedliche Listen.

Der Status ist ein Wort, kein Symbol: *jetzt alarmiert*, *wartet auf fahrzeuge*,
*auf anfahrt*, *beim verband · noch 6 min*, *abgedeckt*. Die Fahrzeuge stehen mit Typ und
FMS-Status da, nicht mit ihrem Funkrufnamen — „BP 2-40" sagt nichts darüber, was für ein
Fahrzeug angerückt ist. Gelb heißt: noch auf Anfahrt. Alter und Countdown laufen
sekündlich weiter, und ein Einsatz, der über eine Stunde auf Fahrzeuge wartet, färbt sich.

### konsole

Dieselben Zeilen wie im Terminal, im Browser. Jede Entscheidung ist mitlesbar.

![Konsole](img/dispo.bot.cmd.jpg)

Je Einsatz eine Zeile, dazu am Ende jedes Durchlaufs eine Zusammenfassung: was alarmiert
wurde, was auf Fahrzeuge wartet, was fertig ist und wie viele Fahrzeuge frei sind.

### engpässe

![Engpässe](img/panel-engpaesse.jpg)

Woran die Einsätze wirklich scheitern, gezählt **je Einsatz** statt je Abfrage — ein Einsatz,
der eine Stunde auf einen FuStW wartet, ist ein fehlender FuStW, nicht hundert.
`nicht im bestand` heißt: dieses Fahrzeug fehlt komplett, davon ist keines gekauft.
`keins frei` heißt: es gibt welche, aber keines war frei oder in Reichweite — das eine ist
eine Lücke im Fuhrpark, das andere ein Durchsatzproblem, und es sind zwei verschiedene
Käufe. Dazu, seit wann, wie oft und für welchen Einsatz zuletzt. Je Zeile ein Knopf zum
Zurücksetzen, für den Tag, an dem das Fahrzeug gekauft ist.

Das ist die Antwort auf „was kaufe ich als nächstes" — aus dem, was tatsächlich passiert
ist, nicht aus einem Gefühl.

### lehrgänge

![Lehrgänge](img/panel-lehrgaenge.jpg)

Was deine Leute gerade lernen und was sie fertig haben, *laufend* und *abgeschlossen*
getrennt, mit Restlaufzeit je Kurs. Das Spiel führt keine Liste abgeschlossener Lehrgänge —
die Historie entsteht daraus, dass der Bot mitschreibt, und beginnt deshalb an dem Tag, an
dem er das erste Mal geschaut hat.

Oben rechts die zweite Hälfte derselben Frage: **wer ausgebildet ist und auf keinem
Fahrzeug sitzt**, je Lehrgang und je Wache. Ein fertiger Kurs bringt nichts, solange
niemand gebunden ist — und welcher Lehrgang Leute übrig hat, entscheidet, ob ein Ziel
wirklich noch offen ist.

### fahrzeuge

Deine Flotte als Tabelle: Typ, Bestand, wie viele davon frei sind, und die Vorlage für den
Funkrufnamen. Ein Typ, für den keine Zuordnung hinterlegt ist, wird rot markiert — das sind
die, die nie alarmiert werden. Ein Typ, von dem gerade keins frei ist, wird gelb.
Darunter die Abdeckung: jeder Anforderungsschlüssel des Spiels gegen die Zahl eigener
Fahrzeugtypen, die ihn erfüllen. Eine 0 kann nie beantwortet werden.

![Funkrufnamen — die Vorlagen](img/panel-funkrufnamen.jpg)

Auf derselben Seite steht, was in eine Namensvorlage hineindarf: die vier Variablen, dass
beide Zahlen eine Rechnung vertragen (`{N+1}`, `{N/10}`), und drei durchgerechnete
Beispiele. Die Vorlage wird **genau so verwendet, wie sie dasteht** — leer heißt, dieser Typ
wird nie umbenannt, und ohne `{N}` gibt es keine Nummer.

Der **Expertenmodus** schaltet frei, was normalerweise gesperrt ist: Schlüssel und
Kapazitäten sind aus den Marktseiten des Spiels gelesene Tatsachen, kein Geschmack — ein
Tippfehler dort schickt still das falsche Fahrzeug. Die Namensvorlage ist die eine Spalte,
die niemand nachschlagen kann, und bleibt immer editierbar.

### einstellungen

`config.json`, jede Zeile davon, als Formular — mit Suche über alle Bereiche, einer
deutschen Beschriftung je Zeile und einem Satz Erklärung hinter jedem `?`.

---

## Die Einstellungen

Sieben Bereiche in einer Leiste links. Was normalerweise keiner anfasst, liegt hinter dem
Schalter **erweitert**.

| Bereich | Was drin steht |
|---|---|
| **konto** | Deine Spiel-Logins und der Lizenzschlüssel. Je Konto ein An/Aus-Schalter, dazu die Auswahl, welches gerade spielt |
| **dienst** | Dienstplan (Zeitblöcke, je Block ein Konto), tägliche Verschiebung, und der Takt: Pause zwischen zwei Durchläufen, Streuung, Leerlauf-Verlängerung |
| **einsätze** | Radius, Mindest-Credits, ob unvollständig ausgerückt wird — und die Alarmierungs-Interna: Fehlbedarf vom Spiel übernehmen, Sperrzeit, Wiederholungsschutz |
| **verband** | Verbandseinsätze annehmen (Radius, Fahrzeuge je Einsatz, fester Satz mit Obergrenze) und eigene Einsätze teilen (Mindest-Credits, Mindestgröße, ausgenommene Einsatzarten, Vorsprung in Minuten) |
| **transport** | Patient → Krankenhaus und Gefangener → Zelle: eigene Häuser, Mindestbetten, Höchstgebühr, Höchstentfernung |
| **personal** | Die drei Hälften eines Themas, in der Reihenfolge, in der sie passieren: anwerben, ausbilden, aufs Fahrzeug setzen |
| **fahrzeuge** | Funkrufnamen: an/aus, nur unbenannte, Schrittweite, eigene Ortsnamen — dazu eine Liste, welche Wache der Geocoder wie nennt und was daraus wird |
| **system** | Port des Panels und die Tailscale-Adresse |

![Einstellungen — Dienst](img/panel-dienst.jpg)

**dienst** — der Dienstplan als Liste von Zeitblöcken, je Block ein Konto. Mit einem Konto
ist das schlicht die Dienstzeit, eine Zeile. Über Mitternacht (`21:00`–`01:00`) ist
erlaubt, eine Zeit, die kein Block abdeckt, ist Pause. *zeiten täglich verschieben* rückt
jede Grenze jeden Tag um bis zu 20 Minuten — sonst ist der Bot jeden Tag auf die Minute
genau zur selben Zeit online, und genau das fällt auf.

![Einstellungen — Verband](img/panel-verband.jpg)

**verband** — Radius, Fahrzeuge je Einsatz, fester Fahrzeugsatz mit stehender Obergrenze,
und wann und was im Verband geteilt wird. Die auszunehmenden Einsatzarten sind Kästchen,
keine Textzeile: es sind achtzehn, und ein Tippfehler wäre eine Einsatzart, die still
weiter geteilt wird.

![Einstellungen — Transport](img/panel-transport.jpg)

**transport** — wohin ein beladenes Fahrzeug fährt. Vier Zahlen je Richtung, und das sind
genau die Premium-Einstellungen des Spiels, hier ohne Premium.

![Einstellungen — Personal](img/panel-personal.jpg)

**personal** — die drei Schritte untereinander: anwerben, ausbilden, aufs Fahrzeug setzen.
Die Zieltabelle unten ist der Kern: je Zeile eine Wache (oder ein ganzer Wachentyp), ein
Lehrgang und wie viele Leute ihn haben sollen. Die **Priorität** ist eine eigene Spalte —
Rang 1 wird an *jeder* Wache bedient, bevor irgendwo Rang 2 anfängt, sonst gewinnt immer
die größte Lücke. Darunter ausklappbar, auf welche Wachen eine Regel tatsächlich fällt und
welche davon zu dünn besetzt sind, um jemanden abzugeben.

![Einstellungen — eigene Ortsnamen](img/panel-ortsnamen.jpg)

**fahrzeuge** — Funkrufnamen, und die Tabelle *eigene Ortsnamen*: was der Ortsname auf dem
Fahrzeug werden soll. Links steht entweder ein Name, wie ihn der Geocoder liefert, oder
eine **Postleitzahl** — die zählt dann als eigener Ort. Genau dafür ist sie da: `60549` ist
der Frankfurter Flughafen, und die Stadt allein unterscheidet ihn von keiner anderen
Frankfurter Wache. Darunter ausklappbar, welche Wache wie ermittelt wurde und was daraus
wird; das ist die Antwort auf „warum heißt das Fahrzeug so".

---

## Was ihn unterscheidet

- **Er liest den echten Fehlbestand des Spiels**, nicht eine feste Vorlage. Damit zählen
  auch die Fahrzeuge der Verbandspartner mit, die deine eigene Fahrzeugliste gar nicht sieht.
- **Kein Raten.** Ein Fahrzeugtyp ohne hinterlegte Zuordnung wird gemeldet, nicht auf
  Verdacht losgeschickt. Ein unbekannter Text im Fehlbestand wird protokolliert, nicht
  interpretiert. Zu wenig zu schicken ist die sichere Richtung.
- **Sparsam.** Zwei Anfragen pro Durchlauf, egal ob drei oder dreißig Einsätze offen sind.
  Kein Abruf je Einsatz, keine Seite, die zweimal geholt wird.
- **Unauffällig.** Zufällige Abstände zwischen den Durchläufen, zufällige Reihenfolge beim
  Alarmieren, zufällige Pausen zwischen zwei Alarmen. Außerhalb der Dienstzeit passiert gar
  nichts, und das Konto ist dann ausgeloggt statt sechzehn Stunden am Stück online.
- **Nichts läuft heimlich.** Jede Entscheidung steht in der Konsole und im Logfile, mit dem
  Grund daneben — auch die, nichts zu tun.
- **Deine Daten bleiben bei dir.** Die Zugangsdaten liegen verschlüsselt auf deinem Rechner
  (an diesen Rechner gebunden, nicht in einer zweiten Datei danebengelegt), und der gesamte
  Spielverkehr läuft über deine eigene IP-Adresse. Der Bot fragt genau eine Adresse außerhalb
  des Spiels — OpenStreetMap für `{ORT}`, einmal je Wache, und nur wenn du Funkrufnamen mit
  Ortsnamen benutzt.

---

## Systemvoraussetzungen

Kein Node.js, keine Installation, keine Adminrechte — ein Programm und ein paar
Textdateien. Rund 90 MB Speicherplatz. Es gibt je ein Paket:

| | |
|---|---|
| **Windows** | 10/11, 64 Bit — `dispo.bot-win-*.zip`, entpacken und `dispo.exe` doppelklicken. Beim ersten Start meldet sich eventuell SmartScreen: *Weitere Informationen* → *Trotzdem ausführen*. Das liegt an der fehlenden (teuren) Signatur, nicht am Inhalt |
| **macOS** | 11 (Big Sur) oder neuer, Apple Silicon — `dispo.bot-mac-*.zip`. macOS sperrt heruntergeladene Programme, deshalb liegt im Paket eine `LIESMICH-mac.txt` mit dem einen Befehl, der das aufhebt. Für einen älteren Intel-Mac im Discord fragen |

Ein Browser für das Panel. Sonst nichts — insbesondere kein offener Spiel-Tab.

---

## Einrichten in fünf Schritten

1. **Herunterladen** — das Paket für dein System, aus den *Releases* hier.
2. **Entpacken und starten** — in einen eigenen Ordner, dann `dispo.exe` doppelklicken
   (macOS: `./dispo`).
3. **Panel öffnen** — im Fenster steht nach ein paar Sekunden eine Adresse wie
   `http://127.0.0.1:8787`. Die im Browser öffnen; das ist die ganze Bedienung.
4. **Lizenz eintragen** — unter *einstellungen → konto*, dann *aktivieren*.
   **Ab diesem Klick läuft deine Laufzeit, nicht ab dem Kauf** — ein Schlüssel kann also
   monatelang ungenutzt liegen, ohne einen Tag zu verlieren.
5. **Konto und Dienstzeit setzen** — dein Login für leitstellenspiel.de unter
   *einstellungen → konto*, danach den Dienstplan. Den Rest in Ruhe durchgehen; jede
   Einstellung hat ein `?` mit einem Satz dazu.

---

## Vom Handy aus

Das Panel hat kein Passwort, und deshalb hört es standardmäßig nur auf `127.0.0.1` —
erreichbar von dem Rechner, auf dem es läuft, und von sonst nirgendwo.

Wer es vom Handy aus lesen will, installiert **[Tailscale](https://tailscale.com)** auf
beiden Geräten unter demselben Konto. Mehr ist nicht zu tun: der Bot findet seine
Tailscale-Adresse selbst und nennt sie beim Start als zweite Zeile. Diese Adresse ist nur
über das eigene, verschlüsselte Netz erreichbar — das ersetzt das Passwort, das diese Seite
sonst bräuchte. **Eine andere Adresse wird abgelehnt**, ausdrücklich und mit Meldung im Log:
diese Seite schreibt deine Zugangsdaten, sie gehört nicht ins offene Internet.

Auf dem Telefon wird jede Tabellenzeile zu einem Block, die Bedienelemente werden größer,
und alle sechs Reiter sind gleichzeitig sichtbar.

---

## Aktualisieren

Neues Paket herunterladen und **über den vorhandenen Ordner entpacken**, alles überschreiben
lassen. Deine Einstellungen bleiben: `config.json`, der Ordner `accounts/`, die Zugangsdaten,
die Lizenz und die Funkrufnamen in `data/vehicleMap.json` liegen **nicht im Paket** und
werden nicht angefasst. Neue Fahrzeugtypen aus dem Update werden beim nächsten Start
automatisch ergänzt, ohne deine eigenen Zeilen zu berühren.

Was sich in welcher Version geändert hat, steht im Discord unter `#changelog`.

---

## Lizenz

Der Bot braucht einen Lizenzschlüssel; eingetragen wird er direkt im Panel. Ein Schlüssel
läuft **ab der ersten Aktivierung** und gilt für **eine laufende Installation** — beliebig
viele Spielaccounts, aber nicht zwei Rechner gleichzeitig.

Die Planung läuft auf einem Server; der Bot fragt einmal je Durchlauf nach, was zu tun ist,
und alarmiert dann selbst. Deine Spiel-Zugangsdaten sehen diesen Server nie, und der gesamte
Spielverkehr geht von deinem eigenen Anschluss aus.

Schlüssel gibt es über Discord.

---

## Häufige Fragen

**Muss ein Spiel-Tab offen bleiben?**
Nein. Der Bot übernimmt auch das Anfordern neuer Einsätze — ohne das füllt sich die Karte
gar nicht, egal wer sonst zuschaut.

**Läuft er rund um die Uhr?**
Nur wenn du das willst. Mit Dienstplan arbeitet er in den eingetragenen Zeiten, verschiebt
die Grenzen täglich um ein paar Minuten und ist außerhalb ausgeloggt.

**Was passiert bei einem Absturz?**
Er startet sich 30 Sekunden später neu. Was er sich merken muss — laufende Werbekampagnen,
Sperrzeiten, ermittelte Ortsnamen — liegt auf der Platte und übersteht das.

**Kann ich sehen, was er tut, bevor er es tut?**
Ja: die Konsole schreibt je Einsatz eine Zeile mit dem Grund. Und alles Zusätzliche ist
ab Werk aus, du schaltest es einzeln frei.

**Wird mein Spielaccount gesperrt?**
Automatisierung kann gegen die Spielregeln verstoßen. Der Bot gibt sich Mühe, nicht wie
einer auszusehen — feste Taktung, starre Reihenfolge und Dauerpräsenz sind die auffälligsten
Merkmale, und keines davon hat er. Eine Garantie ist das nicht.

---

## Support & Kontakt

Discord: <!-- TODO: Einladungslink eintragen -->

Fehler und Wünsche gehören in `#bugs-und-wünsche` — bitte mit Version, was du erwartet hast,
was passiert ist und dem passenden Auszug aus `logs/`. Alles Persönliche (Kauf, Schlüssel,
dein Account) über ein Ticket. **Niemals Passwörter, `credentials.json` oder Screenshots mit
Login posten** — auch nicht an das Team, wir fragen danach nie.

## Hinweise

Dieses Projekt steht in keiner Verbindung zu leitstellenspiel.de oder deren Betreibern.
Die Nutzung von Automatisierung kann gegen die Spielregeln verstoßen — die Entscheidung und
das Risiko liegen bei dir.
