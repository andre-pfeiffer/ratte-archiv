# independent.library / A 15-bit chunky-to-planar graphics subsystem for the Amiga

> **EN:** independent.library is a small experimental graphics subsystem from 1998. It keeps the picture in one common 15-bit chunky buffer (320 × 240 pixels) and shows it on whatever graphics hardware is available: CyberGraphX (RTG) or the native AGA chipset.
>
> **DE:** independent.library ist ein kleines experimentelles Grafiksubsystem von 1998. Es hält das Bild in einem gemeinsamen 15-Bit-Chunky-Puffer (320 × 240 Pixel) und zeigt es auf der jeweils vorhandenen Grafikhardware an: CyberGraphX (RTG) oder dem nativen AGA-Chipsatz.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 1998-01 |
| **First release / Erste Veröffentlichung** | 2005-12 (source code shared in the A1K forum); archive made available again 2009-01 |
| **Latest version / Aktuelle Version** | Historical beta release (the code dates from 1998) / Historische Beta-Version (Code von 1998) |
| **Platform / Plattform** | Amiga AGA and RTG (CyberGraphX), AmigaOS |
| **Type / Art** | Software (graphics library, with assembler routines) / Software (Grafikbibliothek, mit Assembler-Routinen) |
| **Status** | Historical beta project; no plans to resume, but not considered permanently closed / Historisches Beta-Projekt; keine konkreten Pläne zur Fortsetzung, aber nicht endgültig abgeschlossen |
| **Distribution / Verbreitung** | A1K forum (archive with source code, include files and demos) |
| **License / Lizenz** | Free: may be inspected, used, modified and redistributed; no formal open-source license / Frei: darf eingesehen, genutzt, verändert und weitergegeben werden; keine formale Open-Source-Lizenz |
| **Related projects / Verwandte Projekte** | none |

---

## English

### Overview

`independent.library` provides a simple and consistent way of putting graphics on the screen without dealing with the differences between the various Amiga graphics systems. The basic idea:

**Store graphics in a common chunky pixel format and let the library take care of displaying them on the available graphics hardware.**

The library keeps an internal 15-bit RGB image buffer of 320 × 240 pixels. Depending on the hardware, it selects an output method: 15-bit or 8-bit output through CyberGraphX, or 8-bit output on AGA in a Multiscan or a PAL display mode. Where the hardware has no 15-bit output, the library converts the colours and, where needed, converts chunky data to planar.

### Why it was made

The motivation was quite practical. During my early programming experiments, I kept wishing for a simple way to put something on the screen without first dealing with the details of the underlying graphics system. Sometimes I just wanted to draw a few pixels, try an idea, or make a quick graphical experiment.

It was planned as a personal tool for my own experiments, not as a general-purpose graphics framework or a commercial development product. The goal was one simple graphics interface that works on as many Amiga configurations as possible: ideally, an application would not need to know whether the machine has an RTG card or only the native AGA chipset. Backward compatibility was an important design goal from the beginning.

### Background

At that time, the Amiga offered several graphics configurations. RTG graphics cards provided higher colour depths and chunky pixel formats, while the native AGA chipset still used a planar representation. Hiding these differences behind one common internal image representation was an interesting technical challenge.

My main development machine was an Amiga 4000, first with a CyberVision 64/3D graphics card, and later with a CyberVision 64. The latter caused some problems with the graphics output; some of them, such as display errors and flickering on older CyberVision 64 configurations, are mentioned in the comments of the source code.

### Project History

| Date | Event |
|---|---|
| 1998-01 | Development starts |
| 1998 | Together with a friend and A1K forum member, Scrat, I develop several small test programs: animations, simple graphical objects and partially interactive controls. Most of them worked as intended |
| later | Development comes to a halt. It was not one single technical problem: everyday life took over, with other interests, a job, private commitments and less time for programming |
| 2005-12 | I start sharing older programming experiments in the A1K forum, including the source code, so that others can see my earlier work. `independent.library` is one of them |
| 2009-01 | After renewed interest and several requests for updated download links, the archive is made available again. The code had been untouched for about ten years. The published version is explicitly a beta release |

### Technical Description

**The internal image.** The central element is a chunky image buffer with a fixed size:

| Property | Value |
|---|---:|
| Width | 320 pixels |
| Height | 240 pixels |
| Colour depth | 15 bit |
| Colours | 32,768 |
| Pixel storage | 16 bit (one WORD) |
| Format | RGB555 |

320 × 240 pixels was a common and practical size for Amiga games and demos at that time. The 15-bit format was a compromise between a reasonably large number of colours, low memory consumption and fast, straightforward pixel processing. Each pixel occupies one WORD, of which 15 bits carry colour information. That suits the 16-bit data types of the Amiga.

**Chunky pixels.** Unlike the planar representation of the native chipset, each WORD is one complete pixel. Reading and writing a pixel means calculating its position in the buffer and accessing one WORD, without manipulating bitplanes. The library converts the image into the format of the output hardware.

**Double buffering.** The output screen has a virtual height of 580 pixels. This provides two image areas of 320 × 240 pixels, with spacing between them. While one image is displayed, the next is prepared in the other. Then the visible area is switched. This reduces flickering and avoids showing partially updated frames.

**Output paths.** The library detects the available graphics system and selects the first suitable path:

1. CyberGraphX with 15-bit output: the RGB555 data is copied directly to the graphics bitmap.
2. CyberGraphX with 8-bit output: the 15-bit data is converted to 8-bit colour indices with a lookup table, then copied to the RTG bitmap.
3. AGA in a Multiscan mode with 8 bit: the data is converted to 8 bit and then to planar data.
4. AGA in a PAL mode with 8 bit: a fallback for systems without a suitable 31 kHz display mode.

The application does not select these modes itself.

**Colour conversion.** The conversion from 15 bit to 8 bit uses a lookup table named `converter` in the source code, and it runs in real time during the screen refresh. The AGA palette has 216 distinct colours forming a regular 6 × 6 × 6 colour cube, with the levels 0, 51, 102, 153, 204 and 255 per channel. The remaining 40 palette entries are black. This was a straightforward choice for the experiments, though it does not give the best perceived colour distribution for every picture.

**Chunky-to-planar.** The native chipset needs planar data: each bitplane stores one bit of every pixel. The library contains an assembler routine that rearranges the 8-bit chunky data with bit masks and shift operations. According to the source comments, it is optimised for the 68020 and Fast RAM, with a target of under 90 ms for a 320 × 200 × 256 conversion on a 14 MHz 68020. This is a development target from the comments, not a verified benchmark. The routine assumes a fixed screen size and a specific memory layout, so it is a specialised implementation and not a general conversion library.

**The programming interface.**

| Function | Purpose |
|---|---|
| `InitSystem` | Initialises the subsystem and selects an available output mode |
| `CloseSystem` | Shuts the subsystem down and releases resources |
| `RefreshScreen` | Updates the visible screen from the internal image buffer |
| `SetCustomScreen` | Uses an image buffer supplied by the application |
| `SetSystemScreen` | Restores the library's own image buffer |
| `GetColor` | Reads the colour value of a pixel |
| `SetColor` | Sets the current drawing colour |
| `DrawPoint` | Draws a pixel with the current colour (with bounds checks) |
| `DrawDirect` | Writes a pixel directly into the image buffer (without bounds checks) |

The source also contains one function, `Funktion`, which is marked as a test function. Applications using `DrawDirect` must take care not to write outside the buffer.

### Demonstration programs

The archive contains demos in addition to the source code and the include files. The demo mentioned in the A1K forum discussion loads three raw 15-bit images and shows them one after another until the left mouse button is pressed. It uses `SetCustomScreen` and `RefreshScreen`, and it contains the library directly instead of needing an installed shared library. The experiments with Scrat went further, with animations, graphical objects and partly interactive controls.

### An idea that was never implemented

I considered simple BOB-like objects: movable objects like sprites or traditional blitter objects, but drawn in software. The unused 16th bit of each pixel WORD was meant as a transparency flag. It remained an idea and was never part of the released version.

### Features

- One simple interface for RTG and native AGA graphics
- 15-bit RGB buffer with 32,768 colours, 320 × 240 pixels
- Automatic selection of the best output mode
- Double buffering
- Demo programs and complete source code

### Requirements

- AmigaOS with an AGA chipset or a CyberGraphX graphics card
- A processor and memory in the range the routines were written for (68020, Fast RAM)

### Known Limitations

The comments in the source code describe problems at the time of development: display errors on older CyberVision 64 cards with 2 MB of graphics memory, flickering or wrongly displayed areas in some configurations, problems on DraCo systems with CyberGraphX, performance limits, the fixed 320 × 240 size and the assumptions about the planar memory layout. Some CyberGraphX modes use BGR instead of RGB ordering for the 15-bit format, so the demo uses 8-bit output. These comments are not a complete compatibility assessment of every Amiga configuration.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Development | 1998-01 | Library, include files, demos, test programs with Scrat |
| Beta release | 2005-12 | Shared in the A1K forum |
| Archive again | 2009-01 | After renewed interest; the code was about ten years old |

### Gallery / Galerie

<!-- TODO: Screenshots der Demos (Beitrag vom 2009-01) und der Experimente mit Scrat nachreichen (Ablage in images/). -->

### Downloads

| File / Datei | Contents | Source / Quelle |
|---|---|---|
| *to be added / wird ergänzt* | Library source code, include files, demonstration programs | A1K forum |

### References / Quellen

- A1K forum: sharing of older experiments (2005-12) and re-release of the archive (2009-01)

https://www.a1k.org/forum/index.php?threads/7211/



### Notes / Hinweise

`independent.library` is a historical beta project and a snapshot of an earlier period of Amiga programming. The source code is freely available and may be inspected, used, modified and redistributed. No formal open-source license has been assigned; the permission reflects my explicit intention to allow free use and further experimentation. Please keep in mind that it is an old beta release that has not been maintained for many years. It is a starting point for experiments, not a production-ready graphics library.

The project started with a simple idea: drawing a few pixels on the Amiga screen without worrying every time about the graphics hardware. It was never meant to become a large framework. Looking back, it is a snapshot of the challenges of Amiga graphics programming in the late 1990s: chunky against planar, RTG against native AGA, colour conversion, memory management and the wish to support different hardware through one simple interface.

---

## Deutsch

### Übersicht

`independent.library` bietet einen einfachen, einheitlichen Weg, Grafik auf den Bildschirm zu bringen, ohne sich mit den Unterschieden der verschiedenen Amiga-Grafiksysteme zu befassen. Die Grundidee:

**Grafik in einem gemeinsamen Chunky-Pixelformat ablegen und die Bibliothek die Darstellung auf der vorhandenen Grafikhardware übernehmen lassen.**

Die Bibliothek hält einen internen 15-Bit-RGB-Bildpuffer mit 320 × 240 Pixeln. Je nach Hardware wählt sie eine Ausgabemethode: 15-Bit- oder 8-Bit-Ausgabe über CyberGraphX oder 8-Bit-Ausgabe auf AGA in einem Multiscan- oder einem PAL-Modus. Wo die Hardware keine 15-Bit-Ausgabe hat, rechnet die Bibliothek die Farben um und wandelt, falls nötig, Chunky in Planar.

### Warum es entstand

Der Anlass war ganz praktisch. Bei meinen frühen Programmierexperimenten wünschte ich mir ständig einen einfachen Weg, etwas auf den Bildschirm zu bringen, ohne mich zuerst mit den Details des darunterliegenden Grafiksystems zu befassen. Manchmal wollte ich nur ein paar Pixel zeichnen, eine Idee ausprobieren oder ein schnelles grafisches Experiment machen.

Es war als persönliches Werkzeug für meine eigenen Experimente gedacht, nicht als allgemeines Grafik-Framework oder kommerzielles Entwicklungsprodukt. Das Ziel war eine einfache Grafikschnittstelle, die auf möglichst vielen Amiga-Konfigurationen funktioniert: Idealerweise müsste eine Anwendung nicht wissen, ob der Rechner eine RTG-Karte hat oder nur den nativen AGA-Chipsatz. Rückwärtskompatibilität war von Anfang an ein wichtiges Entwurfsziel.

### Hintergrund

Damals bot der Amiga mehrere Grafikkonfigurationen. RTG-Grafikkarten brachten höhere Farbtiefen und Chunky-Pixelformate, während der native AGA-Chipsatz weiterhin eine planare Darstellung verwendete. Diese Unterschiede hinter einer gemeinsamen internen Bilddarstellung zu verstecken, war eine interessante technische Herausforderung.

Mein wichtigster Entwicklungsrechner war ein Amiga 4000, zuerst mit einer CyberVision 64/3D, später mit einer CyberVision 64. Die letztere verursachte einige Probleme bei der Grafikausgabe; einige davon, etwa Darstellungsfehler und Flackern auf älteren CyberVision-64-Konfigurationen, sind in den Kommentaren des Quellcodes erwähnt.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 1998-01 | Die Entwicklung beginnt |
| 1998 | Zusammen mit einem Freund und A1K-Forumsmitglied, Scrat, entwickle ich mehrere kleine Testprogramme: Animationen, einfache grafische Objekte und teilweise interaktive Steuerelemente. Die meisten funktionierten wie gedacht |
| später | Die Entwicklung kommt zum Erliegen. Es war nicht ein einzelnes technisches Problem: Der Alltag übernahm, mit anderen Interessen, Beruf, privaten Verpflichtungen und weniger Zeit zum Programmieren |
| 2005-12 | Ich beginne, ältere Programmierexperimente im A1K-Forum zu teilen, samt Quellcode, damit andere meine frühere Arbeit sehen können. `independent.library` ist eines davon |
| 2009-01 | Nach erneutem Interesse und mehreren Anfragen nach aktuellen Download-Links wird das Archiv wieder verfügbar gemacht. Der Code war etwa zehn Jahre unberührt. Die veröffentlichte Version ist ausdrücklich eine Beta-Version |

### Technische Beschreibung

**Das interne Bild.** Das zentrale Element ist ein Chunky-Bildpuffer mit fester Größe:

| Eigenschaft | Wert |
|---|---:|
| Breite | 320 Pixel |
| Höhe | 240 Pixel |
| Farbtiefe | 15 Bit |
| Farben | 32.768 |
| Pixelspeicher | 16 Bit (ein WORD) |
| Format | RGB555 |

320 × 240 Pixel war damals eine übliche und praktische Größe für Amiga-Spiele und -Demos. Das 15-Bit-Format war ein Kompromiss aus einer ausreichend großen Zahl von Farben, geringem Speicherverbrauch und schneller, einfacher Pixelverarbeitung. Jedes Pixel belegt ein WORD, von dem 15 Bit Farbinformation tragen. Das passt zu den 16-Bit-Datentypen des Amiga.

**Chunky-Pixel.** Anders als bei der planaren Darstellung des nativen Chipsatzes ist jedes WORD ein vollständiges Pixel. Ein Pixel zu lesen oder zu schreiben heißt, seine Position im Puffer zu berechnen und auf ein WORD zuzugreifen, ohne Bitplanes zu bearbeiten. Die Bibliothek wandelt das Bild dann in das Format der Ausgabehardware um.

**Double Buffering.** Der Ausgabebildschirm hat eine virtuelle Höhe von 580 Pixeln. Das ergibt zwei Bildbereiche von 320 × 240 Pixeln mit Abstand dazwischen. Während ein Bild angezeigt wird, wird das nächste im anderen vorbereitet. Dann wird der sichtbare Bereich umgeschaltet. Das verringert Flackern und verhindert, dass teilweise aktualisierte Bilder gezeigt werden.

**Ausgabewege.** Die Bibliothek erkennt das vorhandene Grafiksystem und wählt den ersten passenden Weg:

1. CyberGraphX mit 15-Bit-Ausgabe: Die RGB555-Daten werden direkt in die Grafik-Bitmap kopiert.
2. CyberGraphX mit 8-Bit-Ausgabe: Die 15-Bit-Daten werden mit einer Lookup-Tabelle in 8-Bit-Farbindizes umgewandelt und dann in die RTG-Bitmap kopiert.
3. AGA in einem Multiscan-Modus mit 8 Bit: Die Daten werden in 8 Bit und dann in planare Daten umgewandelt.
4. AGA in einem PAL-Modus mit 8 Bit: ein Rückfall für Systeme ohne passenden 31-kHz-Modus.

Die Anwendung wählt diese Modi nicht selbst aus.

**Farbumwandlung.** Die Umwandlung von 15 auf 8 Bit nutzt im Quellcode eine Lookup-Tabelle namens `converter` und läuft in Echtzeit beim Bildaufbau. Die AGA-Palette hat 216 verschiedene Farben, die einen regelmäßigen 6 × 6 × 6-Farbwürfel bilden, mit den Stufen 0, 51, 102, 153, 204 und 255 je Kanal. Die übrigen 40 Paletteneinträge sind schwarz. Das war für die Experimente ein einfacher Ansatz, auch wenn er nicht bei jedem Bild die beste wahrgenommene Farbverteilung liefert.

**Chunky-to-Planar.** Der native Chipsatz braucht planare Daten: Jede Bitplane speichert ein Bit jedes Pixels. Die Bibliothek enthält eine Assembler-Routine, die die 8-Bit-Chunky-Daten mit Bitmasken und Schiebeoperationen umordnet. Laut den Kommentaren im Quellcode ist sie für den 68020 und Fast RAM optimiert, mit einem Ziel von unter 90 ms für eine Umwandlung von 320 × 200 × 256 auf einem 68020 mit 14 MHz. Das ist ein Entwicklungsziel aus den Kommentaren, kein überprüfter Benchmark. Die Routine setzt eine feste Bildschirmgröße und ein bestimmtes Speicherlayout voraus, sie ist also eine spezialisierte Implementierung und keine allgemeine Umwandlungsbibliothek.

**Die Programmierschnittstelle.**

| Funktion | Zweck |
|---|---|
| `InitSystem` | Initialisiert das Subsystem und wählt einen verfügbaren Ausgabemodus |
| `CloseSystem` | Beendet das Subsystem und gibt Ressourcen frei |
| `RefreshScreen` | Aktualisiert den sichtbaren Bildschirm aus dem internen Bildpuffer |
| `SetCustomScreen` | Verwendet einen von der Anwendung gelieferten Bildpuffer |
| `SetSystemScreen` | Stellt den eigenen Bildpuffer der Bibliothek wieder her |
| `GetColor` | Liest den Farbwert eines Pixels |
| `SetColor` | Setzt die aktuelle Zeichenfarbe |
| `DrawPoint` | Zeichnet ein Pixel mit der aktuellen Farbe (mit Grenzprüfung) |
| `DrawDirect` | Schreibt ein Pixel direkt in den Bildpuffer (ohne Grenzprüfung) |

Der Quellcode enthält außerdem eine Funktion `Funktion`, die als Testfunktion gekennzeichnet ist. Anwendungen, die `DrawDirect` verwenden, müssen darauf achten, nicht außerhalb des Puffers zu schreiben.

### Demonstrationsprogramme

Das Archiv enthält neben dem Quellcode und den Include-Dateien Demos. Die in der A1K-Forumsdiskussion erwähnte Demo lädt drei rohe 15-Bit-Bilder und zeigt sie nacheinander, bis die linke Maustaste gedrückt wird. Sie nutzt `SetCustomScreen` und `RefreshScreen` und enthält die Bibliothek direkt, statt eine installierte Shared Library zu brauchen. Die Experimente mit Scrat gingen weiter, mit Animationen, grafischen Objekten und teilweise interaktiven Steuerelementen.

### Eine Idee, die nie umgesetzt wurde

Ich hatte einfache BOB-ähnliche Objekte erwogen: bewegliche Objekte wie Sprites oder klassische Blitter-Objekte, aber in Software gezeichnet. Das ungenutzte 16. Bit jedes Pixel-WORDs sollte als Transparenz-Flag dienen. Es blieb eine Idee und war nie Teil der veröffentlichten Version.

### Funktionen

- Eine einfache Schnittstelle für RTG und nativen AGA
- 15-Bit-RGB-Puffer mit 32.768 Farben, 320 × 240 Pixel
- Automatische Wahl des besten Ausgabemodus
- Double Buffering
- Demoprogramme und vollständiger Quellcode

### Voraussetzungen

- AmigaOS mit AGA-Chipsatz oder einer CyberGraphX-Grafikkarte
- Ein Prozessor und Speicher in dem Bereich, für den die Routinen geschrieben wurden (68020, Fast RAM)

### Bekannte Einschränkungen

Die Kommentare im Quellcode beschreiben Probleme zur Entwicklungszeit: Darstellungsfehler auf älteren CyberVision-64-Karten mit 2 MB Grafikspeicher, Flackern oder falsch dargestellte Bereiche in einigen Konfigurationen, Probleme auf DraCo-Systemen mit CyberGraphX, Leistungsgrenzen, die feste Größe von 320 × 240 und die Annahmen über das planare Speicherlayout. Einige CyberGraphX-Modi verwenden für das 15-Bit-Format BGR statt RGB, deshalb nutzt die Demo 8-Bit-Ausgabe. Diese Kommentare sind keine vollständige Kompatibilitätsbewertung aller Amiga-Konfigurationen.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Entwicklung | 1998-01 | Bibliothek, Include-Dateien, Demos, Testprogramme mit Scrat |
| Beta-Veröffentlichung | 2005-12 | Im A1K-Forum geteilt |
| Archiv wieder verfügbar | 2009-01 | Nach erneutem Interesse; der Code war etwa zehn Jahre alt |

### Downloads

| File / Datei | Inhalt | Source / Quelle |
|---|---|---|
| *to be added / wird ergänzt* | Quellcode der Bibliothek, Include-Dateien, Demoprogramme | A1K-Forum |

### Quellen

- A1K-Forum: Weitergabe älterer Experimente (2005-12) und erneute Bereitstellung des Archivs (2009-01)

https://www.a1k.org/forum/index.php?threads/7211/



### Hinweise

`independent.library` ist ein historisches Beta-Projekt und eine Momentaufnahme einer früheren Zeit der Amiga-Programmierung. Der Quellcode ist frei verfügbar und darf eingesehen, genutzt, verändert und weitergegeben werden. Es wurde keine formale Open-Source-Lizenz vergeben; die Erlaubnis spiegelt meine ausdrückliche Absicht wider, freie Nutzung und weitere Experimente zu erlauben. Bitte bedenkt, dass es eine alte Beta-Version ist, die seit vielen Jahren nicht gepflegt wird. Es ist ein Ausgangspunkt für Experimente, keine produktionsreife Grafikbibliothek.

Das Projekt begann mit einer einfachen Idee: ein paar Pixel auf den Amiga-Bildschirm zeichnen, ohne sich jedes Mal um die Grafikhardware kümmern zu müssen. Es sollte nie ein großes Framework werden. Im Rückblick ist es eine Momentaufnahme der Herausforderungen der Amiga-Grafikprogrammierung in den späten 1990er Jahren: Chunky gegen Planar, RTG gegen nativen AGA, Farbumwandlung, Speicherverwaltung und der Wunsch, verschiedene Hardware über eine einfache Schnittstelle zu unterstützen.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-24</sub>
