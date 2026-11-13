# SwitchControl / Control software for the MonitorSwitch

> **EN:** SwitchControl is a small resident program for the Amiga that watches the screen mode in front and sets the control signal of the MonitorSwitch: native Amiga mode or graphics card mode. This makes the switching automatic.
>
> **DE:** SwitchControl ist ein kleines residentes Programm für den Amiga, das den Bildschirmmodus im Vordergrund überwacht und das Steuersignal des MonitorSwitch setzt: nativer Amiga-Modus oder Grafikkartenmodus. Dadurch wird das Umschalten automatisch.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2009-08 (version 0.8 on 2009-08-15; first test tool on 2009-07-13) |
| **First release / Erste Veröffentlichung** | 2009-08-26 (version 1.0) |
| **Latest version / Aktuelle Version** | 1.1a (2010-01-17), the recommended version. Experimental: 1.1d (2013-08-15) |
| **Platform / Plattform** | Amiga with an RTG graphics card (Picasso96 or CyberGraphX), Kickstart 3.1 or higher |
| **Type / Art** | Software (assembler) |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum |
| **License / Lizenz** | Free; the source code of version 1.1a is free to use / Frei; der Quellcode von Version 1.1a ist frei verwendbar |
| **Related projects / Verwandte Projekte** | [MonitorSwitch](../monitorswitch/) · [Radeon Switch](../radeonswitch/) |

---

## English

### Overview

SwitchControl is the software half of the [MonitorSwitch](../monitorswitch/). The switch board needs a signal that tells it which source to show. SwitchControl creates this signal. It evaluates the screen mode that is currently in front, decides whether it is a native Amiga mode or a graphics card mode, and sets the level of the control line accordingly. Only this software makes the automatic switching possible.

### Background

For the hardware, see the [MonitorSwitch](../monitorswitch/) page. The software idea was to hook into the operating system and react to screen mode changes, because the native Amiga modes have well-known IDs. Everything else can be assumed to be a graphics card mode.

### Project History

- **13 July 2009:** The first approach was a small test tool, SWTE (SwitchTest), that evaluated screen mode changes. It hooked into the `MakeViewPort` routine and reacted to every screen mode change, for example from PAL to NTSC or from Super72 to MultiScan. To make it visible, the background turned red, and the program waited for a mouse click.
- **15 August 2009:** Version 0.8.
- **23 August 2009:** Version 0.9 was my internal test version with the new `LoadView` patch. I had thrown away the code completely. The screen mode detection now worked down to the last detail, even when screens were dragged down (CyberGraphX "draggable" or Amiga graphics).
- **26 August 2009:** Version 1.0. The first MonitorSwitches with the piggyback board were released with this version.
- **02 January 2010:** A bug report said that some programs refused to switch. A few logs and tests later, version 1.1 with the NULL pointer fix was ready. In further tests it proved to be 100 % reliable.
- **17 January 2010:** I updated the version string and made version 1.1a out of it. This is the version I recommend to everybody: fast and reliable. It has been in use for more than ten years without complaints.
- **15 August 2013:** Version 1.1d, an experimental version with DPMS support (see below).
- **5 February 2012:** SwitchHack, a derivative for AmigaOS 4 and MorphOS (see below). It was added as an edit to the forum thread of version 1.1a.

About ten beta testers tried the software. The forum member **chkamiga** was particularly active.

### Technical Description

SwitchControl patches the function `LoadView()` of `graphics.library`. Whenever the system shows a different screen, the patched routine runs first.

1. It looks at the screen mode ID of the front screen (with `GetDisplayInfoData`) and takes the **monitor ID** from it.
2. If the monitor ID is `$000F` or lower, it is a native Amiga mode (internal source). If it is higher, it is a graphics card mode (external source).
3. It sets the control line accordingly: Bit 4 at `$BFD000` of the CIA, the CTS line of the serial port. A cleared bit selects the external source, a set bit selects the internal one.
4. It then calls the original `LoadView()` from the ROM.

**NULL pointer fix (from version 1.1).** Some programs, such as XCopy, games and demos, call `LoadView(NULL)`. In this case the routine switches to the internal source.

**Memory.** The patch is copied into its own block of cleared public Fast RAM and stays resident.

**Native monitor IDs.** These are the native Amiga monitor IDs. Everything above `$000F`, for example the modes of Picasso96 and CyberGraphX, is treated as a graphics card.

| ID | Mode | ID | Mode |
|---|---|---|---|
| `$0001` | NTSC | `$0008` | Super72 |
| `$0002` | PAL | `$0009` | DblNTSC |
| `$0003` | Multiscan/VGA | `$000A` | DblPAL |
| `$0004` | A2024 monitor | `$000B` | HD720 |
| `$0005` | HighGFX | `$000C` | Film24 |
| `$0006` | Euro72 | `$000D` | SuperPlus |
| `$0007` | Euro36 | `$000E` | Xtreme |

The native screen modes were designed by Commodore for OS 3. Euro36 and Euro72 are part of Workbench 3.1. Film24 was less well known and was apparently supplied with some genlocks.

The native modes of my own graphics projects [HighGFX](../highgfx/) (including HD720, SuperPlus and Xtreme) are therefore treated as native Amiga modes.

**Two builds.** The source code contains two variants of the control line. By swapping the commented sections when compiling, I build either the parallel version (SEL line) or the serial version (CTS line). The listing below is the serial version.

### Features

- Automatic switching, no settings required
- Works with Picasso96 and CyberGraphX
- Also works when screens are dragged down
- Small, fast and reliable (version 1.1a)

### Requirements

- Amiga with Kickstart 3.1 or higher. The version check in the source code is faulty: the comment says V39, the code requires V40. This is not a disadvantage, because all RTG software requires Kickstart 3.1.
- An RTG graphics card with Picasso96 or CyberGraphX
- A [MonitorSwitch](../monitorswitch/)

### Installation and Usage

1. Copy the file `SwitchControl` to `SYS:C`.
2. Add a line with `SwitchControl` to the `Startup-Sequence`, **directly before** the entry `IPrefs`.

There are no arguments or tooltypes. The program cannot be switched off, but it is deactivated automatically at every reset.

### Versions

| Version | Date | Notes |
|---|---|---|
| SWTE (test tool) | 2009-07-13 | Minimal demo, hooks into `MakeViewPort` |
| 0.8 | 2009-08-15 | |
| 0.9 | 2009-08-23 | Internal test version, rewritten, new `LoadView` patch |
| 1.0 | 2009-08-26 | First release, delivered with the piggyback boards |
| 1.1 | 2010-01-02 | NULL pointer fix, after a bug report; 100 % reliable in tests |
| **1.1a** | 2010-01-17 | Updated version string, with a clean readme and source listing. **Recommended.** In use for more than ten years without complaints |
| 1.1d | 2013-08-15 | Experimental, switches more slowly and sends DPMS (see below) |

### Version 1.1d (experimental)

Version 1.1d is an experimental version that deliberately switches more slowly. When switching to an RTG resolution, it makes the AGA sync signals send a DPMS signal to the monitor. A monitor with two inputs then switches to the other input. That input should work as a slave, so that when switching back to AGA, the monitor automatically returns to the master input. With a suitable monitor, SwitchControl 1.1d can therefore create the automatic experience even **without** a MonitorSwitch.

The source code of version 1.1d is still to be found in my archives.

### SwitchHack

SwitchHack is a derivative of SwitchControl. It simply switches the SEL and CTS lines to RTG, without any RTG software having to be loaded. It is meant to be called for OS4 and MorphOS, so that the system is already configured for graphics card output, because neither system requires AGA and both benefit more from RTG. The small file sends a short pulse to the switch to put it into graphics card mode, both internally and externally. This should not really be a problem during the boot phase.


---

## Deutsch

### Übersicht

SwitchControl ist die Software-Hälfte des [MonitorSwitch](../monitorswitch/). Die Schalterplatine braucht ein Signal, das ihr sagt, welche Quelle sie zeigen soll. SwitchControl erzeugt dieses Signal. Es wertet den Bildschirmmodus aus, der gerade im Vordergrund liegt, entscheidet, ob es ein nativer Amiga-Modus oder ein Grafikkartenmodus ist, und setzt den Pegel der Steuerleitung entsprechend. Erst diese Software ermöglicht das automatische Umschalten.

### Hintergrund

Zur Hardware siehe die Seite [MonitorSwitch](../monitorswitch/). Die Softwareidee war, sich ins Betriebssystem einzuhängen und auf Wechsel des Bildschirmmodus zu reagieren, denn die nativen Amiga-Modi haben bekannte IDs. Alles andere lässt sich als Grafikkartenmodus annehmen.

### Projektgeschichte

- **13. Juli 2009:** Der erste Ansatz war ein kleines Testprogramm, SWTE (SwitchTest), das Wechsel des Bildschirmmodus auswertete. Es hängte sich in die Routine `MakeViewPort` ein und reagierte auf jeden Wechsel des Screenmodes, zum Beispiel von PAL auf NTSC oder von Super72 auf MultiScan. Zur Veranschaulichung wurde der Hintergrund rot, und das Programm wartete auf einen Mausklick.
- **15. August 2009:** Version 0.8.
- **23. August 2009:** Version 0.9 war meine interne Testversion mit dem neuen `LoadView`-Patch. Ich hatte den Code komplett umgeworfen. Die Screenmode-Erkennung funktionierte nun bis ins Detail, auch wenn Screens heruntergezogen wurden (CyberGraphX „draggable“ oder Amiga-Grafik).
- **26. August 2009:** Version 1.0. Die ersten MonitorSwitche mit der Huckepack-Platine wurden mit dieser Version herausgegeben.
- **02. Januar 2010:** Ein Fehlerbericht meldete, dass einige Programme nicht umschalten wollten. Ein paar Logs und Tests später war Version 1.1 mit dem NULL-Pointer-Fix fertig. Sie erwies sich im weiteren Test als zu 100 % zuverlässig.
- **17. Januar 2010:** Ich habe den Versionsstring aktualisiert und daraus gleich Version 1.1a gemacht. Das ist die Version, die ich jedem empfehle: schnell und zuverlässig. Sie ist seit über zehn Jahren im Einsatz, ohne Beanstandungen.
- **15. August 2013:** Version 1.1d, eine experimentelle Version mit DPMS-Unterstützung (siehe unten).
- **5. Februar 2012:** SwitchHack, eine Ableitung für AmigaOS 4 und MorphOS (siehe unten). Es wurde als Edit im Forenthread zur Version 1.1a ergänzt.

Etwa zehn Beta-Tester haben die Software ausprobiert. Besonders aktiv getestet hat das Forenmitglied **chkamiga**.

### Technische Beschreibung

SwitchControl patcht die Funktion `LoadView()` der `graphics.library`. Immer wenn das System einen anderen Screen anzeigt, läuft zuerst die gepatchte Routine.

1. Sie ermittelt die ScreenModeID des vordersten Screens (mit `GetDisplayInfoData`) und entnimmt ihr die **Monitor-ID**.
2. Ist die Monitor-ID `$000F` oder kleiner, handelt es sich um einen nativen Amiga-Modus (interne Quelle). Ist sie größer, ist es ein Grafikkartenmodus (externe Quelle).
3. Sie setzt die Steuerleitung entsprechend: Bit 4 an `$BFD000` des CIA, die CTS-Leitung der seriellen Schnittstelle. Ein gelöschtes Bit wählt die externe Quelle, ein gesetztes die interne.
4. Danach ruft sie das originale `LoadView()` aus dem ROM auf.

**NULL-Pointer-Fix (ab Version 1.1).** Manche Programme, etwa XCopy, Spiele und Demos, rufen `LoadView(NULL)` auf. In diesem Fall schaltet die Routine auf die interne Quelle.

**Speicher.** Der Patch wird in einen eigenen Block gelöschten öffentlichen Fast RAMs kopiert und bleibt resident.

**Native Monitor-IDs.** Das sind die nativen Amiga-Monitor-IDs. Alles oberhalb von `$000F`, zum Beispiel die Modi von Picasso96 und CyberGraphX, wird als Grafikkarte behandelt.

| ID | Modus | ID | Modus |
|---|---|---|---|
| `$0001` | NTSC | `$0008` | Super72 |
| `$0002` | PAL | `$0009` | DblNTSC |
| `$0003` | Multiscan/VGA | `$000A` | DblPAL |
| `$0004` | A2024-Monitor | `$000B` | HD720 |
| `$0005` | HighGFX | `$000C` | Film24 |
| `$0006` | Euro72 | `$000D` | SuperPlus |
| `$0007` | Euro36 | `$000E` | Xtreme |

Die nativen Bildschirmmodi wurden noch von Commodore für OS3 entworfen. Euro36 und Euro72 sind Bestandteil von Workbench 3.1. Film24 war weniger bekannt und wurde scheinbar einigen Genlocks beigelegt.

Die nativen Modi meiner eigenen Grafikprojekte [HighGFX](../highgfx/) (einschließlich HD720, SuperPlus und Xtreme) werden deshalb als native Amiga-Modi behandelt.

**Zwei Varianten.** Der Quellcode enthält zwei Varianten der Steuerleitung. Durch Tauschen der auskommentierten Bereiche beim Kompilieren erstelle ich entweder die parallele Version (SEL-Leitung) oder die serielle Version (CTS-Leitung). Das Listing unten ist die serielle Version.

### Funktionen

- Automatisches Umschalten, keine Einstellungen nötig
- Funktioniert mit Picasso96 und CyberGraphX
- Funktioniert auch, wenn Screens heruntergezogen werden
- Klein, schnell und zuverlässig (Version 1.1a)

### Voraussetzungen

- Amiga mit Kickstart 3.1 oder höher. Die Versionsabfrage im Quellcode ist fehlerhaft: Der Kommentar sagt V39, der Code verlangt V40. Das ist kein Nachteil, weil jede RTG-Software Kickstart 3.1 voraussetzt.
- Eine RTG-Grafikkarte mit Picasso96 oder CyberGraphX
- Ein [MonitorSwitch](../monitorswitch/)

### Installation und Verwendung

1. Die Datei `SwitchControl` nach `SYS:C` kopieren.
2. Eine Zeile mit `SwitchControl` in die `Startup-Sequence` einfügen, und zwar **direkt vor** dem Eintrag `IPrefs`.

Es gibt keine Argumente und keine Tooltypes. Das Programm lässt sich nicht abschalten, wird aber bei jedem Reset automatisch deaktiviert.

### Versionen

| Version | Datum | Hinweise |
|---|---|---|
| SWTE (Testprogramm) | 2009-07-13 | Minimaldemo, hängt sich in `MakeViewPort` |
| 0.8 | 2009-08-15 | |
| 0.9 | 2009-08-23 | Interne Testversion, neu geschrieben, neuer `LoadView`-Patch |
| 1.0 | 2009-08-26 | Erste Veröffentlichung, mit den Huckepack-Platinen ausgeliefert |
| 1.1 | 2010-01-02 | NULL-Pointer-Fix nach einem Fehlerbericht; im Test zu 100 % zuverlässig |
| **1.1a** | 2010-01-17 | Aktualisierter Versionsstring, mit sauberer Readme und sauberem Quellcode-Listing. **Empfohlen.** Seit über zehn Jahren im Einsatz, ohne Beanstandungen |
| 1.1d | 2013-08-15 | Experimentell, schaltet langsamer um und sendet DPMS (siehe unten) |

### Version 1.1d (experimentell)

Version 1.1d ist eine experimentelle Version, die gezielt langsamer umschaltet. Beim Umschalten auf eine RTG-Auflösung sorgt sie dafür, dass die AGA-Syncs ein DPMS-Signal an den Monitor senden. Ein Monitor mit zwei Eingängen schaltet dann auf den anderen Eingang um. Dieser sollte als Slave arbeiten, sodass der Monitor beim Zurückschalten auf AGA automatisch auf den Master-Eingang zurückschaltet. Mit einem passenden Monitor kann SwitchControl 1.1d also auch **ohne** MonitorSwitch ein automatisches Bilderlebnis erzeugen.

Der Quellcode von Version 1.1d muss noch in meinen Archiven gefunden werden.

### SwitchHack

SwitchHack ist eine Ableitung von SwitchControl. Es schaltet einfach nur die Leitungen SEL und CTS auf RTG, ohne dass eine RTG-Software geladen sein muss. Gedacht ist es für den Aufruf von OS4 und MorphOS, damit das System bereits auf Grafikkartenausgabe konfiguriert ist, da beide Systeme AGA nicht zwingend voraussetzen und eher von RTG profitieren. Die kleine Datei sendet einen kurzen Impuls an den Switch, um ihn auf Grafikkartenmodus zu schalten, sowohl intern als auch extern. In der Bootphase sollte das nicht wirklich problematisch sein.

---

## Source Code / Quellcode

Version 1.1a, serial version (CTS line). The comments are in German. / Version 1.1a, serielle Version (CTS-Leitung). Die Kommentare sind deutsch.

<details>
<summary>SWITCHCONTROL.ASM (V1.1a)</summary>

```asm
; Source:SWITCHCONTROL.ASM		REV: 1.1a

StartupASM
	move.l	(4).w,a6		; ExecBase sichern
	movem.l	d0/a0,-(sp)		; Rette Kommandozeile
	clr.l	_WBenchMsg		; sicherheitshalber

; Teste, von wo gestartet wurde
; -----------------------------
	sub.l	a1,a1			; a1=0 = eigener Task
	jsr	-$126(a6)		; wo sind wir?
	move.l	d0,a4			; Adresse retten

	tst.l	$ac(a4)			; Laufen wir unter WB?
	beq.s	fromWorkbench		; wenn so

; Wir wurden vom CLI gestartet
; ----------------------------
	movem.l	(sp)+,d0/a0		; Parms Kommandozeile holen
	bra	run			; und starten

; Wir wurden von Workbench gestartet
; ----------------------------------
fromWorkbench
	lea	$5c(a4),a0		; Warten auf
	jsr	-$180(a6)		; Start-Message
	lea	$5c(a4),a0		; Message ist da
	jsr	-$174(a6)		; abholen und
	move.l	d0,_WBenchMsg		; sichen

	movem.l	(sp)+,d0/a0		; bringe Stack i.O.

run
	bsr	_main			; rufe unser Programm auf
	move.l	d0,-(sp)		; rette seinen Return-Code
	tst.l	_WBenchMsg		; gibt´s eine WB-Message
	beq.s	_exit			; nein: dann war´s CLI
	
	jsr	-$84(a6)		; keine Unterbrechung jetzt
	move.l	_WBenchMsg(pc),a1	; hole die Message
	jsr	-$17a(a6)		; und gib sie zurück

_exit
	move.l	(sp)+,d0		; hole Return-Code
	rts				; das war´s

_WBenchMsg:
	ds.l	1
	cnop	0,2
	
; CLI und WB landen hier ...
; --------------------------
_main
	move.l	(4).w,a6		; ExecBase sichern
	moveq	#0,d0			; LONGWORD löschen
	move.w	$14(a6),d0		; Exec-Version laden (WORD)
	cmp.w	#39,d0			; Version abfragen (V39 oder höher)
	bls	_errorcode		; ansonsten Fehler
	move.l	#PROG_ENDE-PROG_START,d0; benötigte Speichergröße ermittlen
	move.l	#$10005,d1		; Clear Fast Public als Speichertyp
	jsr	-$c6(a6)		; und Speicher anforden
	cmp.l	#0,d0			; ist Speicher vorhanden
	beq	_errorcode		; nein: abbruch
	jsr	-$84(a6)		; keine Unterbrechung jetzt

	jsr	_switchpatch		; unser Programm...

	jsr	-$8a(a6)		; Unterbrechungen wieder zulassen
	cmp.l	#0,d0			; war die routine erfolgreich
	beq	_leave			; ja: dann raus hier
	move.l	d0,a1			; Adresse des Speichers
	move.l	#PROG_ENDE-PROG_START,d0; Speicher
	jsr	-$d2(a6)		; wieder freigeben
_errorcode
	moveq	#5,d0			; Return-Code auf Fehler setzen
	bra	_bye			; und zum Ende gehen

_leave
	moveq	#0,d0			; Return-Code auf OK setzen
_bye
	rts				; das war´s

; ----------------------------------------------------------------------------
; >>>>>>>>>>>>>>>>>>>>>>>>>>> unser Programm... <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
; ----------------------------------------------------------------------------

_switchpatch
	move.l	d0,_patchbase		; D0 = Start des reservierten Speichers für unseren Patch

	lea	_intname,a1		; intuition.library
	jsr	-$198(a6)		; öffnen
	move.l	d0,INTBASE		; und den Zeiger in INTBASE sichern
	beq	ERROR			; bei Misserfolg raus hier

	move.l	d0,a1			; Zeiger auf intuition.library
	jsr	-$19e(a6)		; und wieder schließen

	lea	_gfxname,a1		; graphics.library
	jsr	-$198(a6)		; öffnen
	move.l	d0,_libbase		; und den Zeiger in _libbase sichern
	move.l	d0,GFXBASE		; und für den Patch in GFXBASE sichern
	beq	ERROR			; bei Misserfolg raus hier

	sub.l	#$dc,d0			; Offset für Funktion LOADVIEW errechen
	move.l	d0,a0			; Ergebnis auf A0 ablegen
	lea	LOADVIEW,a1		; Offset für unseren Speicher laden
	move.l	(a0),(a1)		; die physikalische ROM-Adr von LOADVIEW in den Patch schreiben
	
	lea	PROG_START,a0		; Basis unseres eigentlichen Patches ermitteln
	move.l	_patchbase,a1		; und Basis unseres reservierten Speichers laden
	move.l	#PROG_ENDE-PROG_START,d0; das Länge unseres Patches errechnen
	jsr	-$270(a6)		; und den Patch in den reservierten Speicher kopieren

	move.l	_libbase,a1		; Zeiger der graphics.library nach A1 laden
	move.l	_patchbase,d0		; Zeiger auf unseren reservierten Speicher nach D0 laden

	addi.l	#$4,d0			; unseren Config-Pointer überspringen und auf Code zeigen

	lea	-$de,a0			; Offset für LOADVIEW in A0 ablegen
	jsr	-$1a4(a6)		; Unsere Routine anstelle von LOADVIEW in die GFXLIB einbinden

	move.l	_libbase,a1		; Zeiger auf graphics.library
	jsr	-$19e(a6)		; und wieder schließen
	
	moveq	#0,d0			; Return-Code auf OK setzen
	bra	BYE

ERROR
	moveq	#5,d0			; Return-Code auf ERROR setzen

BYE
	rts				; und unseren Code verlassen

	even

; ----------------------------------------------------------------------------
; >>>>>>>>>>>>>>>>>>>>>>>>>>>>> PATCH - START <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
; ----------------------------------------------------------------------------

PROG_START

_configpointer
	dc.l	$FFFFFFFF	; noch nicht unterstützt / + hw-check

_code
	movem.l	d0-d7/a0-a6,-(sp)

	move.l	a1,d0		; NULL-PointerFix
	tst.l	d0		; (XCopy, Games & Demos)
	beq	_tricky		; SwitchControl V1.1

	move.l	INTBASE(pc),a6

	tst.l	$3c(a6)
	beq	_null

	move.l	$3c(a6),a6
	move.l	$16e(a6),a0
	bra	_handle

_null
	move.l	#0,a0

_handle
	move.l	GFXBASE(pc),a6

	lea	BUFFER(pc),a1	; bufferpointer
	move.l	#$00000060,d0	; buffergröße
	move.l	#$80002000,d1	; tagid (MonitorInfo)
	move.l	#$00000000,d2	; id2 = NULL
	jsr	-$2f4(a6)	; GetDisplayInfoData
	tst.l	d0
	beq	_nochanges

	move.l	SCID(pc),d0	; ermittelte ScreenModeID nach D0 laden

_tricky
	andi.l	#$ffff1000,d0	; aus D0 neue MonitorID extrahieren
	lea	MONID(pc),a1	; vorherige MonitorID nach A1 laden

	cmp.l	(a1),d0		; vorherige MonitorID mit neuer vergleichen
	beq	_nochanges	; keine Veränderung, dann so weiter

	move.l	d0,(a1)		; neue MonitorID sichern
	moveq	#0,d0
	move.w	(a1),d0		; MonitorID als Indikator laden

	cmp.w	#$000f,d0	; alles unter Mode $10 ist AmigaChipSet
	bls	_internalgfx	; kleiner gleich ist intern

_externalgfx
	; port auf externe grafikquelle setzen
	bset	#$4,$bfd200		; ser.cts-leitung auf ausgang schalten
	bclr	#$4,$bfd000		; auf externe bildquelle schalten

;	bset	#$2,$bfd200		; par.sel-leitung auf ausgang schalten
;	bclr	#$2,$bfd000		; auf externe bildquelle schalten

	movem.l	(sp)+,d0-d7/a0-a6
	bsr	_romloadview
	bra	_leavepatch

_internalgfx
	; port auf interne grafikquelle setzen
	bset	#$4,$bfd200		; ser.cts-leitung auf ausgang schalten
	bset	#$4,$bfd000		; auf interne bildquelle schalten

;	bset	#$2,$bfd200		; par.sel-leitung auf ausgang schalten
;	bset	#$2,$bfd000		; auf interne bildquelle schalten

_nochanges
	movem.l	(sp)+,d0-d7/a0-a6
	bsr	_romloadview

_leavepatch
	rts

; ----------------------------------------------------------------------------
; >>>>>>>>>>>>>>>>>>>>>>>>>>>>> PATCH - DATAS <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
; ----------------------------------------------------------------------------

	even

_romloadview
		dc.w	$4eb9		; jsr - Befehl
LOADVIEW	dc.l	$00000000	; Adresse für "echtes" LOADVIEW im ROM
		dc.w	$4e75		; rts - Befehl

GFXBASE		dc.l	$00000000	; Offset für graphics.library
INTBASE		dc.l	$00000000	; Offset für intuition.library

MONID		dc.l	$FFFFFFFF	; Speicher für bereinigte MonitorID

BUFFER		dc.l	$00000000	; Bufferspeicher für GetDisplayInfoData
SCID		dc.l	$00000000	; ScreenModeID des vordersten Screens
		dc.l	$00000000	; die restlichen Daten sind für uns
		dc.l	$00000000	; nicht von Bedeutung (alles 96 Bytes)

		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000

		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000

		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000

		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000

		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000
		dc.l	$00000000

_version
		dc.b	"$VER: SwitchControl V1.1a (17.01.10) by André (Ratte) Pfeiffer",0
		even


PROG_ENDE

; ----------------------------------------------------------------------------
; >>>>>>>>>>>>>>>>>>>>>>>>>>>>>> PATCH - END <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
; ----------------------------------------------------------------------------

_datasection
	even
_patchbase
	dc.l	0
	even
_libbase
	dc.l	0
	even
_gfxname
	dc.b	"graphics.library",0	; 
	even
_intname
	dc.b	"intuition.library",0	;
	even
```

</details>

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| `SwitchControl` (executable / ausführbare Datei) | 1.1a | 2010-01-17 | A1K forum (link to be added) |

<!-- TODO: Download-Link zur Version 1.1a ergänzen. Quellcode von Version 1.1d suchen. -->

---

## References / Quellen

- A1K forum, SwitchControl 0.8 (2009-08-15), thread "gfx.lib patchen… Fragen zum View/Viewport": <https://www.a1k.org/forum/index.php?threads/17566/>
- A1K forum, MonitorSwitch development thread (0.9 on 2009-08-23, 1.0 on 2009-08-26): <https://www.a1k.org/forum/index.php?threads/16232/>
- A1K forum, SwitchControl 1.1 (2010-01-02): <https://www.a1k.org/forum/index.php?threads/19511/>
- A1K forum, SwitchControl 1.1a (2010-01-17), with the SwitchHack edit of 2012-02-05: <https://www.a1k.org/forum/index.php?threads/20017/>
- A1K forum, SwitchControl 1.1d (2013-08-15): <https://www.a1k.org/forum/index.php?threads/32435/>

---

## Notes / Hinweise

**EN:** SwitchControl 1.1a is free, and its source code may be used freely. Thanks to the beta testers, especially chkamiga.

**DE:** SwitchControl 1.1a ist frei, und der Quellcode darf frei verwendet werden. Dank an die Beta-Tester, besonders an chkamiga.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-13</sub>
