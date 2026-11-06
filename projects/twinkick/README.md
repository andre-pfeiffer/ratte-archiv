# TwinKick / Kickstart 1.3 and 3.1 on one disk for the Amiga 1000

> **EN:** TwinKick is a dual Kickstart environment for expanded Amiga 1000 systems. The tool TKG.exe turns the user's own Kickstart ROM files into one boot disk with Kickstart 1.3 and Kickstart 3.1, and the user can switch between them at every reset.
>
> **DE:** TwinKick ist eine Dual-Kickstart-Umgebung für erweiterte Amiga-1000-Systeme. Das Programm TKG.exe macht aus den eigenen Kickstart-ROM-Dateien des Anwenders eine Startdiskette mit Kickstart 1.3 und Kickstart 3.1, zwischen denen bei jedem Reset umgeschaltet werden kann.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | ca. 1992 |
| **First release / Erste Veröffentlichung** | 2002-09-08 (version 2.0, Aminet) |
| **Latest version / Aktuelle Version** | 2.0 (2002-09-08) |
| **Platform / Plattform** | Amiga 1000 with at least 2 MB Fast RAM / mit mindestens 2 MB Fast RAM |
| **Type / Art** | Software |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Aminet (util/sys) |
| **License / Lizenz** | TKG.exe on Aminet, may be freely distributed / frei verteilbar. Source code currently not available / Quellcode derzeit nicht verfügbar |
| **Related projects / Verwandte Projekte** | [KickWork](../kickwork/) · [KickTOS](../kicktos/) · [Kickstart 3.9](../kickstart3x/) · [A1000 ROM Socket](../a1000romsocket/) |

---

## English

### Overview

TwinKick is a dual Kickstart environment for expanded Amiga 1000 systems. It combines the compatibility of the original Kickstart 1.3 with the functionality of Kickstart 2.x/3.x. A modified 256 KB Kickstart 1.3 sits in the Writable Control Store (WCS) and loads a second, 512 KB Kickstart into the memory expansion. At every reset the user can switch between the two.

### Background

Unlike later Amiga models, the Amiga 1000 does not contain a permanent Kickstart ROM. The operating system is loaded into a Writable Control Store (WCS), also commonly known as Write Once Memory (WOM). The WCS holds 256 KB.

This design offered considerable flexibility in 1985, but later became a limitation because newer Kickstart versions need 512 KB and no longer fit. TwinKick was developed to extend the capabilities of the original Amiga 1000 without modifying its fundamental architecture.

### Project History

**Before TwinKick.** My Amiga 1000 was equipped with a Roßmöller Handshake A8MB-1000 memory expansion, which I acquired around 1990 or 1991. It had 2 MB and no AutoConfig. On this card I wrote a small loader in GFA Basic that loaded a 512 KB Kickstart into the Fast RAM. I do not count it as TwinKick. It was a dirty hack and only my entry into the technique of running a Kickstart from Fast RAM.

**The start of TwinKick (around 1992).** I replaced the Roßmöller card with a Phase 5 Blizzard turbo card (14 MHz, AutoConfig). From then on my GFA Basic hack no longer ran, and I had to dig deeper into the system. This is the start of TwinKick. The Blizzard card is made for other computers, so I had to build an adapter for the 68000 socket so that it fitted mechanically into the Amiga 1000 housing. This was also the start of my hardware tinkering.

**Version 1.0** was for my own use only and could not be distributed for legal reasons. It used Kickstart 2.05 (V37.210) as the second Kickstart. At this point the changes to Kickstart 1.3 were already finished, and they stayed the same up to the version with Kickstart 3.9. Only the boot block, the boot screen and the second 512 KB Kickstart changed later.

**Version 2.0** used Kickstart 3.1 (V40.063) as the second Kickstart. As far as I remember, it was finished somewhere around 1994 to 1996.

**2002: TKG.exe and the Aminet release.** TwinKick was the project that was especially cool to me at the time, but it could not be uploaded to Aminet for legal reasons, because it contains Kickstart ROMs. HighGFX, in contrast, had found its way to Aminet, and felt "safe" for posterity. TwinKick did not. In 2002, as my last effort for the Amiga, I created a way to preserve TwinKick digitally: I programmed TKG.exe. It contains only the changes to the Kickstart ROMs, the loader code and the instructions, and uses the ROM files supplied by the user to write the finished Kickstart to a floppy disk. It was meant as my farewell gift to the Amiga. Version 2.0 was published on Aminet on 8 September 2002 under the title "Kickstart 3.1 for A1000".

**2006.** An internal development version with Kickstart 3.9 (V45.60) was created, but never released.

### Hardware Used

| Hardware | Notes |
|---|---|
| Roßmöller Handshake A8MB-1000 | Memory expansion for the Amiga 1000 (1989), up to 8 MB Fast RAM, installed in the 68000 socket; mine had 2 MB and no AutoConfig |
| Phase 5 Blizzard Turbo Memory | Turbo card with 14 MHz and AutoConfig (1992); fitted with a 68010; adapter for the 68000 socket built by me |

The Blizzard card has a ShadowROM. I used it in daily operation, but it made hardly any difference: it only mirrored the ROM (the Kickstart 1.3 from TwinKick), or another Kickstart could be loaded, which I have to do on the Amiga 1000 anyway. 512 KB Kickstarts could be loaded there as well, but that was rather counterproductive, because with TwinKick I could switch during operation.

### Technical Description

The WCS holds only the modified 256 KB Kickstart 1.3. The Kickstart 2.x/3.x with 512 KB (or 1 MB) is located in the memory expansion.

**Boot sequence**

1. **BootROM (16 KB).** The Amiga 1000 BootROM exists only to load the WCS. It is called at every reset. It checks the WCS checksum. If the content is invalid, it asks for a Kickstart disk. If the content is valid, it write-protects the WCS immediately (this can only be undone by a reset) and jumps into the Kickstart inside the WCS, as on a computer with a ROM chip.
2. **Modified Kickstart 1.3.** From here on, the mechanisms are in the modified Kickstart 1.3. It also contains the TwinKick boot logo, the Workbench hand with the request to insert a disk. This Kickstart checks the Fast RAM for another Kickstart, checks the operating mode and hands over control if required.
3. **Disk detection.** The small routine in Kickstart that checks inserted disks for bootability has been extended and also recognises a TwinKick disk. A dedicated TwinKick marker in the boot block identifies it.
4. **Loading the second Kickstart.** If a TwinKick disk is found, the second Kickstart is loaded into the Fast RAM and started with another reset. It stays resident in memory.

**Default and switching**

- The default is Kickstart 2.x/3.x.
- If the disk is removed during the first reset, TwinKick misses the second Kickstart and runs in single mode with Kickstart 1.3.
- **Right mouse button** held at reset: switches to the respective other Kickstart.
- **Both mouse buttons** held at reset in Kickstart 1.3 mode: **game mode**. This is a function of the modified Kickstart 1.3. It bypasses the mechanism for configuring expansions and external drives, so that as many expansions as possible are disabled and even the oldest software can be made to run.
- Both mouse buttons at reset in Kickstart 2.0 and higher open the OS 2.x/3.x boot menu as usual.

**Memory**

Memory expansions with and without AutoConfig are supported. The Fast RAM must be located at $200000.

**Changes to Kickstart 1.3**

- **Better Kickstart protection:** fewer crashes that erase the Kickstart.
- **2 MB ChipMem fix:** if an A1000 has been expanded to 2 MB Chip RAM, the reset-proof RAM disk (RAD:) works without a patch (`SetPatch -r`).
- **New PAL check:** the computer always starts in PAL resolution, the DOS window opens in PAL size, and the mouse pointer is no longer displayed twice in the lower part of the screen.
- **Workbench title bar:** shows "Workbench release 1.3."
- **Game mode:** external drives and expansions are disabled and only the Chip RAM is active (in this case just 512 KB). The Exec library is built in memory at $676, which helps with older games.
- **Virus checker** and further bug fixes.

Kickstart 3.1 also works with memory expansions that do not support AutoConfig.

**Other computers**

In theory, the 256 KB Kickstart 1.3 from TwinKick burned into a ROM chip and installed in an A500 or A2000 would allow these computers to load a second Kickstart as well, given enough memory. This is of little interest for A500/A2000 users, who usually install Kickstart 3.1 ROMs or stay with Kickstart 1.3 or even 1.2.

### Features

- Kickstart 1.3 and Kickstart 2.x/3.x resident side by side
- Switching at every reset with the right mouse button
- Game mode for the oldest software
- Support for memory expansions with and without AutoConfig
- TKG.exe creates the Kickstart disk from the user's own ROM files

### Requirements

- Amiga 1000 with at least 2 MB Fast RAM at $200000
- Only one external memory expansion is supported
- Kickstart 1.3 (V34.5) as a file named `KICK13.ROM` (from A500/A1000/A2000)
- Kickstart 3.1 (V40.063) as a file named `KICK31.ROM` (from A500/A600/A2000)
- A blank, AmigaDOS-formatted floppy disk

For copyright reasons, the Kickstart files must be supplied by the user. They can be created with the tool GRABKICK from Aminet, and must carry exactly the names above.

### Installation and Usage

TKG.exe is an Amiga program. The extension ".exe" comes from my PC parallel world at the time and has no special meaning.

1. Copy `TKG.exe` and your own ROM files `KICK13.ROM` and `KICK31.ROM` onto the blank AmigaDOS disk.
2. Start `TKG.exe` from the CLI or the Shell.
3. The program modifies the ROMs accordingly and writes everything back to the same disk in Amiga 1000 Kickstart format. **The source disk is overwritten.** The AmigaDOS disk with two ROM files and TKG.exe has become a finished Kickstart disk for the Amiga 1000.
4. Switch on the Amiga 1000 and insert the new disk.

### Known Limitations

- More than one external memory expansion is not supported.
- At least 2 MB of Fast RAM at $200000 is required.

### Kickstart Versions

| Version | Notes |
|---------|-------|
| Kickstart 1.3 (V34.5) | In the WCS (256 KB), modified by TwinKick. Used in all versions |
| Kickstart 2.05 (V37.210) | Second Kickstart of version 1.0 (internal) |
| Kickstart 3.1 (V40.063) | Second Kickstart of version 2.0 |
| Kickstart 3.9 (V45.60) | Internal development version (2006), never released |

### Version History

| Version | Date | Notes |
|---------|------|-------|
| GFA Basic loader | ca. 1990/91 to 1992 | Private hack on the Roßmöller card, loads a 512 KB Kickstart into Fast RAM; not counted as TwinKick |
| 1.0 | from ca. 1992 | Internal, not distributable; Kickstart 2.05 (V37.210); changes to Kickstart 1.3 complete |
| 2.0 (internal) | ca. 1994–1996 (from memory) | Kickstart 3.1 (V40.063); changes to boot block, boot screen and the second 512 KB Kickstart |
| 2.0 (Aminet) | 2002-09-08 | Public release with TKG.exe |
| Development version | 2006-05-15 | Kickstart 3.9 (V45.60); internal, never released |

---

## Deutsch

### Übersicht

TwinKick ist eine Dual-Kickstart-Umgebung für erweiterte Amiga-1000-Systeme. Sie verbindet die Kompatibilität des ursprünglichen Kickstart 1.3 mit den Möglichkeiten von Kickstart 2.x/3.x. Ein modifiziertes 256-KB-Kickstart 1.3 liegt im Writable Control Store (WCS) und lädt ein zweites, 512 KB großes Kickstart in die Speichererweiterung. Bei jedem Reset kann zwischen beiden umgeschaltet werden.

### Hintergrund

Im Gegensatz zu späteren Amiga-Modellen besitzt der Amiga 1000 kein fest eingebautes Kickstart-ROM. Das Betriebssystem wird in einen Writable Control Store (WCS) geladen, der vielen Anwendern auch als Write Once Memory (WOM) bekannt ist. Der WCS fasst 256 KB.

Dieses Konzept bot 1985 eine hohe Flexibilität, wurde aber später zur Einschränkung, weil neuere Kickstart-Versionen 512 KB benötigen und nicht mehr hineinpassen. TwinKick entstand, um die Möglichkeiten des Amiga 1000 zu erweitern, ohne dessen ursprüngliche Architektur grundlegend zu verändern.

### Projektgeschichte

**Vor TwinKick.** Mein Amiga 1000 war mit einer Roßmöller-Handshake-A8MB-1000-Speichererweiterung ausgestattet, die ich um 1990 oder 1991 erworben hatte. Sie hatte 2 MB und kein AutoConfig. Auf dieser Karte schrieb ich einen kleinen Loader in GFA Basic, der ein 512-KB-Kickstart ins Fast RAM lud. Ich bezeichne ihn nicht als TwinKick. Es war ein dreckiger Hack und nur mein Einstieg in die Technik, ein Kickstart aus dem Fast RAM zu betreiben.

**Der Beginn von TwinKick (um 1992).** Ich tauschte die Roßmöller-Karte gegen eine Phase-5-Blizzard-Turbokarte (14 MHz, AutoConfig). Ab dann lief mein GFA-Basic-Hack nicht mehr, und ich musste tiefer ins System. Das ist der Beginn von TwinKick. Die Blizzard-Karte ist für andere Rechner gebaut, deshalb musste ich einen Adapter für den 68000-Sockel bauen, damit sie mechanisch in das Gehäuse des Amiga 1000 passt. Damit ging auch die Hardwarebastelei los.

**Version 1.0** war nur für den Eigengebrauch und konnte aus rechtlichen Gründen nicht verteilt werden. Sie nutzte Kickstart 2.05 (V37.210) als zweites Kickstart. Die Änderungen am Kickstart 1.3 waren zu diesem Zeitpunkt schon fertig und blieben bis zur Version mit Kickstart 3.9 unverändert. Später änderten sich nur Bootblock, Bootscreen und das zweite 512-KB-Kickstart.

**Version 2.0** nutzte Kickstart 3.1 (V40.063) als zweites Kickstart. Nach meiner Erinnerung war sie irgendwann um 1994 bis 1996 fertig.

**2002: TKG.exe und die Aminet-Veröffentlichung.** TwinKick war damals das Projekt, das ich besonders „cool“ fand, aber es konnte aus rechtlichen Gründen nicht auf Aminet hochgeladen werden, weil es Kickstart-ROMs enthält. HighGFX dagegen hatte den Weg ins Aminet gefunden und war damit gefühlt für die Nachwelt „sicher“. TwinKick nicht. 2002 schuf ich als meine letzte Kraftanstrengung für den Amiga eine Möglichkeit zum digitalen Erhalt von TwinKick: Ich programmierte TKG.exe. Es enthält nur die Änderungen an den Kickstart-ROMs, den Ladecode und die Anleitung und schreibt mit den vom Anwender bereitgestellten ROM-Dateien das fertige Kickstart auf Diskette. Es sollte mein Abschiedsgeschenk an den Amiga sein. Version 2.0 erschien am 8. September 2002 auf Aminet unter dem Titel „Kickstart 3.1 for A1000“.

**2006.** Es entstand eine interne Entwicklungsversion mit Kickstart 3.9 (V45.60), die nie veröffentlicht wurde.

### Verwendete Hardware

| Hardware | Hinweise |
|---|---|
| Roßmöller Handshake A8MB-1000 | Speichererweiterung für den Amiga 1000 (1989), bis zu 8 MB Fast RAM, wird in den 68000-Sockel gesteckt; meine hatte 2 MB und kein AutoConfig |
| Phase 5 Blizzard Turbo Memory | Turbokarte mit 14 MHz und AutoConfig (1992); mit einem 68010 bestückt; Adapter für den 68000-Sockel selbst gebaut |

Die Blizzard-Karte hat ein ShadowROM. Ich habe es im Alltag genutzt, es hat aber kaum einen Unterschied gemacht: Es spiegelte nur das eigentliche ROM (das Kickstart 1.3 aus TwinKick), oder man konnte ein anderes Kickstart laden, was ich beim Amiga 1000 ohnehin machen muss. Auch 512-KB-Kickstarts ließen sich dort laden, das war aber eher kontraproduktiv, weil ich mit TwinKick im Betrieb umschalten konnte.

### Technische Beschreibung

Im WCS liegt nur das modifizierte 256-KB-Kickstart 1.3. Das Kickstart 2.x/3.x mit 512 KB (oder 1 MB) liegt in der Speichererweiterung.

**Bootvorgang**

1. **BootROM (16 KB).** Das BootROM des Amiga 1000 ist nur zum Beladen des WCS gedacht. Es wird bei jedem Reset angesprungen und prüft die Checksumme des WCS. Ist der Inhalt ungültig, fordert es eine Kickstart-Diskette an. Ist er gültig, schützt es den WCS sofort gegen Schreiben (aufheben lässt sich das nur durch einen Reset) und springt in das Kickstart im WCS, wie bei einem Rechner mit ROM-Chip.
2. **Modifiziertes Kickstart 1.3.** Ab hier liegen die Mechanismen im geänderten Kickstart 1.3. Es enthält auch das TwinKick-Bootlogo, die Workbench-Hand mit der Aufforderung zum Einlegen einer Diskette. Dieses Kickstart prüft das Fast RAM auf ein anderes Kickstart, prüft den Betriebsmodus und übergibt gegebenenfalls die Kontrolle.
3. **Diskettenerkennung.** Die kleine Routine im Kickstart, die eingelegte Disketten auf Bootfähigkeit prüft, ist erweitert und erkennt auch eine TwinKick-Diskette. Ein spezielles TwinKick-Kennzeichen im Bootblock identifiziert sie.
4. **Laden des zweiten Kickstarts.** Wird eine TwinKick-Diskette gefunden, wird das zweite Kickstart ins Fast RAM geladen und mit einem weiteren Reset gestartet. Es bleibt resident im Speicher.

**Standard und Umschalten**

- Standard ist Kickstart 2.x/3.x.
- Entfernt man die Diskette während des ersten Resets, „vermisst“ TwinKick das zweite Kickstart und läuft im Einzelbetrieb mit Kickstart 1.3.
- **Rechte Maustaste** beim Reset gedrückt: schaltet auf das jeweils andere Kickstart um.
- **Beide Maustasten** beim Reset im Kickstart-1.3-Modus: **Spiel-Modus**. Das ist eine Funktion des geänderten Kickstart 1.3. Es hebelt den Mechanismus zum Konfigurieren von Erweiterungen und externen Laufwerken aus, sodass möglichst alle Erweiterungen abgeschaltet sind und auch älteste Software zum Laufen gebracht werden kann.
- Beide Maustasten beim Reset ab Kickstart 2.0 öffnen wie gewohnt das OS-2.x/3.x-Bootmenü.

**Speicher**

Speichererweiterungen mit und ohne AutoConfig werden unterstützt. Das Fast RAM muss ab Adresse $200000 liegen.

**Änderungen am Kickstart 1.3**

- **Besserer Kickstartschutz:** weniger Abstürze, die das Kickstart löschen.
- **Korrektur beim 2-MB-ChipMem:** Wurde ein A1000 auf 2 MB Chip RAM erweitert, funktioniert die resetfeste RAM-Disk (RAD:) auch ohne Patch (`SetPatch -r`).
- **Neuer PAL-Check:** Der Rechner startet immer in PAL-Auflösung, das DOS-Fenster öffnet in PAL-Größe, und der Mauszeiger wird im unteren Bildbereich nicht mehr doppelt dargestellt.
- **Workbench-Titelzeile:** zeigt „Workbench release 1.3.“ an.
- **Spiel-Modus:** Externe Laufwerke und Erweiterungen sind abgeschaltet, und nur das Chip RAM ist aktiv (hier nur 512 KB). Die Exec-Library wird im Speicher ab $676 aufgebaut, was für ältere Spiele hilfreich ist.
- **Virenprüfung** und weitere Fehlerkorrekturen.

Kickstart 3.1 arbeitet außerdem mit Speichererweiterungen ohne AutoConfig.

**Andere Rechner**

Theoretisch könnte man das 256-KB-Kickstart 1.3 aus TwinKick in einen ROM-Baustein brennen und in einen A500 oder A2000 einsetzen. Auch diese Rechner könnten dann bei genügend Speicher ein zweites Kickstart laden. Für A500/A2000-Nutzer ist das wenig interessant, weil sie in der Regel Kickstart-3.1-ROMs einbauen oder bei Kickstart 1.3 oder sogar 1.2 bleiben.

### Funktionen

- Kickstart 1.3 und Kickstart 2.x/3.x resident nebeneinander
- Umschalten bei jedem Reset mit der rechten Maustaste
- Spiel-Modus für älteste Software
- Unterstützung für Speichererweiterungen mit und ohne AutoConfig
- TKG.exe erzeugt die Kickstart-Diskette aus den eigenen ROM-Dateien des Anwenders

### Voraussetzungen

- Amiga 1000 mit mindestens 2 MB Fast RAM ab $200000
- Es wird nur eine externe Speichererweiterung unterstützt
- Kickstart 1.3 (V34.5) als Datei `KICK13.ROM` (von A500/A1000/A2000)
- Kickstart 3.1 (V40.063) als Datei `KICK31.ROM` (von A500/A600/A2000)
- Eine leere, AmigaDOS-formatierte Diskette

Aus urheberrechtlichen Gründen muss der Anwender die Kickstart-Dateien selbst bereitstellen. Sie lassen sich mit dem Tool GRABKICK aus dem Aminet erzeugen und müssen genau die oben genannten Namen tragen.

### Installation und Verwendung

TKG.exe ist ein Amiga-Programm. Die Endung „.exe“ stammt aus meiner damaligen PC-Parallelwelt und hat keine besondere Bedeutung.

1. `TKG.exe` und die eigenen ROM-Dateien `KICK13.ROM` und `KICK31.ROM` auf die leere AmigaDOS-Diskette kopieren.
2. `TKG.exe` aus dem CLI oder der Shell aufrufen.
3. Das Programm ändert die ROMs entsprechend ab und schreibt alles im Amiga-1000-Kickstart-Format auf dieselbe Diskette zurück. **Die Quelldiskette wird überschrieben.** Aus dem AmigaDOS-Datenträger mit zwei ROM-Dateien und TKG.exe ist eine fertige Kickstart-Diskette für den Amiga 1000 geworden.
4. Den Amiga 1000 einschalten und die neue Diskette einlegen.

### Bekannte Einschränkungen

- Mehr als eine externe Speichererweiterung wird nicht unterstützt.
- Mindestens 2 MB Fast RAM ab $200000 sind erforderlich.

### Kickstart-Versionen

| Version | Hinweis |
|---------|---------|
| Kickstart 1.3 (V34.5) | Im WCS (256 KB), von TwinKick angepasst. In allen Versionen verwendet |
| Kickstart 2.05 (V37.210) | Zweites Kickstart von Version 1.0 (intern) |
| Kickstart 3.1 (V40.063) | Zweites Kickstart von Version 2.0 |
| Kickstart 3.9 (V45.60) | Interne Entwicklungsversion (2006), nie veröffentlicht |

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| GFA-Basic-Loader | ca. 1990/91 bis 1992 | Privater Hack auf der Roßmöller-Karte, lädt ein 512-KB-Kickstart ins Fast RAM; nicht als TwinKick gezählt |
| 1.0 | ab ca. 1992 | Intern, nicht verteilbar; Kickstart 2.05 (V37.210); Änderungen am Kickstart 1.3 abgeschlossen |
| 2.0 (intern) | ca. 1994–1996 (aus der Erinnerung) | Kickstart 3.1 (V40.063); Änderungen an Bootblock, Bootscreen und zweitem 512-KB-Kickstart |
| 2.0 (Aminet) | 2002-09-08 | Veröffentlichung mit TKG.exe |
| Entwicklungsversion | 2006-05-15 | Kickstart 3.9 (V45.60); intern, nie veröffentlicht |

---

## Gallery / Galerie

<!-- TODO: Fotos und Screenshots werden nachgereicht (Ablage in images/): A1000 mit Roßmöller-Karte, Blizzard mit selbstgebautem Adapter, Bootscreen mit TwinKick-Hinweis, Kickstart-Diskette. -->

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| [twinkick.lha](https://aminet.net/package/util/sys/twinkick) | 2.0 | 2002-09-08 | Aminet (util/sys), contains `tkg.exe` and `tkg.readme` |

---

## References / Quellen

- Aminet, TwinKick: <https://aminet.net/package/util/sys/twinkick>
- Amiga Hardware Database, Roßmöller Handshake A8MB-1000: <https://amiga.resource.cx/expde/a8mb1000>
- Amiga Hardware Database, Phase 5 Blizzard Turbo Memory: <https://amiga.resource.cx/expde/blizzard500>

---

## Notes / Hinweise

**EN:** The source code of TwinKick and TKG.exe is currently not available; I still have to locate it in my archives. Whether it will be published is not yet decided.

**DE:** Der Quellcode von TwinKick und TKG.exe ist derzeit nicht verfügbar; ich muss ihn erst in meinen Archiven ausfindig machen. Ob er veröffentlicht wird, ist noch nicht entschieden.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-06</sub>
