# HighGFX / 1024×768 display modes for Amiga ECS and AGA

> **EN:** HighGFX is a high-resolution graphics mode extension for Amiga ECS and AGA systems, providing Workbench resolutions up to 1024×768 on suitable hardware, without an RTG graphics card.
>
> **DE:** HighGFX erweitert Amiga-ECS- und AGA-Systeme um hochauflösende Grafikmodi und ermöglicht Workbench-Auflösungen bis 1024×768 auf kompatibler Hardware, ohne RTG-Grafikkarte.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | ca. 1995 *(exact date cannot be reconstructed / genaues Datum nicht rekonstruierbar)* |
| **First release / Erste Veröffentlichung** | October–November 1996 / Oktober–November 1996 *(genaues Datum unbekannt / exact date unknown)* |
| **Latest version / Aktuelle Version** | v40.6 (2008-09-09); package HighGFX'n'more v1.0 (2020-09-20) |
| **Platform / Plattform** | Amiga ECS/AGA |
| **Type / Art** | Software |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Aminet (driver/moni) |
| **License / Lizenz** | Closed source; the HighGFX'n'more archive may be freely distributed as long as it remains unchanged / HighGFX'n'more darf unverändert frei weitergegeben werden |
| **Related projects / Verwandte Projekte** | [SuperPlus](../superplus/) · [HD720](../hd720/) · [Xtreme](../xtreme/) |

---

## English

### Overview

HighGFX adds high-resolution display modes to Amiga systems with ECS or AGA chipsets. It provides Workbench resolutions up to 1024×768 using the native Amiga graphics hardware. No Picasso96-compatible RTG card is required.

### Background

In the mid-1990s, many Amiga users wanted larger Workbench desktops for productivity software. The standard ECS and AGA display modes were limited compared to contemporary PC systems. I developed HighGFX to make better use of the existing graphics hardware and to offer additional high-resolution modes without extra hardware. The project dates from the ECS/AGA era, before RTG solutions became widespread.

### Project History

I started HighGFX around 1995; the exact date can no longer be reconstructed. The early versions (V0.1 to V0.8, numbered 40.0) were internal releases only. The first official release, V0.9 Beta (40.1), appeared on Aminet in October or November 1996, before the article in Amiga Magazin 12/1996. It attracted many bug reports, which shaped the following versions.

I originally developed HighGFX directly on my Idek Iiyama MF-5017 multisync monitor, which could display the modes natively. Later I used a CompServ AGA FlickerFixer, which could also display HighGFX. For its time, that flicker fixer was a really impressive device. Version 40.6 was published on Aminet on 9 September 2008. It raised the AGA and ECS frequencies, fixed known bugs and included the experimental HD720 driver.

Version 40.6 was the final polish. It was prompted when Jens Schönfeld of individual Computers (icomp) considered a new flicker fixer in the A1K forum. I optimised the driver thoroughly, and Jens Schönfeld and his developer Oliver Achten also implemented HighGFX in the new device, the Indivision AGA (2008). The HAM8 test picture in the archive helped to convince them quickly of 24-bit support; the earliest considerations for the Indivision had been heading towards 12-bit colour depth.

HighGFX was the starting point for further experiments with extended native Amiga display modes. Later projects such as SuperPlus, HD720 and Xtreme continued this idea. The archive HighGFX'n'more combines all of these modes (HighGFX, HD720, SuperPlus, Xtreme) in one package; its HighGFX mode is identical to version 40.6. Version 1.0 was released on 20 September 2020 as part of the collaboration with icomp, because some of the additional modes are only supported by the new flicker fixer. It is available on Aminet and in the download area of icomp, where it serves as the complete driver package for the Indivision.

### Cooperation with icomp

The collaboration with individual Computers (icomp) was worthwhile for both sides. I received hardware samples for my development work:

- a prototype of the Indivision AGA for the Amiga 4000
- later, two samples of the Indivision ECS, for the development of SuperPlus and the dual display experiments
- later still, a version of the Indivision AGA MK2, for Xtreme

Support for the HighGFX'n'more modes in the Indivision series, according to the icomp wiki and the Amiga Hardware Database:

| Model | Year | HighGFX'n'more modes supported |
|---|---|---|
| Indivision classic (external flicker fixer) | 2002 | none, not supported |
| Indivision AGA (A1200, A4000/CD32) | 2008 | HighGFX |
| Indivision ECS | 2009 | HighGFX, HD720, SuperPlus (16 colours from 4096) |
| Indivision AGA MK2 / MK2cr | 2012/2013 | HighGFX, HD720, Xtreme, SuperPlus |

Later models (Indivision ECS V2, V3, V4 and AGA MK3) are not covered here; see the icomp wiki.

### Technical Description

HighGFX adds new display modes to the Amiga graphics system by extending the available monitor and screen mode definitions. The modes make use of the native ECS/AGA graphics architecture. HighGFX works with the native display system and does not depend on Picasso96.

#### Mode geometry

Amiga display resolutions are defined by the picture geometry and the beam resolution (pixel clock). HighGFX combines both and therefore provides a large number of screen modes.

- **Horizontal resolution:** the beam can run at 35 ns (SuperHires), 70 ns (HiRes) or 140 ns (LowRes).
- **Vertical resolution:** Interlace (768 lines), NonLace (384 lines) or DblScan (192 lines).

| Resolution | Beam | Lines | Usable for Workbench |
|---|---|---|---|
| 1024×768 | 35 ns (SuperHires) | Interlace | **yes** |
| 1024×384 | 35 ns (SuperHires) | NonLace | **yes** |
| 1024×192 | 35 ns (SuperHires) | DblScan | no |
| 512×768 | 70 ns (HiRes) | Interlace | no |
| 512×384 | 70 ns (HiRes) | NonLace | no |
| 512×192 | 70 ns (HiRes) | DblScan | no |
| 256×768 | 140 ns (LowRes) | Interlace | no |
| 256×384 | 140 ns (LowRes) | NonLace | no |
| 256×192 | 140 ns (LowRes) | DblScan | no |

A mode counts as usable for the Workbench if it is at least 640×200. Only 1024×768 (interlaced) and 1024×384 (non-interlaced) meet this requirement.

#### Colour depth

- **AGA:** all modes support up to 8 bit (256 colours). HAM8 is also available, but only for graphics, not for the Workbench.
- **ECS:** the resolutions are the same, but the colour depth is the limiting factor:

| Beam | ECS colours |
|---|---|
| 35 ns | 4 colours from 64 |
| 70 ns | 16 colours from 4096 |
| 140 ns | 32 colours from 4096, or 64 colours in EHB or HAM6 |

#### Display frequencies

The frequencies below (version 40.6) are identical for Interlace and NonLace modes. In Interlace mode, two slightly offset fields are displayed. This allows the higher number of lines, but only optically, and with flicker.

| Chipset | Horizontal | Vertical |
|---|---|---|
| AGA | 22.22 kHz | 55 Hz |
| ECS | 21.81 kHz | 54 Hz |

The frequencies differ slightly between AGA and ECS because of the way the chipsets access the bus. OCS/ECS use "normal" bus access. AGA can use normal access, CAS, BURST, or CAS and BURST combined, which gives the system one, two or four times the amount of data per bus cycle. At a 35 ns pixel clock, ECS can just transfer 2 bitplanes (4 colours), while AGA can transfer four times as many, 8 bitplanes (256 colours or HAM8). To do this, AGA requires the DMA slots to be divisible by 2, whereas ECS can serve single slots.

<!-- MERKEN für SuperPlus-Seite: DMA-Slot-Verhalten (AGA: Slots durch 2 teilbar, ECS: einzelne Slots) und Bus-Zugriffsarten (normal/CAS/BURST) spielen dort eine größere Rolle. -->

### Features

- Native ECS/AGA graphics modes
- High-resolution Workbench support
- Resolutions up to 1024×768
- No additional RTG graphics card required

### Requirements

- Amiga with ECS or AGA chipset
- AmigaOS 3.0 or higher
- A multisync monitor that supports the frequencies listed above, **or** a flicker fixer

Flicker fixers are an ideal match for HighGFX:

- CompServ AGA FlickerFixer
- Indivision AGA series
- Indivision ECS series

Multisync monitors known to be suitable (examples):

| Manufacturer | Models |
|---|---|
| Aydin | Ranger 5015LP, Ranger 5021 |
| Commodore | 1950, 1960, 21" FST |
| Eizo | 8060H |
| Idek Iiyama | MF-5017, MF-5021 |
| Microvitec | M1438, M1538, M1764 (Amiga versions) |
| NEC | Multisync 3D |
| Nokia | 417TV |
| Sony | CPD-1402E, GVM-1310, GVM-2020 |

All other monitors that support 22 kHz modes also work.

### Installation and Usage

1. Copy the HighGFX driver from the archive to `sys:devs/monitors`.
2. Reboot the system.

#### Archive contents (version 40.6)

- HighGFX driver
- HD720, a new experimental driver for a 16:9 "wide" mode with 1280×720
- The HighGFX test picture in HAM8
- Alternative icons for Workbench 3.1, 3.9 and MagicWB

#### HighGFX'n'more (v1.0, 2020-09-20)

A package with additional screen modes for classic AmigaOS (V3.0 or higher). Requirements: ECS or AGA chipset, and a display or flicker fixer that can handle the screen mode frequencies. To use it, copy your favourite screen modes to `sys:devs/monitors/` and reboot.

| Mode | Up to | Version | Date |
|---|---|---|---|
| HighGFX | 1024×768 | 40.6 | 2008-09-09 |
| HD720 | 1280×720 | 40.3 | 2008-09-09 |
| SuperPlus | 800×600 | 40.5 | 2012-01-26 |
| Xtreme | 1280×1024 | 40.5 | 2012-04-24 |

### Known Limitations

Usability depends on the Amiga model, graphics chipset, memory configuration and monitor compatibility.

### Version History

Source: change log of the original HighGFX archive and the Aminet readme.

| Version | Date | Notes |
|---------|------|-------|
| 40.0 (V0.1–V0.8) | ca. 1995–1996 | Internal releases only |
| 40.1 (V0.9 Beta) | 1996-10/11 | First official release (Aminet); 45 Hz / 18 kHz; many bug reports |
| 40.2 (Demo) | unknown | Aminet; 50 Hz / 20 kHz, equal to PAL (50 frames); removed the animation and the ChipMem limitation (the main source of bug reports); works 100% with M1438 monitors (Microvitec or AT types) |
| 40.3 | unknown | Internal release; 50 Hz / 20 kHz; corrected overscan values, no more crashes with too high settings |
| 40.4 | unknown | Aminet; 52 Hz / 21 kHz; archive split into driver (with installation), testgfx (1024×768 HAM8 demo screen), xen icons (MWB icons for 1024×384), patterns (background patterns for MWB and HighGFX) and screenshots |
| 40.5 | unknown | Aminet; 54 Hz / 22 kHz (AGA: 22.24 kHz per the 40.6 readme; ECS: 50 Hz / 20.25 kHz); VGAOnly bug removed |
| 40.6 | 2008-09-09 | Higher AGA frequencies (55 Hz / 22.22 kHz) and ECS frequencies (54 Hz / 21.81 kHz), bug fixes; HD720 included as experimental driver; final polish, also implemented in the new icomp flicker fixer |
| HighGFX'n'more 1.0 | 2020-09-20 | Combined archive with HighGFX 40.6, HD720 40.3, SuperPlus 40.5 and Xtreme 40.5 (see above) |

---

## Deutsch

### Übersicht

HighGFX fügt Amiga-Systemen mit ECS- oder AGA-Chipsatz hochauflösende Bildschirmmodi hinzu. Es ermöglicht Workbench-Auflösungen bis 1024×768 mit der nativen Amiga-Grafikhardware. Eine Picasso96-kompatible RTG-Karte ist nicht nötig.

### Hintergrund

Mitte der 1990er Jahre wünschten sich viele Amiga-Anwender größere Workbench-Arbeitsflächen für Anwendungen. Die damaligen ECS- und AGA-Modi waren gegenüber zeitgenössischen PCs eingeschränkt. Ich entwickelte HighGFX, um die vorhandene Grafikhardware besser auszunutzen und zusätzliche hochauflösende Modi ohne weitere Hardware anzubieten. Das Projekt entstand in der Zeit der nativen ECS/AGA-Grafik, bevor RTG-Systeme weit verbreitet waren.

### Projektgeschichte

Mit HighGFX habe ich etwa 1995 begonnen; das genaue Datum lässt sich nicht mehr rekonstruieren. Die frühen Versionen (V0.1 bis V0.8, nummeriert als 40.0) waren reine interne Versionen. Die erste offizielle Veröffentlichung, V0.9 Beta (40.1), erschien im Oktober oder November 1996 auf Aminet, noch vor dem Artikel im Amiga Magazin 12/1996. Sie löste viele Fehlerberichte aus, die die folgenden Versionen prägten.

Ursprünglich habe ich HighGFX direkt auf meinem Idek Iiyama MF-5017 Multisync entwickelt, der die Modi nativ darstellen konnte. Später nutzte ich einen CompServ AGA FlickerFixer, der HighGFX ebenfalls darstellen konnte. Für seine Zeit war dieser FlickerFixer ein richtig beeindruckendes Gerät. Am 9. September 2008 erschien auf Aminet die Version 40.6. Sie erhöhte die AGA- und ECS-Frequenzen, behob bekannte Fehler und enthielt den experimentellen Treiber HD720.

Version 40.6 war der letzte Feinschliff. Anlass war, dass Jens Schönfeld von individual Computers (icomp) im A1K-Forum über einen neuen FlickerFixer nachdachte. Ich habe den Treiber gründlich durchoptimiert, und Jens Schönfeld und sein Entwickler Oliver Achten haben HighGFX in das neue Gerät, den Indivision AGA (2008), mit implementiert. Das HAM8-Testbild im Archiv half, die beiden schnell vom 24-Bit-Support zu überzeugen; die allerersten Überlegungen für den Indivision gingen in Richtung 12 Bit Farbtiefe.

HighGFX war der Ausgangspunkt für weitere Experimente mit erweiterten nativen Amiga-Grafikmodi. Spätere Projekte wie SuperPlus, HD720 und Xtreme führten diese Idee fort. Das Archiv HighGFX'n'more fasst alle diese Modi (HighGFX, HD720, SuperPlus, Xtreme) in einem Paket zusammen; sein HighGFX-Modus ist mit Version 40.6 identisch. Version 1.0 erschien am 20. September 2020 im Rahmen der Zusammenarbeit mit icomp, weil einige der zusätzlichen Modi nur vom neuen FlickerFixer unterstützt werden. Es liegt auf Aminet und im Downloadbereich von icomp, wo es als Gesamtarchiv (Treiberpaket) für den Indivision dient.

### Zusammenarbeit mit icomp

Die Zusammenarbeit mit individual Computers (icomp) lohnte sich für beide Seiten. Für meine Entwicklungsarbeit erhielt ich Hardwaremuster:

- einen Prototyp des Indivision AGA für den Amiga 4000
- später zwei Muster des Indivision ECS, für die Entwicklung von SuperPlus und die Dual-Display-Experimente
- noch später eine Version des Indivision AGA MK2, für Xtreme

Unterstützung der HighGFX'n'more-Modi in der Indivision-Serie, laut icomp-Wiki und Amiga Hardware Database:

| Modell | Jahr | Unterstützte HighGFX'n'more-Modi |
|---|---|---|
| Indivision classic (externer FlickerFixer) | 2002 | keine, nicht unterstützt |
| Indivision AGA (A1200, A4000/CD32) | 2008 | HighGFX |
| Indivision ECS | 2009 | HighGFX, HD720, SuperPlus (16 Farben aus 4096) |
| Indivision AGA MK2 / MK2cr | 2012/2013 | HighGFX, HD720, Xtreme, SuperPlus |

Spätere Modelle (Indivision ECS V2, V3, V4 und AGA MK3) werden hier nicht behandelt; siehe icomp-Wiki.

### Technische Beschreibung

HighGFX erweitert die verfügbaren Amiga-Bildschirmmodi durch zusätzliche Monitor- und Screenmode-Definitionen. Die Modi nutzen die native ECS/AGA-Grafikarchitektur. HighGFX arbeitet mit der nativen Grafikausgabe und benötigt kein Picasso96.

#### Modegeometrie

Die Amiga-Grafikauflösungen ergeben sich aus der Bildgeometrie und der Beam-Auflösung (Pixeltakt). HighGFX kombiniert beides und stellt dadurch eine große Zahl von Screenmodes bereit.

- **Horizontale Auflösung:** Der Beam kann mit 35 ns (SuperHires), 70 ns (HiRes) oder 140 ns (LowRes) arbeiten.
- **Vertikale Auflösung:** Interlace (768 Zeilen), NonLace (384 Zeilen) oder DblScan (192 Zeilen).

| Auflösung | Beam | Zeilen | Für die Workbench nutzbar |
|---|---|---|---|
| 1024×768 | 35 ns (SuperHires) | Interlace | **ja** |
| 1024×384 | 35 ns (SuperHires) | NonLace | **ja** |
| 1024×192 | 35 ns (SuperHires) | DblScan | nein |
| 512×768 | 70 ns (HiRes) | Interlace | nein |
| 512×384 | 70 ns (HiRes) | NonLace | nein |
| 512×192 | 70 ns (HiRes) | DblScan | nein |
| 256×768 | 140 ns (LowRes) | Interlace | nein |
| 256×384 | 140 ns (LowRes) | NonLace | nein |
| 256×192 | 140 ns (LowRes) | DblScan | nein |

Als für die Workbench brauchbar gilt ein Modus ab 640×200. Nur 1024×768 (Interlace) und 1024×384 (NonLace) erfüllen diese Bedingung.

#### Farbtiefe

- **AGA:** Alle Modi unterstützen bis zu 8 Bit (256 Farben). Zusätzlich ist HAM8 verfügbar, allerdings nur für Grafik, nicht für die Workbench.
- **ECS:** Die Auflösungen sind dieselben, die Einschränkung liegt in der Farbtiefe:

| Beam | ECS-Farben |
|---|---|
| 35 ns | 4 Farben aus 64 |
| 70 ns | 16 Farben aus 4096 |
| 140 ns | 32 Farben aus 4096 oder 64 Farben in EHB bzw. HAM6 |

#### Bildfrequenzen

Die folgenden Frequenzen (Version 40.6) sind bei Interlace- und NonLace-Modi identisch. Im Interlace-Modus werden zwei leicht versetzte Halbbilder dargestellt. Das ermöglicht die höhere Zeilenzahl, aber nur optisch und flackernd.

| Chipsatz | Horizontal | Vertikal |
|---|---|---|
| AGA | 22,22 kHz | 55 Hz |
| ECS | 21,81 kHz | 54 Hz |

Die Frequenzen unterscheiden sich zwischen AGA und ECS geringfügig, weil die Chipsätze unterschiedlich auf den Bus zugreifen. OCS/ECS arbeiten mit „normalem“ Buszugriff. AGA kann normal, mit CAS, mit BURST oder mit CAS und BURST gemeinsam zugreifen. Dadurch erhält das System die einfache, doppelte oder vierfache Datenmenge pro Buszugriff. Bei einem Pixeltakt von 35 ns kann ECS gerade 2 Bitplanes übertragen (4 Farben), AGA dagegen das Vierfache, also 8 Bitplanes (256 Farben oder HAM8). Dafür müssen bei AGA die DMA-Slots durch 2 teilbar sein, während ECS einzelne Slots bedienen kann.

### Funktionen

- Native ECS/AGA-Grafikmodi
- Hochauflösende Workbench-Darstellung
- Auflösungen bis 1024×768
- Kein zusätzlicher RTG-Grafikadapter erforderlich

### Voraussetzungen

- Amiga mit ECS- oder AGA-Chipsatz
- AmigaOS 3.0 oder höher
- Ein Multisync-Monitor, der die oben genannten Frequenzen unterstützt, **oder** ein Flicker-Fixer

Flicker-Fixer sind für HighGFX ideal:

- CompServ AGA FlickerFixer
- Indivision-AGA-Serie
- Indivision-ECS-Serie

Multisync-Monitore, die sich eignen (Beispiele):

| Hersteller | Modelle |
|---|---|
| Aydin | Ranger 5015LP, Ranger 5021 |
| Commodore | 1950, 1960, 21" FST |
| Eizo | 8060H |
| Idek Iiyama | MF-5017, MF-5021 |
| Microvitec | M1438, M1538, M1764 (Amiga-Versionen) |
| NEC | Multisync 3D |
| Nokia | 417TV |
| Sony | CPD-1402E, GVM-1310, GVM-2020 |

Alle anderen Monitore, die 22-kHz-Modi unterstützen.

### Installation und Verwendung

1. Den HighGFX-Treiber aus dem Archiv nach `sys:devs/monitors` kopieren.
2. Den Rechner neu starten.

Um die horizontale Größe des Bildschirmmodus zu verkleinern, wird dem HighGFX-Icon der Tooltype `TOTCLKS=0xB0` hinzugefügt. Nebenwirkung ist eine niedrigere Bildwiederholrate (50 Hz, 20,25 kHz). Die Monitoreinstellungen lassen sich auch mit MonSpecsMUI anpassen (siehe Hinweise).

#### Archivinhalt (Version 40.6)

- HighGFX-Treiber
- HD720, ein neuer experimenteller Treiber für einen 16:9-Breitbildmodus mit 1280×720
- Das HighGFX-Testbild in HAM8
- Alternative Icons für Workbench 3.1, 3.9 und MagicWB

#### HighGFX'n'more (v1.0, 2020-09-20)

Ein Paket mit zusätzlichen Bildschirmmodi für das klassische AmigaOS (ab V3.0). Voraussetzungen: ECS- oder AGA-Chipsatz sowie ein Monitor oder FlickerFixer, der die Frequenzen der Modi verarbeiten kann. Zur Verwendung die gewünschten Modi nach `sys:devs/monitors/` kopieren und neu starten.

| Modus | Bis zu | Version | Datum | 
|---|---|---|---|
| HighGFX | 1024×768 | 40.6 | 2008-09-09 |
| HD720 | 1280×720 | 40.3 | 2008-09-09 |
| SuperPlus | 800×600 | 40.5 | 2012-01-26 |
| Xtreme | 1280×1024 | 40.5 | 2012-04-24 |

### Bekannte Einschränkungen

Die Nutzbarkeit hängt von Amiga-Modell, Grafikchip, Speicheraufbau und Monitor-Kompatibilität ab.

### Versionsgeschichte

Quelle: Änderungsverlauf im ursprünglichen HighGFX-Archiv und Aminet-Readme.

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| 40.0 (V0.1–V0.8) | ca. 1995–1996 | Nur interne Versionen |
| 40.1 (V0.9 Beta) | 1996-10/11 | Erste offizielle Veröffentlichung (Aminet); 45 Hz / 18 kHz; viele Fehlerberichte |
| 40.2 (Demo) | unbekannt | Aminet; 50 Hz / 20 kHz, entspricht PAL (50 Bilder); Animation und ChipMem-Begrenzung entfernt (Hauptursache der Fehlerberichte); läuft zu 100 % mit M1438-Monitoren (Microvitec oder AT-Typen) |
| 40.3 | unbekannt | Interne Version; 50 Hz / 20 kHz; Overscan-Werte korrigiert, keine Abstürze mehr bei zu hohen Einstellungen |
| 40.4 | unbekannt | Aminet; 52 Hz / 21 kHz; Archiv in Teile aufgeteilt: Treiber (mit Installation), testgfx (Demo-Bild 1024×768 HAM8), xen-icons (MWB-Icons für 1024×384), patterns (Hintergrundmuster für MWB und HighGFX) und Screenshots |
| 40.5 | unbekannt | Aminet; 54 Hz / 22 kHz (AGA: 22,24 kHz laut Readme von 40.6; ECS: 50 Hz / 20,25 kHz); VGAOnly-Fehler behoben |
| 40.6 | 2008-09-09 | Höhere AGA-Frequenzen (55 Hz / 22,22 kHz) und ECS-Frequenzen (54 Hz / 21,81 kHz), Fehlerkorrekturen; HD720 als experimenteller Treiber enthalten; letzter Feinschliff, auch im neuen icomp-FlickerFixer implementiert |
| HighGFX'n'more 1.0 | 2020-09-20 | Gesamtarchiv mit HighGFX 40.6, HD720 40.3, SuperPlus 40.5 und Xtreme 40.5 (siehe oben) |

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| [HighGFX 40.6](https://aminet.net/package/driver/moni/HighGFX40_6) | 40.6 | 2008-09-09 | Aminet (driver/moni) |
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 | 2020-09-20 | Aminet and icomp download area; combined archive with HighGFX, HD720, SuperPlus and Xtreme (driver package for the Indivision) |

---

## References / Quellen

- Amiga Magazin 12/1996, article "Workbench-Tool HighGFX", page 30 (printed page number and PDF page number are identical; scanned magazine pages): [Amiga Magazin 1996-12.pdf](http://www.homecomputerworld.at/magazine/amiga/Amiga%20Magazin%201996-12.pdf), Home Computer World
- Aminet, HighGFX 40.6 (including readme): <https://aminet.net/package/driver/moni/HighGFX40_6>
- Aminet, HighGFX'n'more: <https://aminet.net/package/driver/moni/HighGFXnmore>
- Aminet, MonSpecsMUI: <https://aminet.net/package/util/misc/MonSpecsMUI>
- icomp wiki, Indivision: <https://wiki.icomp.de/wiki/Indivision>
- Amiga Hardware Database, Indivision: <https://amiga.resource.cx/search.pl?product=indivision>

---

## Notes / Hinweise

**EN:** HighGFX is closed source. At some point I received the monitor source code of the original Commodore Amiga operating system from Amiga Technologies under a non-disclosure agreement (NDA), so the source code of HighGFX cannot be published.

**DE:** HighGFX ist Closed Source. Ich habe irgendwann die Monitor-Quellcodes des originalen Commodore-Amiga-Betriebssystems von Amiga Technologies unter einer Geheimhaltungsvereinbarung (NDA) erhalten, deshalb kann der Quellcode von HighGFX nicht veröffentlicht werden.

**Related software / Zusatzsoftware**

**EN:** MonSpecsMUI by Thomas Krafzik (freeware, 1995–1997, version 40.375 of 7 February 1997; Aminet: util/misc/MonSpecsMUI) is a MUI-based monitor specification editor in the style of MonED. It lets the user change blank and sync timing, TotClk/TotRow, overscan, BeamCon0 flags and mode properties, and save them in the icons of the monitor files. The included MIPrefs applies the saved settings at startup. According to its guide, a monitor with the ID PROTO_MONITOR_ID (0x51000) is displayed as "HighGFX", and the author sends greetings to me. HighGFX is compatible with MonSpecsMUI, and I used the tool intensively for my own tests. The guide warns that wrong settings, especially for TotClk and TotRow, can damage a monitor.

**DE:** MonSpecsMUI von Thomas Krafzik (Freeware, 1995–1997, Version 40.375 vom 7. Februar 1997; Aminet: util/misc/MonSpecsMUI) ist ein MUI-basierter Editor für Monitorspezifikationen im Stil von MonED. Damit lassen sich Blank- und Sync-Timing, TotClk/TotRow, Overscan, BeamCon0-Flags und Modus-Eigenschaften ändern und in den Piktogrammen der Monitordateien sichern. Das enthaltene MIPrefs setzt die gesicherten Einstellungen beim Start. Laut Anleitung wird ein Monitor mit der ID PROTO_MONITOR_ID (0x51000) als „HighGFX“ angezeigt, und der Autor grüßt mich darin. HighGFX ist mit MonSpecsMUI kompatibel, und ich habe das Werkzeug für meine eigenen Tests intensiv genutzt. Die Anleitung warnt, dass falsche Einstellungen, besonders bei TotClk und TotRow, einen Monitor beschädigen können.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-04</sub>
