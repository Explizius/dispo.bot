# dispo.bot

Auto-Disponent für [leitstellenspiel.de](https://www.leitstellenspiel.de). Er fährt die
Einsätze, während du etwas anderes machst: alarmieren, nachalarmieren, Transporte,
Personal einstellen, Lehrgänge, Funkrufnamen.

**Dieses Repository enthält keinen Quellcode — nur die Releases.**

## Download

Die fertige `dispo.exe` liegt unter **[Releases](../../releases/latest)**. Node muss nicht
installiert sein. ZIP entpacken, `dispo.exe` starten — das Bedienpanel öffnet sich im
Browser unter `http://127.0.0.1:8787`.

Windows meldet beim ersten Start eventuell SmartScreen („Unbekannter Herausgeber") —
*Weitere Informationen* → *Trotzdem ausführen*. Die Datei ist nicht signiert.

## Lizenz

Der Bot braucht einen Lizenzschlüssel. Den gibt es über Discord; eingetragen wird er im
Panel unter **einstellungen → konto**.

Ein Schlüssel läuft ab dem Zeitpunkt der ersten Aktivierung und gilt für **eine laufende
Installation** — beliebig viele Spielaccounts, aber nicht zwei Rechner gleichzeitig.

## Support

Discord: <!-- TODO: Einladungslink -->

## Hinweise

- Die Zugangsdaten zum Spiel bleiben auf deinem Rechner und werden verschlüsselt abgelegt.
  Der gesamte Spielverkehr läuft über deine eigene IP.
- Der Bot spielt in einer einstellbaren Dienstzeit und mit zufälligen Abständen, nicht rund
  um die Uhr im Sekundentakt.
