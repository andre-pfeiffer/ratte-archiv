# Xtreme / A hardware laboratory for 1280×1024 on native AGA graphics

> **EN:** Xtreme is a spin-off of the HighGFX project. While HighGFX focused on practical high-resolution Workbench modes, Xtreme explored the technical limits of native AGA graphics in combination with the Indivision AGA hardware. It began as a hardware experiment and ended as a usable screen mode with a 1280×1024 output.
>
> **DE:** Xtreme ist ein Spin-off des HighGFX-Projekts. Während HighGFX auf praktische hochauflösende Workbench-Modi zielte, erkundete Xtreme die technischen Grenzen nativer AGA-Grafik in Kombination mit der Indivision-AGA-Hardware. Es begann als Hardwareexperiment und endete als nutzbarer Bildschirmmodus mit einer Ausgabe von 1280×1024.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2009-09 |
| **Prehistory / Vorgeschichte** | 2008-08 (first 1280×1024 test driver), 2009-03 (public preview "INDIVISION-XTREME") |
| **First release / Erste Veröffentlichung** | 2012-04-24 (version 40.5, part of HighGFX'n'more) |
| **Latest version / Aktuelle Version** | 40.5 (2012-04-24) |
| **Platform / Plattform** | Amiga ECS/AGA; supported by the Indivision AGA MK2 |
| **Type / Art** | Software (screen mode driver), developed together with hardware / zusammen mit Hardware entwickelt |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Only as part of [HighGFX'n'more](../highgfx/) (Aminet and icomp download area) |
| **License / Lizenz** | Like HighGFX: closed source, free to use / Wie HighGFX: Closed Source, frei verwendbar |
| **Related projects / Verwandte Projekte** | [HighGFX](../highgfx/) · [HD720](../hd720/) · [SuperPlus](../superplus/) |

---

## English

### Overview

Xtreme is not really a "resolution project". It is a hardware laboratory project from which, in the end, a usable screen mode emerged. This sets it apart from [HighGFX](../highgfx/) and [HD720](../hd720/). It is a spin-off of HighGFX, but with a different question behind it: how far can a flicker fixer actually be driven?

The aim was explicitly not to replace RTG graphics. It was to prove that even 1280×1024 can be realised on native AGA hardware. Xtreme really is extreme: we explored the limits of what is feasible.

### Why it was made

The development began during conversations with Jens Schönfeld and Oliver Achten of individual Computers (icomp) about the technical limits of the Indivision AGA of that time. The question was, in essence: how far can you drive the flicker fixer?

**The Indivision AGA MK2.** The original Indivision AGA was the starting point of the experiments. While the MK2 was being developed, Jens worked on new FPGA cores in parallel. These made higher pixel clocks, better timings and higher refresh rates possible. Driver and firmware were developed together. I received a version of the Indivision AGA MK2 for the development of Xtreme.

### Project History

| Date | Event |
|---|---|
| 2008-08 | The first test drivers for 1280×1024 (A1K forum thread 12097) |
| 2009-03 | Public preview "INDIVISION-XTREME" (A1K forum thread 12485) |
| 2009-09 | The actual project start |
| 2012 | Development of the Indivision AGA MK2 and its firmware (A1K forum thread 31568), with various test versions |
| 2012-04-24 | Xtreme 40.5 |
| 2020-09-20 | Part of HighGFX'n'more 1.0 |

The early publications of 2008 and the beginning of 2009 belong to the prehistory of the project. The first hardware test was done on a Mitsubishi Multisync monitor at the home of the forum user Boing4000, who sadly has passed away (R.I.P.).

### Technical Description

- **Output:** 1280×1024
- **Frequencies:** 34 Hz and 18 kHz
- **Overscan:** none
- **Screen position:** not freely adjustable
- **Dragging screens:** the screen remains "draggable"

**Modes and colours.** The widths and colour depths are exactly as with [HD720](../hd720/):

| Width | Beam | ECS | AGA |
|---|---|---|---|
| 1280 | 35 ns | 4 colours from 64 | 256 colours or HAM8 |
| 640 | 70 ns | 16 colours from 4096 | 256 colours or HAM8 |
| 320 | 140 ns | 32 colours from 4096, EHB or HAM6 | 256 colours or HAM8 |

The heights are 1024 lines (Interlace), 512 lines (NonLace) and 256 lines (DblScan).

**Chip RAM.** The Chip RAM requirement of about 1.3 MB refers to the test picture in 1280×1024 with 8 bitplanes in HAM8 mode.


### Features

- 1280×1024 output on native AGA hardware
- A hardware experiment that became a usable screen mode
- Developed together with the Indivision AGA MK2 firmware
- Screens stay draggable

### Requirements

- Amiga with AGA chipset (and the Indivision AGA MK2)
- Chip RAM: the test picture in 1280×1024 with 8 bitplanes (HAM8) needs about 1.3 MB
- A display or flicker fixer that can handle 34 Hz and 18 kHz
- HighGFX'n'more (copy the mode to `sys:devs/monitors/` and reboot)

### Supported flicker fixers

According to the icomp wiki and the Amiga Hardware Database, the Indivision AGA MK2 and MK2cr support the HighGFX'n'more modes HighGFX, HD720, Xtreme and SuperPlus.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Test drivers | 2008-08 | The first 1280×1024 drivers |
| Preview | 2009-03 | Public preview "INDIVISION-XTREME" |
| Test versions | 2012 | During the development of the MK2 and its firmware |
| 40.5 | 2012-04-24 | Final version, part of HighGFX'n'more |

### Gallery / Galerie

<!-- TODO: Fotos nachreichen (Ablage in images/): erster Hardwaretest auf dem Mitsubishi Multisync, spätere Tests mit dem Indivision AGA MK2. -->

### Downloads

Xtreme has no package of its own. It is included in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet and icomp download area |

### References / Quellen

- A1K forum, first 1280×1024 test driver (August 2008): <https://www.a1k.org/forum/index.php?threads/12097/>
- A1K forum, presentation "INDIVISION-XTREME" (March 2009): <https://www.a1k.org/forum/index.php?threads/12485/>
- A1K forum, MK2 and firmware development (2012): <https://www.a1k.org/forum/index.php?threads/31568/>
- HighGFX'n'more readme (Xtreme 40.5, 2012-04-24)
- icomp wiki, Indivision: <https://wiki.icomp.de/wiki/Indivision>
- Amiga Hardware Database, Indivision: <https://amiga.resource.cx/search.pl?product=indivision>

---

## Deutsch

### Übersicht

Xtreme ist eigentlich kein „Auflösungsprojekt“. Es ist ein Hardware-Laborprojekt, aus dem am Ende ein nutzbarer Bildschirmmodus entstanden ist. Das unterscheidet es deutlich von [HighGFX](../highgfx/) und [HD720](../hd720/). Es ist ein Spin-off von HighGFX, aber mit einer anderen Frage dahinter: Wie weit lässt sich ein FlickerFixer eigentlich treiben?

Das Ziel war ausdrücklich kein RTG-Ersatz. Es sollte der Nachweis sein, dass sich selbst 1280×1024 noch auf nativer AGA-Hardware realisieren lassen. Xtreme ist wirklich extrem: Wir haben die Grenzen des Machbaren erkundet.

### Warum es entstand

Die Entwicklung begann während der Gespräche mit Jens Schönfeld und Oliver Achten von individual Computers (icomp) über die technischen Grenzen des damaligen Indivision AGA. Die Frage war sinngemäß: Wie weit kann man den FlickerFixer eigentlich treiben?

**Der Indivision AGA MK2.** Der ursprüngliche Indivision AGA war Ausgangspunkt der Experimente. Während der Entwicklung des MK2 arbeitete Jens parallel an neuen FPGA-Cores. Dadurch wurden höhere Pixeltakte, bessere Timings und höhere Bildwiederholraten möglich. Treiber und Firmware entwickelten sich gemeinsam. Für die Entwicklung von Xtreme erhielt ich eine Version des Indivision AGA MK2.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2008-08 | Die ersten Testtreiber für 1280×1024 (A1K-Forenthread 12097) |
| 2009-03 | Öffentliche Vorschau „INDIVISION-XTREME“ (A1K-Forenthread 12485) |
| 2009-09 | Der eigentliche Projektbeginn |
| 2012 | Entwicklung des Indivision AGA MK2 und seiner Firmware (A1K-Forenthread 31568), mit verschiedenen Testversionen |
| 2012-04-24 | Xtreme 40.5 |
| 2020-09-20 | Teil von HighGFX'n'more 1.0 |

Die frühen Veröffentlichungen von 2008 und Anfang 2009 gehören zur Vorgeschichte des Projekts. Der erste Hardwaretest erfolgte auf einem Mitsubishi-Multisync-Monitor zu Hause bei dem Forennutzer Boing4000, der leider bereits verstorben ist (R.I.P.).

### Technische Beschreibung

- **Ausgabe:** 1280×1024
- **Frequenzen:** 34 Hz und 18 kHz
- **Overscan:** keiner
- **Bildlage:** nicht frei verschiebbar
- **Verschieben von Screens:** Der Bildschirm bleibt „dragable“

**Modi und Farben.** Die Breiten und Farbtiefen sind genau wie bei [HD720](../hd720/):

| Breite | Beam | ECS | AGA |
|---|---|---|---|
| 1280 | 35 ns | 4 Farben aus 64 | 256 Farben oder HAM8 |
| 640 | 70 ns | 16 Farben aus 4096 | 256 Farben oder HAM8 |
| 320 | 140 ns | 32 Farben aus 4096, EHB oder HAM6 | 256 Farben oder HAM8 |

Die Höhen sind 1024 Zeilen (Interlace), 512 Zeilen (NonLace) und 256 Zeilen (DblScan).

**Chip RAM.** Der ChipRAM-Bedarf von etwa 1,3 MB bezieht sich auf das Testbild in 1280×1024 mit 8 Bitplanes im HAM8-Modus.

### Funktionen

- 1280×1024-Ausgabe auf nativer AGA-Hardware
- Ein Hardwareexperiment, das zu einem nutzbaren Bildschirmmodus wurde
- Gemeinsam mit der Firmware des Indivision AGA MK2 entwickelt
- Screens bleiben verschiebbar

### Voraussetzungen

- Amiga mit AGA-Chipsatz (und dem Indivision AGA MK2)
- Chip RAM: Das Testbild in 1280×1024 mit 8 Bitplanes (HAM8) braucht etwa 1,3 MB
- Ein Monitor oder FlickerFixer, der 34 Hz und 18 kHz verarbeiten kann
- HighGFX'n'more (den Modus nach `sys:devs/monitors/` kopieren und neu starten)

### Unterstützte FlickerFixer

Laut icomp-Wiki und Amiga Hardware Database unterstützen der Indivision AGA MK2 und MK2cr die HighGFX'n'more-Modi HighGFX, HD720, Xtreme und SuperPlus.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Testtreiber | 2008-08 | Die ersten 1280×1024-Treiber |
| Vorschau | 2009-03 | Öffentliche Vorschau „INDIVISION-XTREME“ |
| Testversionen | 2012 | Während der Entwicklung des MK2 und seiner Firmware |
| 40.5 | 2012-04-24 | Finale Version, Teil von HighGFX'n'more |

### Downloads

Xtreme hat kein eigenes Paket. Es ist enthalten in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet und icomp-Downloadbereich |

### Quellen

- A1K-Forum, erster 1280×1024-Testtreiber (August 2008): <https://www.a1k.org/forum/index.php?threads/12097/>
- A1K-Forum, Vorstellung „INDIVISION-XTREME“ (März 2009): <https://www.a1k.org/forum/index.php?threads/12485/>
- A1K-Forum, MK2- und Firmwareentwicklung (2012): <https://www.a1k.org/forum/index.php?threads/31568/>
- Readme von HighGFX'n'more (Xtreme 40.5, 24.04.2012)
- icomp-Wiki, Indivision: <https://wiki.icomp.de/wiki/Indivision>
- Amiga Hardware Database, Indivision: <https://amiga.resource.cx/search.pl?product=indivision>

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-18</sub>
