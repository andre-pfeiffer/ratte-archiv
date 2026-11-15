# Holzbrett / Amiga 1000 and x86 PC on one wooden board

> **EN:** The Holzbrett ("wooden board") is an Amiga 1000 and an x86 PC on a large sheet of plywood, connected by a KVM switch. It grew over several years into a complete system from my own developments, hardware from the scene and PC integration, and was later enclosed as the wall display "Holzkasten".
>
> **DE:** Das Holzbrett ist ein Amiga 1000 und ein x86-PC auf einer großen Sperrholzplatte, verbunden über einen KVM-Switch. Es wuchs über mehrere Jahre zu einem Gesamtsystem aus eigenen Entwicklungen, Szene-Hardware und PC-Integration und wurde später als Wandvitrine „Holzkasten“ eingehaust.

## Release Information / Eckdaten

| | |
|---|---|
| **Also known as / Auch bekannt als** | Holzkasten, Wandkasten (after the case modding / nach dem Case Modding) |
| **Project start / Projektbeginn** | 2007-05 (first post in the A1K forum on 2007-05-26) |
| **Latest stage / Letzter Ausbau** | Wall display (2008-02); Protein turbo card (2013) |
| **Platform / Plattform** | Amiga 1000 and x86 PC (Amithlon-capable) |
| **Type / Art** | Hardware (complete system) |
| **Status** | Completed; the system still exists and is stored in the cellar / Abgeschlossen; das System besteht noch und ist im Keller eingelagert |
| **Distribution / Verbreitung** | Documented in the A1K forum thread; build descriptions of the parts |
| **License / Lizenz** | *zu ergänzen / to be added* |
| **Related projects / Verwandte Projekte** | [Video Port](../a1000videoport/) · [PSU Tick](../a1000psutick/) · [ROM Socket](../a1000romsocket/) · [Audio](../a1000audio/) · [Audio Mixer](../a1000audiomixer/) · [Case Modding](../casemodding/) |

---

## English

### Overview

The Holzbrett started in May 2007 as an Amiga 1000 mainboard on a plywood board, to be developed freely: connect video, power, ROM, floppy, keyboard and expansions in a way a normal case would not allow. It became an Amiga 1000 and an x86 PC side by side on one board, with one monitor, one keyboard and one mouse, and a KVM switch to change between the two computers with a keystroke. The Amiga can be switched off separately while the PC keeps running.

In February 2008, the board was built into a case with a plexiglass window and hung on the wall. This enclosed version is called the Holzkasten (also "Wandkasten", see [Case Modding](../casemodding/)).

### Background

The thread in the A1K forum starts on 26 May 2007 with these words: in the beginning there was only an Amiga 1000 mainboard (Rev. A, PiggyPack, PAL) on a wooden board. The to-do list at that time was: FlickerFixer, ROM upgrade, FloppyFix and Babylon interface.

The plywood sheet measured 2 × 1 meters and cost about four euros in a hardware store. In September 2007 I replaced it with a larger board, which my wife designed to her wishes. The later wall display took over the colour: my wife painted the plywood in a rich red.

### What is on the board

| Part | Description | More |
|---|---|---|
| Amiga 1000 | Mainboard Rev. A with PiggyPack, PAL Agnus, 512 KB Chip RAM | |
| Video | An internal video slot for the flicker fixer, with a MultiVision2000, delivers a 31 kHz VGA signal; the RGB signals are taken from Denise | [Video Port](../a1000videoport/) |
| Power supply | Modified 250 W ATX power supply with a TICK circuit; it supplies +12 V, −12 V, +5 V, ground and the TICK signal | [PSU Tick](../a1000psutick/) |
| ROM | CPU socket board with a socket for a 512 KB ROM (Kickstart 3.x), an add-on board in the BootROM sockets; start with Kickstart 3.x or, as in the old days, with a Kickstart disk | [ROM Socket](../a1000romsocket/) |
| Audio | Audio low-pass filter switchable by the power LED, mixer for three sources, speakers on 12 V from the PC power supply | [Audio](../a1000audio/), [Audio Mixer](../a1000audiomixer/) |
| Floppy drive | A PC drive (Teac FD-235HF) with a prototype of the HD-FloppyFix, which allows HD disks (from OS 2.x on) | |
| Keyboard and mouse | A PC keyboard through a PS/2-to-A2000 adapter and a self-built A2000-to-A1000 adapter, a PS/2 mouse or trackball, fixed with Velcro so that they can be taken off | |
| KVM switch | Switches monitor, keyboard and mouse between the Amiga and the PC (Digitus DC OC-12) | |
| PC | ASUS A7V266-E, 1 GHz Athlon, 128 MB DDR, 10 GB hard disk, GeForce2 Ti Pro, Realtek 8139 network; chosen so that Amithlon runs an Amiga emulation on it | |
| Control box | A small wooden box with switches for the Amiga (power off without switching off the PC, choice of KickROM or BootROM), the PC speaker and LEDs | |
| Expansion connector | Above the control box: on the left a connector that is about 99 % compatible with the Phoenix CPU slot, on the right the important signals of the PCI bus; intended for the Babylon interface | |
| Case | Four side walls, a hood that opens, an illuminated wooden frame and a plexiglass window | [Case Modding](../casemodding/) |

### Own developments and integrated hardware

The Holzbrett Amiga was not a single hobby project but a system that grew over years from my own developments, hardware from the Amiga scene and the integration of a PC.

**My own developments**

- ROM socket solutions (three parts: BootROM version, CPU socket version, switchable between disk and ROM operation)
- the Babylon interface
- adapter solutions
- video and audio modifications
- KVM integration
- building the case

**Hardware from others, integrated into the system**

- **HD-FloppyFix prototype:** provided by Botfixer.
- **PS/2 keyboard adapter for the Amiga:** provided by Reptile.
- **TurboFE:** the accelerator card was provided by Georg Braun, the developer of the famous GBA1000 mainboard. I tested it in January 2008 on the Phoenix-compatible CPU slot. It was probably the first use of a Phoenix accelerator on a "normal" Amiga.
- **Protein:** a turbo card that Botfixer offered as a soldering workshop in the environment of the A1K forum (see below).

The Babylon interface was on the Holzbrett. The planned Babylon bridge card, which would have connected the two computers, was never built.

### The Protein

The Protein is an Amiga turbo card that Botfixer offered as a soldering workshop in the environment of the A1K forum. The aim was for everybody to build their own turbo card. It has the following features:

- 14 MHz acceleration
- entirely through-hole technology (THT), no SMD parts, so even beginners can solder it
- sockets for up to 8 MB of Fast RAM
- an IDE interface

In the Holzbrett Amiga, it is permanently installed and the final stage of the system:

- it replaces the original 68000 with a 68010
- a small hard disk is connected
- OS 3.9 is in use
- the Kickstart/OS 3.9 ROM runs through the ROM socket solution I had developed earlier
- the EPROM was prepared by an acquaintance, because I had no programmer of my own

### Timeline

| Date | Event |
|---|---|
| 2007-05-26 | The thread starts: an Amiga 1000 mainboard on a wooden board |
| 2007-05-28 to 06-01 | Video Port on the board, first test with 15 and 31 kHz |
| 2007-06 to 07 | Problems with the ATX power supply, TICK circuit for ATX power supplies |
| 2007-08 to 10 | ROM adapter in three parts, ROM/disk switch, KVM switch |
| 2007-09 | A larger board, designed by my wife |
| 2007-11 | Audio filter switchable by the power LED, Phoenix-compatible CPU slot |
| 2007-12 | Overview of the whole system, audio mixer |
| 2008-01 | TurboFE test |
| 2008-02 | Plexiglass window, logo, the board hangs on the wall as the Holzkasten |
| 2008-11 | CPU-ROM adapter as a board layout |
| 2013 | Protein turbo card |

### Today

The system still exists and is basically working. It is stored properly in the cellar, not permanently set up: because of changes in the family (we have children), there is no hobby room any more.

### Gallery / Galerie

<!-- TODO: Fotos aus dem Thread auswählen und beschriften (Ablage in images/): Anfang 2007-05-26, VideoPort-Testlauf, ROM-Adapter, Gesamtaufbau Dezember 2007, Wandkasten Februar 2008, Protein 2013. -->

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [Holzbrett movie](https://www.a1k.org/download/area51/OLD/Holzbrett.mpg) | A1K forum download area |
| [VideoPort movie (test run)](https://www.a1k.org/download/area51/OLD/VideoPort.mpg) | A1K forum download area |
| [VideoPort boards incl. indicator for WinXP, ready for a board service](https://www.a1k.org/download/area51/OLD/VideoPort.zip) | A1K forum download area |

### References / Quellen

- A1K forum, "Amiga 1000 - Holzbrett Edition (Ratte)", 16 pages, 26 May 2007 to 15 December 2013: 

<https://www.a1k.org/forum/index.php?threads/6745/>
- Amiga Future Special, page 36: "Amiga Modding Teil 11: Der Amiga im Wandkasten" by Henning W. Knopp (March 2011), in the online article database: 

<https://www.amigafuture.de/app.php/kb/viewarticle?a=3683>

### Credits / Dank

Thanks to the members of the A1K forum for their help and ideas, especially Reptile, Ralf, Georg Braun, Botfixer, Boing4000 (R.I.P.) and AmigaFuture1000, and to my wife.

---

## Deutsch

### Übersicht

Das Holzbrett begann im Mai 2007 als Amiga-1000-Mainboard auf einer Sperrholzplatte, die sich frei weiterentwickeln lassen sollte: Video, Strom, ROM, Diskette, Tastatur und Erweiterungen so anzuschließen, wie es ein normales Gehäuse nicht erlaubt. Daraus wurden ein Amiga 1000 und ein x86-PC nebeneinander auf einem Brett, mit einem Monitor, einer Tastatur und einer Maus und einem KVM-Switch, mit dem man per Tastendruck zwischen den beiden Rechnern umschaltet. Der Amiga lässt sich getrennt ausschalten, während der PC weiterläuft.

Im Februar 2008 wurde das Brett in ein Gehäuse mit Plexiglasscheibe eingebaut und an die Wand gehängt. Diese eingehauste Fassung heißt Holzkasten (auch „Wandkasten“, siehe [Case Modding](../casemodding/)).

### Hintergrund

Der Thread im A1K-Forum beginnt am 26. Mai 2007 mit dem Satz: Am Anfang war nur ein A1000-Mainboard (Rev. A, PiggyPack, PAL) auf einem Holzbrett. Die To-do-Liste lautete damals: FlickerFixer, ROM-Upgrade, FloppyFix und Babylon-Interface.

Die Sperrholzplatte war 2 × 1 Meter groß und kostete im Baumarkt etwa vier Euro. Im September 2007 ersetzte ich sie durch ein größeres Brett, das meine Frau nach ihren Wünschen gestalten durfte. Die spätere Wandvitrine übernahm die Farbe: Meine Frau lackierte die Sperrholzplatte in einem satten Rot.

### Was auf dem Brett sitzt

| Teil | Beschreibung | Mehr |
|---|---|---|
| Amiga 1000 | Mainboard Rev. A mit PiggyPack, PAL-Agnus, 512 KB Chip RAM | |
| Video | Ein interner Video-Slot für den FlickerFixer, mit einer MultiVision2000, liefert ein VGA-Signal mit 31 kHz; die RGB-Signale werden vom Denise abgegriffen | [Video Port](../a1000videoport/) |
| Netzteil | Umgebautes 250-W-ATX-Netzteil mit TICK-Schaltung; es liefert +12 V, −12 V, +5 V, Masse und das TICK-Signal | [PSU Tick](../a1000psutick/) |
| ROM | CPU-Sockel-Platine mit Sockel für ein 512-KB-ROM (Kickstart 3.x), eine Zusatzplatine in den BootROM-Sockeln; Start mit Kickstart 3.x oder wie früher mit einer Kickstart-Diskette | [ROM Socket](../a1000romsocket/) |
| Audio | Per Power-LED schaltbarer Audio-Tiefpassfilter, Mixer für drei Quellen, Lautsprecher an 12 V aus dem PC-Netzteil | [Audio](../a1000audio/), [Audio Mixer](../a1000audiomixer/) |
| Diskettenlaufwerk | Ein PC-Laufwerk (Teac FD-235HF) mit einem Prototyp des HD-FloppyFix, der HD-Disketten (ab OS 2.x) erlaubt | |
| Tastatur und Maus | Eine PC-Tastatur über einen PS/2-auf-A2000-Adapter und einen selbstgebauten A2000-auf-A1000-Adapter, eine PS/2-Maus oder ein Trackball, mit Klettband befestigt, sodass sie abnehmbar sind | |
| KVM-Switch | Schaltet Monitor, Tastatur und Maus zwischen Amiga und PC um (Digitus DC OC-12) | |
| PC | ASUS A7V266-E, 1-GHz-Athlon, 128 MB DDR, 10-GB-Festplatte, GeForce2 Ti Pro, Realtek-8139-Netzwerk; so gewählt, dass Amithlon darauf eine Amiga-Emulation laufen lässt | |
| Kontrollbox | Eine kleine Holzkiste mit Schaltern für den Amiga (Ausschalten, ohne den PC auszuschalten, Wahl zwischen KickROM und BootROM), dem PC-Speaker und LEDs | |
| Erweiterungsanschluss | Über der Kontrollbox: links ein zu etwa 99 % zum Phoenix-CPU-Slot kompatibler Anschluss, rechts die wichtigen Signale des PCI-Busses; gedacht für das Babylon-Interface | |
| Gehäuse | Vier Seitenwände, eine aufklappbare Haube, ein beleuchteter Holzrahmen und eine Plexiglasscheibe | [Case Modding](../casemodding/) |

### Eigene Entwicklungen und integrierte Hardware

Das Holzbrett-Amiga war kein einzelnes Bastelprojekt, sondern ein über Jahre gewachsenes Gesamtsystem aus eigenen Entwicklungen, Hardware aus der Amiga-Szene und der Integration eines PCs.

**Eigene Entwicklungen**

- ROM-Sockel-Lösungen (drei Teile: BootROM-Version, CPU-Sockel-Version, umschaltbar zwischen Disk- und ROM-Betrieb)
- das Babylon-Interface
- Adapterlösungen
- Video- und Audio-Umbauten
- KVM-Integration
- Gehäusebau

**Hardware von anderen, ins System integriert**

- **HD-FloppyFix-Prototyp:** von Botfixer zur Verfügung gestellt.
- **PS/2-Tastaturadapter für den Amiga:** von Reptile zur Verfügung gestellt.
- **TurboFE:** Die Turbokarte wurde von Georg Braun zur Verfügung gestellt, dem Entwickler des berühmten GBA1000-Mainboards. Ich habe sie im Januar 2008 auf dem Phoenix-kompatiblen CPU-Slot getestet. Es war vermutlich der erste Einsatz einer Phoenix-Turbokarte auf einem „normalen“ Amiga.
- **Protein:** eine Turbokarte, die Botfixer im Umfeld des A1K-Forums als Lötworkshop anbot (siehe unten).

Das Babylon-Interface war auf dem Holzbrett. Die geplante Babylon-Brückenkarte, die beide Rechner verbunden hätte, wurde nie verwirklicht.

### Die Protein

Die Protein ist eine Amiga-Turbokarte, die Botfixer im Umfeld des A1K-Forums als Lötworkshop anbot. Ziel war, dass jeder eine eigene Turbokarte aufbauen kann. Sie hat diese Merkmale:

- 14 MHz Beschleunigung
- komplett in THT (Through Hole Technology), keine SMD-Bauteile, deshalb auch für Anfänger lötbar
- Sockel für bis zu 8 MB FastRAM
- eine IDE-Schnittstelle

Im Holzbrett-Amiga ist sie dauerhaft eingebaut und die letzte Ausbaustufe des Systems:

- sie ersetzt die originale 68000-CPU durch eine 68010
- eine kleine Festplatte ist angeschlossen
- OS 3.9 ist im Einsatz
- das Kickstart/OS-3.9-ROM läuft über die zuvor entwickelte ROM-Socket-Lösung
- das EPROM wurde von einem Bekannten vorbereitet, weil ich keinen eigenen Brenner hatte

### Zeitleiste

| Datum | Ereignis |
|---|---|
| 2007-05-26 | Der Thread beginnt: ein Amiga-1000-Mainboard auf einem Holzbrett |
| 2007-05-28 bis 06-01 | Video Port auf dem Brett, erster Test mit 15 und 31 kHz |
| 2007-06 bis 07 | Probleme mit dem ATX-Netzteil, TICK-Schaltung für ATX-Netzteile |
| 2007-08 bis 10 | ROM-Adapter in drei Teilen, ROM/Disk-Umschalter, KVM-Switch |
| 2007-09 | Ein größeres Brett, von meiner Frau gestaltet |
| 2007-11 | Per Power-LED schaltbarer Audiofilter, Phoenix-kompatibler CPU-Slot |
| 2007-12 | Gesamtübersicht des Systems, Audiomixer |
| 2008-01 | TurboFE-Test |
| 2008-02 | Plexiglasscheibe, Logo, das Brett hängt als Holzkasten an der Wand |
| 2008-11 | CPU-ROM-Adapter als Platinenlayout |
| 2013 | Protein-Turbokarte |

### Heute

Das System besteht noch und ist grundsätzlich funktionsfähig. Es ist ordentlich im Keller eingelagert, nicht dauerhaft aufgebaut: Durch Veränderungen in der Familie (wir haben Kinder) gibt es keinen Hobbyraum mehr.

### Gallery / Galerie

<!-- TODO: Siehe oben. -->

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [Holzbrett-Film](https://www.a1k.org/download/area51/OLD/Holzbrett.mpg) | A1K-Forum, Download-Bereich |
| [VideoPort-Film (Testlauf)](https://www.a1k.org/download/area51/OLD/VideoPort.mpg) | A1K-Forum, Download-Bereich |
| [VideoPort-Platinen inkl. Anzeiger für WinXP, fertig für Platinenservice](https://www.a1k.org/download/area51/OLD/VideoPort.zip) | A1K-Forum, Download-Bereich |

### Quellen

- A1K-Forum, „Amiga 1000 - Holzbrett Edition (Ratte)“, 16 Seiten, 26. Mai 2007 bis 15. Dezember 2013:

<https://www.a1k.org/forum/index.php?threads/6745/>
- Amiga Future Special, Seite 36: „Amiga Modding Teil 11: Der Amiga im Wandkasten“ von Henning W. Knopp (März 2011), in der Online-Artikeldatenbank: 

<https://www.amigafuture.de/app.php/kb/viewarticle?a=3683>

### Dank

Dank an die Mitglieder des A1K-Forums für ihre Hilfe und Ideen, besonders an Reptile, Ralf, Georg Braun, Botfixer, Boing4000 (R.I.P.) und AmigaFuture1000, und an meine Frau.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-15</sub>
