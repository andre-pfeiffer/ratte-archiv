# SuperPlus / The Workbench accelerator for 800×600 on ECS and AGA

> **EN:** SuperPlus is a native 800×600 Workbench mode for Amiga ECS and AGA, named after Commodore's own Super72 mode. At first glance both look identical, but SuperPlus has the "plus": 16 instead of 4 colours under ECS, and a clearly higher speed under AGA.
>
> **DE:** SuperPlus ist ein nativer 800×600-Workbench-Modus für Amiga ECS und AGA, benannt nach Commodores eigenem Super72-Modus. Auf den ersten Blick sehen beide gleich aus, aber SuperPlus hat das „Plus“: 16 statt 4 Farben unter ECS und eine deutlich höhere Geschwindigkeit unter AGA.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2010-02 (first test driver on 2010-02-06) |
| **First release / Erste Veröffentlichung** | 2012-01-26 (version 40.5, part of HighGFX'n'more) |
| **Latest version / Aktuelle Version** | 40.5 (2012-01-26) |
| **Platform / Plattform** | Amiga ECS/AGA, AmigaOS 3.0 or higher |
| **Type / Art** | Software (screen mode driver); a spin-off of HighGFX / Ableger von HighGFX |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Only as part of [HighGFX'n'more](../highgfx/) (Aminet and icomp download area); there never was a package of its own |
| **License / Lizenz** | closed source, free to use / Closed Source, frei verwendbar |
| **Related projects / Verwandte Projekte** | [HighGFX](../highgfx/) · [HD720](../hd720/) · [Xtreme](../xtreme/) · [Dual Screen Mode](../dualscreenmode/) |

<!-- TODO: Projektbeginn bestätigen. In der Übersicht stand bisher 2012-01 (= Veröffentlichung). Aus dem Indivision-ECS-Thread: erster Testtreiber für 800×600 am 2010-02-06; der Autor erwähnte außerdem, dass die Arbeit schon 2009 parallel zu den Dual-Screen-Experimenten begann. -->

---

## English

### Overview

SuperPlus gives the Amiga an 800×600 Workbench, like Commodore's Super72 mode. It is the first Workbench accelerator of my graphics projects. It offers more speed than Super72 on AGA and ECS, and more colours on ECS. Like HD720 and Xtreme, it is a spin-off of [HighGFX](../highgfx/).

### Why it was made

The name comes from Commodore's own screen mode **Super72**, which also delivers 800×600 pixels on the screen. I derived "SuperPlus" from it, because for the end user both look identical at first glance: 800×600 pixels. The "wow effect", the "plus" of the driver, shows only on a closer look:

- **ECS:** 16 colours from 4096, compared with 4 from 64 with Super72.
- **AGA:** the performance is noticeably higher than with Super72. This is due to the different pixel clock. It relieves the system DMA, which gives the chipset more access to the Chip RAM, and as a result graphics operations are much faster, with an apparently identical resolution of 800×600.

Starting from 800×600 pixels on the screen, it is therefore a visual acceleration under AGA, and that is why SuperPlus is a real Workbench accelerator.

### Project History

| Date | Event |
|---|---|
| 2010-02-06 | First test driver: an ECS screen driver for 800×600 in 16 colours (the test limit was 8 colours); photos on the Iiyama MF5017 without Indivision, and on an AOC and a Fujitsu-Siemens TFT with it |
| 2010-07 | Jens Schönfeld explains why the mode is so demanding: it breaks the 256-pixel burst scheme of the Indivision, so the early termination of a burst has to be built into the hardware. The detection of the mode is difficult. My drivers only run from OS 3.0 |
| 2011-01 | The work is a cooperation with icomp. The test mode shows a requester at start: it must not be published, and one should wait for the dual screen driver |
| 2012-01-26 | SuperPlus 40.5 |
| 2020-09-20 | Part of HighGFX'n'more 1.0 |

The work was done together with Jens Schönfeld and Oliver Achten of individual Computers (icomp), who adapted the firmware of the Indivision ECS.

### Technical Description

**Modes and colours.** The widths and colour depths of SuperPlus:

| Width | Beam | ECS | AGA |
|---|---|---|---|
| 1600 | 35 ns | n/a | **This pixel clock is deliberately blocked in the driver; this resolution is not offered.** |
| 800 | 70 ns | 16 colours from 4096 | 256 colours or HAM8 |
| 400 | 140 ns | 32 colours from 4096, EHB or HAM6 | 256 colours or HAM8 |

This makes the "trick" behind SuperPlus visible: SuperPlus works one pixel clock step lower than Super72. It gets 800×600 pixels with the 70 ns beam, where Super72 needs the faster 35 ns pixel clock.

**Why 35 ns is blocked.** For a width of 1600 pixels, AGA would switch to CAS burst. With this picture geometry, that results in a different DMA structure than on ECS. At this point, the DMA of the AGA, quite literally, breaks down. SuperPlus is really at the limit, right on the edge.

**ECS compared with AGA.** The reason for the difference lies in the chipset:

| Property | ECS (Agnus / Denise) | AGA (Alice / Lisa) |
|---|---|---|
| Chip RAM data bus | 16 bit | 32 bit (for Lisa and the CPU) |
| Memory cycle (DMA) | Single CAS (1 × 16 bit) | Single or double CAS (up to 2 × 32 bit) |
| Maximum transfer per DMA slot | 16 bit (2 bytes) | 64 bit (8 bytes) |
| Maximum bitplanes (LowRes) | 6 (64 colours, EHB or HAM6) | 8 (256 colours or HAM8) |
| Memory alignment | 16 bit (word-aligned) | 16, 32 or 64 bit (depending on FMODE) |

On AGA, the DMA slots have to be divisible by 2, while ECS can serve single slots.

<!-- TODO: Höhen (Interlace, NonLace, DblScan) und Frequenzen für 800×600 ergänzen. -->

### Features

- Native 800×600 Workbench mode for ECS and AGA
- 16 colours from 4096 under ECS, instead of 4 from 64 with Super72
- Noticeably faster than Super72 under AGA, because of the relieved system DMA
- Faster than Super72 under ECS as well

### Requirements

- Amiga with ECS or AGA chipset, AmigaOS 3.0 or higher
- A display or flicker fixer that can handle the screen mode frequencies, for example the Indivision ECS or the Indivision AGA MK2 (the Indivision AGA of the first generation does not support SuperPlus, according to the icomp wiki and the Amiga Hardware Database)
- HighGFX'n'more (copy the mode to `sys:devs/monitors/` and reboot)

### Known Limitations

- The 1600-pixel mode (35 ns) is blocked on purpose.
- The driver does not run under OS 2.x.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Test drivers | 2010-02 to 2011-01 | 800×600 in 16 colours, cooperation with icomp; the test mode may not be published |
| 40.5 | 2012-01-26 | The first Workbench accelerator, part of HighGFX'n'more: more speed (AGA and ECS) and more colours (ECS only) compared with the Super72 driver |

### Gallery / Galerie

<!-- TODO: Fotos und Screenshots nachreichen (Ablage in images/; Fotos und Filme von Jens, Oliver und mir): Testtreiber 2010-02-06 auf Iiyama MF5017, AOC und Fujitsu-Siemens-TFT, Vergleich Super72 und SuperPlus, Workbench in 800×600. -->

### Downloads

SuperPlus has no package of its own. It is included in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet and icomp download area |

### References / Quellen

- A1K forum, Indivision ECS thread: first test driver for 800×600 (2010-02-06): 

<https://www.a1k.org/forum/index.php?goto/post&id=320772>

- A1K forum, Indivision ECS thread: the technical challenge of the 800×600 mode (2010-07-20)

- HighGFX'n'more readme (SuperPlus 40.5, 2012-01-26)

- icomp wiki, Indivision: 

<https://wiki.icomp.de/wiki/Indivision>

- Amiga Hardware Database, Indivision: 

<https://amiga.resource.cx/search.pl?product=indivision>

**Credits.** Photos and films are by Jens Schönfeld, Oliver Achten and me. Thanks to icomp for the cooperation.

---

## Deutsch

### Übersicht

SuperPlus gibt dem Amiga eine 800×600-Workbench, wie Commodores Super72-Modus. Es ist der erste Workbench-Beschleuniger unter meinen Grafikprojekten. Es bietet mehr Geschwindigkeit als Super72 unter AGA und ECS und mehr Farben unter ECS. Wie HD720 und Xtreme ist es ein Spin-off von [HighGFX](../highgfx/).

### Warum es entstand

Der Name stammt von Commodores eigenem Bildschirmmodus **Super72**, der ebenfalls 800×600 Pixel auf den Bildschirm bringt. Aus „Super72“ habe ich den Namen „SuperPlus“ abgeleitet, weil beide für den Endnutzer auf den ersten Blick identisch sind: 800×600 Pixel. Der „Wow-Effekt“, das „Plus“ an dem Treiber, zeigt sich erst beim genaueren Hinsehen:

- **ECS:** 16 Farben aus 4096, im Gegensatz zu 4 aus 64 bei Super72.
- **AGA:** Die Performance ist spürbar höher als bei Super72. Das liegt am anderen Pixeltakt. Er entlastet das System-DMA, was dem Chipset mehr Zugriff auf das Chip RAM ermöglicht, und als Ergebnis sind Grafikoperationen deutlich schneller, bei scheinbar gleicher Grafikauflösung von 800×600.

Ausgehend von 800×600 Pixeln auf dem Bildschirm ist es unter AGA also eine visuelle Beschleunigung, und deshalb ist SuperPlus ein echter Workbench-Beschleuniger.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2010-02-06 | Erster Testtreiber: ein ECS-Bildschirmtreiber für 800×600 in 16 Farben (das Testlimit waren 8 Farben); Fotos auf dem Iiyama MF5017 ohne Indivision und auf einem AOC und einem Fujitsu-Siemens-TFT mit Indivision |
| 2010-07 | Jens Schönfeld erklärt, warum der Modus so aufwendig ist: Er durchbricht das 256-Pixel-Burst-Schema des Indivision, deshalb muss das vorzeitige Abbrechen eines Bursts in die Hardware eingebaut werden. Die Erkennung des Modus ist schwierig. Meine Treiber laufen erst ab OS 3.0 |
| 2011-01 | Die Arbeit ist eine Kooperation mit icomp. Der Testmodus zeigt beim Start einen Requester: Er darf nicht veröffentlicht werden, und man soll auf den Dualscreen-Treiber warten |
| 2012-01-26 | SuperPlus 40.5 |
| 2020-09-20 | Teil von HighGFX'n'more 1.0 |

Die Arbeit entstand zusammen mit Jens Schönfeld und Oliver Achten von individual Computers (icomp), die die Firmware des Indivision ECS anpassten.

### Technische Beschreibung

**Modi und Farben.** Die Breiten und Farbtiefen bei SuperPlus:

| Breite | Beam | ECS | AGA |
|---|---|---|---|
| 1600 | 35 ns | n/a | **Dieser Pixeltakt ist im Treiber absichtlich gesperrt, diese Auflösung wird nicht angeboten.** |
| 800 | 70 ns | 16 Farben aus 4096 | 256 Farben oder HAM8 |
| 400 | 140 ns | 32 Farben aus 4096, EHB oder HAM6 | 256 Farben oder HAM8 |

Damit wird der „Trick“ hinter SuperPlus sichtbar: SuperPlus arbeitet einen Pixeltakt-Schritt niedriger als Super72. Es erreicht 800×600 Pixel mit dem 70-ns-Beam, wo Super72 den schnelleren 35-ns-Pixeltakt braucht.

**Warum 35 ns gesperrt sind.** Für eine Breite von 1600 Pixeln würde AGA auf CAS Burst schalten. Bei dieser Bildgeometrie hat das einen anderen DMA-Aufbau zur Folge als bei ECS. An dieser Stelle springt das DMA der AGA sprichwörtlich über die Klinge, ab hier bricht das DMA-System zusammen. SuperPlus ist wirklich am Limit, auf Kante.

**ECS im Vergleich zu AGA.** Der Grund für den Unterschied liegt im Chipsatz:

| Eigenschaft | ECS (Agnus / Denise) | AGA (Alice / Lisa) |
|---|---|---|
| Chip-RAM-Datenbus | 16 Bit | 32 Bit (für Lisa und die CPU) |
| Speicherzyklus (DMA) | Single-CAS (1 × 16 Bit) | Single- oder Double-CAS (bis 2 × 32 Bit) |
| Maximaler Transfer pro DMA-Slot | 16 Bit (2 Bytes) | 64 Bit (8 Bytes) |
| Maximale Bitplanes (LowRes) | 6 (64 Farben, EHB oder HAM6) | 8 (256 Farben oder HAM8) |
| Speicher-Alignment | 16 Bit (Word-aligned) | 16, 32 oder 64 Bit (je nach FMODE) |

Bei AGA müssen die DMA-Slots durch 2 teilbar sein, während ECS einzelne Slots bedienen kann.

### Funktionen

- Nativer 800×600-Workbench-Modus für ECS und AGA
- 16 Farben aus 4096 unter ECS, statt 4 aus 64 bei Super72
- Unter AGA spürbar schneller als Super72, wegen des entlasteten System-DMA
- Auch unter ECS schneller als Super72

### Voraussetzungen

- Amiga mit ECS- oder AGA-Chipsatz, AmigaOS 3.0 oder höher
- Ein Monitor oder FlickerFixer, der die Frequenzen des Bildschirmmodus verarbeiten kann, zum Beispiel der Indivision ECS oder der Indivision AGA MK2 (der Indivision AGA der ersten Generation unterstützt SuperPlus laut icomp-Wiki und Amiga Hardware Database nicht)
- HighGFX'n'more (den Modus nach `sys:devs/monitors/` kopieren und neu starten)

### Bekannte Einschränkungen

- Der 1600-Pixel-Modus (35 ns) ist absichtlich gesperrt.
- Der Treiber läuft nicht unter OS 2.x.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Testtreiber | 2010-02 bis 2011-01 | 800×600 in 16 Farben, Kooperation mit icomp; der Testmodus darf nicht veröffentlicht werden |
| 40.5 | 2012-01-26 | Der erste Workbench-Beschleuniger, Teil von HighGFX'n'more: mehr Geschwindigkeit (AGA und ECS) und mehr Farben (nur ECS) im Vergleich zum Super72-Treiber |

### Downloads

SuperPlus hat kein eigenes Paket. Es ist enthalten in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet und icomp-Downloadbereich |

### Quellen

- A1K-Forum, Indivision-ECS-Thread: erster Testtreiber für 800×600 (06.02.2010): 

<https://www.a1k.org/forum/index.php?goto/post&id=320772>

- A1K-Forum, Indivision-ECS-Thread: die technische Herausforderung des 800×600-Modus (20.07.2010)

- Readme von HighGFX'n'more (SuperPlus 40.5, 26.01.2012)

- icomp-Wiki, Indivision: 

<https://wiki.icomp.de/wiki/Indivision>

- Amiga Hardware Database, Indivision: 

<https://amiga.resource.cx/search.pl?product=indivision>

**Dank.** Fotos und Filme stammen von Jens Schönfeld, Oliver Achten und mir. Dank an icomp für die Zusammenarbeit.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-22</sub>
