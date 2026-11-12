# DONOP / An April Fools' joke: USB for the Amiga 4000D

> **EN:** DONOP was an April Fools' joke by Chris Hodges and André Pfeiffer from 1 April 2010. It pretended to add a USB port to the Amiga 4000D by using the internal header J975. In reality, J975 is not designed for USB devices at all. This page explains the joke.
>
> **DE:** DONOP war ein Aprilscherz von Chris Hodges und André Pfeiffer vom 1. April 2010. Er tat so, als würde ein USB-Anschluss für den Amiga 4000D entstehen, indem man die interne Steckleiste J975 benutzt. In Wirklichkeit ist J975 gar nicht für USB-Geräte ausgelegt. Diese Seite erklärt den Scherz.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2010-04 |
| **First release / Erste Veröffentlichung** | 2010-04-01 (announcement in the A1K forum) |
| **Platform / Plattform** | Amiga 4000D |
| **Type / Art** | April Fools' joke (hardware and software prank) / Aprilscherz |
| **Authors / Autoren** | Chris Hodges (developer of the Amiga USB stack Poseidon) and André Pfeiffer |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | A1K forum |
| **License / Lizenz** | License-free; there is nothing to license / Lizenzfrei; es gibt nichts zu lizenzieren |
| **Related projects / Verwandte Projekte** | none |

---

## English

### Overview

On 1 April 2010, the A1K forum saw an announcement that the Amiga 4000D could get a simple USB port through its internal header J975. The announcement was an April Fools' joke, devised by Chris Hodges, the developer of the Amiga USB stack Poseidon, and me. Because of its publication date, it could be recognised as a joke.

The name is a pun: "DONOP" stands for "do NOP", that is, "do no operation" (NOP is the processor instruction that does nothing).

### What it really was

J975 is not designed to connect USB devices. It is merely a connector on the mainboard that happens to fit mechanically. According to Commodore's documents, something like a VGA-only jumper was meant to be realised there, but that was never implemented. We connected a USB socket, fixed on a slot bracket, to this header. That is what the photo shows. It is only a connector and has no USB function.

The device that Chris programmed does not talk to any USB hardware. It only simulates a few inputs, lets the mouse pointer wander across the screen and makes a few lines of text appear.

| What the announcement suggested | What it really was |
|---|---|
| A USB port made from the J975 header | A USB socket on a slot bracket, wired to a header that only fits mechanically |
| A wrapper that redirects the accesses of a known USB card | A device by Chris Hodges that only simulates a few inputs |
| USB 1.1 for mice and keyboards | The pointer moves by itself and a few lines of text appear |
| An experiment that needed a name | The name is a pun: "do NOP" |

### Background

The announcement was written in the style of a serious experiment: findings that should be published, a collaborator who could not decide, a trick to get software running, and a wrapper that was still to be packed. All of this was part of the joke. One claim in the announcement is true: according to Commodore's documents, registers of Denise can be influenced through this header. It was meant for something like a VGA-only jumper, which was never implemented. The header is still **not** suitable for USB.

### Project History

Chris Hodges compiled a fitting `donop.device` for the Poseidon stack, and together we published the joke on 1 April 2010 in the A1K forum. I posted the logo "=DONOP=" and a video of a (fake) use of the device in the forum.

### Technical Description

There is no real USB technology in DONOP.

- **Hardware:** A USB socket on a slot bracket, connected to the internal header J975 of the Amiga 4000D.
- **Software:** The fake device `donop.device`, compiled by Chris Hodges for the Poseidon USB stack. It simulates a few inputs, moves the mouse pointer across the screen and displays a few lines of text.

Please do not connect real USB devices to the header.


### Version History

| Version | Date | Notes |
|---------|------|-------|
| Announcement | 2010-04-01 | April Fools' joke in the A1K forum, with `donop.device`, logo and video |

---

## Deutsch

### Übersicht

Am 1. April 2010 erschien im A1K-Forum eine Ankündigung, der Amiga 4000D könne über seine interne Steckleiste J975 einen einfachen USB-Anschluss bekommen. Die Ankündigung war ein Aprilscherz, den sich Chris Hodges, der Entwickler des Amiga-USB-Stacks Poseidon, und ich ausgedacht hatten. Wegen des Veröffentlichungsdatums war er als Scherz erkennbar.

Der Name ist ein Wortspiel: „DONOP“ steht für „do NOP“, also „tue keine Operation“ (NOP ist der Prozessorbefehl, der nichts tut).

### Was es wirklich war

J975 ist nicht dafür ausgelegt, USB-Geräte anzuschließen. Es ist lediglich ein Anschluss auf dem Mainboard, der zufällig mechanisch passt. Laut den Commodore-Unterlagen sollte dort einmal so etwas wie ein VGA-Only-Jumper verwirklicht werden, was aber nie umgesetzt wurde. Wir haben eine USB-Buchse, die auf einem Slotblech befestigt ist, mit dieser Steckleiste verbunden. Das zeigt das Foto. Es ist nur ein Stecker und hat keine USB-Funktion.

Das Device, das Chris programmiert hat, spricht mit keiner USB-Hardware. Es simuliert nur ein paar Eingaben, lässt den Mauszeiger über den Bildschirm wandern und ein paar Zeilen Text auf dem Bildschirm erscheinen.

| Was die Ankündigung nahelegte | Was es wirklich war |
|---|---|
| Ein USB-Anschluss aus der Steckleiste J975 | Eine USB-Buchse auf einem Slotblech, verdrahtet mit einer Steckleiste, die nur mechanisch passt |
| Ein Wrapper, der die Zugriffe einer bekannten USB-Karte umleitet | Ein Device von Chris Hodges, das nur ein paar Eingaben simuliert |
| USB 1.1 für Mäuse und Tastaturen | Der Zeiger bewegt sich von allein, und ein paar Zeilen Text erscheinen |
| Ein Experiment, das einen Namen brauchte | Der Name ist ein Wortspiel: „do NOP“ |

### Hintergrund

Die Ankündigung war im Stil eines ernsthaften Experiments geschrieben: Erkenntnisse, die veröffentlicht werden sollten, ein Mitstreiter, der sich nicht entscheiden konnte, ein Trick, um Software ans Laufen zu bringen, und ein Wrapper, der noch gepackt werden musste. All das war Teil des Scherzes. Eine Aussage der Ankündigung stimmt: Laut den Commodore-Unterlagen lassen sich über diese Steckleiste Register von Denise beeinflussen. Gedacht war sie für so etwas wie einen VGA-Only-Jumper, der nie umgesetzt wurde. Für USB ist die Steckleiste trotzdem **nicht** geeignet.

### Projektgeschichte

Chris Hodges hat damals passend das `donop.device` für den Poseidon-Stack kompiliert, und wir haben den Scherz am 1. April 2010 gemeinsam im A1K-Forum veröffentlicht. Ich habe das Logo „=DONOP=“ und ein Video eines (Fake-)Einsatzes des Devices im Forum gepostet.

### Technische Beschreibung

In DONOP steckt keine echte USB-Technik.

- **Hardware:** Eine USB-Buchse auf einem Slotblech, verbunden mit der internen Steckleiste J975 des Amiga 4000D.
- **Software:** Das Fake-Device `donop.device`, von Chris Hodges für den Poseidon-USB-Stack kompiliert. Es simuliert ein paar Eingaben, lässt den Mauszeiger über den Bildschirm wandern und ein paar Zeilen Text anzeigen.

Bitte keine echten USB-Geräte an die Steckleiste anschließen.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Ankündigung | 2010-04-01 | Aprilscherz im A1K-Forum, mit `donop.device`, Logo und Video |

---

## Gallery / Galerie

<!-- TODO: Das Logo "=DONOP=" wird nachgereicht (Ablage in images/). Das Foto ist sehr klein (150 × 113 Pixel); eine größere Version wäre gut. Link zum Video des (Fake-)Einsatzes im Forum ergänzen. -->

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| `donop.device` (fake device for the Poseidon stack / Fake-Device für den Poseidon-Stack) | – | 2010-04-01 | A1K forum |

<!-- TODO: Download-Link zum donop.device ergänzen. -->

---

## References / Quellen

- A1K forum, announcement of 2010-04-01

https://www.a1k.org/forum/index.php?threads/21189/

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-11</sub>
