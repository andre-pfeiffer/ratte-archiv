# A1000 Video Port / An internal video slot for flicker fixers in the Amiga 1000

> **EN:** A1000 Video Port gives the Amiga 1000 an internal video slot for a flicker fixer card such as the MultiVision2000. A small adapter on Denise and a few signal lines from the RGB port feed the card, so that the Amiga delivers a 31 kHz VGA signal without an external scandoubler.
>
> **DE:** A1000 Video Port gibt dem Amiga 1000 einen internen Video-Slot für eine FlickerFixer-Karte wie die MultiVision2000. Ein kleiner Adapter am Denise und ein paar Signalleitungen vom RGB-Port speisen die Karte, sodass der Amiga ohne externen Scandoubler ein 31-kHz-VGA-Signal liefert.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2007-05 (2007-05-28) |
| **First release / Erste Veröffentlichung** | 2007-06-06 (board layouts in the A1K forum) |
| **Platform / Plattform** | Amiga 1000 (tested with a PiggyPack PAL board) |
| **Type / Art** | Hardware (two small boards and a cable) |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum (layout files for download) |
| **License / Lizenz** | None needed: anyone can rebuild it / Keine nötig: Jeder kann es nachbauen |
| **Related projects / Verwandte Projekte** | [Holzbrett](../holzbrett/) |

---

## English

### Overview

Like all old Amigas, the Amiga 1000 has the problem that its graphics output does not deliver a usable VGA signal. A flicker fixer solves this, but it needs signals from inside the computer. The Video Port brings these signals out of the A1000 to a slot for a flicker fixer card, so that the Amiga delivers a 31 kHz signal and modern PC monitors can be used.

The Video Port consists of three things:

- a **Denise adapter** that plugs on the Denise chip and provides the colour signals (16 signal lines),
- four lines taken from the **RGB port** (CSync, HSync, VSync and the C1 clock),
- the **VideoPort board** with the slot for the flicker fixer card, connected through a 40-pin IDE ribbon cable.

### Background

My first attempt dates from 1994: a mess of wires that I describe as a deterrent example. In May 2007, I built the Video Port new for the [Holzbrett](../holzbrett/), as a rework of this old construction. The flicker fixer card was a MultiVision2000, which I restored for this purpose.

### How it was built

To build it, I took the pin assignment of the video port from a book (for example "Amiga Intern") and looked at the flicker fixer. The signals the card uses are taken from the mainboard. I only had to take three sync signals and a clock signal from the RGB port. The rest of the signals are directly at Denise.

Forum members made suggestions: Reptile advised me to take the sync signals from Agnus, but I did not want to build another adapter. Ralf pointed out that in the A2000, most video slot signals are taken from the video hybrid, and that it had not worked for him when the RGB bits are taken directly from Denise. It worked for me.

### Project History

| Date | Event |
|---|---|
| 2007-05-28 | The flicker fixer is restored. The Video Port is screwed onto the Holzbrett: Denise adapter, four lines (CSync, HSync, VSync, C1 clock) from the RGB port, ribbon cable to the Video Port |
| 2007-05-29 | Wiring soldered and measured. The "possible" installation position in the Amiga |
| 2007-05-31 | "Rework of the rework": instead of a cable mess, a tidy connection. There were no 36-pin slot sockets left in my town, so I modified an existing 50-pin socket. Large holes in the adapter board allow mounting to the board. The solution would also fit into a later case |
| 2007-06-01 | **First test run:** 15 kHz signal from the RGB port, then the fully wired setup (still 15 kHz), then 31 kHz from the flicker fixer with the RGB cable pulled off. A movie documents it |
| 2007-06-06 | The finished boards, with layout files for the VideoPort and the Denise adapter |
| 2007-06-08 | Forum members suggest a group order of boards |
| 2007-06-10 | Installation hints: how to attach the four-wire cable, orientation of the ribbon cable and of the flicker fixer card |

**Test setup:** Amiga 1000 PiggyPack PAL with 256 KB, Kickstart 1.1 and an EA graphics demo; monitor Idek Iiyama MF5017 (15 to 40 kHz, 17 inch). The setup worked with the MultiVision2000 only; I do not know how other flicker fixers behave.

### The boards

| Board | Size |
|---|---|
| VideoPort board | 25.40 × 99.06 mm |
| Denise adapter | 30.48 × 60.96 mm |

The layout files (`.LAY`) were created with SprintLayout 5.0. The ZIP archive contains the freeware viewer with a print function, for those who want to etch the boards themselves. The boards are single-sided and should not need a placement print. A solder mask should perhaps be used, because it became a little tight. The files are accepted, for example, by the Conrad board service. Please note the dimensions of the boards when ordering. I would like to hear about cheaper alternatives, and about a parts list with Conrad article numbers.

### Installation hints

- The four-wire cable with the signals from the RGB port has to be attached as shown in the photos.
- The large ribbon cable is a **40-pin IDE cable**. The coloured wire has to point to the cross on the respective boards.
- The flicker fixer card has to be installed with its component side facing the ribbon cable connector.

### Notes

- **Audio through the video port:** I also considered it, because two lines of the ribbon cable are still free and would be ideal for left and right audio. The chip for the audio part of the MultiVision2000 (AD7053) was missing, and the grounds of the audio part are not at the same potential: speaker grounds must not be connected, or the chip dies. I dropped the idea. The cinch connectors are still there.
- **Other Amigas:** In January 2013, I wrote that the adapter works only in the A1000. For the A500 and A2000, drivers are needed to amplify the signals, because the A1000 apparently has more "punch" on the line.
- **Microway Deb 2000:** In January 2008, a forum member pointed to a commercial video slot solution, the Deb 2000, which can be rebuilt. My own solution is also easy to rebuild, less cumbersome, and works without problems in my computer.

**Disclaimer.** I accept no liability for any damage to your hardware. If you are not sure, better keep your hands off it.

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [VideoPort.zip (boards, layout files `.LAY` and viewer)](https://www.a1k.org/download/area51/OLD/VideoPort.zip) | A1K forum download area |
| [VideoPort movie (test run)](https://www.a1k.org/download/area51/OLD/VideoPort.mpg) | A1K forum download area |

### Gallery / Galerie

<!-- TODO: Fotos aus dem Thread auswählen (Ablage in images/): Denise-Adapter und Kabel (#2, 28.05.2007), Einbauposition (#10), neuer Adapter mit 50-poliger Buchse (#13), Testlauf 15 und 31 kHz (#19), fertige Platinen (#47), Einbauhinweis (#55). -->

### References / Quellen

- A1K forum, Holzbrett thread: 

[the Video Port on the board (28 May 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100091), 

[wiring (29 May)](https://www.a1k.org/forum/index.php?threads/6745/post-100102), 

[rework (31 May)](https://www.a1k.org/forum/index.php?threads/6745/post-100104), 

[first test run (1 June)](https://www.a1k.org/forum/index.php?threads/6745/post-100108), 

[boards and layouts (6 June)](https://www.a1k.org/forum/index.php?threads/6745/post-100136), 

[installation hints (10 June)](https://www.a1k.org/forum/index.php?threads/6745/post-100144)

---

## Deutsch

### Übersicht

Wie bei allen alten Amigas gibt es auch beim Amiga 1000 das Problem, dass der Grafikausgang kein brauchbares VGA-Signal liefert. Ein FlickerFixer löst das, braucht aber Signale aus dem Inneren des Rechners. Der Video Port führt diese Signale aus dem A1000 zu einem Slot für eine FlickerFixer-Karte, sodass der Amiga ein 31-kHz-Signal liefert und moderne PC-Monitore nutzbar sind.

Der Video Port besteht aus drei Teilen:

- einem **Denise-Adapter**, der auf den Denise-Chip gesteckt wird und die Farbsignale bereitstellt (16 Signalleitungen),
- vier Leitungen vom **RGB-Port** (CSync, HSync, VSync und der C1-Takt),
- der **VideoPort-Platine** mit dem Slot für die FlickerFixer-Karte, verbunden über ein 40-poliges IDE-Flachbandkabel.

### Hintergrund

Mein erster Versuch stammt von 1994: ein Kabelsalat, den ich als abschreckendes Beispiel bezeichne. Im Mai 2007 baute ich den Video Port für das [Holzbrett](../holzbrett/) neu, als Rework dieses alten Aufbaus. Die FlickerFixer-Karte war eine MultiVision2000, die ich dafür restauriert hatte.

### So wurde es gebaut

Zum Bau habe ich die Belegung des Videoports aus einem Buch (zum Beispiel „Amiga Intern“) genommen und mir den FlickerFixer angesehen. Die Signale, die die Karte verwendet, werden vom Mainboard abgegriffen. Ich musste nur drei Sync-Signale und ein Taktsignal vom RGB-Port ziehen. Der Rest der Signale liegt direkt am Denise an.

Forumsmitglieder machten Vorschläge: Reptile riet mir, die Syncs vom Agnus zu nehmen, aber ich wollte keinen weiteren Adapter bauen. Ralf wies darauf hin, dass im A2000 die meisten Videoslot-Signale am Video-Hybrid abgegriffen werden und dass es bei ihm nicht lief, wenn die RGB-Bits direkt vom Denise genommen werden. Bei mir lief es.

### Projektgeschichte

| Datum | Ereignis |
|---|---|
| 2007-05-28 | Der FlickerFixer ist restauriert. Der Video Port wird aufs Holzbrett geschraubt: Denise-Adapter, vier Leitungen (CSync, HSync, VSync, C1-Takt) vom RGB-Port, Flachbandkabel zum Video Port |
| 2007-05-29 | Verdrahtung gelötet und durchgemessen. Die „mögliche“ Einbauposition im Amiga |
| 2007-05-31 | „Rework des Reworks“: statt Kabelsalat eine aufgeräumte Verbindung. In unserem Ort gab es keine 36-poligen Slotbuchsen mehr, deshalb habe ich eine vorhandene 50-polige Buchse umgearbeitet. Große Löcher in der Adapterplatine erlauben die Montage am Brett. Die Lösung würde auch in ein späteres Gehäuse passen |
| 2007-06-01 | **Erster Testlauf:** 15-kHz-Signal vom RGB-Port, dann der fertig verkabelte Aufbau (noch 15 kHz), dann 31 kHz vom FlickerFixer bei abgezogenem RGB-Kabel. Ein Film dokumentiert es |
| 2007-06-06 | Die fertigen Platinen, mit Layoutdateien für den VideoPort und den Denise-Adapter |
| 2007-06-08 | Forumsmitglieder schlagen eine Sammelbestellung der Platinen vor |
| 2007-06-10 | Einbauhinweise: Anbringung des vieradrigen Kabels, Ausrichtung des Flachbandkabels und der FlickerFixer-Karte |

**Testaufbau:** Amiga 1000 PiggyPack PAL mit 256 KB, Kickstart 1.1 und einer EA-Grafikdemo; Monitor Idek Iiyama MF5017 (15 bis 40 kHz, 17 Zoll). Der Aufbau lief nur mit der MultiVision2000; wie sich andere FlickerFixer verhalten, weiß ich nicht.

### Die Platinen

| Platine | Größe |
|---|---|
| VideoPort-Platine | 25,40 × 99,06 mm |
| Denise-Adapter | 30,48 × 60,96 mm |

Die Layoutdateien (`.LAY`) wurden mit SprintLayout 5.0 erstellt. Das ZIP-Archiv enthält den Freeware-Viewer mit Druckfunktion, für alle, die die Platinen selbst ätzen wollen. Die Platinen sind einseitig und sollten ohne Bestückungsdruck auskommen. Eventuell sollte Lötstopp verwendet werden, weil es etwas eng geworden ist. Die Dateien werden zum Beispiel vom Conrad-Leiterplattenservice akzeptiert. Bitte die Abmessungen der Platinen bei der Bestellung beachten. Günstigere Alternativen und eine Stückliste mit Conrad-Artikelnummern wären willkommen.

### Einbauhinweise

- Das vieradrige Kabel mit den Signalen vom RGB-Port muss wie auf den Fotos angebracht werden.
- Das große Flachbandkabel ist ein **40-poliges IDE-Kabel**. Die farbige Ader muss zum Kreuz auf den jeweiligen Platinen zeigen.
- Die FlickerFixer-Karte muss mit der bestückten Oberseite zum Flachbandkabelanschluss eingebaut werden.

### Hinweise

- **Audio über den Video Port:** Ich habe es ebenfalls erwogen, weil zwei Leitungen des Flachbandkabels noch frei und ideal für Audio links und rechts wären. Der Chip für den Audioteil der MultiVision2000 (AD7053) fehlte, und die Massen des Audioteils liegen nicht auf demselben Potenzial: Die Massen der Lautsprecher dürfen nicht verbunden werden, sonst stirbt der Chip. Ich habe die Idee verworfen. Die Cinch-Anschlüsse gibt es ja noch.
- **Andere Amigas:** Im Januar 2013 schrieb ich, dass der Adapter nur im A1000 funktioniert. Für A500 und A2000 braucht man Treiber, die die Signale verstärken, weil der A1000 scheinbar mehr „Bums“ auf der Leitung hat.
- **Microway Deb 2000:** Im Januar 2008 verwies ein Forumsmitglied auf eine kommerzielle Video-Slot-Lösung, die Deb 2000, die sich nachbauen lässt. Meine eigene Lösung ist ebenfalls leicht nachbaubar, weniger umständlich und funktioniert in meinem Rechner problemlos.

**Haftungsausschluss.** Ich hafte für nichts, was an eurer Hardware kaputtgeht. Wenn ihr euch nicht sicher seid, lasst lieber die Finger davon.

### Downloads

| File / Datei | Source / Quelle |
|---|---|
| [VideoPort.zip (Platinen, Layoutdateien `.LAY` und Viewer)](https://www.a1k.org/download/area51/OLD/VideoPort.zip) | A1K-Forum, Download-Bereich |
| [VideoPort-Film (Testlauf)](https://www.a1k.org/download/area51/OLD/VideoPort.mpg) | A1K-Forum, Download-Bereich |

### Quellen

- A1K-Forum, Holzbrett-Thread: 

[der Video Port auf dem Brett (28. Mai 2007)](https://www.a1k.org/forum/index.php?threads/6745/post-100091), 

[Verdrahtung (29. Mai)](https://www.a1k.org/forum/index.php?threads/6745/post-100102), 

[Rework (31. Mai)](https://www.a1k.org/forum/index.php?threads/6745/post-100104), 

[erster Testlauf (1. Juni)](https://www.a1k.org/forum/index.php?threads/6745/post-100108), 

[Platinen und Layouts (6. Juni)](https://www.a1k.org/forum/index.php?threads/6745/post-100136), 

[Einbauhinweise (10. Juni)](https://www.a1k.org/forum/index.php?threads/6745/post-100144)

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-16</sub>
