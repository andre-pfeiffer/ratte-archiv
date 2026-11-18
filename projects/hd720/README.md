# HD720 / A native 1280×720 widescreen mode for Amiga ECS and AGA

> **EN:** HD720 was developed as part of the continuing HighGFX project and introduced a native widescreen display mode for modern 16:9 LCD monitors while retaining compatibility with ECS and AGA Amiga systems.
>
> **DE:** HD720 entstand als Teil des fortgesetzten HighGFX-Projekts und brachte einen nativen Breitbild-Bildschirmmodus für moderne 16:9-LCD-Monitore, bei voller Kompatibilität mit Amiga-ECS- und AGA-Systemen.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2008-07 |
| **First release / Erste Veröffentlichung** | 2008-09-09 (V40.3, the final version, as part of HighGFX 40.6) |
| **Latest version / Aktuelle Version** | V40.3 (2008-09-09), the final version / die finale Version |
| **Platform / Plattform** | Amiga ECS/AGA |
| **Type / Art** | Software (screen mode driver); a spin-off of HighGFX / Ableger von HighGFX |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Only as part of [HighGFX 40.6](../highgfx/) (Aminet) and HighGFX'n'more (Aminet and icomp); there never was a package of its own |
| **License / Lizenz** | Like HighGFX: closed source, free to use / Wie HighGFX: Closed Source, frei verwendbar |
| **Related projects / Verwandte Projekte** | [HighGFX](../highgfx/) · [SuperPlus](../superplus/) · [Xtreme](../xtreme/) |

---

## English

### Overview

HD720 is a native 1280×720 screen mode for Amiga ECS and AGA systems. It is a 16:9 widescreen mode and the direct continuation of the idea of [HighGFX](../highgfx/), but with a completely different aim. It is more of an "Amiga-optimised widescreen mode": the resolution is 1280×720, but the timings are fully tuned to the Amiga.

I do not treat HD720 as a project of its own. Historically, it is a spin-off of HighGFX, like Xtreme and SuperPlus later. That explains why there never was an Aminet package of its own and why the development was relatively short: HD720 was a deliberate extension of the HighGFX concept for the widescreen monitors that were emerging at that time.

### Background

HighGFX was created in a time when practically all monitors were 4:3. From around 2007/2008, that changed: 16:9 and 16:10 TFT displays came onto the market everywhere. The existing HighGFX modes still worked, but they made poor use of these displays.

At the same time, I was in contact with Jens Schönfeld (individual Computers) about HighGFX and the Indivision AGA. The Indivision allowed much higher pixel clocks and much freer timings. That gave me the idea to develop, for the first time, a real native 1280×720 mode for ECS and AGA. The project start in July 2008 fits exactly this phase of development.

### Project History

| Date | Event |
|---|---|
| 2008-07 | Project start. Several internal test versions followed, until the best frequencies were found |
| 2008-09-09 | V40.3, the final version, announced as the "perfect mode for modern 16:9 displays", as part of the HighGFX 40.6 archive |
| 2020-09-20 | Part of the package HighGFX'n'more 1.0 |

HD720 was presented, and its development documented, in the A1K forum thread of HighGFX. Later, the development flowed into further graphics modes.

The mode is called **experimental** in the archive for a simple reason: I did not own a 16:9 monitor and could not test it myself.

### Technical Description

The aim was a 16:9 mode. The mode works with approximately:

- horizontal frequency **17.86 kHz**
- vertical frequency about **47 Hz**

It was designed to offer as much visible working area as possible and still run stably on as many TFTs as possible. It works with both AGA and ECS. The focus is clearly on the **Workbench** (1280×720 or 1280×360), not on games.

**Modes and colours.** The colour depth corresponds to the other modes:

| Width | Beam | ECS | AGA |
|---|---|---|---|
| 1280 | 35 ns | 4 colours from 64 | 256 colours or HAM8 |
| 640 | 70 ns | 16 colours from 4096 | 256 colours or HAM8 |
| 320 | 140 ns | 32 colours, EHB or HAM6 | 256 colours or HAM8 |

The heights are 720 lines (Interlace), 360 lines (NonLace) and the half again (DblScan).

### Features

- Native 1280×720 widescreen mode for ECS and AGA
- Fully tuned to the Amiga, with stable timings
- Made for the Workbench, with as much working area as possible
- Compatible with ECS and AGA

### Requirements

- Amiga with ECS or AGA chipset
- A display or flicker fixer that can handle the frequencies (about 17.86 kHz, 47 Hz)
- HighGFX 40.6 or HighGFX'n'more (copy the mode to `sys:devs/monitors/` and reboot)

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Test versions | 2008-07 to 2008-09 | Internal; the best frequencies were determined |
| V40.3 | 2008-09-09 | The final version. "Perfect mode for modern 16:9 displays"; included in HighGFX 40.6 as a new experimental driver |

### Gallery / Galerie

<!-- TODO: Fotos und Screenshots nachreichen (Ablage in images/): Workbench in 1280×720, Monitor-OSD mit 1280×720, Vergleich 1024×768 und 1280×720, Overscan-Einstellungen, Screenshot von HighGFX'n'more. -->

### Downloads

HD720 has no package of its own. It is included in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX 40.6](https://aminet.net/package/driver/moni/HighGFX40_6) | 40.6 (2008-09-09) | Aminet |
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet and icomp download area |

### References / Quellen

- A1K forum, presentation and development of HD720: 

<https://www.a1k.org/forum/index.php?threads/3356/page-33#post-185425>

- Aminet, HighGFX 40.6 (with HD720): 

<https://aminet.net/package/driver/moni/HighGFX40_6>

---

## Deutsch

### Übersicht

HD720 ist ein nativer 1280×720-Bildschirmmodus für Amiga-ECS- und AGA-Systeme. Es ist ein 16:9-Breitbildmodus und die direkte Fortsetzung der Idee von [HighGFX](../highgfx/), aber mit einem völlig anderen Ziel. Es ist eher ein „Amiga-optimierter Widescreen-Modus“: Die Auflösung ist 1280×720, die Timings sind aber vollständig auf den Amiga abgestimmt.

Ich behandle HD720 nicht als völlig eigenständiges Projekt. Historisch ist es ein Spin-off von HighGFX, ähnlich wie später Xtreme und SuperPlus. Das erklärt, warum es nie ein eigenes Aminet-Paket gab und weshalb die Entwicklung relativ kurz war: HD720 war eine gezielte Erweiterung des HighGFX-Konzepts für die damals aufkommenden Breitbildmonitore.

### Hintergrund

HighGFX entstand in einer Zeit, als praktisch alle Monitore noch 4:3 waren. Ab etwa 2007/2008 änderte sich das: Überall kamen 16:9- und 16:10-TFTs auf den Markt. Die bisherigen HighGFX-Modi funktionierten weiterhin, nutzten diese Displays aber schlecht aus.

Zeitgleich hatte ich Kontakt zu Jens Schönfeld (individual Computers) wegen HighGFX und dem Indivision AGA. Mit dem Indivision wurden sehr viel höhere Pixeltakte und wesentlich freiere Timings möglich. Dadurch entstand die Idee, erstmals einen echten nativen 1280×720-Modus für ECS und AGA zu entwickeln. Der Projektbeginn im Juli 2008 passt genau zu dieser Entwicklungsphase.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2008-07 | Projektbeginn. Es folgten mehrere interne Testversionen, bis die besten Frequenzen feststanden |
| 2008-09-09 | V40.3, die finale Version, angekündigt als „perfect mode for modern 16:9 displays“, als Teil des Archivs HighGFX 40.6 |
| 2020-09-20 | Teil des Pakets HighGFX'n'more 1.0 |

HD720 wurde im A1K-Forenthread zu HighGFX vorgestellt und seine Entwicklung dort dokumentiert. Später floss die Entwicklung in weitere Grafikmodi ein.

Der Modus heißt im Archiv **experimentell**, aus einem einfachen Grund: Ich besaß keinen 16:9-Monitor und konnte ihn selbst nicht prüfen.

### Technische Beschreibung

Das Ziel war ein 16:9-Modus. Der Modus arbeitet mit ungefähr:

- Horizontalfrequenz **17,86 kHz**
- Vertikalfrequenz ca. **47 Hz**

Er war darauf ausgelegt, möglichst viel sichtbare Arbeitsfläche zu bieten und trotzdem auf möglichst vielen TFTs stabil zu laufen. Er funktioniert sowohl mit AGA als auch mit ECS. Der Schwerpunkt liegt eindeutig auf der **Workbench** (1280×720 oder 1280×360), nicht auf Spielen.

**Modi und Farben.** Die Farbtiefe entspricht den übrigen Modi:

| Breite | Beam | ECS | AGA |
|---|---|---|---|
| 1280 | 35 ns | 4 Farben aus 64 | 256 Farben oder HAM8 |
| 640 | 70 ns | 16 Farben aus 4096 | 256 Farben oder HAM8 |
| 320 | 140 ns | 32 Farben, EHB oder HAM6 | 256 Farben oder HAM8 |

Die Höhen sind 720 Zeilen (Interlace), 360 Zeilen (NonLace) und noch einmal die Hälfte (DblScan).

### Funktionen

- Nativer 1280×720-Breitbildmodus für ECS und AGA
- Vollständig auf den Amiga abgestimmt, mit stabilen Timings
- Für die Workbench gemacht, mit möglichst viel Arbeitsfläche
- Kompatibel mit ECS und AGA

### Voraussetzungen

- Amiga mit ECS- oder AGA-Chipsatz
- Ein Monitor oder FlickerFixer, der die Frequenzen verarbeiten kann (etwa 17,86 kHz, 47 Hz)
- HighGFX 40.6 oder HighGFX'n'more (den Modus nach `sys:devs/monitors/` kopieren und neu starten)

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Testversionen | 2008-07 bis 2008-09 | Intern; die besten Frequenzen wurden ermittelt |
| V40.3 | 2008-09-09 | Die finale Version. „Perfekter Modus für moderne 16:9-Displays“; in HighGFX 40.6 als neuer experimenteller Treiber enthalten |

### Downloads

HD720 hat kein eigenes Paket. Es ist enthalten in:

| File / Datei | Version | Source / Quelle |
|---|---|---|
| [HighGFX 40.6](https://aminet.net/package/driver/moni/HighGFX40_6) | 40.6 (2008-09-09) | Aminet |
| [HighGFX'n'more](https://aminet.net/package/driver/moni/HighGFXnmore) | 1.0 (2020-09-20) | Aminet und icomp-Downloadbereich |

### Quellen

- A1K-Forum, Vorstellung und Entwicklung von HD720: 

<https://www.a1k.org/forum/index.php?threads/3356/page-33#post-185425>

- Aminet, HighGFX 40.6 (mit HD720): 

<https://aminet.net/package/driver/moni/HighGFX40_6>

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-18</sub>
