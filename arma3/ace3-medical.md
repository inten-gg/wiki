---
title: ACE 3 Medical Guide
description: 
published: true
date: 2023-10-03T23:41:47.955Z
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
| Bluttransfusion | ↑ | ↑ |
| Bluttransfusion Bandage | ↑ | ↑ |
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


```mermaid
flowchart TD
    Start[Start] --> Puls{Puls vorhanden?}
    Puls -- Ja --> Ansprechbar{Ansprechbar?}
    Puls -- Nein --> Prio1[Prio 1]
    Ansprechbar -- Ja --> Prio3[Prio 3]
    Ansprechbar -- Nein --> Prio2[Prio 2]
    Prio1 --> Material
    Prio2 --> Material
    Prio3 --> Question[Abfragen, Reagieren]
    Question --> Material{Ausreichend Material?}
    Material -- Ja --> VieleBlutungen{Blutungen \nan Extremitäten?}
    Material -- Nein --> Nope[Keine Behandlung]
    Nope ---> Ende
    VieleBlutungen -- Ja --> Tourniquets[Tourniquets anlegen]
    VieleBlutungen -- Nein --> Torso[Kopf & Körperstamm verbinden]
    Tourniquets --> Torso
    Torso --> Extreminaeten[Extremitäten verbinden]
    Extreminaeten --> TourniquetsDel[Tourniquets entfernen]
    TourniquetsDel --> Stitch[Wunden vernähen]
    Stitch --> PulsAfterStitch{Puls vorhanden?}
    PulsAfterStitch -- Ja --> Pain{Schmerzen?}
    PulsAfterStitch -- Nein --> CPR
    CPR --> PulsAfterStitch
    Pain -- Ja --> Morphium
    Pain -- Nein --> BloodPressure[Blutdruck <100/50]
    Morphium --> BloodPressure
    BloodPressure -- Ja --> IVs    
    BloodPressure -- Nein --> PulseAfterBloodPressure{Puls <60?}
    IVs --> PulseAfterBloodPressure
    PulseAfterBloodPressure -- Ja --> Epiniphrin
    PulseAfterBloodPressure -- Nein ---> Ende
    Epiniphrin ---> Ende    
		class Prio1 fc-node-red
    class Prio2 fc-node-orange
    class Prio3 fc-node-green
```