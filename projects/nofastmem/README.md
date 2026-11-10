# NoFastMem / Switching off AutoConfig Fast RAM for one reset

> **EN:** NoFastMem is a small assembler tool that keeps an AutoConfig Fast RAM expansion from being registered by the system for one reset. This lets older games run that refuse to work on an Amiga with more than 512 KB or 1 MB of memory.
>
> **DE:** NoFastMem ist ein kleines Assembler-Werkzeug, das verhindert, dass eine AutoConfig-Fast-RAM-Erweiterung für einen Reset vom System angemeldet wird. So laufen ältere Spiele, die auf einem Amiga mit mehr als 512 KB oder 1 MB Speicher den Dienst verweigern.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2013-04 (2013-04-12) |
| **First release / Erste Veröffentlichung** | 2013-04-13 |
| **Latest version / Aktuelle Version** | Only version (2013-04-13) / Einzige Version (2013-04-13) |
| **Platform / Plattform** | Amiga with AutoConfig Fast RAM (designed for an A600 with an A608 expansion) |
| **Type / Art** | Software (assembler) |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum, only for logged-in members; never uploaded to Aminet / nur für angemeldete Mitglieder; nie auf Aminet hochgeladen |
| **License / Lizenz** | Freely available / Frei verfügbar |
| **Related projects / Verwandte Projekte** | none |

---

## English

### Overview

Some older Amiga game classics, mainly those from the 1980s, do not like it when the Amiga has more memory than 512 KB or 1 MB. They refuse to work. NoFastMem switches off the Fast RAM expansion for one reset without unplugging it, so that such a game can be started.

The tool of the same name in the Workbench is not suitable for this: it needs a running Workbench, so it cannot be used for programs that have to be booted, such as games or demos. My tool switches the memory off before the operating system sets up its internals. The operating system and the games or demos have no knowledge of the memory; it is simply not present.

### Background

The project started with a question in the A1K forum on 11 April 2013. A user had put an A608 Fast RAM expansion into his Amiga 600 and noticed that old games no longer worked. He asked for a way to switch off the Fast RAM by software:

- A tool on the disk "Vogue Tools" switches off a 512 KB Fast RAM expansion on an A500, which would be reset-proof. On his A600, it crashed when he tried to switch off the A608. Another tool did the same.
- He could switch off the A608 in Workbench, but after a reset the Fast RAM was on again.
- An Action Replay 2 could not be used, because a PCMCIA adapter permanently occupies the port in that A600.

A suggestion from another forum member was to create a modified Kickstart without AutoConfig using Remus. That was too elaborate for two or three games.

### Project History

On 12 April 2013, I suggested a solution in the thread: use the ColdCapture vector to activate the AutoConfig function of the card early. A little hardware banging on `$E80048` and `$E8004A` would activate the card before `expansion.library` searches for AutoConfig boards. The library then finds nothing, because the card is already active. A side effect is that the memory is active but is not registered in the system by `expansion.library`.

On 13 April 2013, I posted the finished program in the same thread. I did not own the expansion, so I could not test it myself and asked for feedback.

The user who had asked tested it on his A600 with the A608 and reported that it works perfectly. He described the result like this: the boot disk works almost like a Relokick disk. Insert it, let it start, and when the Amiga resets, remove the disk, and the Fast RAM is off. Then load the software that does not cope with Fast RAM. After the next reset, the Fast RAM is on again. All older classics ran without problems from disk again. According to him, the other tools that can switch off Fast RAM did not manage to switch off the A608 and keep it off after a reset. He also suggested uploading the tool to Aminet, where such an A608 tool did not exist.

### Technical Description

The tool works in two stages, a start program and a short piece of code that runs at the next cold start.

**Start program**

1. It allocates a small block of Chip RAM and copies the cold-start code into it.
2. It disables multitasking and interrupts, and switches to supervisor mode. In supervisor mode, it also switches off interrupts and DMA, turns off the power LED and clears the background colour.
3. It sets the ColdCapture vector in `ExecBase` to the code in Chip RAM, and recalculates the `ExecBase` checksum, so that the vector is valid at the next reset.
4. It calls `ColdReboot`.

**Cold-start code**

At the next boot, the ColdCapture code runs before `expansion.library` looks for AutoConfig boards. It writes `$00` to `$E80048` and `$20` to `$E8004A`. This switches the AutoConfig card through to address `$200000` early, so that it is **not configured any more**. Then the code returns to the normal start-up.

The result: the Fast RAM is active, but the system does not know about it, so programs cannot use it. For the operating system and for games or demos, the memory is simply not present.

### Features

- Switches off AutoConfig Fast RAM for one reset, without unplugging the expansion
- No hardware modification
- Works before the operating system is set up, so it also suits bootable games and demos
- Small program

### Requirements

- Amiga with an AutoConfig Fast RAM expansion, for example an A600 with an A608
- The card to be switched off must be the first AutoConfig board. The tool picks up the first AutoConfig card and switches it through

### Installation and Usage

1. Start the program once.
2. The Amiga performs a cold reboot by itself. It restarts without the registered Fast RAM.
3. Start the game.

The tool can be put on a boot disk: insert the disk, let it start, and when the Amiga resets, remove the disk. The Fast RAM is then off, and the software can be loaded from disk.

One call gives one run without Fast RAM. After the next reset, everything is normal again.


### Known Limitations

- The effect lasts for one run. After the next reset, everything is normal again.
- It only works with the first AutoConfig card. With other cards, the tool will probably tend to crash.
- The card is switched through to the fixed address `$200000`.
- I could not test the program myself. The user who asked tested it on an A600 with an A608.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| Only version | 2013-04-13 | Posted in the A1K forum. The feedback was positive, so there was no need for a second version |

---

## Deutsch

### Übersicht

Einige ältere Amiga-Spieleklassiker, vorwiegend aus den 1980er Jahren, mögen es nicht, wenn der Amiga mehr Speicher hat als 512 KB oder 1 MB. Sie verweigern dann ihren Dienst. NoFastMem schaltet die Fast-RAM-Erweiterung für einen Reset ab, ohne sie auszustecken, sodass sich ein solches Spiel starten lässt.

Das gleichnamige Werkzeug der Workbench eignet sich dafür nicht: Es setzt eine laufende Workbench voraus und taugt deshalb nicht für Programme, die gebootet werden müssen, wie Spiele oder Demos. Mein Werkzeug schaltet den Speicher bereits vor dem Einrichten der Betriebssystem-Interna ab. Das Betriebssystem und die Spiele oder Demos haben kein Wissen von dem Speicher, er ist schlicht nicht vorhanden.

### Hintergrund

Das Projekt begann mit einer Frage im A1K-Forum am 11. April 2013. Ein Nutzer hatte in seinen Amiga 600 eine A608-Fast-RAM-Erweiterung eingebaut und bemerkte, dass alte Spiele nicht mehr liefen. Er fragte nach einer Möglichkeit, das Fast RAM per Software abzuschalten:

- Ein Werkzeug auf der Diskette „Vogue Tools“ schaltet bei einem A500 eine 512-KB-Fast-RAM-Erweiterung ab, und zwar resetfest. Auf seinem A600 stürzte es ab, wenn er die A608 abschalten wollte. Ein anderes Werkzeug tat dasselbe.
- In der Workbench konnte er die A608 abschalten, aber nach einem Reset war das Fast RAM wieder an.
- Ein Action Replay 2 war nicht nutzbar, weil in diesem A600 dauerhaft ein PCMCIA-Adapter am Port steckt.

Ein Vorschlag eines anderen Forenmitglieds war, mit Remus ein angepasstes Kickstart ohne AutoConfig zu erzeugen. Das war für zwei oder drei Spiele zu aufwendig.

### Projektgeschichte

Am 12. April 2013 schlug ich im Thread eine Lösung vor: Mit dem ColdCapture-Vektor die AutoConfig-Funktion der Karte frühzeitig ansprechen. Ein kleines Hardware-Banging auf `$E80048` und `$E8004A` aktiviert die Karte, bevor die `expansion.library` nach AutoConfig-Karten sucht. Die Bibliothek findet dann nichts, weil die Karte schon aktiv ist. Nebeneffekt ist, dass der Speicher zwar aktiv ist, von der `expansion.library` aber nicht im System angemeldet wird.

Am 13. April 2013 postete ich das fertige Programm im selben Thread. Ich besaß die Erweiterung nicht, konnte es also selbst nicht testen und bat um Rückmeldung.

Der Nutzer, der gefragt hatte, testete es auf seinem A600 mit der A608 und meldete, dass es einwandfrei funktioniert. Das Ergebnis beschrieb er so: Die Bootdiskette funktioniert fast wie eine Relokick-Diskette. Einlegen, starten lassen, und wenn der Amiga resettet, die Diskette entfernen, und das Fast RAM ist aus. Dann lädt man die Software, die mit Fast RAM nicht klarkommt. Nach dem nächsten Reset ist das Fast RAM wieder an. Alle älteren Klassiker liefen wieder problemlos von Diskette. Die anderen Werkzeuge, die Fast RAM abschalten können, schafften es laut ihm nicht, die A608 abzuschalten und nach einem Reset abgeschaltet zu lassen. Er regte auch an, das Werkzeug auf Aminet hochzuladen, wo es kein solches A608-Werkzeug gab.

### Technische Beschreibung

Das Werkzeug arbeitet in zwei Stufen, einem Startprogramm und einem kurzen Codestück, das beim nächsten Kaltstart läuft.

**Startprogramm**

1. Es reserviert einen kleinen Block Chip RAM und kopiert den Kaltstart-Code dorthin.
2. Es schaltet Multitasking und Interrupts ab und wechselt in den Supervisor-Modus. Dort schaltet es außerdem Interrupts und DMA ab, die Power-LED aus und setzt die Hintergrundfarbe zurück.
3. Es trägt den ColdCapture-Vektor in `ExecBase` auf den Code im Chip RAM ein und berechnet die `ExecBase`-Prüfsumme neu, damit der Vektor beim nächsten Reset gültig ist.
4. Es ruft `ColdReboot` auf.

**Kaltstart-Code**

Beim nächsten Start läuft der ColdCapture-Code, bevor die `expansion.library` nach AutoConfig-Karten sucht. Er schreibt `$00` nach `$E80048` und `$20` nach `$E8004A`. Dadurch wird die AutoConfig-Karte frühzeitig auf die Adresse `$200000` durchgeschaltet, sodass sie **nicht mehr konfiguriert** wird. Danach kehrt der Code in den normalen Start zurück.

Das Ergebnis: Das Fast RAM ist aktiv, aber das System kennt es nicht, und Programme können es nicht benutzen. Für das Betriebssystem und für Spiele oder Demos ist der Speicher schlicht nicht vorhanden.

### Funktionen

- Schaltet AutoConfig-Fast-RAM für einen Reset ab, ohne die Erweiterung auszustecken
- Kein Hardware-Eingriff
- Wirkt, bevor das Betriebssystem eingerichtet wird, und eignet sich deshalb auch für bootbare Spiele und Demos
- Kleines Programm

### Voraussetzungen

- Amiga mit einer AutoConfig-Fast-RAM-Erweiterung, zum Beispiel ein A600 mit A608
- Die abzuschaltende Karte muss die erste AutoConfig-Karte sein. Das Werkzeug greift die erste AutoConfig-Karte auf und schaltet sie durch

### Installation und Verwendung

1. Das Programm einmal starten.
2. Der Amiga führt von selbst einen Kaltstart durch und startet ohne angemeldetes Fast RAM neu.
3. Das Spiel starten.

Das Werkzeug lässt sich auf eine Bootdiskette legen: Diskette einlegen, starten lassen, und wenn der Amiga resettet, die Diskette entfernen. Das Fast RAM ist dann aus, und die Software lässt sich von Diskette laden.

Ein Aufruf ergibt einen Lauf ohne Fast RAM. Nach dem nächsten Reset ist wieder alles normal.

### Bekannte Einschränkungen

- Der Effekt gilt für einen Lauf. Nach dem nächsten Reset ist wieder alles normal.
- Es funktioniert nur mit der ersten AutoConfig-Karte. Mit anderen Karten wird das Werkzeug wahrscheinlich zu Abstürzen neigen.
- Die Karte wird auf die feste Adresse `$200000` durchgeschaltet.
- Ich konnte das Programm selbst nicht testen. Der Nutzer, der gefragt hatte, testete es auf einem A600 mit A608.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Einzige Version | 2013-04-13 | Im A1K-Forum veröffentlicht. Da die Rückmeldung positiv war, war keine zweite Version nötig |

---

## Source Code / Quellcode

<details>
<summary>Assembler source as posted in the A1K forum on 2013-04-13 / Assembler-Quellcode, wie am 13.04.2013 im A1K-Forum veröffentlicht</summary>

```asm
;    ------------------------------
;     ejaculatio praecox / noacafast
;    ------------------------------

START:
    move.l    4,a6                    ; execbase        
    move.l    #CODEEND-COLDCODE,d0            ; size coldcode        
    moveq    #$02,d1                    ; MEMF_CHIP        
    jsr    _LVOAllocMem(a6)            ; xx bytes        
    tst.l    d0
    bne    COLDCOPY                ; this time enough    
    moveq    #-1,d0                    ; error -> exit        
    rts                        ; add some cpu code    

COLDCOPY:
    move.l    d0,a4                    ; chipmem-pointer for    
    move.l    d0,a1                    ; ColdCapture & CopyDest
    lea    COLDCODE,a0                ; CopySrc, our chipstuff

    move.l    #CODEEND-COLDCODE,d0            ; a0=src,a1=dest,d0=size
    jsr    _LVOCopyMem(a6)                ; copy code        

    jsr    _LVOForbid(a6)                ; disable as much as    
    jsr    _LVODisable(a6)                ; possible and start    
    lea    SUPERCODE,a5                ; our code in         
    jsr    _LVOSupervisor(a6)            ; supervisor-mode    
    even

SUPERCODE:
    or.w    #$0700,sr                ; disable        
    bset    #1,$bfe001                ; toggle power-led off    
    lea    $dff000,a0                ; custom-reg        
    moveq    #0,d0                    ; clear d0        
    move.w    #$7fff,d1                ; disable:        
    move.w    d1,$09a(a0)                ; interrupts        
    move.w    d1,$096(a0)                ; dma            
    move.w    d0,$110(a0)                ; bitplane data        
    move.w    d0,$180(a0)                ; background color    
SETCOLDCAPTURE:
    move.l    a4,$2a(a6)                ; ColdCapture        
    clr.w    $52(a6)                    ; CheckSum        
    lea    $22(a6),a0                ; SoftVer        
    moveq    #24,d0                    ; (ChkSum-SoftVer)/2    
    clr.l    d1
SUM:
    add.w    (a0)+,d1                ; calc checksum        
    dbf    d0,SUM                    ; for valid entry    
    not.w    d1                    ; the next reset    
    move.w    d1,$52(a6)                ; starts our code    

    jsr    _LVOColdReboot(a6)            ; COLDREBOOT -> COLDCODE

; ------------------------------------------------------------------------------
;                 RESET -> COLDSTART                
; ------------------------------------------------------------------------------

COLDCODE:
    move.b    #$00,$e80048    ; AutoConfig-Karte vorzeitig durchschalten auf
    move.b    #$20,$e8004a    ; Adr. $200000! Wird NICHT mehr konfiguriert !
    jmp    (a5)
CODEEND:
```

</details>

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| *to be added later / wird später ergänzt* | first version | 2013-04-13 | Currently only available in the A1K forum for logged-in members |

<!-- TODO: Das Archiv wird später zum Download ergänzt (Dateiname). Im Forum wurde die Datei laut Beitrag mit zusätzlicher Endung ".pdf" angehängt. -->

---

## References / Quellen

- A1K forum thread on switching off Fast RAM, 2013-04-11 to 2013-04-13 (question in post 1, suggestion in post 8, solution in post 10): <https://www.a1k.org/forum/index.php?threads/37495/>

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-07</sub>
