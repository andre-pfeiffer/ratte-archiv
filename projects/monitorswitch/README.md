# automatic Monitorswitch / Ratte Switch
# MonitorSwitch / Automatic switching between native Amiga video and RTG graphics

> **EN:** MonitorSwitch is a hardware solution that automatically switches one monitor between the native Amiga video output (for example an Indivision flicker fixer) and an RTG graphics card. The software SwitchControl controls it.
>
> **DE:** MonitorSwitch ist eine Hardwarelösung, die einen Monitor automatisch zwischen der nativen Amiga-Bildausgabe (zum Beispiel einem Indivision-FlickerFixer) und einer RTG-Grafikkarte umschaltet. Gesteuert wird sie von der Software SwitchControl.

## Release Information / Eckdaten

| | |
|---|---|
| **Also known as / Auch bekannt als** | Ratte Switch, Ratte Auto Switch |
| **Project start / Projektbeginn** | 2009-05 (first forum post 2009-05-09) |
| **First release / Erste Veröffentlichung** | 2011-04 (final series version, presented 2011-04-03) |
| **Latest version / Aktuelle Version** | Final series 2011; add-ons until 2015 / Serienversion 2011; Zusätze bis 2015 |
| **Platform / Plattform** | Amiga with native video output (ECS/AGA) and an RTG graphics card |
| **Type / Art** | Hardware + Software |
| **Status** | Completed / Abgeschlossen |
| **Distribution / Verbreitung** | Kits and assembled units from various users in several Amiga forums; build instructions in Amiga Future |
| **License / Lizenz** | Open source, free to use and to publish anywhere / Open Source, frei verwendbar, darf überall publiziert werden |
| **Related projects / Verwandte Projekte** | [SwitchControl](../switchcontrol/) · [Radeon Switch](../radeonswitch/) · [HighGFX](../highgfx/) |

---

## English

### Overview

Many Amiga systems have two video sources: the native chipset output (AGA/ECS, often through a flicker fixer such as the Indivision) and an RTG graphics card. Normally you need two monitors, or you have to swap the monitor cable by hand. MonitorSwitch connects both sources to a single monitor and switches between them automatically. A standard 17" PC monitor is sufficient.

The switch is controlled by the software [SwitchControl](../switchcontrol/). It must be started from the Startup-Sequence. How SwitchControl works is described on its own page.

### Background

In 2009 my Amiga 4000 changed. Before, it had a CompServ AGA FlickerFixer and a CyberVision 64. Now it had an Indivision AGA (a prototype from individual Computers, which I received on 7 February 2009 in exchange for my HighGFX software), a Mediator PCI busboard and a Radeon 9200 with 64 MB. I suddenly had two high-quality picture sources, but the monitor had only one VGA input.

The idea was not entirely new. The forum member **chkamiga** had already built a switch for graphics cards, and his project was the groundwork for mine. Without it, I might never have had the idea. What motivated me in the end was to automate the switching. The forum members supported me again and again during the implementation.

### Project History

**Planning (May 2009).** On 9 May 2009 I started a thread in the A1K forum, "Prototype – Monitorswitch für Indivision4000", and asked the hardware people for their opinion. I had looked at two existing designs: on the Picasso, the switch uses three relays (G6H-2-100), and chkamiga's circuit uses an LT1675 for RGB and a 4053 for the sync signals. My first idea for the control line, CIA-B pin 18, turned out to be unusable because the port is in constant use. The serial port was the better choice: the modem era was over, and the lines could simply be blocked and used. On 30 May 2009 I considered the STMAV340 for the first time, a chip commonly used in PC video equipment.

**Prototype 1 (June 2009).** Built with the components from chkamiga's design. A local electronics technician made the board in the old way, with an exposure and an etching bath, from my layout printed on overhead foil. I drilled the holes for the through-hole parts myself and soldered the components. I assembled two identical boards in case something broke. I posted the first photos on 23 June 2009. The first test run on 26 June 2009 worked, with manual switching between Indivision and Radeon. The board was mainly intended for software experiments.

**Software (July to August 2009).** On 13 July 2009 I posted a first small test tool that evaluates screen mode changes. On 23 August 2009 I rewrote the code completely, and from 26 August 2009 SwitchControl 1.0 was available. See the [SwitchControl](../switchcontrol/) page.

**Prototype 2 (October to November 2009).** I started the design with the STMAV340 on 18 October 2009. The basic design was finished on 24 October, including a special prototype for the Radeon. Both are carrier boards for a piggyback switch module with the STMAV340 and the STG719. On 2 November 2009, all boards were designed and ordered from PCB-Pool, and I received them on 17 November. Prototype 2 was finished on 30 November 2009.

**Pre-series (2010).** For the final versions I dropped the module concept and soldered the components directly. The pre-series was presented, assembled, on 22 September 2010. The PCB was 99.9 % final. It is labelled "Monitorswitch 2010-11 Ratte A1K.org", which was only my guess at the delivery date, because I had never dealt with a PCB manufacturer before and did not know the lead time. A layout error connects the SELECT line to ground, which is easy to fix with a cutter or a rotary tool.

**Final series (April 2011).** The final version was presented in the forum on 3 April 2011. The underside is labelled "AMIGA – Monitorswitch", "www.amigafuture.de / www.a1k.org" and "Andre 'Ratte' Pfeiffer 2011".

**Build instructions in a magazine (2011).** The soldering workshop "VGA-Monitorswitch zum selberlöten" (Parts 1 and 2) appeared in the printed magazine Amiga Future, issues 92 (dated September/October 2011) and 93. It presents the final version and covers the complete DIY process for assembling a switch yourself.

**Add-ons (2012 to 2015).** See the table below. The Radeon version has its own page: [Radeon Switch](../radeonswitch/).

### Technical Description

MonitorSwitch consists of a hardware circuit and the software SwitchControl.

**Switching**

- The red, green and blue lines are switched by an **STMAV340**, a bidirectional quad SPDT video switch (4.0 to 5.5 V, 300 MHz bandwidth, about 4 Ω on-resistance). The circuit is based on the STMAV340 evaluation board schematic. Port A goes to the monitor, ports B and C are the two sources, for example Indivision and Radeon.
- HSync and VSync are switched by one **STG719** each.
- Audio is not switched.
- The idea of the circuit comes from the PC world, where the STMAV340 is widely used.

**Control signal**

- The circuit receives a high or low level from the CIA port chip (8520). It is the **CTS line** of the serial port. A line that is actually meant as an input is used as an output.
- The signal is tapped directly at the 8520 CIA chip and not behind the bus drivers, so there is no conflict with the operating system.
- SwitchControl detects whether a graphics card mode or a native Amiga mode is in front and sets the line high or low accordingly.

**Connection**

- The switch board is mounted in the computer case, for example on a slot bracket.
- A small adapter that is plugged **upside down** onto the SMD 8520 CIA takes off three lines: +5 V, ground and the CTS control signal. These go to the switch. In the Amiga 4000D the CIA to use is U300, in the Amiga 4000T it is U560 (according to highpuff).
- On the monitor side, the VGA connector carries the common output.

<!-- TODO: Pinbelegung der Anschlüsse, Pegel der CTS-Leitung, Bauteilwerte, genaue Stückliste (Fundorte im A1K-Forum). -->

### Hardware Versions

| Version | Size | Date | Notes |
|---|---|---|---|
| Prototype 1 | 41 × 100 mm | 2009-06 | Components from chkamiga's design (LT1675, 4053); board made by a local technician; through-hole assembly by me; two identical boards |
| Prototype 2 | 48 × 41 mm | 2009-10 to 2009-11 | Piggyback module with STMAV340 and STG719 on a carrier board; manufactured by PCB-Pool; finished 2009-11-30 |
| Radeon prototype | n/a | design 2009-10-24 | Same module on a special carrier board for the Radeon |
| Pre-series | 36 × 31 mm | presented 2010-09-22 | Components soldered directly; labelled "2010-11"; SELECT line wrongly connected to ground |
| Final series | 36 × 31 mm | presented 2011-04-03 | Labelled "Andre 'Ratte' Pfeiffer 2011" |
| Radeon version | n/a | 2014 | Plugs directly onto the VGA port of the Radeon, see [Radeon Switch](../radeonswitch/) |

### Add-ons

| Date | Add-on | Notes |
|---|---|---|
| 2012-03-06 | SwitchHack | Tool for AmigaOS 4: switches once, hard, to the graphics card during boot (see [SwitchControl](../switchcontrol/)) |
| 2013-01-11 | MK2 adapter (first design) | Plugs onto the switch; boards ordered 2013-05-10, presented with pictures 2013-05-25 |
| 2015-10-09 | MK2cr adapter cable (prototype) | Finished connection cable presented 2015-10-25 |
| 2015-10-30 | CIA connector | Board with a socket instead of wires soldered to the CIA pins; holds better and is more reliable |
| 2015-10-31 | Tristate switch (design) | Possible use: native Amiga, graphics card and PC bridge card |

All designs are by me and, as always, free: schematics and layouts are published. highpuff built these add-ons and offered them together with the switches. He later added an MK3 adapter and a switch based entirely on DVI/HDMI technology himself.

### Distribution

I built about 20 units myself, so that I could keep the material cost down by buying other quantities, and to supply the beta testers of SwitchControl with hardware. It was non-profit. I do not know the total number of units. Various users in various Amiga forums offered kits and assembled units. highpuff stands out for his very good, careful instructions.

The switch was tested by a larger number of users in the community. It quickly became clear that it works without problems with every graphics card, so no list of card types is needed. highpuff's later test on his website sums it up: "It just works!"

### Requirements

- An Amiga with a native video output, for example with an Indivision, and an RTG graphics card
- A monitor with a VGA input; a standard 17" PC monitor is enough
- The MonitorSwitch board and the CIA adapter
- The software [SwitchControl](../switchcontrol/), started from the Startup-Sequence

### Installation and Usage

1. Mount the switch board in the case.
2. Plug the CIA adapter onto the CIA chip. Make sure the orientation is correct.
3. Connect the video cables of the two sources to the correct ports of the switch (see the safety note below), and connect the monitor.
4. Install SwitchControl and start it from the Startup-Sequence.
5. The monitor now follows the front screen: native Amiga modes use the native source, graphics card modes use the RTG card.

**Safety note.** Connect the correct graphics signal to the correct port. A wrong connection can damage your Amiga. Cables are different for each source: for example, highpuff points out that a DCE scandoubler has a different pinout than the CyberVision PPC, so its cable must not be used for the other.

### Hardware Documentation

| Item | Link |
|---|---|
| Schematic | *to be added* (A1K forum) |
| Board layout | *to be added* (A1K forum) |
| Parts list | *to be added* (A1K forum) |
| Pinout | *to be added* |

---

## Deutsch

### Übersicht

Viele Amiga-Systeme haben zwei Bildquellen: die native Chipsatz-Ausgabe (AGA/ECS, oft über einen FlickerFixer wie den Indivision) und eine RTG-Grafikkarte. Normalerweise braucht man zwei Monitore, oder man muss das Monitorkabel von Hand umstecken. MonitorSwitch verbindet beide Quellen mit einem einzigen Monitor und schaltet automatisch um. Ein normaler 17"-PC-Bildschirm genügt.

Gesteuert wird der Switch von der Software [SwitchControl](../switchcontrol/). Sie muss in der Startup-Sequence gestartet werden. Die Funktionsweise von SwitchControl steht auf der eigenen Seite.

### Hintergrund

2009 veränderte sich mein Amiga 4000. Vorher hatte er einen CompServ AGA FlickerFixer und eine CyberVision 64. Jetzt hatte er einen Indivision AGA (ein Prototyp von individual Computers, den ich am 7. Februar 2009 im Austausch gegen meine HighGFX-Software erhielt), ein Mediator-PCI-Busboard und eine Radeon 9200 mit 64 MB. Plötzlich standen zwei hochwertige Bildquellen zur Verfügung, aber der Monitor hatte nur einen VGA-Eingang.

Die Idee war nicht ganz neu. Das Forenmitglied **chkamiga** hatte bereits einen Umschalter für Grafikkarten gebaut, und sein Projekt war die Vorarbeit für meines. Ohne sein Projekt wäre ich vielleicht gar nicht auf die Idee gekommen. Was mich am Ende motivierte, war das Umschalten zu automatisieren. Die Forenmitglieder haben mich bei der Umsetzung immer wieder unterstützt.

### Projektgeschichte

**Planung (Mai 2009).** Am 9. Mai 2009 eröffnete ich im A1K-Forum den Thread „Prototype – Monitorswitch für Indivision4000“ und fragte die Hardware-Leute nach ihrer Meinung. Ich hatte zwei vorhandene Entwürfe angesehen: Auf der Picasso wird der Umschalter mit drei Relais (G6H-2-100) betrieben, und chkamigas Schaltung nutzt einen LT1675 für RGB und einen 4053 für die Sync-Signale. Meine erste Idee für die Steuerleitung, CIA-B Pin 18, erwies sich als unbrauchbar, weil der Port ständig benutzt wird. Der serielle Port war die bessere Wahl: Das Modemzeitalter war vorbei, und die Leitungen ließen sich einfach blockieren und nutzen. Am 30. Mai 2009 erwog ich erstmals den STMAV340, einen Baustein, der im PC-Bereich häufig verwendet wird.

**Prototyp 1 (Juni 2009).** Gebaut mit den Bauteilen aus chkamigas Entwurf. Ein örtlicher Elektroniker fertigte die Platine auf die alte Art mit Belichtung und Ätzbad aus meinem auf Overheadfolie gedruckten Layout. Die Löcher für die bedrahteten Bauteile habe ich selbst gebohrt und die Bauteile aufgelötet. Ich habe zwei identische Platinen bestückt, falls etwas kaputtgeht. Die ersten Fotos habe ich am 23. Juni 2009 gepostet. Der erste Testlauf am 26. Juni 2009 funktionierte, mit manueller Umschaltung zwischen Indivision und Radeon. Die Platine war in erster Linie für Softwareexperimente gedacht.

**Software (Juli bis August 2009).** Am 13. Juli 2009 stellte ich ein erstes kleines Testprogramm vor, das Bildschirmmodus-Wechsel auswertet. Am 23. August 2009 habe ich den Code komplett umgeworfen, und ab dem 26. August 2009 gab es SwitchControl 1.0. Siehe die Seite [SwitchControl](../switchcontrol/).

**Prototyp 2 (Oktober bis November 2009).** Am 18. Oktober 2009 begann ich den Entwurf mit dem STMAV340. Am 24. Oktober war das Grunddesign fertig, dabei auch ein spezieller Prototyp für die Radeon. Beide sind Trägerplatinen für ein Huckepack-Schaltmodul mit dem STMAV340 und dem STG719. Am 2. November 2009 waren alle Platinen fertig entworfen und bei PCB-Pool bestellt, am 17. November erhielt ich sie. Prototyp 2 war am 30. November 2009 fertig.

**Vorserie (2010).** Für die finalen Versionen habe ich das Modulkonzept verworfen und die Bauteile direkt verlötet. Die Vorserie wurde am 22. September 2010 bestückt vorgestellt. Die Platine war zu 99,9 % final. Sie trägt die Aufschrift „Monitorswitch 2010-11 Ratte A1K.org“. Das war nur meine Schätzung des Liefertermins, weil ich noch nie mit einem Platinenfertiger zu tun hatte und die Laufzeit nicht kannte. Ein Layoutfehler verbindet die SELECT-Leitung mit Masse, was sich mit Cutter oder Dremel leicht beheben lässt.

**Finale Serie (April 2011).** Die finale Version wurde am 3. April 2011 im Forum vorgestellt. Die Unterseite trägt die Aufschrift „AMIGA – Monitorswitch“, „www.amigafuture.de / www.a1k.org“ und „Andre ‚Ratte‘ Pfeiffer 2011“.

**Bauanleitung in der Zeitschrift (2011).** Der Lötworkshop „VGA-Monitorswitch zum selberlöten“ (Teil 1 und 2) erschien im Printmagazin Amiga Future, in den Ausgaben 92 (datiert auf September/Oktober 2011) und 93. Er stellt die finale Version vor und behandelt den kompletten DIY-Prozess, mit dem man sich selbst einen Switch bestückt.

**Zusätze (2012 bis 2015).** Siehe die Tabelle unten. Die Radeon-Version hat eine eigene Seite: [Radeon Switch](../radeonswitch/).

### Technische Beschreibung

MonitorSwitch besteht aus einer Hardwareschaltung und der Software SwitchControl.

**Umschaltung**

- Die Leitungen Rot, Grün und Blau schaltet ein **STMAV340**, ein bidirektionaler Vierfach-SPDT-Videoschalter (4,0 bis 5,5 V, 300 MHz Bandbreite, rund 4 Ω Durchlasswiderstand). Die Schaltung ist an das Schaltbild des STMAV340-Evaluation-Boards angelehnt. Port A geht zum Monitor, die Ports B und C sind die beiden Quellen, zum Beispiel Indivision und Radeon.
- HSync und VSync schaltet je ein **STG719**.
- Audio wird nicht umgeschaltet.
- Die Schaltungsidee stammt aus dem PC-Bereich, in dem der STMAV340 weit verbreitet ist.

**Steuersignal**

- Die Schaltung erhält ein High- oder Low-Signal vom CIA-Portbaustein (8520). Es ist die **CTS-Leitung** der seriellen Schnittstelle. Eine eigentlich als Eingang vorgesehene Leitung wird als Ausgang verwendet.
- Das Signal wird direkt am 8520-CIA abgegriffen und nicht hinter den Bustreibern, damit es keinen Konflikt mit dem Betriebssystem gibt.
- SwitchControl erkennt, ob ein Grafikkartenmodus oder ein nativer Amiga-Modus im Vordergrund ist, und setzt die Leitung entsprechend auf High oder Low.

**Anschluss**

- Die Switch-Platine wird im Rechnergehäuse montiert, zum Beispiel an einem Slotblech.
- Ein kleiner Adapter, der **kopfüber** auf den SMD-8520-CIA gesteckt wird, greift drei Leitungen ab: +5 V, Masse und das CTS-Steuersignal. Sie führen zum Switch. Im Amiga 4000D ist der CIA U300, im Amiga 4000T U560 (laut highpuff).
- Auf der Monitorseite führt der VGA-Anschluss den gemeinsamen Ausgang.

### Hardwareversionen

| Version | Größe | Datum | Hinweise |
|---|---|---|---|
| Prototyp 1 | 41 × 100 mm | 2009-06 | Bauteile aus chkamigas Entwurf (LT1675, 4053); Platine von einem örtlichen Elektroniker; THT-Bestückung durch mich; zwei identische Platinen |
| Prototyp 2 | 48 × 41 mm | 2009-10 bis 2009-11 | Huckepack-Modul mit STMAV340 und STG719 auf Trägerplatine; von PCB-Pool gefertigt; fertig am 2009-11-30 |
| Radeon-Prototyp | – | Entwurf 2009-10-24 | Gleiches Modul auf spezieller Trägerplatine für die Radeon |
| Vorserie | 36 × 31 mm | vorgestellt 2010-09-22 | Bauteile direkt verlötet; Aufdruck „2010-11“; SELECT-Leitung fälschlich mit Masse verbunden |
| Finale Serie | 36 × 31 mm | vorgestellt 2011-04-03 | Aufschrift „Andre ‚Ratte‘ Pfeiffer 2011“ |
| Radeon-Version | – | 2014 | Steckt direkt auf dem VGA-Port der Radeon, siehe [Radeon Switch](../radeonswitch/) |

### Zusätze

| Datum | Zusatz | Hinweise |
|---|---|---|
| 2012-03-06 | SwitchHack | Tool für AmigaOS 4: schaltet beim Booten einmal hart auf die Grafikkarte um (siehe [SwitchControl](../switchcontrol/)) |
| 2013-01-11 | MK2-Adapter (erster Entwurf) | Wird auf den Switch gesteckt; Platinen bestellt am 2013-05-10, mit Bildern vorgestellt am 2013-05-25 |
| 2015-10-09 | MK2cr-Adapterkabel (Prototyp) | Fertiges Anschlusskabel am 2015-10-25 vorgestellt |
| 2015-10-30 | CIA-Connector | Platine mit Sockel statt an die CIA-Beinchen gelöteter Kabel; hält besser und ist zuverlässiger |
| 2015-10-31 | Tristate-Switch (Entwurf) | Mögliche Anwendung: nativer Amiga, Grafikkarte und PC-Brückenkarte |

Alle Entwürfe stammen von mir und sind wie immer frei: Schaltpläne und Layouts sind veröffentlicht. highpuff hat diese Zusätze angefertigt und zusammen mit den Switches angeboten. Später hat er selbst einen MK3-Adapter und einen Switch komplett in DVI/HDMI-Technik ergänzt.

### Verbreitung

Ich habe etwa 20 Stück selbst gebaut, um die Materialkosten über andere Gebindegrößen niedrig zu halten und um die Beta-Tester von SwitchControl mit Hardware zu versorgen. Es war nicht profitorientiert. Die Gesamtstückzahl kenne ich nicht. Verschiedene Nutzer in verschiedenen Amiga-Foren boten Bausätze und bestückte Geräte an. highpuff fällt durch seine sehr guten, gewissenhaften Anleitungen auf.

Der Switch wurde von einer größeren Zahl von Nutzern in der Community getestet. Es war schnell klar, dass er mit jeder Grafikkarte problemlos funktioniert, deshalb braucht es keine Liste einzelner Kartentypen. Der spätere Test von highpuff auf seiner Website bringt es auf den Punkt: „It just works!“

### Voraussetzungen

- Ein Amiga mit nativer Bildausgabe, zum Beispiel mit einem Indivision, und eine RTG-Grafikkarte
- Ein Monitor mit VGA-Eingang; ein normaler 17"-PC-Bildschirm genügt
- Die MonitorSwitch-Platine und der CIA-Adapter
- Die Software [SwitchControl](../switchcontrol/), gestartet aus der Startup-Sequence

### Installation und Verwendung

1. Die Switch-Platine im Gehäuse montieren.
2. Den CIA-Adapter auf den CIA-Chip stecken. Dabei auf die richtige Ausrichtung achten.
3. Die Videokabel der beiden Quellen an die richtigen Anschlüsse des Switches stecken (siehe Sicherheitshinweis) und den Monitor anschließen.
4. SwitchControl installieren und aus der Startup-Sequence starten.
5. Der Monitor folgt nun dem vordersten Screen: Native Amiga-Modi nutzen die native Quelle, Grafikkartenmodi die RTG-Karte.

**Sicherheitshinweis.** Das richtige Grafiksignal muss an den richtigen Anschluss. Ein falscher Anschluss kann den Amiga beschädigen. Die Kabel sind für jede Quelle anders: highpuff weist zum Beispiel darauf hin, dass ein DCE-Scandoubler eine andere Belegung hat als die CyberVision PPC, deshalb darf dessen Kabel nicht für die jeweils andere Quelle verwendet werden.

### Hardware-Dokumentation

| Inhalt | Link |
|---|---|
| Schaltplan | *zu ergänzen* (A1K-Forum) |
| Platinenlayout | *zu ergänzen* (A1K-Forum) |
| Stückliste | *zu ergänzen* (A1K-Forum) |
| Anschlussbelegung | *zu ergänzen* |

---

## Gallery / Galerie

<!-- TODO: Fotos werden nachgereicht (Ablage in images/): Prototyp 1 (geätzte Platine), Prototyp 2 mit Modul, Vorserie, finale Serie, Aufschrift der Platinenunterseite, CIA-Adapter und CIA-Connector, Einbau im Amiga 4000, MK2-Adapter. -->

---

## References / Quellen

- A1K forum thread "Prototype – Monitorswitch für Indivision4000" (the 2009 development thread): <https://www.a1k.org/forum/index.php?threads/16232/>
- A1K forum thread "Automatischer Monitorumschalter (Ratte)": <https://www.a1k.org/forum/index.php?threads/19230/>
- A1K forum project thread with later posts (2011 to 2015): <https://www.a1k.org/forum/index.php?threads/26275/>
- A1K forum thread on the MK2 adapter: <https://www.a1k.org/forum/index.php?threads/35627/>
- Amiga Future issues 92 and 93, "VGA-Monitorswitch zum selberlöten", Parts 1 and 2: <https://www.amigafuture.de/app.php/kb/viewarticle?a=4688>
- highpuff, "Ratte Auto Switch", iKod.se, 2015-05-01: <https://www.ikod.se/ratte-auto-switch/>
- highpuff, project category on iKod.se: <https://www.ikod.se/category/projects/ratte-auto-monitor-switch/>
- mfilos Computers & Consoles blog, "auto vga switch": <http://www.mfilos.com/search/label/auto%20vga%20switch>
- STMicroelectronics, STMAV340: <https://www.st.com/en/switches-and-multiplexers/stmav340.html>

---

## Notes / Hinweise

**EN:** The name "Ratte Switch" is used on the internet as well. It goes back to my community nickname and crept into everyday use; it is not an official project name. Thanks to chkamiga for the groundwork, to Jens Schönfeld of individual Computers for the Indivision AGA prototype, to the A1K forum members for their support, and to highpuff for his tests, instructions and kits.

**DE:** Im Internet ist auch vom „Ratte Switch“ die Rede. Der Name geht auf meinen Community-Nick zurück und hat sich im Alltagsgebrauch eingeschlichen; er ist keine offizielle Projektbezeichnung. Dank an chkamiga für die Vorarbeit, an Jens Schönfeld von individual Computers für den Indivision-AGA-Prototyp, an die Mitglieder des A1K-Forums für ihre Unterstützung und an highpuff für Tests, Anleitungen und Bausätze.

---

<sub>Project page last updated / Seite zuletzt aktualisiert: 2026-11-07</sub>
