# Containerteknik för chefer i offentlig sektor

**Undertitel:** Att leda förändringen från manuell IT-drift till automatiserade, säkrare och mer förvaltningsbara plattformar

**Författare:** Erland Lindmark

Detta är ett arbetsprojekt för en svensk lärobok/förändringsguide om containerteknik för chefer och beslutsfattare i statlig myndighet.

Projektet är tänkt att kompletteras kapitel för kapitel. Nuvarande version innehåller:

- bokspecifikation
- kapitelplan
- pedagogisk canon
- terminologi
- projektstatus
- exportmetadata
- kapitel 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13 och 14

## Rekommenderat arbetssätt

1. Läs `docs/bokspecifikation.md`.
2. Använd `docs/kapitelplan.md` som styrande plan.
3. Kontrollera `docs/pedagogisk-canon.md` innan nya kapitel skrivs.
4. Skriv nya kapitel i `chapters/`.
5. Uppdatera `docs/projektstatus.md`, `docs/terminologi.md` och `docs/pedagogisk-canon.md` efter varje kapitel.

## Mappstruktur

```text
book-project/
├── README.md
├── docs/
│   ├── bokspecifikation.md
│   ├── kapitelplan.md
│   ├── pedagogisk-canon.md
│   ├── terminologi.md
│   ├── projektstatus.md
│   └── export-metadata.yaml
├── chapters/
│   ├── 01-fran-personberoende-drift-till-styrbar-leverans.md
│   ├── 02-vad-en-container-ar-utan-att-borja-med-tekniken.md
│   ├── 03-fran-servrar-till-plattformar.md
│   ├── 04-podman-kubernetes-och-andra-delar-av-ekosystemet.md
│   ├── 05-images-registries-och-sparbarhet.md
│   ├── 06-automation-pipelines-och-vagen-till-produktion.md
│   ├── 07-hur-utvecklingsarbetet-forandras.md
│   ├── 08-hur-testarbetet-forandras.md
│   ├── 09-hur-forvaltningen-forandras.md
│   ├── 10-hur-driften-forandras.md
│   ├── 11-sakerhet-regelefterlevnad-och-kontroll.md
│   ├── 12-roller-ansvar-och-organisation.md
│   ├── 13-upphandling-leverantorer-och-kravstallning.md
│   └── 14-fardplanen-fran-nulage-till-fungerande-containerplattform.md
├── exercises/
├── examples/
├── code/
└── exports/
```

## Nuvarande version

Version 1.5 innehåller samtliga 14 planerade kapitel i utkastform samt uppdaterad exportmetadata med författare och EPUB-export.. Nästa rekommenderade steg är helhetsgranskning, kompletterande checklistor och eventuell export.
