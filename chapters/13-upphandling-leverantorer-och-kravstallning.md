# Kapitel 13: Upphandling, leverantörer och kravställning

## Varför detta kapitel finns

Många statliga myndigheter bygger inte alla sina IT-stöd själva. Utveckling, drift, test, support, plattformar, specialistkompetens och systemförvaltning kan helt eller delvis levereras av externa parter. Därför blir containerteknik inte bara en fråga för den interna IT-organisationen. Den blir också en fråga för upphandling, avtal, leverantörsstyrning och kravställning.

När en myndighet inför containerteknik förändras vad som bör beställas. Det räcker inte längre att upphandla ett system som “ska fungera” eller en leverantör som “ska drifta lösningen”. Myndigheten behöver kunna ställa krav på hur IT-stödet byggs, paketeras, testas, levereras, uppdateras, övervakas och förvaltas över tid.

Det här kapitlet handlar om hur chefer kan se till att upphandling och leverantörsstyrning inte låser fast organisationen i gamla manuella arbetssätt.

Kapitlets huvudbudskap är:

**Containerteknik ger störst nytta när kravställningen omfattar hela leveransförmågan, inte bara den färdiga funktionen.**

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förstå varför upphandling och leverantörsstyrning påverkas av containerteknik
- skilja mellan funktionskrav, leveranskrav, plattformskrav och förvaltningskrav
- identifiera krav som bör ställas på paketering, testbarhet, spårbarhet och driftbarhet
- se varför avtal behöver stödja förändring över tid, inte bara leverans vid ett startdatum
- ställa bättre frågor till upphandling, juridik, IT, säkerhet, förvaltning och leverantörer

## Innan vi börjar

Tidigare kapitel har visat att containerteknik påverkar flera delar av organisationen:

- utveckling behöver ta ansvar för byggbarhet och paketering
- test behöver arbeta med reproducerbara testmiljöer och automatiserade kontroller
- förvaltning behöver hantera livscykel, beroenden och tekniskt underhåll
- drift behöver gå från serverhantering till plattformsdrift och observability
- säkerhet behöver bygga in kontroller i image-flöden, registries, pipelines och plattform
- roller och ansvar behöver bli tydliga mellan plattformsteam, produktteam och stödjande funktioner

I detta kapitel flyttar vi samma resonemang till relationen mellan myndigheten och dess leverantörer.

Frågan är inte bara:

> Kan leverantören leverera systemet?

Frågan är snarare:

> Kan leverantören bidra till en lösning som är körbar, testbar, spårbar, säker och förvaltningsbar i vår containerbaserade målmiljö?

## Från att köpa system till att köpa leveransförmåga

Traditionell IT-upphandling har ofta fokuserat på funktion:

- vilka verksamhetsprocesser systemet ska stödja
- vilka användarroller som ska finnas
- vilka rapporter, formulär eller integrationer som ska levereras
- vilka servicenivåer som ska gälla efter införande

Det är fortfarande viktigt. Containerteknik gör inte verksamhetskraven mindre viktiga.

Men när IT-stöd ska köras i en containerplattform behöver kravställningen även omfatta hur lösningen levereras och förvaltas. En applikation kan uppfylla många verksamhetskrav men ändå vara svår att driftsätta, svår att testa, svår att felsöka eller svår att uppdatera.

Det skapar en viktig chefsinsikt:

**Ett IT-stöd är inte färdigt bara för att funktionen är levererad. Det är färdigt först när organisationen kan köra, testa, övervaka, uppdatera och förvalta det på ett kontrollerat sätt.**

För en myndighet innebär det att upphandlingen behöver fånga mer än “vad systemet gör”. Den behöver också fånga:

- hur applikationen paketeras
- hur den byggs och testas
- hur den konfigureras för olika miljöer
- hur den lämnar spår efter sig
- hur den övervakas
- hur säkerhetskrav följs upp
- hur uppdateringar och sårbarheter hanteras
- hur ansvar delas mellan myndighet och leverantör
- hur lösningen kan tas vidare om leverantören byts ut

## Fyra typer av krav

För chefer är det användbart att skilja mellan fyra kravtyper.

### 1. Funktionskrav

Funktionskrav beskriver vad IT-stödet ska göra för verksamheten.

Exempel:

- Handläggare ska kunna registrera ett ärende.
- Systemet ska kunna skicka beslut till ett annat myndighetssystem.
- Administratörer ska kunna ta ut statistik per period.
- Användare ska kunna logga in med myndighetens valda identitetslösning.

Funktionskrav är nödvändiga, men de räcker inte för containerbaserade leveranser.

### 2. Leveranskrav

Leveranskrav beskriver hur leverantören ska leverera lösningen så att den kan tas emot, testas och driftsättas kontrollerat.

Exempel:

- Applikationen ska levereras som container image enligt myndighetens standard.
- Byggprocessen ska vara dokumenterad och reproducerbar.
- Varje levererad image ska kunna kopplas till version, kodändring, testresultat och godkännande.
- Leveransen ska kunna gå genom myndighetens beslutade pipeline eller motsvarande kontrollflöde.

Leveranskrav minskar risken att myndigheten får en fungerande applikation som ändå kräver manuell handpåläggning för att nå produktion.

### 3. Plattformskrav

Plattformskrav beskriver hur lösningen ska passa in i myndighetens tekniska målmiljö.

Exempel:

- Applikationen ska kunna köras på myndighetens valda containerplattform.
- Den ska följa beslutade mönster för konfiguration, loggning, hälsokontroller och resurshantering.
- Den ska kunna köras utan manuella ändringar direkt i produktionsmiljön.
- Den ska kunna använda myndighetens beslutade lösningar för identitet, hemligheter, nätverk och övervakning.

Plattformskrav minskar risken att varje system blir ett undantag.

### 4. Förvaltningskrav

Förvaltningskrav beskriver hur lösningen ska kunna hållas aktuell, säker och begriplig över tid.

Exempel:

- Leverantören ska redovisa viktiga beroenden och hur de hålls uppdaterade.
- Det ska finnas rutiner för sårbarhetsåtgärder i images och beroenden.
- Dokumentation ska finnas för drift, felsökning, loggar, larm och återställning.
- Myndigheten ska kunna ta över eller byta leverantör utan att förlora nödvändig kunskap.

Förvaltningskrav skyddar myndigheten mot att tekniska beslut skapar långsiktigt beroende och höga framtida kostnader.

## Scenario: Nordverk upphandlar vidareutveckling

Myndigheten Nordverk ska upphandla vidareutveckling av ett viktigt IT-stöd för ärendehantering. Systemet har funnits länge och har historiskt produktionssatts genom manuella checklistor. En extern leverantör har byggt stora delar av systemet.

Tidigare upphandlingar har fokuserat på:

- ny funktionalitet
- timpris och kompetensprofiler
- leveranstid
- support
- incidenthantering
- dokumentation

När Nordverk nu vill införa containerplattform upptäcker organisationen att de gamla kraven inte räcker.

Leverantören kan utveckla funktioner, men det är oklart:

- vem som ska bygga container images
- var images ska lagras
- hur testresultat kopplas till image-version
- om applikationen kan köras i Nordverks standardiserade plattform
- hur loggar och mätvärden ska exponeras
- vem som uppdaterar grundimages och beroenden
- hur säkerhetsbrister i en levererad image ska hanteras
- om Nordverk kan byta leverantör utan att behöva bygga om hela leveransflödet

Nordverk inser att upphandlingen inte bara behöver köpa vidareutveckling. Den behöver köpa en leverans som passar in i myndighetens nya arbetssätt.

## Krav på containerpaketering

Ett första område är hur applikationen ska paketeras.

Om myndigheten inte ställer tydliga krav kan leverantören leverera på ett sätt som fungerar i leverantörens miljö men inte i myndighetens. Det kan skapa ny manuell hantering, nya undantag och nya beroenden.

Exempel på frågor:

- Ska leverantören leverera färdiga images, bygginstruktioner eller båda?
- Ska images byggas av leverantören, av myndigheten eller i en gemensam pipeline?
- Vilka grundimages får användas?
- Hur ska image-versioner namnges och märkas?
- Ska varje image kunna kopplas till en viss källkodsversion?
- Hur ska konfiguration skiljas från själva image-innehållet?

En viktig princip är att en image inte bör bli en svart låda. Myndigheten behöver förstå vad den innehåller, hur den byggts och hur den kan återskapas.

### Chefsfälla: att acceptera “vi levererar en container” som tillräckligt svar

En leverantör kan säga:

> Vi kan leverera systemet som container.

Det låter bra, men är för otydligt.

Chefen bör be organisationen förtydliga:

- Vad menar leverantören med “container”?
- Är det en image enligt våra standarder?
- Är byggprocessen reproducerbar?
- Kan imagen gå genom våra säkerhets- och testkontroller?
- Kan den köras i vår plattform utan speciallösningar?
- Är den dokumenterad så att vi kan förvalta den?

En containeriserad applikation är inte automatiskt styrbar. Den blir styrbar först när paketering, byggande, kontroll och drift passar in i organisationens arbetssätt.

## Krav på pipelines och testbarhet

Ett andra område är hur leveransen ska testas och kvalitetssäkras.

I äldre leveransmodeller kan leverantören leverera kod, dokumentation eller ett installerat system. Test kan sedan ske i ett separat projektsteg. I containerbaserade flöden bör testbarhet byggas in tidigare.

Exempel på krav eller styrande frågor:

- Vilka tester ska leverantören tillhandahålla?
- Vilka tester ska köras automatiskt?
- Ska tester kunna köras i myndighetens pipeline?
- Ska leverantören tillhandahålla testdata, testinstruktioner eller testmiljödefinitioner?
- Hur visas att en viss image har passerat beslutade tester?
- Hur hanteras misslyckade tester?
- Vilka manuella godkännanden ska finnas kvar, och varför?

Här är det viktigt att inte förväxla automation med avsaknad av kontroll. En pipeline kan vara ett sätt att göra kontroll mer konsekvent.

För chefer är frågan:

> Vilka kontroller vill vi att varje leverans ska passera innan den kan bli aktuell för produktion?

Svaret kan innehålla både tekniska och organisatoriska kontroller.

## Krav på spårbarhet

Spårbarhet är särskilt viktig i myndighetsmiljöer. Myndigheten behöver kunna förstå vad som körs, varför det körs och vem som godkänt det.

I en containerbaserad leverans kan spårbarhet behöva omfatta:

- källkodsversion
- byggtillfälle
- byggverktyg
- grundimage
- beroenden
- testresultat
- säkerhetskontroller
- godkännanden
- produktionssättning
- driftsatt version
- incidenter och ändringar efter driftsättning

Det innebär inte att chefen ska följa varje teknisk detalj. Men chefen behöver säkerställa att organisationen kan svara på grundläggande frågor:

- Vilken version körs i produktion?
- Varifrån kommer den?
- Vilka tester har den passerat?
- Vilka kända risker finns?
- Vem godkände leveransen?
- När behöver den uppdateras?

Utan spårbarhet blir det svårt att hantera incidenter, revision, säkerhetsbrister och leverantörsbyten.

## Krav på driftbarhet och observability

När en applikation körs på en containerplattform behöver den vara byggd för att kunna övervakas och felsökas på ett modernt sätt.

Det kan handla om att applikationen ska:

- skriva loggar på ett sätt som plattformen kan samla in
- exponera hälsokontroller så att plattformen kan upptäcka problem
- ge relevanta mätvärden för kapacitet, prestanda och fel
- hantera omstart utan att data förloras
- tydligt skilja mellan konfiguration, kod och känsliga uppgifter
- dokumentera vanliga felbilder och felsökningsvägar

Detta är inte bara en teknisk bekvämlighet. Det påverkar incidenthantering, support, tillgänglighet och kostnad.

Om leverantören inte tar hänsyn till driftbarhet kan myndigheten få en applikation som fungerar i ett acceptanstest men är svår att förstå i produktion.

### Fråga för chefer

> Har vi kravställt att systemet ska vara möjligt att drifta, övervaka och felsöka i vår målplattform, eller har vi bara kravställt att det ska fungera?

## Krav på säkerhet och beroenden

Kapitel 11 behandlade säkerhet, regelefterlevnad och kontroll. I upphandling behöver dessa frågor bli konkreta krav och avtalsvillkor.

Exempel på områden:

- hur sårbarheter i images ska upptäckas
- hur snabbt kritiska sårbarheter ska åtgärdas
- vem som ansvarar för uppdatering av grundimages
- vilka externa komponenter och bibliotek som får användas
- hur leverantören ska redovisa beroenden
- hur åtkomst till kod, registry, pipeline och miljöer styrs
- hur undantag från säkerhetskrav ska hanteras
- hur säkerhetsbrister kommuniceras till myndigheten

Det är viktigt att skilja mellan två frågor:

1. **Vilka säkerhetskrav gäller för lösningen?**
2. **Hur ska myndigheten kunna följa upp att kraven fortsätter vara uppfyllda över tid?**

Den andra frågan glöms ofta bort. Men containerbaserade miljöer förändras kontinuerligt. Nya sårbarheter upptäcks. Images blir gamla. Beroenden behöver uppdateras. Plattformen uppgraderas. Därför behöver säkerhetskrav vara kopplade till livscykelhantering.

## Krav på dokumentation som går att använda

Dokumentation i IT-upphandlingar kan lätt bli något som levereras i slutet och sedan sällan används. I containerbaserade leveranser behöver dokumentation vara praktiskt användbar för flera grupper.

Utveckling behöver förstå hur applikationen byggs.

Test behöver förstå hur tester körs och hur testmiljöer skapas.

Förvaltning behöver förstå livscykel, beroenden, versionshantering och prioriterade risker.

Drift och plattformsteam behöver förstå loggning, larm, resurser, hälsokontroller och incidentmönster.

Säkerhet behöver förstå kontroller, undantag och sårbarhetshantering.

Upphandling och juridik behöver förstå vilka åtaganden som faktiskt ingår i leveransen.

Därför bör dokumentationskrav inte bara säga:

> Leverantören ska tillhandahålla dokumentation.

Det är bättre att beskriva vad dokumentationen ska göra möjligt.

Exempel:

- En ny utvecklare ska kunna förstå hur applikationen byggs.
- Plattformsteamet ska kunna förstå hur applikationen startas, övervakas och skalas.
- Förvaltningen ska kunna se vilka beroenden som behöver livscykelhanteras.
- Incidenthantering ska kunna genomföras utan att en specifik konsult måste vara tillgänglig.
- Myndigheten ska kunna genomföra leverantörsbyte eller intern övertagning utan orimligt kunskapstapp.

## Undvik leverantörslåsning

Leverantörslåsning kan uppstå på flera sätt.

Det mest uppenbara är teknisk låsning: lösningen fungerar bara med en viss produkt eller en viss leverantörs miljö.

Men det finns också organisatorisk låsning:

- bara leverantören vet hur systemet byggs
- bara leverantören kan felsöka produktionsproblem
- bara leverantören har tillgång till pipeline eller byggmiljö
- bara leverantören vet vilka beroenden som är kritiska
- bara leverantören kan skapa en ny image
- bara leverantören förstår hur plattformen är konfigurerad för just denna applikation

Containerteknik kan minska låsning genom standardisering. Men den kan också skapa ny låsning om allt byggs kring leverantörens egna verktyg, egna rutiner och egna hemliga arbetssätt.

För en statlig myndighet är det därför viktigt att kravställa förvaltningsbarhet och överlämningsbarhet.

### Exempel på kravformulering på chefsnivå

Detta är inte juridiskt färdiga formuleringar, men visar riktningen:

- Leveransen ska kunna byggas och testas i en miljö som myndigheten har insyn i.
- Applikationen ska dokumenteras så att myndigheten kan genomföra leverantörsbyte utan förlust av nödvändig drift- och förvaltningskunskap.
- Leverantören ska redovisa beroenden, byggsteg och konfigurationsprinciper.
- Lösningen ska så långt som möjligt följa myndighetens beslutade plattformsstandarder.
- Avvikelser från standard ska dokumenteras, motiveras och godkännas.

## Avtal behöver stödja förändring

En containerplattform är inte statisk. Under ett flerårigt avtal kan många saker förändras:

- plattformen uppgraderas
- säkerhetskrav skärps
- grundimages byts ut
- beroenden blir för gamla
- nya sårbarheter upptäcks
- arbetssätt för pipeline och test utvecklas
- myndigheten ändrar målarkitektur
- leverantörer byts eller kompletteras

Om avtalet bara beskriver en leverans vid ett visst tillfälle kan det bli svårt att hantera dessa förändringar.

Därför behöver avtal och leverantörsstyrning stödja löpande tekniskt underhåll och anpassning.

Det betyder inte att allt ska vara otydligt eller öppet. Tvärtom: det behöver finnas tydliga principer för vad som ingår, hur förändringar hanteras, hur prioriteringar görs och hur ansvar fördelas.

Chefsfrågan blir:

> Har vi ett avtal som gör det möjligt att hålla lösningen säker, uppdaterad och förvaltningsbar under hela livscykeln?

## Samverkan mellan upphandling, juridik, IT och säkerhet

Upphandling av containerbaserade IT-stöd kan inte lämnas till en funktion ensam.

Om IT skriver tekniska krav utan upphandling och juridik kan kraven bli svåra att använda i upphandlingsdokument och avtal.

Om upphandling driver processen utan teknisk förståelse kan viktiga leveranskrav saknas.

Om säkerhet kommer in för sent kan kraven bli efterhandskontroller i stället för inbyggda krav.

Om förvaltning inte deltar kan lösningen bli möjlig att införa men svår att leva med.

Därför behöver kravställningen vara tvärfunktionell.

Minst följande perspektiv bör finnas med:

- verksamhetens behov
- arkitektur och målplattform
- utveckling och test
- drift och plattform
- informationssäkerhet och regelefterlevnad
- förvaltning och livscykel
- upphandling och juridik
- ekonomi och leverantörsstyrning

Containerteknik gör inte upphandlingen enklare, men den gör det tydligare vilka frågor som måste besvaras.

## Offentlig upphandling och teknikneutralitet

Statliga myndigheter behöver förhålla sig till reglerna för offentlig upphandling. Detta kapitel är inte juridisk rådgivning och ersätter inte upphandlings- eller juristkompetens.

Som chef är det ändå viktigt att förstå en grundläggande balans:

- Kraven behöver vara tillräckligt tydliga för att myndigheten ska få en lösning som fungerar i målmiljön.
- Kraven får inte formuleras slentrianmässigt så att de onödigt låser upphandlingen till en viss produkt eller leverantör.
- Kraven bör kopplas till verkliga behov: säkerhet, spårbarhet, driftbarhet, testbarhet, förvaltningsbarhet och integration med myndighetens styrda plattform.

Det är ofta bättre att kravställa förmågor och standardiserade resultat än att bara nämna produktnamn.

Exempel:

Mindre bra som ensam kravidé:

> Lösningen ska använda Produkt X.

Bättre riktning:

> Lösningen ska kunna köras på myndighetens beslutade containerplattform och följa myndighetens standarder för image-hantering, konfiguration, loggning, hälsokontroller, resursstyrning och säkerhetskontroller.

I vissa situationer kan specifika tekniska krav vara nödvändiga, men då bör de vara motiverade och hanterade tillsammans med upphandling och juridik.

## Vad bör chefen be om inför en upphandling?

En chef behöver inte själv skriva alla tekniska krav. Men chefen bör säkerställa att organisationen tar fram ett tillräckligt underlag.

Ett bra underlag kan innehålla:

### 1. Målbild för leveransflödet

Hur ska en ändring gå från utveckling till produktion?

Beskriv:

- byggsteg
- teststeg
- säkerhetskontroller
- godkännanden
- image-lagring
- produktionssättning
- uppföljning efter driftsättning

### 2. Målplattform och standarder

Vilken miljö ska lösningen passa in i?

Beskriv:

- containerplattform
- registry
- pipeline-principer
- loggning och övervakning
- nätverk och identitet
- hantering av hemligheter
- resurs- och kapacitetsprinciper

### 3. Ansvarskarta

Vem ansvarar för vad?

Beskriv ansvar för:

- kod
- image-byggande
- grundimages
- beroenden
- test
- säkerhetsåtgärder
- driftdokumentation
- incidentstöd
- livscykelhantering
- leverantörsbyte

### 4. Krav på spårbarhet och bevis

Vilka bevis behöver myndigheten kunna se?

Exempel:

- testresultat
- sårbarhetsrapport
- bygglogg
- godkännande
- versionshistorik
- beroendelista
- dokumenterade undantag

### 5. Förvaltnings- och exitkrav

Hur undviker myndigheten framtida inlåsning?

Beskriv:

- dokumentation
- kunskapsöverföring
- rätt till nödvändiga bygg- och konfigurationsunderlag
- möjlighet att återskapa leveranser
- stöd vid överlämning
- hantering av källkod, images och teknisk historik

## Vanliga chefsfällor

### Fälla 1: Att upphandla ny teknik men gamla arbetssätt

Myndigheten kravställer containerplattform, men behåller manuella leveranser, sena tester och otydliga överlämningar.

**Konsekvens:**  
Tekniken införs, men nyttan uteblir.

**Hur man undviker det:**  
Kravställ leveransflöde, testbarhet, spårbarhet och ansvar, inte bara teknik.

### Fälla 2: Att tro att leverantören automatiskt förstår myndighetens målmiljö

Leverantören säger att de har erfarenhet av containrar och Kubernetes. Myndigheten antar att det betyder att leveransen passar den egna plattformen.

**Konsekvens:**  
Lösningen kräver specialanpassningar, undantag eller manuell hantering.

**Hur man undviker det:**  
Beskriv myndighetens standarder och kräv att avvikelser dokumenteras och godkänns.

### Fälla 3: Att kravställa funktion men inte förvaltningsbarhet

Systemet uppfyller verksamhetskraven men är svårt att uppdatera, övervaka och livscykelhantera.

**Konsekvens:**  
Myndigheten får högre framtida kostnader och större risk.

**Hur man undviker det:**  
Lägg till krav på driftbarhet, beroendehantering, dokumentation och livscykelansvar.

### Fälla 4: Att skapa ny personberoende kunskap hos leverantören

Myndigheten minskar internt personberoende men accepterar att leverantören sitter på all praktisk kunskap.

**Konsekvens:**  
Risk flyttas från interna specialister till externa specialister.

**Hur man undviker det:**  
Kravställ insyn, dokumentation, kunskapsöverföring och övertagbarhet.

### Fälla 5: Att ta in säkerhet för sent

Säkerhetskrav läggs till efter att arkitektur, pipeline och leveransmodell redan är beslutade.

**Konsekvens:**  
Säkerhet blir broms, efterhandsgranskning eller undantagshantering.

**Hur man undviker det:**  
Involvera säkerhet tidigt och översätt säkerhetskrav till kontroller i flödet.

## Frågor att ställa i den egna organisationen

### Om upphandlingsstrategi

1. Upphandlar vi ett system, en plattform, en tjänst eller en långsiktig leveransförmåga?
2. Vilka delar av leveransflödet ska leverantören ansvara för?
3. Vilka delar måste myndigheten själv ha kontroll över?
4. Hur säkerställer vi att upphandlingen stödjer vår målarkitektur?

### Om kravställning

5. Har vi krav på hur applikationen ska paketeras som image?
6. Har vi krav på testbarhet och automatiserade kontroller?
7. Har vi krav på spårbarhet från kod till produktion?
8. Har vi krav på loggning, hälsokontroller och observability?
9. Har vi krav på beroendehantering och sårbarhetsåtgärder?
10. Har vi krav på dokumentation som faktiskt går att använda?

### Om ansvar

11. Vem ansvarar för grundimages?
12. Vem ansvarar för att leverantörens images uppdateras?
13. Vem godkänner avvikelser från plattformsstandard?
14. Vem följer upp att leverantören uppfyller tekniska och säkerhetsmässiga åtaganden?
15. Vem äger risken om systemet inte är förvaltningsbart?

### Om leverantörsbyte och långsiktighet

16. Kan en annan leverantör ta över utan orimligt kunskapstapp?
17. Har myndigheten tillgång till nödvändiga bygg- och konfigurationsunderlag?
18. Kan vi återskapa en tidigare leverans?
19. Vet vi vilka beroenden som måste uppdateras under avtalstiden?
20. Stödjer avtalet kontinuerligt tekniskt underhåll?

## Sammanfattning

Containerteknik förändrar vad en myndighet behöver upphandla och kravställa.

Det räcker inte att beställa funktionalitet. Myndigheten behöver också säkerställa att IT-stödet kan byggas, testas, paketeras, spåras, driftsättas, övervakas, säkras och förvaltas i den containerbaserade målmiljön.

De viktigaste punkterna är:

- Upphandling behöver omfatta leveransförmåga, inte bara systemfunktion.
- Leverantörer behöver förstå och följa myndighetens målplattform och standarder.
- Krav bör omfatta paketering, pipeline, testbarhet, spårbarhet, driftbarhet och livscykelhantering.
- Säkerhet och regelefterlevnad behöver byggas in i krav och uppföljning.
- Dokumentation ska göra det möjligt att förvalta, felsöka och byta leverantör.
- Avtal behöver stödja förändring över tid, eftersom plattformar, beroenden och säkerhetskrav utvecklas.
- Chefer behöver säkerställa samverkan mellan upphandling, juridik, IT, säkerhet, drift och förvaltning.

Kapitlets kärna är enkel:

**En modern containerplattform kan inte kompensera för en upphandling som beställer gårdagens arbetssätt.**

## Nästa steg

I nästa kapitel samlas bokens delar i en praktisk färdplan. Då går vi från förståelse och enskilda styrfrågor till hur en myndighet kan planera själva förändringsresan: från nuläge, via pilot och styrmodell, till en fungerande containerplattform som är tekniskt, organisatoriskt och förvaltningsmässigt hållbar.
