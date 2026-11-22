# Dual Screen Mode / Native dual-monitor support with two Indivision ECS units

> **EN:** Dual Screen Mode was an attempt to give the Amiga a native second screen: two Indivision ECS flicker fixers, one as "primary" and one as "secondary", each driving its own monitor, plus a driver that spreads the Workbench over both. The hardware experiments worked, but the driver was never finished.
>
> **DE:** Dual Screen Mode war der Versuch, dem Amiga einen nativen zweiten Bildschirm zu geben: zwei Indivision-ECS-FlickerFixer, einer als „primary“ und einer als „secondary“, die je einen Monitor ansteuern, und ein Treiber, der die Workbench auf beide verteilt. Die Hardwareexperimente funktionierten, der Treiber wurde aber nie fertig.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2009-12 (samples of the Indivision ECS since 2009-07) |
| **First shown / Erstmals gezeigt** | 2009-12-22 (two Indivision ECS in an Amiga 1000), demo video 2009-12-31 |
| **Platform / Plattform** | Amiga ECS (tested in the Amiga 1000, with PiggyPack and with Rejuvenator) |
| **Type / Art** | Hardware experiment and driver (never finished) / Hardwareexperiment und Treiber (nie fertiggestellt) |
| **Status** | Not completed: the driver was never finished / Nicht abgeschlossen: Der Treiber wurde nie fertig |
| **Distribution / Verbreitung** | A1K forum (photos, demo video) |
| **License / Lizenz** | *zu ergänzen / to be added* |
| **Related projects / Verwandte Projekte** | [SuperPlus](../superplus/) · [HighGFX](../highgfx/) · [KickTOS](../kicktos/) |

---

## English

### Overview

The Dual Screen Mode is a native dual-monitor solution for the Amiga with two Indivision ECS units. The aim was independent of Picasso96 and RTG: a second Workbench screen on a second monitor with the native Amiga chipset, where icons and windows can be moved between the two monitors.

### Why it was made

The idea came from icomp. When Jens Schönfeld of individual Computers had to make the design of the Indivision ECS flatter for the A500 turbo cards, the board became so flat that he joked that two would fit on top of each other. He and Oliver Achten then looked for a sensible use for two flicker fixers. The solution was simple but needs a jumper, the "secondary jumper".

For me, the question was whether the Amiga can do a real dual screen natively, without an RTG graphics card, and how far this would go on an Amiga 1000. I had received two samples of the Indivision ECS as a tester (see below) and wrote the Workbench driver.

### Background: samples and the Amiga 1000

On 2 July 2009, Jens chose his test users for the Indivision ECS. I was one of them, because the Rejuvenator was "highly interesting". I received two samples.

An Amiga 1000 is tight: the Denise of the A1000 is hard to reach, and a standard flicker fixer is too high. On 9 July 2009, I suggested a diagonal shift. Jens then designed a board that considers the pin headers in the original A1000, fits in the Rejuvenator, and keeps out of the way of most A500 turbo cards. I also built my own socket displacement for Denise and ordered its boards on 2 November 2009.

### Project History

| Date | Event |
|---|---|
| 2009-07-02 | I become a tester of the Indivision ECS and receive two samples |
| 2009-08-25 | Jens announces the Dual Screen mode |
| 2009-10-05 | Two stacked prototype boards show two independent screens; a driver that spreads the Workbench over two monitors is in the works |
| 2009-11-02 | The boards of my socket displacement for Denise are ordered |
| 2009-12-22 | I show two Indivision ECS in an Amiga 1000, with PiggyPack and with Rejuvenator |
| 2009-12-31 | "The biggest hurdles are overcome." Demo video `IndyECS.MPG` |
| 2010-02-01 | New core version; internal changes so that my dual screen driver would work better |
| 2010-02-06 | An Amiga 1000 with three monitors at the same time |
| 2011-01 | Dualscreen only works with two Indivision units, and only when the driver is finished |

**Why the driver was never finished.** With one of the firmware updates, the "freeze" bit, which was toggled with an offset for the first and the second unit, stopped working. At the same time, another programmer had designed a P96 driver with 256 colours for the Indivision ECS. For icomp, that project had priority, which is understandable. The Dual Screen Mode was therefore never completed.

### The Amiga 1000 setup

I showed the setup on 22 December 2009:

- two Indivision ECS in an Amiga 1000, one with PiggyPack and one with Rejuvenator, with my self-built socket displacement for Denise
- the first unit is jumpered as primary, the second as secondary
- one intermediate socket was removed because of the height in dual operation
- the construction is not higher than the original Amiga 1000 power supply, and with the Rejuvenator it is about as high as the internal floppy drive in dual operation
- I called it "high tech meets low tech"
- a photo of a test under KickTOS ("test the impossible")

### Technical Description

Jens explained the principle in February 2010:

- The Agnus does not wait for Denise to fetch data, it "pushes" the data to Denise. The Indivision ECS captures this data, a second instance of Denise inside the Indivision creates a new picture, and writes it into the local framebuffer. From this framebuffer, the picture is displayed at a much higher frame rate.
- This write interface can be enabled and disabled. With a second Indivision ECS in the system, there is a second interface, and each unit has its own switch for writing into its framebuffer.
- With clever programming, one framebuffer is enabled and the other disabled, and a full frame is output. Then the enable bits are swapped, and a totally different frame is output. While the picture on the first monitor remains untouched, only the picture of the second monitor changes.
- **Consequence:** the Chip RAM performance is not increased. Instead, the total screen update rate is cut in half.

The dual screen mode requires two Indivision units, and it does not work with a monitor on the normal RGB output: a single Indivision jumpered as "secondary" with the primary screen on the normal RGB output results in wild flickering there.

### Features

- Two independent screens on two monitors, from the native Amiga chipset
- Independent from Picasso96 and RTG
- Tested in the Amiga 1000, with PiggyPack and with Rejuvenator
- An Amiga 1000 with three monitors at the same time

### Requirements

- An Amiga with ECS, with two Indivision ECS units (one jumpered as primary, one as secondary)
- For the Amiga 1000: a socket displacement for Denise
- Two monitors with VGA input

### Known Limitations

- The screen update rate is halved.
- The Workbench driver was never finished.
- The setup needs two Indivision units.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Hardware experiment | 2009-08 to 2009-12 | Two Indivision ECS, primary and secondary |
| Demo | 2009-12-31 | `IndyECS.MPG` |
| Test driver | 2010 | Not finished |

### Gallery / Galerie

<!-- TODO: Fotos und das Demovideo aus dem Indivision-ECS-Thread auswählen (Fotos und Filme von Jens, Oliver und mir; Ablage in images/): Beitrag vom 2009-12-22 (zwei Indivision ECS im A1000), 2009-12-31 (Video), 2010-02-06 (drei Monitore). -->

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [IndyECS.MPG (demo video)](https://www.a1k.org/download/area51/HighGFX/IndyECS.MPG) | A1K forum download area |

### References / Quellen

- A1K forum, Indivision ECS thread: announcement of the Dual Screen mode by Jens Schönfeld (2009-08-25): 

<https://www.a1k.org/forum/index.php?goto/post&id=278662>

- A1K forum, Indivision ECS thread: demo video (2009-12-31): 

<https://www.a1k.org/forum/index.php?goto/post&id=310384>

- A1K forum, Indivision ECS thread: A1000 with three monitors (2010-02-06): 

<https://www.a1k.org/forum/index.php?goto/post&id=320772>

- A1K forum, Indivision ECS thread: how the dual screen mode works (2010-02-22): 

<https://www.a1k.org/forum/index.php?goto/post&id=324654>

- icomp wiki, Indivision: 

<https://wiki.icomp.de/wiki/Indivision>

**Credits.** Photos and films are by Jens Schönfeld, Oliver Achten and me. Thanks to icomp for the samples and for the idea.

---

## Deutsch

### Übersicht

Der Dual Screen Mode ist eine native Dual-Monitor-Lösung für den Amiga mit zwei Indivision-ECS-Geräten. Das Ziel war unabhängig von Picasso96 und RTG: ein zweiter Workbench-Bildschirm auf einem zweiten Monitor mit dem nativen Amiga-Chipsatz, bei dem sich Icons und Fenster zwischen den beiden Monitoren verschieben lassen.

### Warum es entstand

Die Idee kam von icomp. Als Jens Schönfeld von individual Computers das Design des Indivision ECS wegen der A500-Turbokarten flacher machen musste, wurde die Platine so flach, dass er scherzte, es passten zwei übereinander. Er und Oliver Achten suchten dann nach einem sinnvollen Einsatz für zwei FlickerFixer. Die Lösung war einfach, braucht aber einen Jumper, den „secondary jumper“.

Für mich lautete die Frage, ob der Amiga nativ, ohne RTG-Grafikkarte, einen echten Dualscreen kann und wie weit das auf einem Amiga 1000 geht. Ich hatte als Tester zwei Muster des Indivision ECS bekommen (siehe unten) und schrieb den Workbench-Treiber.

### Hintergrund: Muster und der Amiga 1000

Am 2. Juli 2009 wählte Jens seine Testnutzer für den Indivision ECS aus. Ich war dabei, weil der Rejuvenator „höchst interessant“ war. Ich erhielt zwei Muster.

Im Amiga 1000 ist es eng: Der Denise des A1000 ist schwer erreichbar, und ein normaler FlickerFixer ist zu hoch. Am 9. Juli 2009 schlug ich eine diagonale Verschiebung vor. Jens entwarf daraufhin eine Platine, die die Stiftleisten im Ur-A1000 berücksichtigt, im Rejuvenator passt und den meisten A500-Turbokarten aus dem Weg geht. Ich baute außerdem meine eigene Sockelverschiebung für Denise und bestellte deren Platinen am 2. November 2009.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2009-07-02 | Ich werde Tester des Indivision ECS und erhalte zwei Muster |
| 2009-08-25 | Jens kündigt den Dual-Screen-Modus an |
| 2009-10-05 | Zwei übereinander gesteckte Prototypen zeigen zwei unabhängige Screens; ein Treiber, der die Workbench über zwei Monitore verteilt, ist in Arbeit |
| 2009-11-02 | Die Platinen meiner Sockelverschiebung für Denise werden bestellt |
| 2009-12-22 | Ich zeige zwei Indivision ECS in einem Amiga 1000, mit PiggyPack und mit Rejuvenator |
| 2009-12-31 | „Die größten Hürden sind genommen.“ Demovideo `IndyECS.MPG` |
| 2010-02-01 | Neue Core-Version; interne Änderungen, damit mein Dualscreen-Treiber besser funktionieren würde |
| 2010-02-06 | Ein Amiga 1000 mit drei Monitoren gleichzeitig |
| 2011-01 | Dualscreen funktioniert nur mit zwei Indivision-Geräten, und erst, wenn der Treiber fertig ist |

**Warum der Treiber nie fertig wurde.** Bei einem der Firmware-Updates funktionierte das „Freeze“-Bit nicht mehr, das bei der ersten und der zweiten Einheit versetzt getoggelt wurde. Zu diesem Zeitpunkt hatte ein anderer Programmierer für den Indivision ECS einen P96-Treiber mit 256 Farben entworfen. Dieses Projekt hatte für icomp Vorrang, was nachvollziehbar ist. Der Dual Screen Mode wurde deshalb nie fertiggestellt.

### Der Aufbau im Amiga 1000

Ich zeigte den Aufbau am 22. Dezember 2009:

- zwei Indivision ECS in einem Amiga 1000, einer mit PiggyPack und einer mit Rejuvenator, mit meiner selbstgebauten Sockelverschiebung für Denise
- die erste Einheit ist als Primary gejumpert, die zweite als Secondary
- ein Zwischensockel wurde wegen der Bauhöhe im Dualbetrieb entfernt
- der Aufbau ist nicht höher als das originale Amiga-1000-Netzteil, und mit dem Rejuvenator im Dualbetrieb etwa so hoch wie das interne Diskettenlaufwerk
- ich nannte es „Hightech meets Lowtech“
- ein Foto eines Tests unter KickTOS („Teste das Unmögliche“)

### Technische Beschreibung

Jens erklärte das Prinzip im Februar 2010:

- Der Agnus wartet nicht darauf, dass der Denise Daten holt, er „schiebt“ die Daten zum Denise. Der Indivision ECS fängt diese Daten ab, eine zweite Instanz des Denise im Indivision erzeugt ein neues Bild und schreibt es in das lokale Framebuffer. Aus diesem Framebuffer wird das Bild mit viel höherer Bildrate ausgegeben.
- Diese Schreibschnittstelle lässt sich ein- und ausschalten. Mit einem zweiten Indivision ECS im System gibt es eine zweite Schnittstelle, und jede Einheit hat ihren eigenen Schalter zum Schreiben in ihr Framebuffer.
- Mit cleverer Programmierung wird das eine Framebuffer eingeschaltet und das andere ausgeschaltet, und ein volles Bild wird ausgegeben. Dann werden die Enable-Bits getauscht, und ein völlig anderes Bild wird ausgegeben. Während das Bild des ersten Monitors unberührt bleibt, ändert sich nur das Bild des zweiten Monitors.
- **Folge:** Die Chip-RAM-Leistung steigt nicht. Stattdessen halbiert sich die gesamte Bildaktualisierungsrate.

Der Dualscreen-Modus braucht zwei Indivision-Geräte, und er funktioniert nicht mit einem Monitor am normalen RGB-Ausgang: Ein einzelner Indivision, als „secondary“ gejumpert, mit dem primären Screen am normalen RGB-Ausgang ergibt dort wildes Geflimmer.

### Funktionen

- Zwei unabhängige Screens auf zwei Monitoren, aus dem nativen Amiga-Chipsatz
- Unabhängig von Picasso96 und RTG
- Im Amiga 1000 getestet, mit PiggyPack und mit Rejuvenator
- Ein Amiga 1000 mit drei Monitoren gleichzeitig

### Voraussetzungen

- Ein Amiga mit ECS, mit zwei Indivision-ECS-Geräten (eines als Primary, eines als Secondary gejumpert)
- Für den Amiga 1000: eine Sockelverschiebung für Denise
- Zwei Monitore mit VGA-Eingang

### Bekannte Einschränkungen

- Die Bildaktualisierungsrate halbiert sich.
- Der Workbench-Treiber wurde nie fertiggestellt.
- Der Aufbau braucht zwei Indivision-Geräte.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Hardwareexperiment | 2009-08 bis 2009-12 | Zwei Indivision ECS, Primary und Secondary |
| Demo | 2009-12-31 | `IndyECS.MPG` |
| Testtreiber | 2010 | Nicht fertiggestellt |

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [IndyECS.MPG (Demovideo)](https://www.a1k.org/download/area51/HighGFX/IndyECS.MPG) | A1K-Forum, Download-Bereich |

### Quellen

- A1K-Forum, Indivision-ECS-Thread: Ankündigung des Dual-Screen-Modus durch Jens Schönfeld (25.08.2009): 

<https://www.a1k.org/forum/index.php?goto/post&id=278662>

- A1K-Forum, Indivision-ECS-Thread: Demovideo (31.12.2009): 

<https://www.a1k.org/forum/index.php?goto/post&id=310384>

- A1K-Forum, Indivision-ECS-Thread: A1000 mit drei Monitoren (06.02.2010): 

<https://www.a1k.org/forum/index.php?goto/post&id=320772>

- A1K-Forum, Indivision-ECS-Thread: Funktionsweise des Dual-Screen-Modus (22.02.2010): 

<https://www.a1k.org/forum/index.php?goto/post&id=324654>

- icomp-Wiki, Indivision: <https://wiki.icomp.de/wiki/Indivision>

**Dank.** Fotos und Filme stammen von Jens Schönfeld, Oliver Achten und mir. Dank an icomp für die Muster und für die Idee.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-22</sub>
