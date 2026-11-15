# A1000 PSU Tick / A TICK circuit to run the Amiga 1000 on an ATX power supply

> **EN:** A1000 PSU Tick is a small circuit that adds the missing TICK signal to a PC (ATX) power supply, so that an Amiga 1000, or another model that needs TICK from its power supply, runs reliably on it.
>
> **DE:** A1000 PSU Tick ist eine kleine Schaltung, die einem PC-Netzteil (ATX) das fehlende TICK-Signal hinzufügt, sodass ein Amiga 1000 oder ein anderes Modell, das TICK vom Netzteil braucht, damit zuverlässig läuft.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2007-06 (the problem appeared on 2007-06-14) |
| **First release / Erste Veröffentlichung** | 2007-06-29 (A1K forum); tested and working on 2007-07-01 |
| **Platform / Plattform** | Amiga 1000, or other models that need a TICK signal from the power supply |
| **Type / Art** | Hardware (small circuit inside the power supply); based on a known hack / beruht auf einem bekannten Hack |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum (photos, build) |
| **License / Lizenz** | None needed: anyone can rebuild it / Keine nötig: Jeder kann es nachbauen |
| **Related projects / Verwandte Projekte** | [Holzbrett](../holzbrett/) |

---

## English

### Overview

The Amiga 1000 needs a TICK signal from its power supply. It is a 5 V TTL signal of 50 Hz that serves as the clock for the timer of the CIA. A normal ATX PC power supply provides the voltages (+5 V, +12 V, ground) but no TICK. The circuit generates this TICK signal inside the ATX power supply, so that an inexpensive PC power supply can replace the original Amiga 1000 power supply.

### Background

For the [Holzbrett](../holzbrett/), I wanted to use a cheap PC power supply. It is a 250 W ATX power supply, which has to supply a naked Amiga 1000, a floppy and a hard disk, a Pentium III 700 and a Matrox graphics card.

### What went wrong

On 14 June 2007, I wrote in the forum: the box lets the Amiga start, but the power seems to be unstable. At the beginning, the picture even flickers, and after loading Kickstart, the computer sporadically hangs. With an original Amiga 1000 power supply, the Amiga runs 100 %.

- First suspicion: not enough power, or unstable voltages. Measuring the +5 V and +12 V gave no fluctuations, as far as my equipment could tell.
- A first hint: switching off the hard disk at the box (with `FDAPM spindown`) let the Amiga work cleanly.
- A forum member remarked that the A1000 is almost the only computer that cannot generate TICK by itself.
- On 17 June 2007, I found the cause. I ran the Amiga with an original A1000 power supply and, as a test, removed the TICK line. The same errors appeared as with the ATX box: the Kickstart picture is shown, Kickstart loads, and the computer hangs in a reset loop. **TICK was missing.**

### Interim solutions

First I tried to take TICK from VSync, which the A500 does as well:

- VSync from pin 12 of the RGB port: Kickstart loads and is recognised, but the signal is not strong enough for flicker fixer and TICK together. TICK works (no reset loop), but the flicker fixer delivers no signal.
- VSync from pin 38 of Agnus: everything runs 100 %, but after some time double images appear, and the picture drops out.
- Resistors of 47 Ω in the lines were tested in all combinations. The best result: TICK directly from the RGB port, and a resistor in the line from Agnus to the flicker fixer. Kickstart ran, the picture was 99 % stable, and in 10 minutes I saw only two very short picture drops (under load, while the floppy was active).

I did not like this "Agnus/TICK hack": with Copper tricks, such as the 60 Hz hack, it would make the clock run wrong. The power-grid TICK is also more accurate, because the mains delivers a constant 50 Hz. One forum member noted that the Amiga does not care, as long as one does not do video editing.

### The circuit

On 29 June 2007, I published the new TICK circuit for ATX power supplies. It uses a TICK circuit from the "PSU-Tick hack" on Aminet, for which a forum member had pointed to the archive `TickIt.lha`.

- **Size:** 65 × 20 × 20 mm.
- **Parts:** a relay (with the unnecessary leg removed), a transistor, diodes, resistors, an IC socket, a capacitor.
- **Connections:** on the left 230 V, on the right +5 V, TICK and ground.
- **Cost:** almost as expensive as a complete cheap ATX power supply. The electronics stores take a lot of money for the few small parts.

Steps of the build: prepare the relay and the transistor, cut and place the board, add the necessary jumpers, diodes, resistors, IC socket and transistor, then capacitor and relay, remove surplus copper, and test.

### Installation

The circuit fits into the ATX power supply. As a protective cover, I used a plastic tube from the hardware store (about 23.5 × 1.5 mm, 0.99 euro), closed at the ends with cable ties. Nothing can fall out. The cable ends got plugs, and the new TICK signal (the red cable) goes into the power supply plug.

On 1 July 2007, the TICK circuit worked: the test run was 100 % successful. Thanks to all advisers.

### Features

- A cheap ATX power supply for the Amiga 1000
- A real TICK signal from the power grid, not from VSync
- No intervention in the video circuit, so no problems with Copper tricks such as the 60 Hz hack
- Very small, fits inside the power supply

### Requirements

- An ATX power supply (a 250 W box was used)
- The small parts for the circuit and soldering skills

**Safety.** The circuit works with mains voltage (230 V) on one side. Please be careful, and use it only if you know what you are doing. As always, I accept no liability for damage.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Interim solutions | 2007-06-17 to 06-21 | TICK from VSync (RGB port or Agnus), tests with 47 Ω resistors |
| TICK circuit | 2007-06-29 | Published in the A1K forum |
| Working installation | 2007-07-01 | Test run 100 % successful |

### Gallery / Galerie

<!-- TODO: Fotos aus dem Thread auswählen (Ablage in images/): Netzteil-Test (#59), Platine und Aufbau (#123), Einbau im ATX-Netzteil (#124). -->

### References / Quellen

- A1K forum, Holzbrett thread: 

[the problem (14 June 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100148), 

[TICK as the cause (17 June 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100166), 

[the TICK circuit for ATX power supplies (29 June 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100210), 

[the build](https://www.a1k.org/forum/index.php?threads/6745/post-100212), 

[the installation (1 July 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100213)

- Aminet, `TickIt.lha` (the "PSU-Tick hack"): 

<https://aminet.net/docs/hard/TickIt.lha>

---

## Deutsch

### Übersicht

Der Amiga 1000 braucht von seinem Netzteil ein TICK-Signal. Es ist ein 5-V-TTL-Signal mit 50 Hz, das als Takt für den Timer des CIA dient. Ein normales ATX-PC-Netzteil liefert die Spannungen (+5 V, +12 V, Masse), aber kein TICK. Die Schaltung erzeugt dieses TICK-Signal im ATX-Netzteil, sodass ein preiswertes PC-Netzteil das originale Amiga-1000-Netzteil ersetzen kann.

### Hintergrund

Für das [Holzbrett](../holzbrett/) wollte ich ein billiges PC-Netzteil verwenden. Es ist ein ATX-Netzteil mit 250 W, das einen nackten Amiga 1000, ein Diskettenlaufwerk und eine Festplatte, einen Pentium III 700 und eine Matrox-Grafikkarte versorgen muss.

### Was schiefging

Am 14. Juni 2007 schrieb ich im Forum: Das Dosennetzteil lässt den Rechner starten, aber der Saft scheint unstabil zu sein. Gerade am Anfang flackert sogar das Bild, und nach dem Laden von Kickstart hängt er sich sporadisch auf. Mit einem originalen A1000-Netzteil rennt der Rechner zu 100 %.

- Erster Verdacht: zu wenig Leistung oder unstabile Spannungen. Beim Durchmessen von +5 V und +12 V gab es im Rahmen meiner Möglichkeiten keine Schwankungen.
- Ein erster Hinweis: Das Abschalten der Festplatte an der Dose (mit `FDAPM spindown`) ließ den Amiga sauber arbeiten.
- Ein Forumsmitglied bemerkte, dass der A1000 fast der einzige Rechner ist, der TICK nicht selbst erzeugen kann.
- Am 17. Juni 2007 fand ich die Ursache. Ich betrieb den Amiga mit einem originalen A1000-Netzteil und entfernte versuchsweise die TICK-Leitung. Es traten dieselben Fehler auf wie an der ATX-Dose: Das Kickstart-Bild wird angezeigt, Kickstart wird geladen, und der Rechner hängt in einer Reset-Schleife. **Es fehlte TICK.**

### Zwischenlösungen

Zuerst versuchte ich, TICK aus VSync zu gewinnen, wie es auch der A500 macht:

- VSync vom Pin 12 des RGB-Ports: Kickstart lädt und wird erkannt, aber das Signal reicht nicht für FlickerFixer und TICK zusammen. TICK arbeitet (keine Reset-Schleife), aber der FlickerFixer liefert kein Signal.
- VSync von Pin 38 des Agnus: Alles läuft zu 100 %, aber nach einiger Zeit kommen Doppelbilder, und das Bild bricht weg.
- Widerstände mit 47 Ω in den Leitungen wurden in allen Kombinationen getestet. Das beste Ergebnis: TICK direkt vom RGB-Port und ein Widerstand in der Leitung vom Agnus zum FlickerFixer. Kickstart lief, das Bild war zu 99 % stabil, und in 10 Minuten hatte ich nur zwei sehr kurze Bildverluste (unter Last, bei Laufwerksaktivität).

Der „Agnus/TICK-Hack“ gefiel mir nicht: Bei Copper-Tricks, zum Beispiel dem 60-Hz-Hack, würde er die Uhr falsch laufen lassen. Außerdem ist das TICK aus dem Stromnetz genauer, weil das Netz konstant 50 Hz liefert. Ein Forumsmitglied meinte, dem Amiga sei das egal, solange man kein Video-Editing macht.

### Die Schaltung

Am 29. Juni 2007 veröffentlichte ich die neue TICK-Schaltung für ATX-Netzteile. Sie nutzt eine TICK-Schaltung aus dem „PSU-Tick-Hack“ im Aminet, auf dessen Archiv `TickIt.lha` ein Forumsmitglied hingewiesen hatte.

- **Größe:** 65 × 20 × 20 mm.
- **Bauteile:** ein Relais (vom unnötigen Beinchen befreit), ein Transistor, Dioden, Widerstände, ein IC-Sockel, ein Kondensator.
- **Anschlüsse:** links 230 V, rechts +5 V, TICK und Masse.
- **Kosten:** fast so teuer wie ein komplettes billiges ATX-Netzteil. Die Elektronikläden nehmen gutes Geld für die paar Kleinteile.

Bauschritte: Relais und Transistor vorbereiten, Platine zuschneiden und bestücken, die nötigen Brücken, Dioden, Widerstände, IC-Sockel und Transistor einsetzen, dann Kondensator und Relais, überschüssiges Kupfer entfernen und testen.

### Einbau

Die Schaltung passt in das ATX-Netzteil. Als Schutzhülle nutzte ich ein Kunststoffrohr aus dem Baumarkt (etwa 23,5 × 1,5 mm, 0,99 Euro), an den Enden mit Kabelbindern verschlossen. Da fällt nichts raus. Die Kabelenden bekamen Stecker, und das neue TICK-Signal (das rote Kabel) geht in den Netzteilstecker.

Am 1. Juli 2007 funktionierte der TICK: Der Testlauf war zu 100 % erfolgreich. Ein Dank an alle mitwirkenden Berater.

### Funktionen

- Ein billiges ATX-Netzteil für den Amiga 1000
- Ein echtes TICK-Signal aus dem Stromnetz, nicht aus VSync
- Kein Eingriff in die Videoschaltung, daher keine Probleme mit Copper-Tricks wie dem 60-Hz-Hack
- Sehr klein, passt in das Netzteil

### Voraussetzungen

- Ein ATX-Netzteil (verwendet wurde eine 250-W-Dose)
- Die Kleinteile für die Schaltung und Löterfahrung

**Sicherheit.** Die Schaltung arbeitet auf einer Seite mit Netzspannung (230 V). Bitte Vorsicht, und nur nachbauen, wenn man weiß, was man tut. Ich übernehme wie immer keine Haftung für Schäden.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Zwischenlösungen | 2007-06-17 bis 06-21 | TICK aus VSync (RGB-Port oder Agnus), Tests mit 47-Ω-Widerständen |
| TICK-Schaltung | 2007-06-29 | Im A1K-Forum veröffentlicht |
| Funktionierender Einbau | 2007-07-01 | Testlauf zu 100 % erfolgreich |

### Quellen

- A1K-Forum, Holzbrett-Thread: 

[das Problem (14. Juni 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100148), 

[TICK als Ursache (17. Juni 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100166), 

[die TICK-Schaltung für ATX-Netzteile (29. Juni 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100210), 

[der Aufbau](https://www.a1k.org/forum/index.php?threads/6745/post-100212), 

[der Einbau (1. Juli 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100213)

- Aminet, `TickIt.lha` (der „PSU-Tick-Hack“): 

<https://aminet.net/docs/hard/TickIt.lha>

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-15</sub>
