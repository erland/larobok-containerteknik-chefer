# Kapitelplan

## Övergripande progression

Boken går i fyra steg:

1. Förstå varför förändringen behövs.
2. Förstå containerteknik på chefsnivå.
3. Förstå påverkan på utveckling, test, förvaltning och drift.
4. Leda förändringen i en statlig myndighet.

## Del 1: Varför containerteknik angår chefer

### Kapitel 1: Från personberoende drift till styrbar leverans

- **Syfte:** Visa varför containerteknik inte bör ses som en isolerad teknisk fråga, utan som en förändring av hur IT-stöd byggs, testas, driftsätts och förvaltas.
- **Läsarens förkunskaper:** Grundläggande förståelse för att organisationen har IT-system i produktion.
- **Nya huvudbegrepp:** manuell produktionsdrift, personberoende, leveransflöde.
- **Praktiskt scenario:** Myndigheten Nordverk har flera samhällsviktiga IT-stöd. Produktionssättning kräver manuella moment, långa checklistor och personer med informell kunskap.
- **Frågor:** Vilka produktionsmoment kräver i dag särskilda personer? Vilka delar av leveransen är dokumenterade men inte automatiserade? Var uppstår väntetider mellan utveckling, test, förvaltning och drift?
- **Svårighetsgrad:** Grundnivå.
- **Bygger vidare på:** Läsarens erfarenhet av organisationens nuvarande IT-förvaltning.

### Kapitel 2: Vad en container är – utan att börja med tekniken

- **Syfte:** Ge en begriplig chefsförklaring av containerbegreppet och varför paketering av applikationer förändrar leverans och ansvar.
- **Nya huvudbegrepp:** container, image, körmiljö.
- **Scenario:** Nordverk upptäcker att samma IT-stöd beter sig olika i utvecklingsmiljö, testmiljö och produktion.
- **Svårighetsgrad:** Grundnivå.
- **Bygger vidare på:** Problemen med manuell och miljöberoende drift från kapitel 1.

### Kapitel 3: Från servrar till plattformar

- **Syfte:** Förklara hur fokus flyttas från enskilda servrar till standardiserade plattformar.
- **Nya huvudbegrepp:** plattform, standardisering, driftmodell.
- **Scenario:** Nordverk har tidigare beställt servrar system för system. Nu diskuteras en gemensam containerplattform.
- **Svårighetsgrad:** Grundnivå.
- **Bygger vidare på:** Container som paketeringssätt.

## Del 2: Tekniken på chefsnivå

### Kapitel 4: Podman, Kubernetes och andra delar av ekosystemet

- **Syfte:** Ge en orientering i vanliga byggstenar utan att göra läsaren till teknisk specialist.
- **Nya huvudbegrepp:** container runtime, orchestration, Kubernetes.
- **Scenario:** Nordverks ledning möter begrepp som Podman, Docker, Kubernetes, OpenShift, registry och pipeline.
- **Svårighetsgrad:** Grundnivå.

### Kapitel 5: Images, registries och spårbarhet

- **Syfte:** Förklara varför container images och registries blir centrala för kontroll, spårbarhet och säkerhet.
- **Nya huvudbegrepp:** registry, versionering, spårbarhet.
- **Scenario:** Nordverk behöver kunna svara på vilken version av ett IT-stöd som körs, vem som godkänt den och varifrån den kommer.
- **Svårighetsgrad:** Grundnivå.

### Kapitel 6: Automation, pipelines och vägen till produktion

- **Syfte:** Visa hur containerteknik hänger ihop med automatiserade leveransflöden, test, kvalitetssäkring och produktionssättning.
- **Nya huvudbegrepp:** pipeline, automatiserad testning, kontrollerad produktionssättning.
- **Scenario:** Nordverk går från manuella överlämningar till ett flöde där kod byggs, testas, paketeras och förbereds för produktionssättning.
- **Svårighetsgrad:** Grundnivå.

## Del 3: Påverkan på utveckling, test, förvaltning och drift

### Kapitel 7: Hur utvecklingsarbetet förändras

- **Syfte:** Förklara hur utvecklingsteam påverkas när applikationer ska byggas, paketeras och levereras som containrar.
- **Nya huvudbegrepp:** byggbarhet, standardiserad applikationspaketering, DevOps-samarbete.
- **Scenario:** Nordverks utvecklingsteam behöver ta större ansvar för hur applikationen paketeras och fungerar i en standardiserad körmiljö.
- **Svårighetsgrad:** Grundnivå.

### Kapitel 8: Hur testarbetet förändras

- **Syfte:** Visa hur containerteknik kan göra test mer reproducerbart, men också kräver tydligare teststrategi.
- **Nya huvudbegrepp:** reproducerbar testmiljö, testautomation, miljöparitet.
- **Scenario:** Nordverk har problem med att fel uppstår i produktion trots att systemet fungerade i test.
- **Svårighetsgrad:** Grundnivå.

### Kapitel 9: Hur förvaltningen förändras

- **Syfte:** Förklara hur systemförvaltning påverkas när applikationer, miljöer, beroenden och uppdateringar blir mer standardiserade men också mer kontinuerliga.
- **Nya huvudbegrepp:** förvaltningsobjekt, livscykelhantering, beroendehantering.
- **Scenario:** Nordverks förvaltningsmodell bygger på årliga planeringscykler och tydliga överlämningar, men containerplattformen kräver tätare hantering.
- **Svårighetsgrad:** Grundnivå till erfaren.

### Kapitel 10: Hur driften förändras

- **Syfte:** Visa hur driftrollen förändras från manuell serverhantering till plattformsdrift, automation, övervakning och kapacitetsstyrning.
- **Nya huvudbegrepp:** plattformsdrift, observability, självläkning och skalning.
- **Scenario:** Nordverks driftorganisation går från manuell serverhantering till plattformskapacitet, larm, standarder och automatiserade driftsmönster.
- **Svårighetsgrad:** Grundnivå till erfaren.

## Del 4: Styrning, säkerhet och offentlig sektor

### Kapitel 11: Säkerhet, regelefterlevnad och kontroll

- **Syfte:** Förklara hur containerteknik påverkar säkerhet, regelefterlevnad, riskhantering och kontroll i en statlig myndighet.
- **Nya huvudbegrepp:** supply chain-säkerhet, policy, kontrollpunkt.
- **Scenario:** Nordverk behöver visa att containerplattformen leder till bättre spårbarhet och tydligare styrning.
- **Svårighetsgrad:** Erfaren.

### Kapitel 12: Roller, ansvar och organisation

- **Syfte:** Beskriva hur roller och ansvar behöver förändras när containerteknik införs.
- **Nya huvudbegrepp:** plattformsteam, produktteam, ansvarsmodell.
- **Scenario:** Den tekniska plattformen fungerar, men gamla ansvarsfördelningar skapar konflikter.
- **Svårighetsgrad:** Erfaren.

### Kapitel 13: Upphandling, leverantörer och kravställning

- **Syfte:** Ge chefer stöd i att ställa bättre krav vid upphandling, avrop, leverantörsstyrning och avtal.
- **Nya huvudbegrepp:** leveranskrav, plattformskrav, förvaltningsbarhet.
- **Scenario:** Nordverk ska upphandla vidareutveckling av ett viktigt IT-stöd och behöver krav på paketering, testbarhet, driftsättning och förvaltningsbarhet.
- **Svårighetsgrad:** Erfaren.

## Del 5: Att leda förändringsresan

### Kapitel 14: Färdplanen – från nuläge till fungerande containerplattform

- **Syfte:** Samla bokens innehåll i en praktisk förändringsmodell för chefer.
- **Nya huvudbegrepp:** mognadsresa, införandefärdplan, styrbar förändring.
- **Scenario:** Nordverk tar fram en flerårig färdplan med nulägesanalys, pilot, plattformsbeslut, kompetensutveckling, styrmodell, säkerhetskontroller och successiv migrering.
- **Svårighetsgrad:** Sammanfattande, grundnivå till erfaren.

## Progressionskontroll

Begrepp introduceras i följande huvudsakliga ordning:

1. manuell produktionsdrift
2. personberoende
3. leveransflöde
4. container
5. image
6. körmiljö
7. plattform
8. standardisering
9. container runtime
10. orchestration
11. registry
12. spårbarhet
13. pipeline
14. testautomation
15. miljöparitet
16. livscykelhantering
17. plattformsdrift
18. supply chain-säkerhet
19. ansvarsmodell
20. införandefärdplan

Det största nivåhoppet finns mellan kapitel 10 och 11, där boken går från drift till säkerhet och regelefterlevnad. Kapitel 11 bör därför inledas med repetition av image, registry, pipeline och plattform.


## Status

Samtliga 14 planerade kapitel har skapats i utkastform till och med version 1.4. Kapitelplanen bör nu användas som underlag för helhetsgranskning och eventuella kompletterande bilagor.
