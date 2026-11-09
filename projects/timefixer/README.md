# TimeFixer / Automatic clock check for Amigas without battery

> **EN:** TimeFixer is an ARexx script for Amigas with a working battery-backed clock chip whose battery has been removed. It notices that the clock has no valid time after power-on and opens Prefs/Time automatically.
>
> **DE:** TimeFixer ist ein ARexx-Skript für Amigas mit funktionierendem Uhrenchip, aus denen die Batterie ausgebaut wurde. Es erkennt, dass die Uhr nach dem Einschalten keine gültige Zeit hat, und öffnet automatisch Prefs/Time.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2008-08 |
| **First release / Erste Veröffentlichung** | 2008-08-13 (version 1.0, "Botfixers Revenge") |
| **Latest version / Aktuelle Version** | 1.0 (no later versions / keine weiteren Versionen) |
| **Platform / Plattform** | Amiga with working battclock and removed battery, Workbench 3.x, ARexx |
| **Type / Art** | Software (ARexx script) |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum download area |
| **License / Lizenz** | Freely distributable; based on DateCheck by Michael Tanzer / Frei verteilbar; basiert auf DateCheck von Michael Tanzer |
| **Related projects / Verwandte Projekte** | none |

---

## English

### Overview

It has become almost normal to remove the battery from every Amiga. On most computers the clock chip still works. Without a battery, however, the operating system finds that the clock has no valid state after power-on, and it uses the date of the last format of the system hard disk as the system time.

TimeFixer takes it from there. It compares the system time with a reference, the date of the system disk (saved once with the command `snoop`), and if both are the same, it calls Prefs/Time automatically. You can then enter a valid, current time and save it on the chip. The computer works with the new value until it is switched off. The time is kept across resets.

### Background

Many Amiga users remove the old battery from their computers, because old batteries tend to leak and can damage the board. The A1K user Botfixer, known in the forum as the godfather of Amiga repairs, has saved many mainboards by desoldering the batteries preventively, if they were not already leaking. After that, the clock chip itself usually still works, but it loses the time at every power-off. Setting the time by hand at every start is easy to forget, and files then get a wrong date. TimeFixer reminds you at the right moment.

### Project History

TimeFixer 1.0 appeared in August 2008 under the subtitle "Botfixers Revenge", a homage to the A1K user Botfixer (see above). It is based on DateCheck by Michael Tanzer, modified by me. There were no later versions. I published it on 13 August 2008 in the A1K forum.

### Technical Description

TimeFixer is a short ARexx script. It works with a small data file, `S:TimeFixer.dat`.

Without a valid clock, the operating system uses the date of the last format of the system disk as the system time. This happens at every cold start, and it also repeats after a reset, because the clock chip contains no valid time until a time has been saved on it actively.

1. **Saving the reference (SNOOP).** After the Amiga has been switched off for a few seconds, the clock chip has no valid time. After the next start, `RX TimeFixer snoop` saves this wrong time, which is the date of the disk, as a reference in the data file.
2. **Checking at every start.** The command `RX >NIL: TimeFixer` in the Startup-Sequence compares the current system time with the saved reference. If they are equal, the clock has no valid time, and the script starts `SYS:Prefs/Time` in the background.
3. **Setting the time.** The user enters the current time and saves it. From then on, the clock chip keeps the valid time, even after a reset. The script sees that the time now differs from the reference, and everything is fine.

The comparison is made by day, not by time of day, to compensate for certain run-time deviations. The script uses the libraries `rexxsupport.library` and `rexxarplib.library`, which come with the archive. If the data file is missing, TimeFixer reports that it cannot open it. Called with a wrong option, it prints a short usage text: `TIMEFIXER <SNOOP>`.

### Features

- Automatic check at every start
- Starts Prefs/Time only when the clock has no valid time
- Time stays valid across resets
- Simple installation, one line in the Startup-Sequence

### Requirements

- Amiga with a working battery-backed clock chip and removed battery
- Workbench 3.x
- ARexx
- The libraries from the `LIBS` directory of the archive

### Installation and Usage

1. Copy all libraries from the `LIBS` directory of the archive to `SYS:LIBS`.
2. Copy `S/TimeFixer.rexx` to `SYS:S`.
3. Add this line to `SYS:S/Startup-Sequence`, between `LoadWB` and `EndCLI`:

```
RX >NIL: TimeFixer
```

4. Switch the Amiga off and wait a few seconds.
5. Start the Amiga, wait until the Workbench has loaded, and open a Shell or CLI.
6. Enter this command:

```
RX TimeFixer snoop
```

That is all. From now on, Prefs/Time opens automatically after every cold start.

### Known Limitations

- Without a battery, the time is lost at every power-off, so it has to be entered at every cold start.
- After the system disk has been formatted again, its date changes. This does not matter, because the operating system and TimeFixer have to be reinstalled anyway.


### Version History

| Version | Date | Notes |
|---------|------|-------|
| 1.0 "Botfixers Revenge" | 2008-08-13 | First and only release in the A1K forum; based on DateCheck by Michael Tanzer |

---

## Deutsch

### Übersicht

Heutzutage ist es beinahe üblich, jedem Amiga die Batterie zu entfernen. Bei den meisten Rechnern funktioniert der Uhrenchip trotzdem noch. Ohne Batterie erkennt das Betriebssystem jedoch, dass die Uhr nach dem Einschalten keinen gültigen Zustand hat, und verwendet als Systemzeit das Datum der letzten Formatierung der Systemfestplatte.

Hier setzt TimeFixer an. Es vergleicht die Systemzeit mit einer Referenz, dem Datum des Datenträgers (einmal mit dem Befehl `snoop` gespeichert), und ruft bei Gleichheit automatisch Prefs/Time auf. Man kann dann eine gültige, aktuelle Systemzeit eingeben und auf dem Chip speichern. Der Rechner arbeitet bis zum Ausschalten mit dem neuen Wert. Die Zeit bleibt bei Resets erhalten.

### Hintergrund

Viele Amiga-Nutzer bauen die alte Batterie aus ihren Rechnern aus, weil alte Batterien auslaufen und die Platine beschädigen können. Der A1K-Nutzer Botfixer, im Forum der Pate der Amiga-Reparaturen, hat etliche Mainboards gerettet, indem er die Batterien vorbeugend auslötete, wenn sie nicht ohnehin schon am Auslaufen waren. Danach funktioniert der Uhrenchip meist noch, verliert aber bei jedem Ausschalten die Zeit. Man kann leicht vergessen die Zeit von Hand einzustellen, geänderte oder neue Dateien bekommen dann ein falsches Datum. TimeFixer erinnert im richtigen Moment daran.

### Projektgeschichte

TimeFixer 1.0 erschien im August 2008 mit dem Untertitel „Botfixers Revenge“, einer Hommage an den A1K-Nutzer Botfixer (siehe oben). Es basiert auf DateCheck von Michael Tanzer und wurde von mir angepasst. Weitere Versionen gab es nicht. Ich habe es am 13. August 2008 im A1K-Forum veröffentlicht.

### Technische Beschreibung

TimeFixer ist ein kurzes ARexx-Skript. Es arbeitet mit einer kleinen Datendatei, `S:TimeFixer.dat`.

Ohne gültige Uhr verwendet das Betriebssystem als Systemzeit das Datum der letzten Formatierung der Systemfestplatte. Das geschieht bei jedem Kaltstart und wiederholt sich auch nach einem Reset, weil der Uhrenchip keine gültige Zeit enthält, bis einmal aktiv eine Zeit auf ihm gespeichert wird.

1. **Die Referenz speichern (SNOOP).** Nachdem der Amiga einige Sekunden ausgeschaltet war, hat der Uhrenchip keine gültige Zeit. Nach dem nächsten Start speichert `RX TimeFixer snoop` diese falsche Zeit, also das Datum des Datenträgers, als Referenz in der Datendatei.
2. **Prüfen bei jedem Start.** Der Befehl `RX >NIL: TimeFixer` in der Startup-Sequence vergleicht die aktuelle Systemzeit mit der gespeicherten Referenz. Sind beide gleich, hat die Uhr keine gültige Zeit, und das Skript startet `SYS:Prefs/Time` im Hintergrund.
3. **Zeit einstellen.** Der Anwender gibt die aktuelle Zeit ein und speichert sie. Ab dann behält der Uhrenchip die gültige Zeit, auch nach einem Reset. Das Skript erkennt die von der Referenz abweichende Zeit, und alles ist gut.

Der Vergleich erfolgt nach Tag, nicht nach Uhrzeit, um gewisse Laufzeitabweichungen auszugleichen. Das Skript nutzt die Bibliotheken `rexxsupport.library` und `rexxarplib.library`, die dem Archiv beiliegen. Fehlt die Datendatei, meldet TimeFixer, dass sie nicht geöffnet werden kann. Bei einer falschen Option gibt es einen kurzen Hilfetext aus: `TIMEFIXER <SNOOP>`.

### Funktionen

- Automatische Prüfung bei jedem Start
- Startet Prefs/Time nur, wenn die Uhr keine gültige Zeit hat
- Zeit bleibt bei Resets erhalten
- Einfache Installation, eine Zeile in der Startup-Sequence

### Voraussetzungen

- Amiga mit funktionierendem Uhrenchip und entfernter Batterie
- Workbench 3.x
- ARexx
- Die Bibliotheken aus dem Verzeichnis `LIBS` des Archivs

### Installation und Verwendung

1. Alle Bibliotheken aus dem Verzeichnis `LIBS` des Archivs nach `SYS:LIBS` kopieren.
2. `S/TimeFixer.rexx` nach `SYS:S` kopieren.
3. Diese Zeile in `SYS:S/Startup-Sequence` zwischen `LoadWB` und `EndCLI` einfügen:

```
RX >NIL: TimeFixer
```

4. Den Amiga ausschalten und einige Sekunden warten.
5. Den Amiga starten, abwarten, bis die Workbench geladen ist, und eine Shell oder ein CLI öffnen.
6. Diesen Befehl eingeben:

```
RX TimeFixer snoop
```

Das ist alles. Ab jetzt öffnet sich Prefs/Time nach jedem Kaltstart automatisch.

### Bekannte Einschränkungen

- Ohne Batterie geht die Zeit bei jedem Ausschalten verloren, sie muss also bei jedem Kaltstart eingegeben werden.
- Nach einer erneuten Formatierung der Systemfestplatte ändert sich ihr Datum. Das spielt keine Rolle, weil das Betriebssystem und TimeFixer ohnehin neu installiert werden müssen.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| 1.0 „Botfixers Revenge“ | 2008-08-13 | Erste und einzige Veröffentlichung im A1K-Forum; basiert auf DateCheck von Michael Tanzer |

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| [TIMEFIXER.LHA](https://www.a1k.org/download/area51/OLD/TIMEFIXER.LHA) | 1.0 | 2008-08-13 | A1K forum download area; contains the script `S/TimeFixer.rexx` and the libraries |

---

## References / Quellen

- A1K forum, TimeFixer 1.0 announcement, 2008-08-13: <https://www.a1k.org/forum/index.php?threads/12074/post-189729>
- Aminet, DateCheck by Michael Tanzer (original program): <https://aminet.net/package/util/rexx/DateCheck>

---

## Notes / Hinweise

**EN:** TimeFixer is based on DateCheck by Michael Tanzer (version 1.01, uploaded to Aminet on 15 August 1992, category util/rexx). DateCheck is a Rexx program that validates the system date by comparing it with the date stored when it was last executed. If the system date is earlier than the stored date or much later, the user is notified by a requester. TimeFixer builds on this idea: it compares the system time with a reference saved once, and starts Prefs/Time. The script is plain text and can be read in the archive.

**DE:** TimeFixer basiert auf DateCheck von Michael Tanzer (Version 1.01, am 15. August 1992 auf Aminet hochgeladen, Kategorie util/rexx). DateCheck ist ein Rexx-Programm, das das Systemdatum prüft, indem es es mit dem Datum vergleicht, das beim letzten Aufruf gespeichert wurde. Liegt das Systemdatum vor dem gespeicherten Datum oder deutlich danach, wird der Anwender mit einem Requester benachrichtigt. TimeFixer baut auf dieser Idee auf: Es vergleicht die Systemzeit mit einer einmal gespeicherten Referenz und startet Prefs/Time. Das Skript ist reiner Text und lässt sich im Archiv lesen.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-07</sub>
