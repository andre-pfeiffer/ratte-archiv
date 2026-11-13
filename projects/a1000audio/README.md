# A1000 Audio / Switchable audio low-pass filter for the Amiga 1000

> **EN:** A1000 Audio is my rebuild of a known Amiga 1000 hack: a small adapter that lets the power LED switch the audio low-pass filter, as on the Amiga 500 and later models. The sound is usually better, and a jumper keeps the filter on for old demos.
>
> **DE:** A1000 Audio ist mein Nachbau eines bekannten Amiga-1000-Hacks: ein kleiner Adapter, mit dem die Power-LED den Audio-Tiefpassfilter schalten kann, wie beim Amiga 500 und späteren Modellen. Der Klang wird meist besser, und ein Jumper hält den Filter für alte Demos dauerhaft eingeschaltet.

## Release Information / Eckdaten

| | |
|---|---|
| **Project start / Projektbeginn** | 2007-11 |
| **First release / Erste Veröffentlichung** | 2007-11-29 (my rebuild in the A1K forum / mein Nachbau im A1K-Forum) |
| **Latest version / Aktuelle Version** | *zu ergänzen / to be added* |
| **Platform / Plattform** | Amiga 1000 |
| **Type / Art** | Hardware (adapter for the CIA 8520); rebuild of a known hack / Nachbau eines bekannten Hacks |
| **Original / Vorlage** | "Commodore Amiga 1000 Low Pass Audio Filter Hack" (author unknown / Urheber unbekannt) |
| **Status** | *zu ergänzen / to be added* |
| **Distribution / Verbreitung** | A1K forum (layout for download); a finished prototype was offered for sale |
| **License / Lizenz** | Free to use; rebuild of a hack without a known author / Frei verwendbar; Nachbau eines Hacks ohne bekannten Urheber |
| **Related projects / Verwandte Projekte** | [Holzbrett](../holzbrett/) · [A1000 Audio Mixer](../a1000audiomixer/) |

---

## English

### Overview

On the Amiga 500 and later models, the state of the power LED controls the audio low-pass filter. The Amiga 1000 cannot do this. A1000 Audio adds this function: a small board takes the state of the power LED from the CIA 8520 and, if needed, routes the audio lines around the filter. The sound is usually better because the filter is no longer always in the audio path.

For old demos that play "uncontrolled" with the power LED, such as the Miami Vice demo, a jumper (or a switch) can keep the filter permanently on.

The modification is not my own invention. It is a rebuild of a known Amiga 1000 hack.

### Background

This is the rebuild of a known Amiga 1000 hack, "Commodore Amiga 1000 Low Pass Audio Filter Hack". I built it while working on my [Holzbrett](../holzbrett/) ("Holzbrett Edition" of the Amiga 1000), and I presented my rebuild on 29 November 2007 in the A1K forum thread of that project. The hack makes the A1000 audio filter switchable by the power LED, like on the A500 and later models. My own contribution is a better description of the build, using the IC4066.

The author of the original hack is not known. The hack can be found in many places on the internet, but nobody seems to have named its originator.

<!-- TODO: Anlass und Zusammenhang mit dem A1000 Audio Mixer ergänzen. -->

### Technical Description

The circuit follows the original hack. The details below come from the description of the original hack and from my announcement.

- The core of the circuit is the **CD4066B** (also written IC4066BE), a CMOS quad bilateral switch, that is, a four-fold analog/digital switch. The chip costs less than one euro.
- Apart from the chip, the circuit needs only a **0.1 µF ceramic capacitor**.
- The board is an adapter for the **CIA 8520 (U6P)**. It reads the state of the power LED from the CIA.
- A **four-wire connection** leads to four marked points on the mainboard. Brown-black and red-orange form two pairs: brown and red are soldered to the two IC pins, black and orange to the two solder points next to the IC. In the circuit description, the pins belong to the op-amp **TL084 (or LF347) at U5G**.
- A **jumper** selects the mode:
  - *Enabled:* the low-pass filter and the LED switch on, off or dim automatically, according to the state of the CIA.
  - *Disabled:* the low-pass filter is always in the audio circuit, even if the LED dims low or high.


### Features

- Audio filter switchable with the power LED, as on the Amiga 500
- Usually better sound, because the filter can be bypassed
- Jumper or switch to keep the filter permanently on for old demos
- Very cheap: the main chip costs less than one euro
- The board can also be etched from the published layout

### Requirements

- Amiga 1000
- CD4066B (IC4066BE), a 0.1 µF ceramic capacitor, a jumper or switch, wires and the board
- Soldering skills

### Installation and Usage

1. Build the board from the published layout, or have it etched.
2. Plug the adapter onto the CIA 8520.
3. Solder the four wires to the marked points on the mainboard (see above).
4. Set the jumper (or switch) to the wanted mode.

**Disclaimer.** I accept no liability for damage to your hardware, as always.

### Version History

| Version | Date | Notes |
|---------|------|-------|
| My rebuild | 2007-11-29 | Announced in the A1K forum with a better description; layout published |

---

## Deutsch

### Übersicht

Beim Amiga 500 und späteren Modellen steuert der Zustand der Power-LED den Audio-Tiefpassfilter. Der Amiga 1000 kann das nicht. A1000 Audio ergänzt diese Funktion: Eine kleine Platine holt sich den Zustand der Power-LED vom CIA 8520 und führt die Audioleitungen bei Bedarf am Filter vorbei. Der Klang wird in der Regel besser, weil der Filter nicht mehr dauernd im Audiopfad liegt.

Für alte Demos, die „unkontrolliert“ mit der Power-LED spielen, zum Beispiel die Miami-Vice-Demo, kann ein Jumper (oder Schalter) den Filter dauerhaft einschalten.

Die Erweiterung ist nicht meine eigene Erfindung. Es ist der Nachbau eines bekannten Amiga-1000-Hacks.

### Hintergrund

Das ist der Nachbau eines bekannten Amiga-1000-Hacks, „Commodore Amiga 1000 Low Pass Audio Filter Hack“. Ich habe ihn bei der Arbeit an meinem [Holzbrett](../holzbrett/) („Holzbrett Edition“ des Amiga 1000) gebaut und meinen Nachbau am 29. November 2007 im A1K-Forenthread zu diesem Projekt vorgestellt. Der Hack macht den Audiofilter des A1000 wie beim A500 und späteren Modellen per Power-LED schaltbar. Mein eigener Beitrag ist die bessere Beschreibung des Aufbaus mit dem IC4066.

Der Urheber des Original-Hacks ist nicht bekannt. Der Hack ist an vielen Stellen im Internet zu finden, aber anscheinend hat niemand seinen Urheber genannt.

### Technische Beschreibung

Die Schaltung folgt dem Original-Hack. Die Angaben unten stammen aus der Beschreibung des Original-Hacks und aus meiner Vorstellung.

- Kernstück der Schaltung ist der **CD4066B** (auch IC4066BE geschrieben), ein CMOS-Vierfachschalter, also ein 4-fach analog/digital Schalter. Der Baustein kostet unter einem Euro.
- Außer dem Baustein braucht die Schaltung nur einen **0,1-µF-Keramikkondensator**.
- Die Platine ist ein Adapter für den **CIA 8520 (U6P)**. Sie liest den Zustand der Power-LED aus dem CIA.
- Eine **Vierdraht-Verbindung** führt zu vier markierten Punkten auf dem Mainboard. Braun-Schwarz und Rot-Orange bilden zwei Paare: Braun und Rot werden mit den beiden IC-Beinchen verlötet, Schwarz und Orange mit den beiden Lötpunkten neben dem IC. In der Schaltungsbeschreibung gehören die Beinchen zum Operationsverstärker **TL084 (oder LF347) an U5G**.
- Ein **Jumper** wählt den Modus:
  - *Enabled:* Der Tiefpassfilter und die LED schalten sich automatisch ein, aus oder dimmen, entsprechend dem Zustand des CIA.
  - *Disabled:* Der Tiefpassfilter liegt immer im Audiopfad, auch wenn die LED hoch oder niedrig dimmt.

### Funktionen

- Audiofilter mit der Power-LED schaltbar, wie beim Amiga 500
- Meist besserer Klang, weil der Filter umgangen werden kann
- Jumper oder Schalter, um den Filter für alte Demos dauerhaft eingeschaltet zu lassen
- Sehr günstig: Der Hauptbaustein kostet unter einem Euro
- Die Platine lässt sich auch nach dem veröffentlichten Layout ätzen

### Voraussetzungen

- Amiga 1000
- CD4066B (IC4066BE), ein 0,1-µF-Keramikkondensator, ein Jumper oder Schalter, Draht und die Platine
- Löterfahrung

### Installation und Verwendung

1. Die Platine nach dem veröffentlichten Layout bauen oder ätzen lassen.
2. Den Adapter auf den CIA 8520 stecken.
3. Die vier Drähte an die markierten Punkte auf dem Mainboard löten (siehe oben).
4. Den Jumper (oder Schalter) auf den gewünschten Modus stellen.

**Haftungsausschluss.** Ich übernehme wie immer keine Haftung für Schäden an eurer Hardware.

### Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Mein Nachbau | 2007-11-29 | Im A1K-Forum mit besserer Beschreibung vorgestellt, Layout veröffentlicht |

---

## Gallery / Galerie

<!-- TODO: Fotos des Adapters, der Verdrahtung und des Einbaus nachreichen (Ablage in images/). -->

---

## Downloads

| File / Datei | Version | Date / Datum | Source / Quelle |
|---|---|---|---|
| [8520-Layout (8520.zip)](http://www.a1k.org/download/area51/OLD/8520/8520.zip) | – | 2007-11 | A1K forum download area |

---

## References / Quellen

- A1K forum, "Amiga 1000 - Holzbrett Edition (Ratte)", page 10 (announcement of 2007-11-29): 

https://www.a1k.org/forum/index.php?threads/6745/page-10#post-127301
