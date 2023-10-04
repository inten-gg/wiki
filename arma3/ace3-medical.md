---
title: ACE 3 Medical Guide
description: 
published: true
date: 2023-10-04T00:33:32.907Z
tags: 
editor: markdown
dateCreated: 2023-10-03T23:08:14.877Z
---

> Status: Work in Progress
{.is-info}


# ACE 3 Medical

## Allgemein

...

### Verletzungsarten

Verletzungsarten und ihre Behandlung.

|  | Schürfwunde | Avulsion | Prellung | Quetschung | Schnittwunde | Platzwunde | Ballistisches Trauma | Stichwunde |
| - | - | - | - | - | - | - | - | - |
| Verbandspäckchen | ✅ 100% | ❌ 20% | ✅ 100% | ✅ 100% | 🟠 30% |🟡 60% |❌ 20% |🟠 30% |
| Mullbinde | ✅ 100% | ✅ 100% | ✅ 100% | ✅ 100% | ❌ 20% | ❌ 20% | ✅ 100% | ❌ 20% |
| Elastische Bandage | ✅ 100% | ❌ 20% | ✅ 100% | ✅ 100% | ✅ 100% | ✅ 100% | 🟠 40% | 🟢 75% |
| QuickClot | 🟡 60% | 🟢 75% | 🟡 60%  | 🟡 60%  | 🟡 60% | 🟡 60% | 🟢 75% | 🟢 75% |
{.matable}


### Injektoren

| Injektor | Wirkung | Gefahren |
| - | - | - |
| Epinephrin | ↑ Puls (ca. 15 Schläge/min), könnte Spieler aus Bewusstlosigkeit holen | bei Herzstillstand tödlich |
| Morphin | ↓ Puls + ↓ Blutdruck + ↓ Schmerzen (ca. 55 Schläge/min) | maximal 2 Injektionen in 15 Minuten, Injektion bei niedrigem Puls/Blutdruck vermeiden |
| Atropin Bandage | ↓ Puls | - |
{.matable}

### IVs

Intravenöser Zugang. Alle IVs haben die selbe Wirkung.
IVs im Stückvolumen 250ml sind vergleichsweise sinnlos, nur 500ml oder 1l mitführen.

| IV | Blutdruck | Blutvolumen |
| - | - | - |
| Bluttransfusion | ↑ | ↑ |
| Plasmatransfusion  | ↑ | ↑ |
| Kochsalzlösung | ↑ | ↑ |
{.matable}

### Gegenstände

| Gegenstand | Wirkung | Voraussetzung | Gefahren | 
| - | - | - | - |
| Tourniquet | Stoppt Blutungen | Verursacht Schmerzen nach ca. 5 Minuten |
| Operationskit | Schließt schließt sich wiederholt öffnende Wunden | stabil | maximal 2 Injektionen in 15 Minuten, Injektion bei niedrigem Puls/Blutdruck vermeiden |
| Triagekarte | Enthält wichtige Informationen (Vor Verabreichung von Autoinjektionen unbedingt prüfen, enthält Infos über IVs, Autoinjektionen uvm) | - | - |
| Erste-Hilfe-Kasten | Vollständige Heilung + beendet Bewusstlosigkeit, stabilisiert, neutralisiert Autoinjektionen, löscht Triagekarte | stabil, in Fahrzeug / Medical Facility | - |
{.matable}


## Behandlungsablauf

<div style="float: left; width: 50%;">

**Priorisierung**

Muss mehr als ein Patient behandelt werden, sollte priorisiert werden, um einen Patienten in kritischer Lage zu erkennen und zuerst zu behandeln.

<div style="padding: 1rem;">
  
```mermaid
flowchart TD
    Start[Eingang] --> Puls{Puls\nvorhanden?}
    Puls -- Ja --> Ansprechbar{Ansprechbar?}
    Puls -- Nein --> Prio1[Prio 1]
    Ansprechbar -- Ja --> Prio3[Prio 3]
    Ansprechbar -- Nein --> Prio2[Prio 2]
    Prio1 --> Behandlung
    Prio2 --> Behandlung
    Prio3 --> Behandlung
		class Prio1 fc-node-red
    class Prio2 fc-node-orange
    class Prio3 fc-node-green
```
  
</div>
  
</div>

<div style="float: right; width: 50%;">

**Behandlung**

<div style="padding: 1rem;">  
  
```mermaid
flowchart TD
    Start[Start] --> Material{Ausreichend\nMaterial?}
    Material -- Ja --> Ansprechbar{Ansprechbar?}    
    Material -- Nein --> Nope[Keine Behandlung]
    Nope --> Ende
    Ansprechbar -- Ja --> Question[Befragung, schnelle Untersuchung]    
    Ansprechbar -- Nein --> CompleteSearch[Vollständige Untersuchung]
    Question --> VieleBlutungen
    CompleteSearch --> VieleBlutungen{Blutungen\nan Extremitäten?}
    VieleBlutungen -- Ja --> Tourniquets[Tourniquets anlegen]
    VieleBlutungen -- Nein --> Torso[Kopf und Körperstamm verbinden]
    Tourniquets --> Torso
    Torso --> Extreminaeten[Extremitäten verbinden]
    Extreminaeten --> TourniquetsDel[Tourniquets entfernen]
    TourniquetsDel --> Stitch[Wunden vernähen]
    Stitch --> PulsAfterStitch{Puls\nvorhanden?}
    PulsAfterStitch -- Ja --> Pain{Schmerzen?}
    PulsAfterStitch -- Nein --> CPR[CPR anordnen]
    CPR --> BloodPressure
    Pain -- Ja --> Morphium
    Pain -- Nein --> BloodPressure[Blutdruck <100/50]
    Morphium --> BloodPressure
    BloodPressure -- Ja --> IVs    
    BloodPressure -- Nein --> PulseAfterBloodPressure{Puls <60?}
    IVs --> PulseAfterBloodPressure
    PulseAfterBloodPressure -- Ja --> EpiniphrinDecision{Epiniphrin\nverabreicht?}
    EpiniphrinDecision -- Ja --> EpiniphrinDelay
    EpiniphrinDecision -- Nein --> Epiniphrin[Epiniphrin verabreichen\nWirken lassen]
    PulseAfterBloodPressure -- Nein --> EndCPR[PCR einstellen] --> WaitGreen{Einsatztauglich?}
    WaitGreen -- Ja --> Green[Patient entlassen]
    WaitGreen -- Nein --> Wait(Warten) --> WaitGreen
    Green --> Ende
    Epiniphrin --> EpiniphrinDelay{Bewirkte\nPulserhöhung}
    EpiniphrinDelay -- Ja --> PulseAfterBloodPressure
    EpiniphrinDelay -- Nein --> Dead[Patient für tot erklären]
    Dead --> Ende
```  

</div>
  
</div>

<span style="clear:both;">&nbsp;</span>
