# Projektstatus

## Bok

**Titel:** Containerteknik för chefer i offentlig sektor  
**Undertitel:** Att leda förändringen från manuell IT-drift till automatiserade, säkrare och mer förvaltningsbara plattformar  
**Språk:** Svenska  
**Författare:** Erland Lindmark  
**Version:** 1.5  
**Senast uppdaterad:** 2026-05-11

## Nuvarande fas

- [ ] Start/intervju
- [ ] Bokspecifikation
- [x] Kapitelplan
- [x] Kapitelgenerering
- [ ] Granskning
- [x] Export

## Kapitelstatus

| Kapitel | Titel | Status | Kommentar |
|---:|---|---|---|
| 1 | Från personberoende drift till styrbar leverans | Utkast | Första kapitel skapat. |
| 2 | Vad en container är – utan att börja med tekniken | Utkast | Andra kapitel skapat. |
| 3 | Från servrar till plattformar | Utkast | Tredje kapitel skapat. |
| 4 | Podman, Kubernetes och andra delar av ekosystemet | Utkast | Fjärde kapitel skapat. |
| 5 | Images, registries och spårbarhet | Utkast | Femte kapitel skapat. |
| 6 | Automation, pipelines och vägen till produktion | Utkast | Sjätte kapitel skapat. |
| 7 | Hur utvecklingsarbetet förändras | Utkast | Sjunde kapitel skapat. |
| 8 | Hur testarbetet förändras | Utkast | Åttonde kapitel skapat. |
| 9 | Hur förvaltningen förändras | Utkast | Nionde kapitel skapat. |
| 10 | Hur driften förändras | Utkast | Tionde kapitel skapat. |
| 11 | Säkerhet, regelefterlevnad och kontroll | Utkast | Elfte kapitel skapat. |
| 12 | Roller, ansvar och organisation | Utkast | Tolfte kapitel skapat. |
| 13 | Upphandling, leverantörer och kravställning | Utkast | Trettonde kapitel skapat. |
| 14 | Färdplanen – från nuläge till fungerande containerplattform | Utkast | Fjortonde kapitel skapat. Planerad kapitelstruktur komplett. |

## Introducerade begrepp

| Begrepp | Kapitel | Kort definition |
|---|---:|---|
| Manuell produktionsdrift | 1 | Drift där viktiga produktionsmoment utförs för hand. |
| Personberoende | 1 | När leverans- eller återställningsförmåga beror på specifika individer. |
| Leveransflöde | 1 | Kedjan från ändringsbehov till testad och driftsatt funktion. |
| Styrbar leverans | 1 | Leverans som kan följas, kontrolleras, upprepas och förbättras. |
| Container | 2 | Standardiserad körmiljö för en applikation och dess beroenden. |
| Image | 2 | Paketerad mall som används för att starta containrar. |
| Körmiljö | 2 | Teknisk miljö där en applikation körs. |
| Miljöparitet | 2 | Strävan efter likhet mellan utveckling, test och produktion. |
| Plattform | 3 | Gemensam teknisk och organisatorisk förmåga för att köra och förvalta applikationer standardiserat. |
| Standardisering | 3 | Gemensamma regler, mönster och lösningar som minskar variation och personberoende. |
| Driftmodell | 3 | Hur ansvar, arbetssätt, verktyg och beslut organiseras för att hålla IT-stöd fungerande över tid. |
| Container runtime | 4 | Den del som faktiskt startar och kör containrar på en maskin. |
| Orchestration | 4 | Samordning av många containrar, exempelvis placering, uppdatering och återstart vid fel. |
| Kubernetes | 4 | En plattform för att orkestrera containeriserade applikationer i större miljöer. |
| Podman | 4 | Ett verktyg för att bygga, köra och hantera containrar och images. |
| Registry | 4 | En plats där container images lagras, hämtas och kontrolleras. |
| Versionering | 5 | Sätt att märka och skilja olika image-versioner från varandra. |
| Spårbarhet | 5 | Förmågan att följa en image från källa, byggtillfälle och test till godkänd produktion. |
| Grundimage | 5 | En image som andra images byggs vidare från, exempelvis med gemensamma tekniska baslager. |
| Image-flöde | 5 | Vägen en image tar från byggande till lagring, test, godkännande och körning. |
| Pipeline | 6 | Ett automatiserat eller delvis automatiserat flöde som bygger, testar, kontrollerar och levererar en ändring. |
| Automatiserad testning | 6 | Tester som körs maskinellt och återkommande som del av leveransflödet. |
| Kontrollerad produktionssättning | 6 | Produktionssättning där steg, ansvar, kontroller och beslut är tydliga och spårbara. |
| Kontrollpunkt | 6 | Ett definierat steg där flödet kontrollerar att ett krav är uppfyllt innan arbetet går vidare. |
| Byggbarhet | 7 | Förmågan att bygga applikationen på ett upprepat, begripligt och kontrollerat sätt. |
| Standardiserad applikationspaketering | 7 | Gemensamma regler för hur applikationer byggs, paketeras, konfigureras, startas och övervakas som images/containrar. |
| DevOps-samarbete | 7 | Tidigare och tydligare samverkan mellan utveckling, test, förvaltning, drift, säkerhet och plattform. |
| Reproducerbar testmiljö | 8 | Testmiljö som kan återskapas på ett förutsägbart och kontrollerat sätt. |
| Teststrategi | 8 | Plan för hur organisationen får tillräcklig kunskap om kvalitet, risk och produktionsberedskap. |
| Testbarhet | 8 | Egenskap hos applikation och leveransflöde som gör det möjligt att testa effektivt och tillförlitligt. |
| Förvaltningsobjekt | 9 | Det samlade ansvar och innehåll som förvaltningen behöver styra, inklusive applikation, images, pipelines, tester, beroenden och plattformsanpassningar. |
| Livscykelhantering | 9 | Aktiv styrning av hur tekniska delar föds, används, uppdateras och avvecklas över tid. |
| Beroendehantering | 9 | Ansvar och arbetssätt för att följa upp och uppdatera de komponenter som applikationen är beroende av. |
| Tekniskt underhåll | 9 | Planerat arbete för att hålla tekniska delar aktuella, säkra, körbara och förvaltningsbara. |
| Plattformsdrift | 10 | Drift av den gemensamma containerplattformens hälsa, kapacitet, standarder, uppgraderingar och säkerhet. |
| Applikationsdrift | 10 | Driftansvar kopplat till ett specifikt IT-stöd och dess funktion, loggar, integrationer, konfiguration och tillgänglighet. |
| Observability | 10 | Förmågan att förstå ett systems tillstånd utifrån signaler som loggar, mätvärden och spårning. |
| Självläkning | 10 | Plattformens förmåga att automatiskt hantera vissa fel, exempelvis genom återstart eller omplacering av containrar. |
| Kapacitetsstyrning | 10 | Planering och uppföljning av hur gemensamma resurser används och prioriteras mellan IT-stöd. |
| Supply chain-säkerhet | 11 | Kontroll över kedjan från kod, beroenden och byggflöde till godkänd och körande produktionsversion. |
| Policy | 11 | En regel eller styrande princip som kan dokumenteras och, där det är möjligt, omsättas till teknisk kontroll. |
| Säkerhetsgrind | 11 | Kontrollpunkt som stoppar eller varnar när en leverans bryter mot beslutade säkerhetskrav. |
| Regelefterlevnad | 11 | Förmågan att följa och visa att organisationen följer beslutade krav, regler och interna styrprinciper. |
| Plattformsteam | 12 | Team med ansvar för den gemensamma containerplattformens förmåga, standarder, drift och stöd till andra team. |
| Produktteam | 12 | Team med ansvar för ett IT-stöds funktion, körbarhet, testbarhet, övervakning och förvaltningsbarhet. |
| Ansvarsmodell | 12 | Beskriven och beslutad struktur för vem som ansvarar för vad längs leveransflödet. |
| Mandat | 12 | Tydlig rätt att fatta beslut, sätta standarder eller prioritera inom ett ansvarsområde. |
| Leveranskrav | 13 | Krav på hur leverantören ska leverera lösningen så att den kan tas emot, testas och driftsättas kontrollerat. |
| Plattformskrav | 13 | Krav på hur lösningen ska passa in i myndighetens beslutade containerplattform och standarder. |
| Förvaltningsbarhet | 13 | Förmågan att hålla ett IT-stöd begripligt, uppdaterbart, driftbart och möjligt att ta över eller vidareutveckla över tid. |
| Leverantörslåsning | 13 | När myndigheten blir beroende av en viss leverantörs kunskap, verktyg, miljö eller arbetssätt på ett sätt som begränsar handlingsfriheten. |
| Exitkrav | 13 | Krav som ska göra det möjligt att byta leverantör, ta hem ansvar eller överlämna lösningen utan orimligt kunskapstapp. |
| Mognadsresa | 14 | Stegvis utveckling av organisationens förmåga från manuella arbetssätt till förvaltad plattformsförmåga. |
| Införandefärdplan | 14 | Samlad plan för hur teknik, ansvar, arbetssätt, säkerhet och förvaltning utvecklas över tid. |
| Styrbar förändring | 14 | Förändring där mål, principer, beslut, risker och uppföljning är tydliga och möjliga att leda. |
| Pilot | 14 | Avgränsat införande som används för att pröva teknik, ansvar och arbetssätt innan bredare skalning. |

## Öppna beslut

- Slutlig titel.
- Författarnamn.
- Om boken ska använda myndighetsnära faktarutor om regler, upphandling och informationssäkerhet.
- Om varje kapitel ska ha en kort checklista utöver reflektionsfrågorna.

## Nästa rekommenderade steg

- Genomför helhetsgranskning av samtliga kapitel.
- Kontrollera progression, terminologi och scenario.
- Komplettera vid behov med checklistor, bilagor och exportunderlag.

## Exportstatus

- EPUB skapad med författare: Erland Lindmark.
- Exportmetadata uppdaterad till version 1.5.
