# Terminologi

| Begrepp | Svensk förklaring | Första kapitel | Kommentar |
|---|---|---:|---|
| Manuell produktionsdrift | Drift där viktiga produktionsmoment utförs för hand, exempelvis genom checklistor, kommandon eller manuella kontroller. | 1 | Används för att visa nulägesproblem. |
| Personberoende | När organisationens leverans- eller återställningsförmåga beror på enskilda personers erfarenhet eller närvaro. | 1 | Centralt chefsbegrepp. |
| Leveransflöde | Kedjan från ändringsbehov till testad och driftsatt funktion i produktion. | 1 | Återkommer i kapitel 6. |
| Styrbar leverans | Ett leveranssätt där organisationen kan följa, kontrollera, upprepa och förbättra vägen till produktion. | 1 | Bärande målbild. |
| Container | En isolerad och standardiserad körmiljö där en applikation kan köras tillsammans med de beroenden den behöver. | 2 | Centralt begrepp från kapitel 2. |
| Image | En paketerad mall som innehåller applikationen och de delar som behövs för att starta den som en container. | 2 | Viktigt för spårbarhet och återkommer i kapitel 5. |
| Kubernetes | En vanlig plattform för att orkestrera containeriserade applikationer i större miljöer. | 4 | Introduceras på chefsnivå, inte som installationshandbok. |
| Podman | Ett verktyg för att bygga, köra och hantera containrar och container images. | 4 | Används som exempel på verktyg nära utveckling och teknikteam. |
| Körmiljö | Den tekniska miljö där en applikation körs, inklusive resurser, inställningar och beroenden som påverkar beteendet. | 2 | Används för att förklara skillnader mellan miljöer. |
| Miljöparitet | Strävan efter att utveckling, test och produktion ska vara så lika att testresultat blir tillförlitliga. | 2 | Behandlas mer i kapitel 8. |
| Plattform | En gemensam teknisk och organisatorisk förmåga som gör det möjligt att köra och förvalta applikationer på ett standardiserat sätt. | 3 | Centralt begrepp från kapitel 3. |
| Standardisering | Gemensamma regler, mönster och lösningar som minskar variation, undantag och personberoende. | 3 | Viktigt chefsbegrepp. |
| Driftmodell | Hur ansvar, arbetssätt, verktyg och beslut organiseras för att hålla IT-stöd fungerande, säkra och förvaltningsbara över tid. | 3 | Återkommer i kapitel 10 och 12. |
| Container runtime | Den del som faktiskt startar och kör containrar på en maskin. | 4 | Hålls på översiktlig nivå. |
| Orchestration | Samordning av många containrar, exempelvis placering, uppdatering, återstart och resurshantering. | 4 | Svensk förklaring: orkestrering. |
| Registry | En plats där container images lagras, hämtas och kontrolleras. | 4 | Behandlas mer i kapitel 5. |
| Versionering | Sätt att märka och skilja olika image-versioner från varandra så att organisationen vet exakt vad som testats och körs. | 5 | Viktigt för incidenthantering och revision. |
| Spårbarhet | Förmågan att följa en image från källa, byggtillfälle och test till godkännande och produktion. | 5 | Bärande begrepp i kapitel 5 och återkommer i kapitel 6, 11 och 13. |
| Grundimage | En image som andra images byggs vidare från, exempelvis med gemensamma tekniska baslager. | 5 | Viktig för säkerhet, standardisering och livscykelhantering. |
| Image-flöde | Vägen en image tar från byggande till lagring, test, godkännande och körning. | 5 | Kopplar kapitel 5 till kapitel 6 om pipelines. |
| Pipeline | Ett automatiserat eller delvis automatiserat flöde som bygger, testar, kontrollerar och levererar en ändring. | 6 | Centralt begrepp för vägen från ändring till produktion. |
| Automatiserad testning | Tester som körs maskinellt och återkommande som del av leveransflödet. | 6 | Behandlas mer i kapitel 8. |
| Kontrollerad produktionssättning | Produktionssättning där steg, ansvar, kontroller och beslut är tydliga och spårbara. | 6 | Viktigt mål för förändringsresan. |
| Kontrollpunkt | Ett definierat steg där flödet kontrollerar att ett krav är uppfyllt innan arbetet går vidare. | 6 | Används för att koppla pipeline till styrning och kvalitet. |
| Byggbarhet | Förmågan att bygga applikationen på ett upprepat, begripligt och kontrollerat sätt. | 7 | Centralt chefsbegrepp för att minska personberoende i utveckling och leverans. |
| Standardiserad applikationspaketering | Gemensamma regler för hur applikationer byggs, paketeras, konfigureras, startas och övervakas som images/containrar. | 7 | Kopplar utvecklingsarbete till plattform, test och förvaltning. |
| DevOps-samarbete | Tidigare och tydligare samverkan mellan utveckling, test, förvaltning, drift, säkerhet och plattform längs hela leveransflödet. | 7 | Används praktiskt, inte som modeord. |
| Reproducerbar testmiljö | En testmiljö som kan återskapas på ett förutsägbart sätt, med kända versioner, beroenden och konfiguration. | 8 | Minskar personberoende och stärker beslutsunderlag. |
| Teststrategi | En plan för hur organisationen får tillräcklig kunskap om kvalitet, risk och produktionsberedskap genom olika tester och kontroller. | 8 | Ska kopplas till pipeline, registry, plattform och förvaltning. |
| Testbarhet | Egenskap hos en applikation och dess leveransflöde som gör det möjligt att testa effektivt, upprepat och tillförlitligt. | 8 | Viktigt krav på både interna team och leverantörer. |
| Förvaltningsobjekt | Det samlade ansvar och innehåll som förvaltningen behöver styra, inklusive applikation, images, pipelines, tester, beroenden och plattformsanpassningar. | 9 | Breddas i boken från system i snäv mening till hela leverans- och körbarhetsförmågan. |
| Livscykelhantering | Aktiv styrning av hur tekniska delar föds, används, uppdateras och avvecklas över tid. | 9 | Centralt för images, grundimages, beroenden och plattformsanpassningar. |
| Beroendehantering | Ansvar och arbetssätt för att följa upp och uppdatera de komponenter som applikationen är beroende av. | 9 | Kopplar förvaltning till säkerhet och tekniskt underhåll. |
| Tekniskt underhåll | Planerat arbete för att hålla tekniska delar aktuella, säkra, körbara och förvaltningsbara. | 9 | Ska synliggöras i förvaltningsplanering och prioritering. |
| Plattformsdrift | Drift av den gemensamma containerplattformens hälsa, kapacitet, standarder, uppgraderingar, policyer och gemensamma övervakning. | 10 | Skiljs från applikationsdrift. |
| Applikationsdrift | Driftansvar kopplat till ett specifikt IT-stöd, exempelvis funktion, loggar, integrationer, konfiguration, versioner och tillgänglighet. | 10 | Kräver samspel mellan applikationsteam och plattformsteam. |
| Observability | Förmågan att förstå ett systems tillstånd utifrån signaler som loggar, mätvärden och spårning. | 10 | Engelsk term används eftersom den är etablerad. |
| Självläkning | Plattformens förmåga att automatiskt hantera vissa fel, exempelvis genom återstart, omplacering eller återställning mot önskat läge. | 10 | Får inte tolkas som ansvarsfrihet. |
| Kapacitetsstyrning | Planering och uppföljning av hur gemensamma resurser används, fördelas och prioriteras mellan IT-stöd. | 10 | Viktigt i delade plattformar. |
| Supply chain-säkerhet | Kontroll över hela kedjan från kod, beroenden och byggflöden till godkänd image och körande produktion. | 11 | Svensk förklaring av software supply chain security. |
| Policy | En regel eller styrande princip som kan dokumenteras och, där det är möjligt, omsättas till teknisk kontroll. | 11 | Används både organisatoriskt och tekniskt. |
| Säkerhetsgrind | Kontrollpunkt i leveransflödet som stoppar eller varnar när säkerhetskrav inte är uppfyllda. | 11 | Används för att konkretisera säkerhetskontroller i pipeline, registry och plattform. |
| Regelefterlevnad | Förmågan att följa och visa att organisationen följer beslutade krav, regler och interna styrprinciper. | 11 | Kopplas till spårbarhet, uppföljning och revision. |
| Plattformsteam | Team med ansvar för den gemensamma containerplattformens förmåga, standarder, drift, uppgraderingar, policies och stöd till produktteam. | 12 | Ska ha tydligt mandat, inte bara tekniskt ansvar. |
| Produktteam | Team med ansvar för ett specifikt IT-stöds funktion, körbarhet, testbarhet, övervakning och förvaltningsbarhet. | 12 | Kan också kallas systemteam, applikationsteam eller förvaltningsteam beroende på organisation. |
| Ansvarsmodell | Beskriven och beslutad struktur för vem som ansvarar för vad, vem som får besluta och hur roller samverkar längs leveransflödet. | 12 | Bör kopplas till kod, image, pipeline, registry, plattform, produktion, säkerhet och förvaltning. |
| Mandat | Tydlig rätt att fatta beslut, sätta standarder eller prioritera inom ett ansvarsområde. | 12 | Viktigt för plattformsteam, förvaltning, säkerhet och produktteam. |
| Leveranskrav | Krav på hur leverantören ska leverera lösningen så att den kan tas emot, testas och driftsättas kontrollerat. | 13 | Kopplar upphandling till pipeline, test, image-hantering och produktionssättning. |
| Plattformskrav | Krav på hur lösningen ska passa in i myndighetens beslutade containerplattform och standarder. | 13 | Minskar behovet av speciallösningar och undantag. |
| Förvaltningsbarhet | Förmågan att hålla ett IT-stöd begripligt, uppdaterbart, driftbart och möjligt att ta över eller vidareutveckla över tid. | 13 | Centralt vid upphandling, avtal och leverantörsstyrning. |
| Leverantörslåsning | När myndigheten blir beroende av en viss leverantörs kunskap, verktyg, miljö eller arbetssätt på ett sätt som begränsar handlingsfriheten. | 13 | Kan vara teknisk, organisatorisk eller kunskapsmässig. |
| Exitkrav | Krav som ska göra det möjligt att byta leverantör, ta hem ansvar eller överlämna lösningen utan orimligt kunskapstapp. | 13 | Viktigt för långsiktig styrbarhet och beredskap. |
| Mognadsresa | Stegvis utveckling av organisationens förmåga från manuella arbetssätt till förvaltad plattformsförmåga. | 14 | Används för att visa att införandet är en långsiktig förändring. |
| Införandefärdplan | Samlad plan för hur teknik, ansvar, arbetssätt, säkerhet och förvaltning utvecklas över tid. | 14 | Bokens sammanfattande förändringsverktyg. |
| Styrbar förändring | Förändring där mål, principer, beslut, risker och uppföljning är tydliga och möjliga att leda. | 14 | Knyter ihop teknikinförande med chefens ansvar. |
| Pilot | Avgränsat införande som används för att pröva teknik, ansvar och arbetssätt innan bredare skalning. | 14 | Ska ge organisatoriskt lärande, inte bara teknisk bekräftelse. |
