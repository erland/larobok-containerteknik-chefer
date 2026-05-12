# Kapitel 14: Färdplanen – från nuläge till fungerande containerplattform

## Varför detta kapitel finns

Boken har hittills byggt upp en helhetsbild av containerteknik ur ett chefsperspektiv. Vi har gått från personberoende drift och manuella överlämningar till containrar, images, registries, pipelines, plattformar, testbarhet, förvaltning, drift, säkerhet, roller och leverantörsstyrning.

Det här kapitlet samlar ihop trådarna.

När en statlig myndighet ska gå mot containerbaserade arbetssätt räcker det inte att besluta om ett verktyg eller en plattform. Förändringen behöver ledas som en sammanhållen mognadsresa. Tekniken måste införas tillsammans med arbetssätt, ansvar, kompetens, säkerhetsstyrning, finansiering, upphandling och förvaltningsmodell.

Kapitlets huvudbudskap är:

**En fungerande containerplattform uppstår inte genom installation. Den uppstår när teknik, organisation och styrning utvecklas tillsammans.**

## Lärandemål

Efter kapitlet ska läsaren kunna:

- beskriva en rimlig förändringsresa från nuläge till fungerande containerplattform
- skilja mellan teknisk installation, organisatoriskt införande och långsiktig förmåga
- identifiera beslut som behöver fattas av ledning, IT, säkerhet, förvaltning och verksamhet
- förstå varför pilot, standardisering och mognadsutveckling behöver hänga ihop
- formulera frågor som hjälper den egna organisationen att ta nästa steg

## Innan vi börjar

Tidigare kapitel har introducerat flera begrepp som återkommer i detta kapitel:

- **container**, en standardiserad körmiljö för en applikation
- **image**, den paketerade mall som används för att starta containern
- **registry**, platsen där images lagras och kontrolleras
- **pipeline**, flödet som bygger, testar, kontrollerar och levererar ändringar
- **plattform**, den gemensamma tekniska och organisatoriska förmågan
- **ansvarsmodell**, beskrivningen av vem som ansvarar för vad
- **förvaltningsbarhet**, förmågan att hålla ett IT-stöd begripligt, uppdaterbart och driftbart över tid

I detta kapitel använder vi dem tillsammans.

Frågan är inte längre:

> Vad är containerteknik?

Frågan är:

> Hur leder vi en förändring där containerteknik faktiskt ger bättre styrbarhet, kvalitet och förvaltningsförmåga?

## Från teknikprojekt till förändringsresa

Det är lätt att beskriva införandet av containerteknik som ett teknikprojekt:

- välj plattform
- installera miljö
- migrera applikationer
- utbilda några specialister
- börja köra containrar

Det kan låta konkret och hanterbart. Men det är en för smal bild.

En myndighet kan ha en tekniskt fungerande plattform och ändå misslyckas med nyttan. Det kan hända om:

- utvecklingsteam inte vet hur applikationer ska paketeras
- testmiljöer fortfarande skapas manuellt
- förvaltningen saknar ansvar för images och beroenden
- driftorganisationen fortsätter felsöka som om varje server vore unik
- säkerhetskrav kommer in sent och stoppar leveranser
- leverantörer levererar enligt gamla mönster
- plattformsteamet saknar mandat att sätta standarder
- ledningen mäter projektleverans men inte långsiktig förmåga

Därför bör införandet ses som en förändringsresa med flera parallella spår.

Ett bra ledningsperspektiv är att fråga:

> Vilken organisatorisk förmåga försöker vi bygga?

Svaret bör inte bara vara “Kubernetes” eller “containerplattform”. Ett bättre svar är:

> Vi vill bygga förmågan att leverera, testa, driftsätta, säkra och förvalta IT-stöd på ett mer standardiserat, spårbart och automatiserat sätt.

## En möjlig färdplan i sex steg

Det finns inte en enda färdplan som passar alla myndigheter. Storlek, säkerhetskrav, tekniskt arv, leverantörsberoenden, intern kompetens och befintliga avtal påverkar vägen framåt.

Men för många organisationer är följande sex steg en rimlig struktur:

1. Förstå nuläget
2. Formulera målbild och principer
3. Välj en kontrollerad pilot
4. Bygg plattformsförmåga och ansvar
5. Skala med standarder, inte undantag
6. Etablera långsiktig styrning och förvaltning

Vi går igenom dem ett i taget.

## Steg 1: Förstå nuläget

En förändringsresa börjar inte med att välja teknik. Den börjar med att förstå hur organisationen faktiskt arbetar i dag.

För en chef innebär nulägesanalysen att synliggöra frågor som ofta är kända i vardagen men sällan dokumenterade som ledningsproblem.

Exempel:

- Vilka produktionssättningar kräver manuella moment?
- Vilka system är beroende av enskilda specialister?
- Vilka testmiljöer skiljer sig tydligt från produktion?
- Var finns långa väntetider mellan utveckling, test, förvaltning och drift?
- Vilka leverantörer har kunskap som myndigheten själv saknar?
- Vilka tekniska beroenden är otydliga eller svåra att uppdatera?
- Vilka återkommande incidenter beror på miljöskillnader, konfiguration eller överlämningar?

Nuläget bör inte beskrivas som skuld eller misslyckande. Många manuella arbetssätt har uppstått för att människor har löst verkliga problem med de verktyg och förutsättningar som funnits.

Men det som tidigare var praktiskt kan med tiden bli riskfyllt.

Ett bra nulägesarbete bör därför skilja mellan:

- vad som fungerar bra och bör bevaras
- vad som fungerar men är personberoende
- vad som är långsamt men kontrollerat
- vad som är snabbt men svårt att följa upp
- vad som är tekniskt möjligt men organisatoriskt otydligt
- vad som innebär risk för säkerhet, tillgänglighet eller regelefterlevnad

### Scenario: Nordverk gör sin nulägeskarta

Myndigheten Nordverk börjar med att kartlägga tre samhällsviktiga IT-stöd. Kartläggningen visar att inget av systemen är “kaosartat”. De fungerar i produktion och förvaltningen har erfarna medarbetare.

Men kartan visar också att:

- produktionssättning kräver flera manuella steg
- samma person ofta granskar, korrigerar och godkänner tekniska detaljer
- testmiljöerna inte alltid motsvarar produktion
- leverantörer levererar på olika sätt
- säkerhetskontroller sker sent i flödet
- dokumentation finns, men den räcker inte alltid för att någon ny ska kunna ta över

Nordverks ledning inser att problemet inte är brist på kompetens. Problemet är att för mycket kompetens är bunden till personer och undantag i stället för till gemensamma arbetssätt.

## Steg 2: Formulera målbild och principer

När nuläget är tydligt behöver organisationen formulera en målbild.

En målbild bör vara tillräckligt konkret för att kunna styra beslut, men inte så tekniskt detaljerad att den blir en produktlista.

En svag målbild kan vara:

> Vi ska införa Kubernetes.

En starkare målbild är:

> Vi ska stegvis bygga en containerbaserad leverans- och driftförmåga där IT-stöd kan paketeras, testas, godkännas, driftsättas, övervakas och förvaltas på ett standardiserat och spårbart sätt.

Den senare målbilden gör det tydligare att förändringen omfattar både teknik och arbetssätt.

Målbilden bör kompletteras med principer. Exempel på principer:

- Nya IT-stöd ska i första hand kunna köras på myndighetens beslutade containerplattform.
- Images ska byggas och hämtas från kontrollerade källor.
- Test och säkerhetskontroller ska automatiseras där det är rimligt.
- Produktionssättning ska vara spårbar från kod eller leverans till körande version.
- Plattformsteamet ska tillhandahålla standarder, stöd och gemensamma mönster.
- Produktteam eller motsvarande ansvarar för applikationens körbarhet och förvaltningsbarhet.
- Undantag ska vara beslutade, tidsatta och följas upp.

Principer är viktiga eftersom de hjälper organisationen att fatta många små beslut utan att varje fråga behöver lyftas till högsta nivå.

## Steg 3: Välj en kontrollerad pilot

En vanlig chefsfälla är att antingen börja för stort eller för försiktigt.

Att börja för stort kan innebära att organisationen försöker migrera många system innan arbetssätt, säkerhet och ansvar är mogna.

Att börja för försiktigt kan innebära att pilotprojektet blir tekniskt intressant men organisatoriskt irrelevant. Då lär sig organisationen inte hur containerteknik påverkar verklig förvaltning, test, drift och styrning.

En bra pilot bör därför vara:

- tillräckligt viktig för att tas på allvar
- tillräckligt avgränsad för att hanteras kontrollerat
- representativ för verkliga behov
- möjlig att följa upp
- lämplig för lärande, inte bara leverans
- vald med både teknik, verksamhet, säkerhet och förvaltning involverade

Piloten ska inte bara svara på frågan:

> Kan vi köra en applikation som container?

Den ska svara på flera frågor:

- Kan vi bygga och lagra images kontrollerat?
- Kan vi testa på ett mer reproducerbart sätt?
- Kan vi följa en version från ändring till produktion?
- Kan vi hantera loggar, larm och incidenter?
- Kan vi beskriva ansvar mellan produktteam, plattformsteam och drift?
- Kan vi hantera säkerhetskrav utan att allt blir manuellt?
- Kan vi förvalta lösningen efter att piloten är avslutad?

### Scenario: Nordverk väljer inte den enklaste piloten

Nordverk överväger först att välja ett mycket enkelt internt stödsystem. Det hade varit tryggt, men ledningen ser att lärandet skulle bli begränsat.

I stället väljer man ett mindre men verkligt verksamhetsnära IT-stöd med tydliga integrationer, rimliga säkerhetskrav och en aktiv förvaltningsorganisation. Systemet är inte det mest kritiska i myndigheten, men det är tillräckligt representativt för att ge användbara erfarenheter.

Piloten får därför två mål:

1. Leverera ett fungerande containerbaserat införande.
2. Dokumentera vilka organisatoriska beslut som krävs för att kunna skala arbetssättet.

Det andra målet visar sig vara minst lika viktigt som det första.

## Steg 4: Bygg plattformsförmåga och ansvar

Efter eller parallellt med piloten behöver myndigheten bygga en stabil plattformsförmåga.

Plattformsförmåga betyder inte bara att tekniken finns installerad. Det betyder att organisationen har en fungerande kombination av:

- teknisk plattform
- plattformsteam
- standarder
- supportmodell
- säkerhetskontroller
- dokumentation
- kapacitetsplanering
- livscykelhantering
- beslutsforum
- finansieringsmodell

En plattform utan ansvar blir snabbt ett tekniskt landskap där alla gör lite olika. En ansvarskarta utan fungerande teknik blir styrning på papper.

Båda behövs.

### Plattformsteamets roll

Plattformsteamet bör inte ses som en traditionell driftgrupp som bara tar emot beställningar. Teamet bör vara en möjliggörare som tillhandahåller gemensamma förmågor:

- standardiserade sätt att köra applikationer
- mallar och vägledning för pipelines
- godkända grundimages och tekniska mönster
- övervakning, loggning och larmstruktur
- kapacitets- och resurshantering
- stöd till produktteam och leverantörer
- uppgraderingar och tekniskt underhåll av plattformen

Samtidigt behöver plattformsteamets mandat vara tydligt. Om teamet förväntas ansvara för standarder men inte får säga nej till avvikelser, kommer plattformen att fyllas av undantag.

### Produktteamens roll

Produktteam, förvaltningsteam eller motsvarande behöver ansvara för att deras IT-stöd är körbart, testbart, övervakningsbart och förvaltningsbart i den gemensamma målmiljön.

Det innebär bland annat ansvar för:

- applikationens image
- konfiguration och miljöberoenden
- automatiserade tester
- loggar och felsökningsinformation
- beroenden och tekniskt underhåll
- dokumentation för drift och förvaltning
- dialog med plattformsteam och säkerhetsfunktion

Det betyder inte att produktteamen ska göra allt själva. Men de behöver äga applikationens beteende i plattformen.

## Steg 5: Skala med standarder, inte undantag

När piloten lyckas uppstår ofta tryck att snabbt flytta fler system. Det är positivt, men också riskfyllt.

Om varje nytt system kräver egna lösningar kan organisationen snabbt återskapa samma problem som containertekniken skulle minska:

- specialfall
- manuella anpassningar
- otydliga ansvar
- svåröverskådliga beroenden
- varierande säkerhetsnivå
- svår förvaltning

Därför bör skalning bygga på standarder.

Standarder kan till exempel omfatta:

- hur images namnges, versioneras och lagras
- vilka grundimages som får användas
- hur pipelines ska byggas
- vilka tester som minst ska finnas
- hur secrets och konfiguration hanteras
- hur loggar och mätvärden ska exponeras
- vilka krav som gäller för produktion
- hur undantag dokumenteras och godkänns
- vilka krav som ska ställas på leverantörer

Standardisering betyder inte att allt blir likadant. Det betyder att variation hanteras medvetet.

En bra princip är:

> Standard där det minskar risk och ökar förvaltningsbarhet. Flexibilitet där verksamhetsnyttan kräver det och riskerna är förstådda.

## Steg 6: Etablera långsiktig styrning och förvaltning

När containerplattformen blir en del av myndighetens ordinarie IT-miljö förändras ledningsfrågorna.

I början handlar mycket om införande:

- fungerar tekniken?
- klarar vi piloten?
- har vi rätt kompetens?
- kan vi få igenom säkerhetskraven?
- kan vi migrera första systemen?

Senare handlar frågorna mer om långsiktig styrning:

- hur finansieras plattformens utveckling?
- hur prioriteras kapacitet mellan IT-stöd?
- hur följs tekniskt underhåll upp?
- hur hanteras plattformsuppgraderingar?
- hur mäts leveransförmåga och kvalitet?
- hur säkerställs att leverantörer följer standarder?
- hur avvecklas gamla arbetssätt?
- hur hanteras undantag över tid?

Det är här många organisationer underskattar arbetet.

En containerplattform är inte “klar” när första systemen körs. Den behöver förvaltas som en central organisatorisk förmåga.

## Mätning: hur vet vi att förändringen hjälper?

Chefer behöver kunna följa om förändringen faktiskt ger nytta.

Det räcker inte att mäta antal migrerade system. Det kan vara ett viktigt mått, men det säger inte om organisationen har blivit mer styrbar, säker eller effektiv.

Möjliga uppföljningsfrågor är:

- Har ledtiden från ändring till testad leverans minskat?
- Har manuella produktionsmoment minskat?
- Har antalet miljörelaterade fel minskat?
- Kan vi snabbare återskapa testmiljöer?
- Vet vi vilka images som körs i produktion?
- Har incidentutredningar blivit enklare tack vare bättre loggar och spårbarhet?
- Har leverantörsleveranser blivit mer enhetliga?
- Har säkerhetskontroller flyttats tidigare i flödet?
- Har förvaltningsorganisationen bättre kontroll över beroenden och tekniskt underhåll?
- Har personberoendet minskat?

Måtten bör kopplas till målbilden. Om målbilden är styrbar leverans bör organisationen mäta styrbarhet, inte bara teknisk aktivitet.

## Vanliga chefsfällor

### Fälla 1: Att tro att plattformen är förändringen

En installerad plattform är bara en förutsättning. Den verkliga förändringen sker när leveransflöden, ansvar och förvaltning ändras.

**Motfråga:** Vilka arbetssätt har faktiskt förändrats efter plattformsinförandet?

### Fälla 2: Att börja med alla system samtidigt

Det kan skapa hög belastning, många undantag och otydligt lärande.

**Motfråga:** Vilken pilot ger bäst kombination av nytta, riskkontroll och organisatoriskt lärande?

### Fälla 3: Att låta undantag bli norm

Varje undantag kan vara rimligt för sig. Tillsammans kan de göra plattformen svår att förvalta.

**Motfråga:** Är undantaget tidsatt, beslutat och följt upp?

### Fälla 4: Att underskatta förvaltningen

Containerteknik kan göra leveranser snabbare, men den ökar också behovet av aktiv livscykelhantering.

**Motfråga:** Vem ansvarar för att images, beroenden, pipelines och plattformsanpassningar hålls aktuella?

### Fälla 5: Att behandla säkerhet som en slutgranskning

Om säkerhet kommer in sent blir den lätt ett stopp i flödet. Om den byggs in tidigt kan den bli en del av styrbarheten.

**Motfråga:** Vilka säkerhetskontroller kan göras automatiskt och tidigt?

### Fälla 6: Att glömma leverantörerna

Om leverantörer fortsätter leverera enligt gamla mönster kommer den interna plattformen inte att ge full effekt.

**Motfråga:** Ställer våra avtal och beställningar krav på paketering, testbarhet, spårbarhet och förvaltningsbarhet?

## Frågor att ställa i den egna organisationen

### Om nuläget

1. Vilka manuella moment är mest riskfyllda i dag?
2. Var är personberoendet störst?
3. Vilka miljöskillnader orsakar återkommande problem?
4. Vilka system är mest lämpliga för en första pilot?

### Om målbilden

1. Vad menar vi med en fungerande containerplattform?
2. Vilken organisatorisk förmåga ska förändringen bygga?
3. Vilka principer ska gälla för nya IT-stöd?
4. Vilka undantag kan accepteras, och hur länge?

### Om ansvar

1. Vem äger plattformens standarder?
2. Vem ansvarar för applikationens körbarhet?
3. Vem ansvarar för images, beroenden och tekniskt underhåll?
4. Hur samverkar utveckling, test, förvaltning, drift och säkerhet?

### Om styrning

1. Hur följer ledningen upp nytta?
2. Hur finansieras plattformens långsiktiga utveckling?
3. Hur prioriteras kapacitet och förbättringar?
4. Hur säkerställs att leverantörer följer målbilden?

## En enkel mognadsmodell

För att göra förändringen mer överskådlig kan myndigheten beskriva sin mognad i fyra nivåer.

### Nivå 1: Manuell och personberoende

Organisationen har fungerande IT-stöd, men många moment kräver handpåläggning. Kunskap finns ofta hos enskilda personer. Test och produktion skiljer sig åt. Leverantörer och interna team arbetar på olika sätt.

**Ledningsfokus:** Synliggör risker och beroenden.

### Nivå 2: Pilot och lärande

Organisationen testar containerteknik i avgränsad form. De första images, pipelines och plattformsbesluten finns. Roller och ansvar börjar diskuteras, men mycket är fortfarande nytt.

**Ledningsfokus:** Lär av piloten och dokumentera beslut.

### Nivå 3: Standardiserad leverans

Flera IT-stöd följer gemensamma mönster. Registry, pipeline, test, säkerhetskontroller och plattformsdrift är etablerade. Leverantörer får tydligare krav. Undantag hanteras mer medvetet.

**Ledningsfokus:** Skala utan att skapa okontrollerad variation.

### Nivå 4: Förvaltad plattformsförmåga

Containerplattformen är en ordinarie del av myndighetens IT-förmåga. Det finns etablerad finansiering, livscykelhantering, kompetensplanering, styrning och uppföljning. Tekniken är inte längre ett projekt utan en förvaltningsbar förmåga.

**Ledningsfokus:** Fortsätt utveckla, mäta och förbättra.

## Scenario: Nordverks färdplan

När Nordverk sammanfattar sin förändringsresa väljer ledningen att beskriva den i tre horisonter.

### Horisont 1: Skapa kontroll över nuläget

Nordverk kartlägger manuella produktionsmoment, personberoenden, kritiska testmiljöskillnader och leverantörernas olika leveranssätt. Man väljer ett pilotområde och formulerar en målbild för styrbar containerbaserad leverans.

Viktiga beslut:

- vilka system som ingår i piloten
- vilka grundprinciper som gäller för images och registries
- vilka funktioner som måste delta: IT, säkerhet, förvaltning, drift, utveckling, test och upphandling
- hur ledningen ska följa lärandet

### Horisont 2: Bygga gemensamma arbetssätt

Nordverk etablerar ett plattformsteam med tydligt mandat. Man tar fram gemensamma mallar för pipelines, testkontroller, loggning och leverantörskrav. Produktteamen får ansvar för att deras applikationer är körbara och testbara i plattformen.

Viktiga beslut:

- ansvarsfördelning mellan plattformsteam och produktteam
- miniminivå för test, spårbarhet och säkerhetskontroller
- hur undantag ska beslutas och följas upp
- hur tekniskt underhåll ska prioriteras i förvaltningen

### Horisont 3: Skala och förvalta

Nordverk börjar flytta fler IT-stöd, men bara när de kan följa gemensamma standarder eller när undantag är tydligt beslutade. Upphandling och leverantörsstyrning uppdateras så att nya leveranser passar målmiljön. Ledningen följer inte bara antal migrerade system, utan även minskat personberoende, bättre spårbarhet och färre miljörelaterade fel.

Viktiga beslut:

- vilka system som ska migreras, moderniseras eller lämnas kvar tills vidare
- hur plattformen finansieras långsiktigt
- hur kompetens ska byggas internt
- hur myndigheten undviker ny leverantörslåsning

Nordverks viktigaste lärdom är att förändringen inte handlar om att allt ska flyttas så snabbt som möjligt. Den handlar om att stegvis öka myndighetens förmåga att leverera och förvalta IT-stöd med bättre kontroll.

## Snabb sammanfattning

- Införande av containerteknik bör ledas som en förändringsresa, inte bara som ett teknikprojekt.
- En fungerande containerplattform kräver teknik, ansvar, standarder, kompetens, säkerhet, finansiering och förvaltning.
- Nulägesanalysen bör synliggöra manuella moment, personberoenden, miljöskillnader, leverantörsberoenden och risker.
- Målbilden bör beskriva önskad organisatorisk förmåga, inte bara vald teknik.
- En pilot bör ge verkligt organisatoriskt lärande, inte bara visa att tekniken fungerar.
- Skalning bör ske med standarder och kontrollerade undantag.
- Långsiktig nytta kräver mätning av styrbarhet, spårbarhet, kvalitet, förvaltningsbarhet och minskat personberoende.

## Nästa steg

Detta kapitel avslutar den planerade första versionen av boken. Nästa steg i bokprojektet är därför inte att skriva ännu ett ordinarie kapitel, utan att granska helheten.

En lämplig fortsättning är att:

1. läsa igenom alla kapitel i ordning
2. kontrollera att begrepp introduceras i rätt takt
3. se om Myndigheten Nordverk används konsekvent
4. markera avsnitt där offentlig sektor, styrning eller säkerhet behöver fördjupas
5. besluta om boken ska kompletteras med checklistor, bilagor eller sammanfattande verktyg

Efter granskningen kan boken kompletteras med till exempel:

- en sammanfattande chefschecklista
- en ordlista
- en mall för nulägesanalys
- en mall för pilotval
- ett beslutsunderlag för ledningsgrupp
- en bilaga om vanliga begrepp i containerplattformar

Bokens centrala slutsats är enkel men viktig:

**Containerteknik är värdefull först när den gör organisationens IT-leveranser mer begripliga, styrbara, säkra och förvaltningsbara.**
