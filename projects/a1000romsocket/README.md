# A1000 ROM Socket / Low-cost ROM adapters for Kickstart in the Amiga 1000

> **EN:** A1000 ROM Socket is a series of two low-cost adapters that let the Amiga 1000 run a Kickstart ROM (256 or 512 KB) instead of loading Kickstart from disk: a BootROM version, a CPU socket version, and a version that can be switched between ROM and disk operation.
>
> **DE:** A1000 ROM Socket ist eine Reihe von zwei preiswerten Adaptern, mit denen der Amiga 1000 ein Kickstart-ROM (256 oder 512 KB) nutzen kann, statt Kickstart von Diskette zu laden: eine BootROM-Version, eine CPU-Sockel-Version und eine Version, die zwischen ROM- und Disk-Betrieb umschaltbar ist.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2007-08 (part 1 published on 2007-08-12) |
| **First release / Erste Veröffentlichung** | 2007-08-12 (A1K forum) |
| **Latest version / Aktuelle Version** | Part 3 (2007-10-24); board layout for the CPU-ROM adapter (2008-11-04) |
| **Platform / Plattform** | Amiga 1000 (with and without PiggyPack) |
| **Type / Art** | Hardware (hand-wired adapters, later a board layout); partly based on known solutions / teils auf bekannten Lösungen beruhend |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum (build descriptions, layout download) |
| **License / Lizenz** | Free; no warranty / Frei; ohne Gewähr |
| **Related projects / Verwandte Projekte** | [Holzbrett](../holzbrett/) |

---

## English

### Overview

The Amiga 1000 has no Kickstart ROM. It loads Kickstart from a disk into a Writable Control Store (WCS), which is protected from writing afterwards. These adapters allow using an ordinary Kickstart ROM instead, from OS 2.x up to OS 3.x, in the Amiga 1000. The third part makes it switchable: the Amiga either uses the Kickstart ROM or, quite like an A1000, boots a Kickstart disk. That gives the whole choice from OS 3.x to 1.x, with one hundred percent retro feeling.

The adapters are cheap, because they need only ordinary parts. They are built by hand with enamelled copper wire. Hand wiring is easy, even for people who touch their soldering iron only every ten years.

### Background

The solutions are not new. I rebuilt them and described them step by step for the [Holzbrett](../holzbrett/):

- **Part 1 (BootROM version)** is known from the Amiga Magazin and from a rework by AmigaFuture1000 and a friend of his. I wrote down the build. For the installation, I refer to the "Kickplatine" description of the Amiga Magazin and to the rework by AmigaFuture1000. His version allows a less destructive conversion.
- **Part 2 (CPU socket version):** the information comes from Aminet, supplemented with a lot of know-how from Ralf.
- **Part 3 (switchable)** builds on the CPU-ROM adapter of part 2. It is my own switchable solution. Ralf already had a ROM/BootROM switch on his own board and would have preferred controlling the BootROMs through their chip select signal. My circuit switches off their supply voltage instead, and it works as well.
- For the thoughts on the RAM, Botfixer and Boing4000 helped with brainstorming. Thanks to both.

### Project History

| Date | Event |
|---|---|
| 2007-05-26 | "ROM upgrade" is on the to-do list of the Holzbrett |
| 2007-08-12 | Part 1: BootROM adapter (pictures, cost, build) |
| 2007-08-13 | Wiring of part 1 |
| 2007-08-20 | Part 2: CPU socket version |
| 2007-08-21 | The adapter passes its test run: the new Kickstart works. Wiring of part 2 and the required changes to the Amiga |
| 2007-08-26 | Discussion with Ralf about a possible fourth part: using the WOM RAM chips as extra memory at `$C00000`. It stays a thought experiment |
| 2007-09-23 | First work on the ROM/disk switch. An attempt to switch the BootROMs via the jumper W2 fails because I interrupted pin 1 instead of pin 28 |
| 2007-09-27 | The switchable Kickstart/BootROM solution works |
| 2007-10-24 | Part 3: the switchable ROM adapter, with the complete build description |
| 2008-11-04 | The CPU-ROM adapter as a board layout (download with a viewer) |

### Part 1: BootROM version

The first part shows the BootROM adapter solution. It costs about 15 euros for a single piece:

| Part | Price |
|---|---|
| 100 nF capacitor | 0.14 € |
| Euro board 160 × 100 mm | 2.35 € |
| IC socket, 40 pin | 0.52 € |
| Enamelled copper wire | 3.10 € |
| 2 × precision contact strip, 32 pin | 3.54 € each |
| 2-pin socket with wire, for the two extra connections | 1.55 € |
| 8-pin pin header (or the remains of a contact strip) for the 2-pin plug to the mainboard | 0.29 € |

An existing ROM (256 or 512 KB) is a prerequisite. The board needs 32/34 rows of holes in width and 16 rows in height.

1. Remove excess copper (with a cutter or a rotary tool, because the connections must only be interrupted at certain points).
2. Solder in two strips of 14 pins and two strips of 12 pins, next to them the IC socket, the capacitor and the plug connection.
3. Prepare about 50 pieces of enamelled wire of about 8 cm. Prepare each contact of the IC socket with one piece of wire. After this, most of the work is done.
4. Connect the wires with the right contacts, and remove surplus wire.
5. Add the two extra lines and clean everything.
6. Measure the finished board for short circuits.

Enamelled wire is a great material: it insulates, and when you touch it with the soldering iron, the enamel burns away at that point. Wire, solder and copper bond there. It is much faster than stripping normal wire.

<details>
<summary>Wiring of part 1 (BootROM version)</summary>

ROM R1/06 → L3/04 means: ROM row 1, contact 6 connects to strip 3, contact 4.

| | | |
|---|---|---|
| ROM R1/01 → ROM R1/11 | ROM R1/16 → L4/13 | ROM R2/11 → L4/01 |
| ROM R1/02 → L3/02 | ROM R1/17 → L1/09 | ROM R2/12 → L4/05 |
| ROM R1/03 → L1/02 | ROM R1/18 → L1/07 | ROM R2/13 → L4/06 |
| ROM R1/04 → L3/03 | ROM R1/19 → L1/10 | ROM R2/14 → L4/07 |
| ROM R1/05 → L1/03 | ROM R1/20 → L1/11 | ROM R2/15 → L4/08 |
| ROM R1/06 → L3/04 | ROM R2/01 → L1/01 | ROM R2/16 → L4/09 |
| ROM R1/07 → L1/04 | ROM R2/02 → L3/01 | ROM R2/17 → L4/10 |
| ROM R1/08 → L3/05 | ROM R2/03 → L2/02 | ROM R2/18 → L4/11 |
| ROM R1/09 → L1/05 | ROM R2/04 → L4/02 | ROM R2/19 → L4/12 |
| ROM R1/10 → L2/01 | ROM R2/05 → L2/03 | ROM R2/20 → S2 |
| ROM R1/11 → L3/14 | ROM R2/06 → L4/03 | ROM R1/11 → K1 |
| ROM R1/12 → L3/06 | ROM R2/07 → L2/04 | K2 → L4/01 |
| ROM R1/13 → L4/14 | ROM R2/08 → L4/04 | K2 → ROM R2/10 |
| ROM R1/14 → L3/13 | ROM R2/09 → S1 |  |
| ROM R1/15 → L1/12 | ROM R2/10 → ROM R1/10 |  |

Additional wiring: ROM R1/11 → K1; K2 → L4/01; K2 → ROM R2/10.

Plug assignment: S1 = A18 address line; S2 = ROM select line.

</details>

### Part 2: CPU socket version

Part 2 is the CPU socket solution. The board measures 32 rows of holes in width and 18 rows in height. It has three separation lines on the underside. The one between ROM and CPU is thinner to save space. Because one row of holes is saved, the adapter has no contact to the CIA. 40 strips of enamelled wire are soldered to the ROM socket and fed through to the CPU. One plug contact for the connection to the mainboard and one additional line are soldered in. Then everything is cleaned and measured.

<details>
<summary>Wiring of part 2 (CPU socket version)</summary>

ROM R2/20 → C1/04 would mean: ROM row 2, contact 20 connects to CPU row 1, contact 4. (This wiring does not occur on the board.)

| | | |
|---|---|---|
| ROM R1/01 → C1/14 | ROM R1/15 → C2/29 | ROM R2/09 → C1/13 |
| ROM R1/02 → C1/04 | ROM R1/16 → C1/28 | ROM R2/10 → C2/19 |
| ROM R1/03 → C1/03 | ROM R1/17 → C2/30 | ROM R2/11 → C1/21 |
| ROM R1/04 → C1/02 | ROM R1/18 → C1/27 | ROM R2/12 → C1/22 |
| ROM R1/05 → C1/01 | ROM R1/19 → C2/31 | ROM R2/13 → C1/30 |
| ROM R1/06 → C2/01 | ROM R1/20 → C1/26 | ROM R2/14 → C1/23 |
| ROM R1/07 → C2/02 | ROM R2/01 → C1/05 | ROM R2/15 → C1/31 |
| ROM R1/08 → C2/03 | ROM R2/02 → C1/06 | ROM R2/16 → C1/24 |
| ROM R1/09 → C2/04 | ROM R2/03 → C1/07 | ROM R2/17 → C1/32 |
| ROM R1/10 → C2/17 | ROM R2/04 → C1/08 | ROM R2/18 → C1/25 |
| ROM R1/11 → C2/17 | ROM R2/05 → C1/09 | ROM R2/19 → C2/32 |
| ROM R1/12 → S1 | ROM R2/06 → C1/10 | ROM R2/20 → C2/19 |
| ROM R1/13 → C2/28 | ROM R2/07 → C1/11 | C1/21 → C2/17 |
| ROM R1/14 → C1/29 | ROM R2/08 → C1/12 |  |

Additional wiring: C1/21 → C2/17.

Plug assignment: S1 = ROM select line.

</details>

**Changes to the Amiga (parts 2 and 3).** The BootROMs have to come out, and three changes to the hardware are required.

For mainboards **with** a PiggyPack:

- Pin 17 / DAUGCAS / U6J: cut the line or bend up the pin (the IC was socketed on my board)
- Pins 1 and 20 / 74LS373 / U4K: connect with a 4.7 kΩ resistor
- Pin 19 / DAUGEN / U6L: connect with the ROM adapter. The old instruction used pin 13 here, which also works but causes problems with the switchable version.

For mainboards **without** a PiggyPack:

- Pin 17 / DAUGCAS / U6N: cut the line or bend up the pin
- Pins 1 and 20 / 74LS373 / U3J: connect with a 4.7 kΩ resistor
- Pin 19 / DAUGEN / U4S: connect with the ROM adapter

Ralf confirmed the same changes for his PAL A1000 Rev. B board.

### Part 3: Switchable ROM adapter

Part 3 is based on the CPU-ROM adapter of part 2. Whoever has built it can turn it into a switchable solution within minutes. Depending on the switch position, the Amiga asks for the Kickstart disk or uses the Kickstart ROM. The switchable solution needs these additional changes:

- **DAUGCAS** (pin 17 of U6J, or U6N without PiggyPack): cut the line. Switch: ROM = open, disk = connected.
- **LS373** (U4K, or U3J without PiggyPack): connect pin 20 with a 4.7 kΩ resistor (high). Then, over a switch, to pin 1: ROM = connected, disk = open.
- **DAUGEN** (pin 19 of U6L, or U4S without PiggyPack): connect to the ROM adapter. The chip select signal for the ROM adapter is switched: ROM = DAUGEN pin 19, disk = high through 4.7 kΩ from pin 20 of the LS373.
- **BootROMs:** cut the trace of pin 28 on each BootROM, or bend up the pin. Switch the BootROMs on and off: ROM = open, disk = connected.

A four-pole switch does the job. My test setup uses a small board for DAUGCAS, because the IC on my PiggyPack Amiga was socketed. A five-pole plug leads all the necessary signals to the switch. The BootROMs are supplied through pin 28, which is bundled and controlled by the switch. For the Kickstart ROM operation, the BootROMs have to be deactivated, so the supply is simply cut. Ralf would have preferred a circuit with control through the chip select signal of the BootROMs, but my solution works as well.

On the Holzbrett, I gave the BootROMs an adapter, but there is no room for it in the original A1000 case. In the case, bend up the pins of the two BootROMs and put the contact to the socket through a switch. That saves the space-consuming socket, and the disk drive can stay in its usual place.

### Board layout (November 2008)

The CPU-ROM adapter was later published as a board layout (download with a viewer). With this solution, the ROM disappears under the CPU, which has to be raised with a second row of sockets.

### Use in the Holzbrett

The Holzbrett Amiga runs its Kickstart3.9 ROM through this solution. The EPROM was prepared by an acquaintance, because I did not have my own programmer. See [Holzbrett](../holzbrett/).

**Disclaimer.** As always, I accept no liability for damage to your hardware.

### Downloads

| File / Datei | Date / Datum | Source / Quelle |
|---|---|---|
| [Board layout with viewer (rom.zip)](https://www.a1k.org/download/area51/OLD/schaltplaene/rom.zip) | 2008-11-04 | A1K forum download area |

### References / Quellen

- A1K forum, Holzbrett thread: part 1 [(pictures)](https://www.a1k.org/forum/index.php?threads/6745/post-100218) and [(wiring)](https://www.a1k.org/forum/index.php?threads/6745/post-100221), part 2 [(pictures)](https://www.a1k.org/forum/index.php?threads/6745/post-100237) and [(wiring)](https://www.a1k.org/forum/index.php?threads/6745/post-100245), part 3 [(switchable)](https://www.a1k.org/forum/index.php?threads/6745/post-100270), [board layout](https://www.a1k.org/forum/index.php?threads/6745/post-208742)
- "Kickplatine" of the Amiga Magazin (installation of part 1): 

<https://www.a1k.org/a1000/hardware/kickswitch/kickswitch.php>

- Rework by AmigaFuture1000 (installation of part 1, less destructive)

---

## Deutsch

### Übersicht

Der Amiga 1000 hat kein Kickstart-ROM. Er lädt Kickstart von Diskette in einen Writable Control Store (WCS), der danach gegen Schreiben geschützt wird. Mit diesen Adaptern lässt sich stattdessen ein gewöhnliches Kickstart-ROM im Amiga 1000 verwenden, von OS 2.x bis OS 3.x. Der dritte Teil macht es umschaltbar: Der Amiga benutzt entweder das Kickstart-ROM oder bootet, ganz A1000-like, eine Kickstart-Diskette. Damit hat man die ganze Auswahl von OS 3.x bis 1.x, mit hundert Prozent Retro-Gefühl.

Die Adapter sind billig, weil sie nur gewöhnliche Bauteile brauchen. Sie werden von Hand mit Kupferlackdraht aufgebaut. Das Verdrahten von Hand ist einfach, auch für Leute, die ihr Lötkolben nur alle zehn Jahre anfassen.

### Hintergrund

Die Lösungen sind nicht neu. Ich habe sie nachgebaut und für das [Holzbrett](../holzbrett/) Schritt für Schritt beschrieben:

- **Teil 1 (BootROM-Version)** ist bekannt aus dem Amiga-Magazin und aus einem Rework von AmigaFuture1000 und einem Kumpel von ihm. Ich habe den Aufbau beschrieben. Für den Einbau verweise ich auf die Beschreibung der „Kickplatine“ des Amiga-Magazins und auf das Rework von AmigaFuture1000. Seine Version erlaubt einen weniger zerstörerischen Umbau.
- **Teil 2 (CPU-Sockel-Version):** Die Informationen stammen aus dem Aminet, ergänzt mit reichlich Know-how von Ralf.
- **Teil 3 (umschaltbar)** baut auf dem CPU-ROM-Adapter aus Teil 2 auf. Es ist meine eigene umschaltbare Lösung. Ralf hatte auf seinem eigenen Board schon eine ROM/BootROM-Umschaltung und hätte die BootROMs lieber über ihr Chip-Select-Signal gesteuert. Meine Schaltung schaltet stattdessen ihre Versorgungsspannung ab, und das funktioniert ebenfalls.
- Beim Nachdenken über das RAM haben Botfixer und Boing4000 beim Brainstorming geholfen. Dank an beide.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2007-05-26 | „ROM-Upgrade“ steht auf der To-do-Liste des Holzbretts |
| 2007-08-12 | Teil 1: BootROM-Adapter (Bilder, Kosten, Aufbau) |
| 2007-08-13 | Verdrahtung von Teil 1 |
| 2007-08-20 | Teil 2: CPU-Sockel-Version |
| 2007-08-21 | Der Adapter besteht den Testlauf: Das neue Kickstart funktioniert. Verdrahtung von Teil 2 und die nötigen Änderungen am Amiga |
| 2007-08-26 | Diskussion mit Ralf über einen möglichen vierten Teil: die WOM-RAM-Chips als zusätzlichen Speicher bei `$C00000` nutzen. Es bleibt ein Gedankenspiel |
| 2007-09-23 | Erste Arbeit am ROM/Disk-Umschalter. Ein Versuch, die BootROMs über die Brücke W2 zu schalten, scheitert, weil ich Pin 1 statt Pin 28 unterbrochen hatte |
| 2007-09-27 | Die umschaltbare Kickstart/BootROM-Lösung läuft |
| 2007-10-24 | Teil 3: der umschaltbare ROM-Adapter mit der vollständigen Bauanleitung |
| 2008-11-04 | Der CPU-ROM-Adapter als Platinenlayout (Download mit Viewer) |

### Teil 1: BootROM-Version

Der erste Teil zeigt die BootROM-Adapter-Lösung. Sie kostet für ein Einzelstück etwa 15 Euro:

| Bauteil | Preis |
|---|---|
| 100-nF-Kondensator | 0,14 € |
| Europlatine 160 × 100 mm | 2,35 € |
| IC-Fassung, 40-polig | 0,52 € |
| Kupferlackdraht | 3,10 € |
| 2 × Präzisionskontaktstreifen, 32-polig | je 3,54 € |
| 2-polige Steckbuchse mit Litze, für die zwei Zusatzverbindungen | 1,55 € |
| 8-polige Stiftleiste (oder die Reste eines Kontaktstreifens) für den 2-poligen Stecker zum Mainboard | 0,29 € |

Ein vorhandenes ROM (256 oder 512 KB) ist Voraussetzung. Die Platine braucht 32/34 Lochreihen in der Breite und 16 Lochreihen in der Höhe.

1. Überschüssiges Kupfer entfernen (mit einem Cuttermesser oder dem Dremel, denn die Verbindungen müssen nur an bestimmten Stellen unterbrochen werden).
2. Zwei Leisten mit je 14 Pins und zwei Leisten mit je 12 Pins einlöten, daneben den IC-Sockel, den Kondensator und die Steckverbindung.
3. Etwa 50 Stücke Lackdraht von etwa 8 cm vorbereiten. Jeden Kontakt des IC-Sockels mit einem Drahtstück versehen. Danach ist die meiste Arbeit erledigt.
4. Die Drähte mit den richtigen Kontakten verbinden und überschüssigen Draht entfernen.
5. Die zwei Extraleitungen ergänzen und alles säubern.
6. Die fertige Platine auf Kurzschlüsse durchmessen.

Lackdraht ist ein tolles Material: Er isoliert, und wenn man mit dem Lötkolben darangeht, verbrennt der Lack an dieser Stelle. Draht, Lötzinn und Kupfer verbinden sich dort. Das geht viel schneller als normales Kabel abzuisolieren.

<details>
<summary>Verdrahtung von Teil 1 (BootROM-Version)</summary>

ROM R1/06 → L3/04 bedeutet: ROM Reihe 1, Kontakt 6 verbinden mit Leiste 3, Kontakt 4.

| | | |
|---|---|---|
| ROM R1/01 → ROM R1/11 | ROM R1/16 → L4/13 | ROM R2/11 → L4/01 |
| ROM R1/02 → L3/02 | ROM R1/17 → L1/09 | ROM R2/12 → L4/05 |
| ROM R1/03 → L1/02 | ROM R1/18 → L1/07 | ROM R2/13 → L4/06 |
| ROM R1/04 → L3/03 | ROM R1/19 → L1/10 | ROM R2/14 → L4/07 |
| ROM R1/05 → L1/03 | ROM R1/20 → L1/11 | ROM R2/15 → L4/08 |
| ROM R1/06 → L3/04 | ROM R2/01 → L1/01 | ROM R2/16 → L4/09 |
| ROM R1/07 → L1/04 | ROM R2/02 → L3/01 | ROM R2/17 → L4/10 |
| ROM R1/08 → L3/05 | ROM R2/03 → L2/02 | ROM R2/18 → L4/11 |
| ROM R1/09 → L1/05 | ROM R2/04 → L4/02 | ROM R2/19 → L4/12 |
| ROM R1/10 → L2/01 | ROM R2/05 → L2/03 | ROM R2/20 → S2 |
| ROM R1/11 → L3/14 | ROM R2/06 → L4/03 | ROM R1/11 → K1 |
| ROM R1/12 → L3/06 | ROM R2/07 → L2/04 | K2 → L4/01 |
| ROM R1/13 → L4/14 | ROM R2/08 → L4/04 | K2 → ROM R2/10 |
| ROM R1/14 → L3/13 | ROM R2/09 → S1 |  |
| ROM R1/15 → L1/12 | ROM R2/10 → ROM R1/10 |  |

Zusatzverdrahtung: ROM R1/11 → K1; K2 → L4/01; K2 → ROM R2/10.

Steckerbelegung: S1 = Adressleitung A18; S2 = ROM-Select-Leitung.

</details>

### Teil 2: CPU-Sockel-Version

Teil 2 ist die CPU-Sockel-Lösung. Die Platine misst 32 Lochreihen in der Breite und 18 in der Höhe. Sie hat auf der Unterseite drei Trennlinien. Die zwischen ROM und CPU ist dünner, um Platz zu sparen. Durch das Einsparen einer Lochreihe hat der Adapter keinen Kontakt zum CIA. 40 Streifen Lackdraht werden mit dem ROM-Sockel verlötet und zur CPU durchgeführt. Ein Steckkontakt für die Verbindung zum Mainboard und eine zusätzliche Leitung werden eingelötet. Dann wird alles gesäubert und durchgemessen.

<details>
<summary>Verdrahtung von Teil 2 (CPU-Sockel-Version)</summary>

ROM R2/20 → C1/04 würde bedeuten: ROM Reihe 2, Kontakt 20 verbinden mit CPU Reihe 1, Kontakt 4. (Diese Verdrahtung kommt auf der Platine nicht vor.)

| | | |
|---|---|---|
| ROM R1/01 → C1/14 | ROM R1/15 → C2/29 | ROM R2/09 → C1/13 |
| ROM R1/02 → C1/04 | ROM R1/16 → C1/28 | ROM R2/10 → C2/19 |
| ROM R1/03 → C1/03 | ROM R1/17 → C2/30 | ROM R2/11 → C1/21 |
| ROM R1/04 → C1/02 | ROM R1/18 → C1/27 | ROM R2/12 → C1/22 |
| ROM R1/05 → C1/01 | ROM R1/19 → C2/31 | ROM R2/13 → C1/30 |
| ROM R1/06 → C2/01 | ROM R1/20 → C1/26 | ROM R2/14 → C1/23 |
| ROM R1/07 → C2/02 | ROM R2/01 → C1/05 | ROM R2/15 → C1/31 |
| ROM R1/08 → C2/03 | ROM R2/02 → C1/06 | ROM R2/16 → C1/24 |
| ROM R1/09 → C2/04 | ROM R2/03 → C1/07 | ROM R2/17 → C1/32 |
| ROM R1/10 → C2/17 | ROM R2/04 → C1/08 | ROM R2/18 → C1/25 |
| ROM R1/11 → C2/17 | ROM R2/05 → C1/09 | ROM R2/19 → C2/32 |
| ROM R1/12 → S1 | ROM R2/06 → C1/10 | ROM R2/20 → C2/19 |
| ROM R1/13 → C2/28 | ROM R2/07 → C1/11 | C1/21 → C2/17 |
| ROM R1/14 → C1/29 | ROM R2/08 → C1/12 |  |

Zusatzverdrahtung: C1/21 → C2/17.

Steckerbelegung: S1 = ROM-Select-Leitung.

</details>

**Änderungen am Amiga (Teil 2 und 3).** Die BootROMs müssen raus, und drei Änderungen an der Hardware sind nötig.

Für Mainboards **mit** PiggyPack:

- Pin 17 / DAUGCAS / U6J: Leitung durchtrennen oder Beinchen hochbiegen (bei mir war der IC gesockelt)
- Pins 1 und 20 / 74LS373 / U4K: über einen 4,7-kΩ-Widerstand verbinden
- Pin 19 / DAUGEN / U6L: mit dem ROM-Adapter verbinden. Die alte Anleitung nannte hier Pin 13, was zwar auch funktioniert, aber bei der umschaltbaren Version Probleme erzeugt.

Für Mainboards **ohne** PiggyPack:

- Pin 17 / DAUGCAS / U6N: Leitung durchtrennen oder Beinchen hochbiegen
- Pins 1 und 20 / 74LS373 / U3J: über einen 4,7-kΩ-Widerstand verbinden
- Pin 19 / DAUGEN / U4S: mit dem ROM-Adapter verbinden

Ralf bestätigte dieselben Änderungen für sein PAL-A1000-Rev.-B-Board.

### Teil 3: Umschaltbarer ROM-Adapter

Teil 3 baut auf dem CPU-ROM-Adapter aus Teil 2 auf. Wer ihn schon gebaut hat, kann daraus in wenigen Minuten eine umschaltbare Lösung machen. Je nach Schalterstellung verlangt der Amiga nach der Kickstart-Diskette oder verwendet das Kickstart-ROM. Die umschaltbare Lösung braucht diese zusätzlichen Änderungen:

- **DAUGCAS** (Pin 17 von U6J, ohne PiggyPack U6N): Leitung durchtrennen. Schalter: ROM = auf, Disk = verbunden.
- **LS373** (U4K, ohne PiggyPack U3J): Pin 20 über einen 4,7-kΩ-Widerstand verbinden (High). Dann über einen Schalter auf Pin 1: ROM = verbunden, Disk = auf.
- **DAUGEN** (Pin 19 von U6L, ohne PiggyPack U4S): mit dem ROM-Adapter verbinden. Das Chip-Select-Signal für den ROM-Adapter wird geschaltet: ROM = DAUGEN Pin 19, Disk = High über 4,7 kΩ von Pin 20 des LS373.
- **BootROMs:** Die Leiterbahn von Pin 28 an jedem BootROM auftrennen oder das Beinchen hochbiegen. Über einen Schalter die BootROMs ein- und ausschalten: ROM = auf, Disk = verbunden.

Ein vierpoliger Schalter genügt. Mein Testaufbau nutzt eine kleine Platine für DAUGCAS, weil der IC bei meinem PiggyPack-Amiga gesockelt war. Ein fünfpoliger Stecker führt alle nötigen Signale zum Schalter. Die BootROMs werden über Pin 28 versorgt, diese Leitung wird zusammengefasst und vom Schalter gesteuert. Für den KickROM-Betrieb müssen die BootROMs deaktiviert werden, deshalb wird einfach die Spannungsversorgung getrennt. Ralf hätte lieber eine Schaltung mit Steuerung über das CS-Signal der BootROMs gehabt, meine Lösung funktioniert aber ebenfalls.

Auf dem Holzbrett habe ich die BootROMs mit einem Adapter versehen, im originalen A1000-Gehäuse ist dafür aber kein Platz. Im Gehäuse sollte man die Beinchen der beiden BootROMs hochbiegen und den Kontakt zum Sockel über einen Schalter legen. Das erspart den platzraubenden Sockel, und das Diskettenlaufwerk kann an seinem gewohnten Platz bleiben.

### Platinenlayout (November 2008)

Der CPU-ROM-Adapter wurde später als Platinenlayout veröffentlicht (Download mit Viewer). Bei dieser Lösung verschwindet das ROM unter der CPU, die mit einer zweiten Sockelreihe höher gelegt werden muss.

### Einsatz im Holzbrett

Das Holzbrett-Amiga betreibt sein Kickstart3.9-ROM über diese Lösung. Das EPROM wurde von einem Bekannten vorbereitet, weil ich keinen eigenen Brenner hatte. Siehe [Holzbrett](../holzbrett/).

**Haftungsausschluss.** Ich übernehme wie immer keine Haftung für Schäden an eurer Hardware.

### Downloads

| File / Datei | Date / Datum | Source / Quelle |
|---|---|---|
| [Platinenlayout mit Viewer (rom.zip)](https://www.a1k.org/download/area51/OLD/schaltplaene/rom.zip) | 2008-11-04 | A1K-Forum, Download-Bereich |

### Quellen

- A1K-Forum, Holzbrett-Thread: Teil 1 [(Bilder)](https://www.a1k.org/forum/index.php?threads/6745/post-100218) und [(Verdrahtung)](https://www.a1k.org/forum/index.php?threads/6745/post-100221), Teil 2 [(Bilder)](https://www.a1k.org/forum/index.php?threads/6745/post-100237) und [(Verdrahtung)](https://www.a1k.org/forum/index.php?threads/6745/post-100245), Teil 3 [(umschaltbar)](https://www.a1k.org/forum/index.php?threads/6745/post-100270), [Platinenlayout](https://www.a1k.org/forum/index.php?threads/6745/post-208742)
- „Kickplatine“ des Amiga-Magazins (Einbau von Teil 1): 

<https://www.a1k.org/a1000/hardware/kickswitch/kickswitch.php>

- Rework von AmigaFuture1000 (Einbau von Teil 1, weniger zerstörerisch)

---

## Gallery / Galerie

<!-- TODO: Fotos aus dem Thread auswählen (Ablage in images/): Teil 1 (Beiträge #129, #132), Teil 2 (#148, #150), Umschalter (#171, #178), Teil 3 (#181). -->

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-15</sub>

