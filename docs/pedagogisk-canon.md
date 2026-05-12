# Pedagogisk canon

## Språk

Svenska, med etablerade engelska tekniska termer där de är vedertagna. Första gången ett engelskt begrepp används ska det förklaras på svenska.

## Ton

Professionell, tydlig, pedagogisk och beslutsnära.

## Målgrupp

Chefer och beslutsfattare i statlig myndighet.

## Svårighetsgrad

Grundnivå med vissa erfarna avsnitt mot slutet.

## Återkommande scenario

**Myndigheten Nordverk**

Nordverk är en fiktiv statlig myndighet med flera samhällsviktiga IT-stöd. Organisationen har historiskt förlitat sig på manuella driftsrutiner, personberoende specialistkunskap och överlämningar mellan utveckling, test, förvaltning och drift.

## Centrala avgränsningar

Boken ska inte bli en installationshandbok. Den ska hjälpa läsaren att förstå, styra, kravställa och leda förändringen.

## Centrala teman

- Från personberoende till styrbarhet
- Från manuella moment till automation
- Från serverfokus till plattformsfokus
- Från överlämningar till sammanhängande leveransflöden
- Från tekniskt införande till organisatorisk förändring
- Från isolerad drift till gemensamt ansvar för utveckling, test, förvaltning och produktion

## Introducerade begrepp

| Begrepp | Första kapitel | Kort definition |
|---|---:|---|
| Manuell produktionsdrift | 1 | Drift där viktiga produktionsmoment utförs för hand av människor, ofta med checklistor, kommandon eller informell kunskap. |
| Personberoende | 1 | När organisationens förmåga att leverera eller återställa IT-stöd är beroende av specifika individers kunskap eller närvaro. |
| Leveransflöde | 1 | Kedjan från idé, ändring eller felrättning till testad och driftsatt funktion i produktion. |
| Styrbar leverans | 1 | Ett leveranssätt där organisationen kan följa, kontrollera, upprepa och förbättra vägen till produktion. |
| Container | 2 | En isolerad och standardiserad körmiljö där en applikation kan köras tillsammans med de beroenden den behöver. |
| Image | 2 | En paketerad mall som innehåller applikationen och de delar som behövs för att starta den som en container. |
| Körmiljö | 2 | Den tekniska miljö där en applikation körs, inklusive resurser, inställningar och beroenden som påverkar beteendet. |
| Miljöparitet | 2 | Strävan efter att utveckling, test och produktion ska vara så lika att testresultat blir tillförlitliga. |
| Plattform | 3 | En gemensam teknisk och organisatorisk förmåga som gör det möjligt att köra och förvalta applikationer på ett standardiserat sätt. |
| Standardisering | 3 | Gemensamma regler, mönster och lösningar som minskar variation, undantag och personberoende. |
| Driftmodell | 3 | Hur ansvar, arbetssätt, verktyg och beslut organiseras för att hålla IT-stöd fungerande, säkra och förvaltningsbara över tid. |
| Container runtime | 4 | Den del som faktiskt startar och kör containrar på en maskin. |
| Orchestration | 4 | Samordning av många containrar, exempelvis placering, uppdatering, återstart, resurser och önskat läge. |
| Kubernetes | 4 | En vanlig plattform för att orkestrera containeriserade applikationer i större miljöer. |
| Podman | 4 | Ett verktyg för att bygga, köra och hantera containrar och container images. |
| Registry | 4 | En plats där container images lagras och hämtas, och som kan fungera som kontrollpunkt i leveransflödet. |
| Versionering | 5 | Sätt att märka, skilja och följa olika image-versioner över tid. |
| Spårbarhet | 5 | Förmågan att följa en image från ursprung, byggtillfälle och test till godkännande och produktion. |
| Grundimage | 5 | En image som andra images byggs vidare från, ofta med gemensamma operativsystemnära lager eller standardiserad teknisk bas. |
| Image-flöde | 5 | Vägen en image tar genom byggande, lagring, test, kontroll, godkännande och körning. |
| Pipeline | 6 | Ett automatiserat eller delvis automatiserat flöde som bygger, testar, kontrollerar och levererar en ändring. |
| Automatiserad testning | 6 | Tester som körs maskinellt och återkommande som del av leveransflödet. |
| Kontrollerad produktionssättning | 6 | Produktionssättning där steg, ansvar, kontroller och beslut är tydliga och spårbara. |
| Kontrollpunkt | 6 | Ett definierat steg där flödet kontrollerar att ett krav är uppfyllt innan arbetet går vidare. |
| Byggbarhet | 7 | Förmågan att bygga applikationen på ett upprepat, begripligt och kontrollerat sätt utan personberoende lokala steg. |
| Standardiserad applikationspaketering | 7 | Gemensamma regler för hur applikationer byggs, paketeras, konfigureras, startas, loggar och övervakas som images/containrar. |
| DevOps-samarbete | 7 | Tidigare och tydligare samverkan mellan utveckling, test, förvaltning, drift, säkerhet och plattform längs hela leveransflödet. |
| Reproducerbar testmiljö | 8 | En testmiljö som kan återskapas på ett förutsägbart sätt, med kända versioner, beroenden och konfiguration. |
| Teststrategi | 8 | En plan för hur organisationen får tillräcklig kunskap om kvalitet, risk och produktionsberedskap genom olika tester och kontroller. |
| Testbarhet | 8 | Egenskap hos en applikation och dess leveransflöde som gör det möjligt att testa effektivt, upprepat och tillförlitligt. |

## Regler för kommande kapitel

- Introducera normalt högst 1–3 nya huvudbegrepp per kapitel.
- Använd inte tekniska begrepp som om de vore kända innan de förklarats.
- Koppla varje kapitel till Myndigheten Nordverk.
- Ersätt traditionella övningar med korta frågor att ställa i den egna organisationen.
- Visa konsekvenser för utveckling, test, förvaltning och drift där det är relevant.
- Markera snabbt föränderliga tekniska rekommendationer som sådant som bör verifieras mot aktuell dokumentation.


## Scenariohistorik

- **Kapitel 1:** Nordverk identifierar risker med personberoende drift och manuella produktionsmoment.
- **Kapitel 2:** Nordverk ser hur containerpaketering kan minska skillnader mellan utveckling, test och produktion.
- **Kapitel 3:** Nordverk går från att beställa miljöer system för system till att formulera en gemensam plattformsförmåga med standarder, ägarskap och driftmodell.
- **Kapitel 4:** Nordverk sorterar begrepp som Podman, Kubernetes, registry och plattform i en gemensam karta över container-ekosystemet.
- **Kapitel 5:** Nordverk upptäcker att image-hantering kräver tydlig versionering, godkända registries, standardiserade grundimages och spårbarhet från källa till produktion.
- **Kapitel 6:** Nordverk inför en första pipeline som bygger applikationen, kör grundläggande tester, skapar en image och publicerar den till internt registry som ett steg mot kontrollerad produktionssättning.
- **Kapitel 7:** Nordverk ser att utvecklingsteam behöver gå från kodleverans till körbara, testbara och förvaltningsbara leveranser.
- **Kapitel 8:** Nordverk upptäcker att testmiljöer och testbesked behöver bli mer reproducerbara, spårbara och kopplade till exakt image-version.

## Kapitel 7: utvecklingsarbetets förändring

Kapitel 7 etablerar att utvecklingsteam inte längre enbart bör betraktas som kodleverantörer. I containerbaserade arbetssätt behöver de bidra till en körbar, testbar, paketerad och spårbar leverans.

Viktiga canon-regler efter kapitel 7:

- Använd “byggbarhet” som chefsbegrepp för att beskriva om applikationen kan återskapas kontrollerat.
- Använd “standardiserad applikationspaketering” för gemensamma regler kring images, konfiguration, loggning, hälsokontroller och startbeteende.
- Använd “DevOps-samarbete” praktiskt och avdramatiserat. Begreppet ska inte framställas som ett mål i sig, utan som nödvändig samverkan mellan roller.
- Skilj mellan att leverera kod och att leverera något som är körbart och förvaltningsbart.
- Fortsätt betona att chefer inte behöver kunna utföra tekniska detaljer, men måste kunna ställa rätt styrningsfrågor.

## Kapitel 8: testarbetets förändring

Kapitel 8 etablerar att containerteknik kan stärka testarbetet, men bara om organisationen samtidigt utvecklar teststrategi, testmiljöer, testautomation och ansvar.

Viktiga canon-regler efter kapitel 8:

- Använd “reproducerbar testmiljö” som chefsbegrepp för miljöer som kan återskapas kontrollerat.
- Använd “miljöparitet” för att beskriva att test och produktion ska vara tillräckligt lika för att testresultat ska vara trovärdiga.
- Koppla testresultat till image-version, testmiljö och beslut om vidare leverans.
- Beskriv testautomation som styrningsförmåga, inte bara som teknisk effektivisering.
- Betona att testförmåga är en del av långsiktig förvaltning, inte bara en projektaktivitet.



## Scenariofortsättning efter kapitel 9

I kapitel 9 upptäcker Nordverk att containerteknik gör tekniskt underhåll mer synligt. En grundimage behöver uppdateras, men ansvar, budget och prioritering är otydliga. Ledningsinsikten blir att tekniskt underhåll behöver ingå i förvaltningsmodellen, inte hanteras som ett osynligt sidospår.
| Plattformsdrift | 10 | Drift av den gemensamma containerplattformens hälsa, kapacitet, standarder, uppgraderingar och säkerhet. |
| Applikationsdrift | 10 | Driftansvar kopplat till ett specifikt IT-stöd och dess funktion, loggar, integrationer, konfiguration och tillgänglighet. |
| Observability | 10 | Förmågan att förstå ett systems tillstånd utifrån signaler som loggar, mätvärden och spårning. |
| Självläkning | 10 | Plattformens förmåga att automatiskt hantera vissa fel, exempelvis genom återstart eller omplacering av containrar. |
| Kapacitetsstyrning | 10 | Planering och uppföljning av hur gemensamma resurser används och prioriteras mellan IT-stöd. |
| Supply chain-säkerhet | 11 | Kontroll över hela kedjan från kod, beroenden och byggflöden till godkänd image och körande produktion. |
| Policy | 11 | En regel eller styrande princip som kan dokumenteras och, där det är möjligt, omsättas till teknisk kontroll. |
| Säkerhetsgrind | 11 | Kontrollpunkt i leveransflödet som stoppar eller varnar när säkerhetskrav inte är uppfyllda. |
| Regelefterlevnad | 11 | Förmågan att följa och visa att organisationen följer beslutade krav, regler och interna styrprinciper. |
| Plattformsteam | 12 | Team med ansvar för den gemensamma containerplattformens förmåga, standarder, drift och stöd till andra team. |
| Produktteam | 12 | Team med ansvar för ett IT-stöds funktion, körbarhet, testbarhet, övervakning och förvaltningsbarhet. |
| Ansvarsmodell | 12 | Beskriven och beslutad struktur för vem som ansvarar för vad, vem som beslutar och hur roller samverkar. |
| Mandat | 12 | Tydlig rätt att fatta beslut, sätta standarder eller prioritera inom ett ansvarsområde. |
| Leveranskrav | 13 | Krav på hur leverantören ska leverera lösningen så att den kan tas emot, testas och driftsättas kontrollerat. |
| Plattformskrav | 13 | Krav på hur lösningen ska passa in i myndighetens beslutade containerplattform och standarder. |
| Förvaltningsbarhet | 13 | Förmågan att hålla ett IT-stöd begripligt, uppdaterbart, driftbart och möjligt att ta över eller vidareutveckla över tid. |
| Leverantörslåsning | 13 | När myndigheten blir beroende av en viss leverantörs kunskap, verktyg, miljö eller arbetssätt. |
| Exitkrav | 13 | Krav som gör det möjligt att byta leverantör, ta hem ansvar eller överlämna lösningen utan orimligt kunskapstapp. |


## Kapitel 11: säkerhet, regelefterlevnad och kontroll

Kapitel 11 etablerar att containerteknik inte automatiskt ger bättre säkerhet, men att den kan ge bättre kontroll om säkerhet byggs in i hela leveransflödet.

Viktiga canon-regler efter kapitel 11:

- Använd “supply chain-säkerhet” som chefsbegrepp för kontroll över kedjan från kod, beroenden och byggflöden till produktionssatt IT-stöd.
- Beskriv policy både som styrande dokument och som tekniska regler som kan följas upp i pipeline, registry och plattform.
- Använd “säkerhetsgrind” för kontrollpunkter som stoppar eller varnar när krav inte uppfylls.
- Betona att automatiserad kontroll inte ersätter ledningsansvar, utan gör ansvar, risk och efterlevnad mer synliga.
- Undantag ska beskrivas som styrda, tidsbegränsade riskbeslut med ägare, inte som informella genvägar.
- Koppla alltid säkerhetsfrågan till utveckling, test, förvaltning och drift, inte bara till säkerhetsfunktionen.

## Scenariofortsättning efter kapitel 11

I kapitel 11 upptäcker Nordverk att de har blivit snabbare men inte tillräckligt styrbara. Olika team använder olika grundimages, säkerhetskontroller sker för sent och plattformen accepterar mer än myndighetens policy borde tillåta. Ledningsinsikten blir att säkerhet behöver byggas in i leveransflödet genom gemensamma regler, automatiserade kontroller, tydliga undantag och uppföljning.


## Kapitel 12: roller, ansvar och organisation

Kapitel 12 etablerar att containerteknik inte bara förändrar teknik och arbetssätt, utan även ansvar, mandat och samverkan mellan utveckling, test, förvaltning, drift, säkerhet och leverantörer.

Viktiga canon-regler efter kapitel 12:

- Använd “plattformsteam” för den funktion som ansvarar för den gemensamma plattformens förmåga, standarder, policies, uppgraderingar, kapacitet och stöd till andra team.
- Använd “produktteam” som samlingsbegrepp för team som ansvarar för ett specifikt IT-stöds funktion, körbarhet, testbarhet, övervakning och förvaltningsbarhet.
- Betona att plattformsteamet inte ska bli en ny manuell flaskhals. Dess uppgift är att skapa standarder, verktyg och kontroller som gör rätt arbetssätt skalbart.
- Beskriv ansvarsmodellen längs leveransflödet: kod, image, pipeline, registry, plattform, produktion, säkerhet, förvaltning och leverantör.
- Koppla mandat till ansvar. Ingen funktion ska bära ansvar för risker den inte har mandat att påverka.
- Framställ säkerhet som integrerad kravställning och uppföljning, inte bara som sen granskning.
- Framställ förvaltning som långsiktigt livscykelansvar, inte bara ärendehantering eller verksamhetsprioritering.

## Scenariofortsättning efter kapitel 12

I kapitel 12 upptäcker Nordverk att tekniken fungerar bättre än ansvarskartan. Produktteam, plattformsteam, säkerhet, förvaltning och leverantörer tolkar sina ansvar olika. Nordverk beslutar därför att ta fram en ansvarsmodell som kopplar roller till hela leveransflödet. Plattformsteamet får mandat att sätta standarder, produktteamen får ansvar för körbarhet och förvaltningsbarhet, och förvaltning samt säkerhet får tydligare roll i livscykel, riskbeslut och uppföljning.


## Scenarioförlopp till och med kapitel 13

- Kapitel 1–3: Nordverk upptäcker riskerna i personberoende drift och börjar formulera plattformstänk.
- Kapitel 4–6: Nordverk förstår container-ekosystemet, image-flöden, registry, spårbarhet och pipeline.
- Kapitel 7–10: Nordverk ser hur utveckling, test, förvaltning och drift förändras.
- Kapitel 11–12: Nordverk tydliggör säkerhet, kontroll, roller och ansvar.
- Kapitel 13: Nordverk upptäcker att upphandling och leverantörsstyrning måste kravställa hela leveransförmågan, inte bara systemfunktion.
| Mognadsresa | 14 | Stegvis utveckling av organisationens förmåga från manuella arbetssätt till förvaltad plattformsförmåga. |
| Införandefärdplan | 14 | Samlad plan för hur teknik, ansvar, arbetssätt, säkerhet och förvaltning utvecklas över tid. |
| Styrbar förändring | 14 | Förändring där mål, principer, beslut, risker och uppföljning är tydliga och möjliga att leda. |
| Pilot | 14 | Avgränsat införande som används för att pröva teknik, ansvar och arbetssätt innan bredare skalning. |

## Status för första kapitelomgången

Samtliga 14 planerade kapitel finns nu i utkastform. Nästa steg är helhetsgranskning, konsistenskontroll och eventuell komplettering med checklistor eller bilagor.
