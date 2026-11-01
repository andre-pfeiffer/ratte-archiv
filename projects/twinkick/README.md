# TwinKick / Dual-Kickstart environment for expanded Amiga 1000 systems, allowing selection between Kickstart versions during reset

## English

### Overview

TwinKick is a dual Kickstart environment developed for expanded Amiga 1000 systems.

Its goal is to combine the compatibility of the original Kickstart 1.3 environment with the functionality of newer Kickstart versions, allowing the user to select between multiple Kickstart versions after a reset.

---

### Background

Unlike later Amiga models, the Amiga 1000 does not contain a permanent Kickstart ROM. Instead, the operating system is loaded into a **Writable Control Store (WCS)**, also commonly known as **Write Once Memory (WOM)**.

Although this design offered considerable flexibility in 1985, it later became a limitation because newer Kickstart versions exceeded the available WCS capacity.

TwinKick was developed to extend the capabilities of the original Amiga 1000 without modifying its fundamental architecture.

---

### Project History

The origins of TwinKick date back to around 1992.

At that time my Amiga 1000 was equipped with a Roßmöller 2 MB memory expansion which did not support AutoConfig. To make use of the additional memory, the system required a specially modified Kickstart 1.3.

Based on this setup I developed a small loader written in GFA Basic. Its purpose was to load a second Kickstart image—initially Kickstart 2.05 (V37.210)—into the memory expansion and activate it by performing a software reset.

Although originally intended only for my own computer, this loader introduced the fundamental concept of switching between multiple Kickstart environments on the Amiga 1000.

During the following years this idea evolved into TwinKick.

A public version was finally released through Aminet in September 2002.

---

### Technical Description

TwinKick first loads a modified Kickstart 1.3 into the Amiga 1000 WCS.

During boot, this modified Kickstart examines the boot block of the inserted floppy disk. A dedicated TwinKick marker identifies a TwinKick boot disk.

If detected, the selected Kickstart image is loaded into Fast RAM and executed.

TwinKick supports memory expansions with and without AutoConfig.

After booting, the user may choose between different Kickstart environments during every reset.

When operating in Kickstart 1.3 mode, TwinKick can temporarily disable Fast RAM together with AutoConfig expansions such as hard disk controllers and external floppy drives. This creates a hardware environment that is much closer to an original unexpanded Amiga 1000 and improves compatibility with older software and games.

---

### Supported Kickstart Versions

Development history included several generations of Kickstart environments:

- Kickstart 2.05 (V37.210)
- Kickstart 3.1 (V40.063)
- Experimental community version based on Kickstart 3.9 (V45.60, never officially released)

---

### Gallery

Screenshots, photographs and development material will be added here.

---

### Release Information

Project start

- around 1992

Public release

- September 2002

Distribution

- Aminet

---

## Deutsch

### Übersicht

TwinKick ist eine Dual-Kickstart-Umgebung für erweiterte Amiga-1000-Systeme.

Ziel des Projekts ist es, die Kompatibilität des ursprünglichen Kickstart 1.3 mit den Möglichkeiten neuerer Kickstart-Versionen zu verbinden und dem Anwender nach einem Reset die Auswahl zwischen mehreren Kickstart-Versionen zu ermöglichen.

---

### Hintergrund

Im Gegensatz zu späteren Amiga-Modellen besitzt der Amiga 1000 kein fest eingebautes Kickstart-ROM. Stattdessen wird das Betriebssystem in einen **Writable Control Store (WCS)** geladen, der vielen Anwendern auch als **Write Once Memory (WOM)** bekannt ist.

Dieses Konzept bot 1985 eine hohe Flexibilität, wurde jedoch später zu einer Einschränkung, da neuere Kickstart-Versionen größer wurden als der vorhandene Speicher.

TwinKick entstand, um die Möglichkeiten des Amiga 1000 zu erweitern, ohne dessen ursprüngliche Architektur grundlegend zu verändern.

---

### Projektgeschichte

Die Ursprünge von TwinKick reichen bis etwa 1992 zurück.

Mein damaliger Amiga 1000 war mit einer Roßmöller-2-MB-Speichererweiterung ausgestattet, die noch kein AutoConfig unterstützte. Damit der zusätzliche Speicher genutzt werden konnte, war ein speziell angepasstes Kickstart 1.3 erforderlich.

Auf dieser Grundlage entwickelte ich einen kleinen Loader in GFA Basic. Seine Aufgabe bestand darin, ein zweites Kickstart – zunächst Kickstart 2.05 (V37.210) – in die Speichererweiterung zu laden und dieses anschließend durch einen Software-Reset zu aktivieren.

Obwohl dieses Programm ursprünglich nur für mein eigenes System gedacht war, entstand dabei die grundlegende Idee, mehrere Kickstart-Umgebungen auf einem Amiga 1000 nutzen und zwischen ihnen wechseln zu können.

Aus diesem Ansatz entwickelte sich TwinKick über die folgenden Jahre schrittweise weiter.

Die erste öffentliche Version wurde schließlich im September 2002 über Aminet veröffentlicht.

---

### Technische Beschreibung

TwinKick lädt zunächst ein modifiziertes Kickstart 1.3 in den WCS des Amiga 1000.

Während des Bootvorgangs untersucht dieses angepasste Kickstart den Bootblock der eingelegten Diskette. Anhand eines speziellen TwinKick-Kennzeichens erkennt das System, ob es sich um eine TwinKick-Startdiskette handelt.

Wird eine solche Diskette erkannt, wird das ausgewählte Kickstart in das Fast RAM geladen und von dort gestartet.

TwinKick unterstützt Speichererweiterungen mit und ohne AutoConfig.

Nach dem Systemstart kann der Anwender bei jedem Reset zwischen den verfügbaren Kickstart-Versionen wählen.

Im Kickstart-1.3-Modus besteht zusätzlich die Möglichkeit, Fast RAM sowie AutoConfig-Erweiterungen wie Festplattencontroller oder externe Diskettenlaufwerke temporär auszublenden. Dadurch entsteht eine Hardwarekonfiguration, die einem ursprünglichen Amiga 1000 deutlich näherkommt und die Kompatibilität zu älterer Software und Spielen verbessert.

---

### Unterstützte Kickstart-Versionen

Im Laufe der Entwicklung wurden verschiedene Kickstart-Versionen unterstützt:

- Kickstart 2.05 (V37.210)
- Kickstart 3.1 (V40.063)
- experimentelle Community-Version auf Basis von Kickstart 3.9 (V45.60, nie offiziell veröffentlicht)

---

### Bildergalerie

Hier sollen später Fotos, Screenshots und historische Entwicklungsunterlagen ergänzt werden.

---

### Veröffentlichungen

Projektbeginn

- ca. 1992

Erste Veröffentlichung

- September 2002

Verbreitung

- Aminet

---

### Quellen

Aminet

https://aminet.net/package/util/sys/twinkick
