# automatic Monitorswitch / Ratte Switch

MonitorSwitch is an hardware and software solution for automatic switching between the native Amiga video output and RTG graphics cards.

MonitorSwitch ermöglicht die automatische Umschaltung zwischen der nativen Amiga-Bildausgabe und RTG-Grafikkarten.

---

# English

## Background

With the increasing use of RTG graphics cards in Amiga systems, many users faced the problem of needing separate monitors or manual switching solutions.

A typical Amiga setup could contain both:

- the native Amiga chipset output (AGA/ECS)
- an additional RTG graphics card

Switching between these two video sources usually required manually changing cables or using external monitor switches.

I developed MonitorSwitch to automate this process and allow both video sources to be used with one monitor.

---

## Development History

The first versions of MonitorSwitch were developed around 2009.

The initial goal was to create an automatic switching solution for Amiga systems equipped with RTG graphics cards.

The concept was designed for systems where the graphics card itself did not provide an integrated monitor switch.

The solution was later adapted for different hardware configurations, including:

- BVision
- CyberVision
- Voodoo based PCI graphics solutions
- Radeon PCI graphics cards
- Indivision based setups

The control software SwitchControl was developed to provide automatic switching from the Amiga operating system.

The hardware received further improvements over time, including compatibility adjustments for different Amiga models and graphics configurations.

In 2014, the Radeon version was revised and reduced in size while keeping the same functionality. It allowed automatic switching between an Indivision Mk2 output and Radeon graphics output.

---

## Technical Description

MonitorSwitch consists of two parts:

- a hardware switching circuit
- software control through SwitchControl

The hardware switches the video signal path between two sources.

Typical configurations include:

- native Amiga RGB/AGA output
- Indivision scan doubler/flicker fixer output
- RTG graphics card output

The software sends the required switching signal from the Amiga system.

SwitchControl can be used to automatically change the active video source depending on the running environment.

It was also extended with experimental DPMS support to reduce possible synchronisation problems during switching.

---

## Features

- Automatic switching between Amiga native video and RTG graphics
- Support for different Amiga graphics solutions
- Hardware-based video switching
- Software controlled operation through SwitchControl
- Suitable for systems with only one connected monitor
- Designed for ECS and AGA Amiga systems with additional graphics hardware

---

## Version History

| Version | Date | Notes |
|---------|------|-------|
| Initial MonitorSwitch | 2009 | First automatic monitor switching experiments |
| Hardware revisions | 2010–2013 | Adaptations for additional graphics solutions |
| SwitchControl | 2013 | Extended software control and DPMS experiments |
| Radeon Switch revision | 2014 | Smaller hardware revision for Radeon systems |

---

# Deutsch

## Hintergrund

Mit der zunehmenden Verbreitung von RTG-Grafikkarten im Amiga-Bereich entstand das Problem, dass viele Systeme sowohl die native Amiga-Grafikausgabe als auch eine zusätzliche Grafikkarte verwendeten.

Ein typisches System verfügte beispielsweise über:

- die native ECS- oder AGA-Ausgabe
- eine zusätzliche RTG-Grafikkarte

Um zwischen beiden Bildquellen umzuschalten, mussten häufig Kabel manuell umgesteckt oder externe Umschalter verwendet werden.

Ich entwickelte MonitorSwitch, um diesen Vorgang zu automatisieren und beide Bildquellen mit einem einzigen Monitor nutzen zu können.

---

## Entwicklungsgeschichte

Die ersten Versionen von MonitorSwitch entstanden ab etwa 2009.

Die ursprüngliche Idee war ein automatischer Umschalter für Amiga-Systeme mit RTG-Grafikkarten, die keinen eigenen Monitorumschalter besaßen.

Die Lösung wurde anschließend für verschiedene Hardware-Konfigurationen angepasst.

Unterstützte Einsatzbereiche waren unter anderem:

- BVision
- CyberVision
- Voodoo-basierte PCI-Grafikkarten
- Radeon PCI-Grafikkarten
- Indivision-basierte Systeme

Zur Steuerung wurde die Software SwitchControl entwickelt. Diese übernimmt die Kommunikation zwischen Amiga-System und Umschalthardware.

Im Laufe der Entwicklung wurden verschiedene Hardwareversionen erstellt, um die Lösung an unterschiedliche Amiga-Modelle und Grafikkonfigurationen anzupassen.

2014 entstand eine überarbeitete Radeon-Version, die gegenüber der ursprünglichen Hardware kompakter aufgebaut wurde und weiterhin automatisch zwischen Indivision-Mk2-Ausgabe und Radeon-Grafikausgabe umschalten konnte. :chatgpt-content-reference{index="3"}

---

## Technische Beschreibung

MonitorSwitch besteht aus zwei Komponenten:

- einer Hardware-Umschaltelektronik
- der Steuerungssoftware SwitchControl

Die Hardware übernimmt das eigentliche Umschalten der Videosignale.

Typische Kombinationen sind:

- native Amiga RGB/AGA-Ausgabe
- Indivision Scan-Doubler/Flicker-Fixer-Ausgabe
- RTG-Grafikkarten-Ausgabe

Die Umschaltung wird durch Signale des Amiga-Systems ausgelöst.

SwitchControl ermöglicht die automatische Steuerung aus dem Betriebssystem heraus.

Zusätzlich wurden Erweiterungen wie experimentelle DPMS-Unterstützung integriert, um mögliche Synchronisationsprobleme beim Umschalten zu reduzieren. :chatgpt-content-reference{index="4"}

---

## Funktionen

- Automatische Umschaltung zwischen Amiga-Ausgabe und RTG-Grafik
- Unterstützung verschiedener Grafikkartenlösungen
- Hardwarebasierte Videosignal-Umschaltung
- Softwaresteuerung über SwitchControl
- Nutzung eines einzigen Monitors für mehrere Bildquellen
- Erweiterbar für verschiedene Amiga-Konfigurationen

---

## Versionsgeschichte

| Version | Datum | Beschreibung |
|---------|-------|--------------|
| Erste MonitorSwitch-Version | 2009 | Erste automatische Umschaltlösungen |
| Hardware-Weiterentwicklungen | 2010–2013 | Anpassungen für verschiedene Grafikkarten |
| SwitchControl | 2013 | Erweiterte Softwaresteuerung und DPMS-Tests |
| Radeon Switch Überarbeitung | 2014 | Kompaktere Hardwareversion für Radeon-Systeme |

---

# Gallery / Galerie

## Photos

(Bilder der Platinen, Verkabelungen und eingebauten Systeme hier einfügen)

## Screenshots

(Screenshots von SwitchControl oder Workbench-Konfigurationen hier einfügen)

## Diagrams

(Schaltpläne und Anschlussdiagramme hier ergänzen)

---

### Downloads

https://www.a1k.org/forum/index.php?threads/16232/

---

# References / Quellen

- a1k.org Forum - MonitorSwitch Projektthread
- Dokumentationen und Veröffentlichungen aus der Amiga-Gemeinschaft
- Amiga-News Berichte zu MonitorSwitch und SwitchControl

---

# Notes / Hinweise

MonitorSwitch entstand aus der praktischen Erfahrung mit Amiga-Systemen, die gleichzeitig native Chipset-Grafik und RTG-Grafikhardware verwenden.

Die Entwicklung stand dabei in engem Zusammenhang mit weiteren Grafikprojekten wie Radeon, RadeonSwitch und SwitchControl.
