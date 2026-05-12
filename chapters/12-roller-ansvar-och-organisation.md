# Kapitel 12: Roller, ansvar och organisation

## Varför detta kapitel finns

När en myndighet börjar använda containerteknik blir det snabbt tydligt att tekniken inte bara ändrar hur applikationer körs. Den ändrar också vem som behöver göra vad, när det ska göras och hur ansvar ska följas upp.

I en traditionell organisation kan ansvar ofta vara uppdelat i tydliga men ganska separata delar:

- utveckling skriver kod
- test testar systemet
- förvaltning prioriterar ändringar och håller ihop systemets livscykel
- drift håller servrar och produktionsmiljöer igång
- säkerhet granskar, ställer krav och följer upp
- upphandling och leverantörsstyrning hanterar externa parter

Den uppdelningen kan fungera när leveranser är få, långsamma och starkt manuella. Men när applikationer byggs som images, testas i pipelines, lagras i registries och körs på en gemensam plattform räcker det inte att varje funktion bara optimerar sin egen del.

Containerteknik skapar ett mer sammanhängande leveransflöde. Därför behöver också ansvarsfördelningen bli mer sammanhängande.

Kapitlets huvudbudskap är:

**En containerplattform blir inte styrbar bara för att tekniken är standardiserad. Den blir styrbar när roller, mandat, ansvar och samverkan är lika tydliga som tekniken.**

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förstå varför containerteknik förändrar roller och ansvar
- skilja mellan plattformsteam, produktteam och stödjande specialistfunktioner
- se varför otydligt ansvar leder till risk även när tekniken fungerar
- identifiera vanliga organisatoriska konflikter vid införande av containerplattform
- formulera frågor som hjälper den egna organisationen att skapa en hållbar ansvarsmodell

## Innan vi börjar

Vi bygger vidare på flera tidigare begrepp:

- **Plattform**: den gemensamma tekniska och organisatoriska förmågan att köra IT-stöd standardiserat.
- **Pipeline**: flödet som bygger, testar, kontrollerar och levererar ändringar.
- **Registry**: platsen där godkända images lagras och hämtas.
- **Plattformsdrift**: drift av den gemensamma containerplattformens hälsa, kapacitet och standarder.
- **Applikationsdrift**: driftansvar kopplat till ett specifikt IT-stöd.
- **Policy**: en regel eller styrande princip som kan dokumenteras och ibland omsättas till teknisk kontroll.
- **Regelefterlevnad**: förmågan att följa och visa att organisationen följer beslutade krav.

I detta kapitel introduceras tre nya huvudbegrepp:

- **Plattformsteam**
- **Produktteam**
- **Ansvarsmodell**

Det viktiga är inte exakt vilka namn organisationen använder. Det viktiga är att ansvar, mandat och samverkan blir tillräckligt tydliga för att fungera i praktiken.

## Huvudförklaring

### Tekniken binder ihop ansvar som tidigare var separerat

I en manuell driftmodell kan problem ofta hamna mellan organisatoriska stolar.

Utveckling kan säga: “Koden fungerar hos oss.”  
Test kan säga: “Vi testade det vi fick.”  
Drift kan säga: “Installationsinstruktionen var otydlig.”  
Förvaltning kan säga: “Vi beställde bara en ändring.”  
Säkerhet kan säga: “Vi kom in för sent i processen.”

När containerteknik införs försvinner inte dessa gränser automatiskt. Men de blir mer synliga.

En container image innehåller inte bara kod. Den uttrycker också antaganden om körmiljö, beroenden, konfiguration, startbeteende, loggning och ibland säkerhetsinställningar. En pipeline innehåller inte bara tekniska steg. Den uttrycker också vilka kontroller organisationen anser nödvändiga före produktion. En plattform är inte bara infrastruktur. Den uttrycker också standarder för hur IT-stöd får köras.

Därför blir frågan om ansvar mycket viktigare.

Vem ansvarar för att en applikation går att bygga?  
Vem ansvarar för att den går att testa?  
Vem ansvarar för att den använder godkända grundimages?  
Vem ansvarar för att den körs med rätt behörigheter?  
Vem ansvarar för larm, loggar och felsökning?  
Vem ansvarar för att tekniska beroenden uppdateras över tid?

Om svaren är otydliga uppstår en risk: organisationen får modern teknik men gamla glapp.

### Plattformsteam: mer än teknisk drift

Ett plattformsteam ansvarar för den gemensamma containerplattformen som flera IT-stöd använder.

Det kan handla om:

- plattformens tillgänglighet
- kapacitet och resursfördelning
- uppgraderingar
- standarder för hur applikationer ska köras
- gemensamma policies
- integration med registry, pipelines och övervakning
- gemensam loggning, mätvärden och larm
- stöd till produktteam och leverantörer

Plattformsteamet ska inte bli en ny flaskhals som manuellt godkänner allt. Då riskerar organisationen att återskapa gamla driftsmönster i en ny teknisk miljö.

Ett väl fungerande plattformsteam gör i stället rätt väg enkel att följa. Det erbjuder standardiserade mönster, tydliga krav, återanvändbara lösningar och gemensamma kontroller.

För chefer är den viktiga frågan:

**Har plattformsteamet mandat att sätta standarder, eller förväntas det bara “hålla tekniken igång”?**

Utan mandat blir plattformsteamet ofta ansvarigt för problem som det inte har möjlighet att förebygga.

### Produktteam: ansvar för IT-stödets körbarhet

Ett produktteam ansvarar för ett specifikt IT-stöd eller en tydlig del av ett IT-stöd. I vissa organisationer används andra namn, till exempel systemteam, applikationsteam, leveransteam eller förvaltningsteam. Här använder vi produktteam som samlingsbegrepp.

I en containerbaserad modell räcker det inte att produktteamet bara ansvarar för funktionalitet. Teamet behöver också ta ansvar för att IT-stödet är körbart, testbart, övervakat och förvaltningsbart inom plattformens ramar.

Det betyder inte att alla i teamet måste vara Kubernetes-specialister. Men teamet behöver förstå vad deras applikation kräver av plattformen och vad plattformen kräver av applikationen.

Produktteamet behöver kunna svara på frågor som:

- Hur byggs applikationens image?
- Vilka grundimages och beroenden används?
- Vilka tester körs automatiskt?
- Vilka konfigurationsvärden skiljer mellan miljöer?
- Vilka loggar och mätvärden behövs för felsökning?
- Hur märks en version?
- Hur återställs tjänsten om något går fel?
- Vem agerar vid incident?

Detta förändrar också relationen mellan utveckling och förvaltning. Förvaltning kan inte bara ta emot en färdig teknisk lösning och sedan “äga” den i ett separat skede. Förvaltningsbarhet måste byggas in tidigare.

### Säkerhet och regelefterlevnad behöver integreras

I kapitel 11 såg vi att säkerhet inte kan vara en sista kontroll i slutet av leveransflödet. Detsamma gäller roller.

Säkerhetsfunktionen behöver fortfarande ställa krav, följa upp risker och säkerställa att myndighetens styrning fungerar. Men i en containerbaserad modell behöver många säkerhetskrav omsättas i arbetssätt, policies och tekniska kontroller.

Det kan till exempel handla om:

- vilka grundimages som är tillåtna
- vilka sårbarhetsnivåer som stoppar en leverans
- vilka behörigheter en container får ha
- hur hemligheter och konfigurationsvärden hanteras
- hur undantag beslutas och tidsbegränsas
- hur loggar och händelser sparas och följs upp

Säkerhetsfunktionen bör därför inte bara vara granskare. Den behöver också vara kravställare, rådgivare och uppföljare i ett flöde där mycket sker automatiserat.

En vanlig chefsfälla är att tro att säkerhet antingen ska “äga” alla kontroller eller att säkerhet helt kan lämnas till tekniken. Båda synsätten är otillräckliga.

Säkerhet äger inte hela leveransen. Men säkerhetskrav måste vara synliga och bindande i hela leveransen.

### Förvaltning behöver mandat över livscykeln

I kapitel 9 såg vi att containerteknik gör livscykelhantering mer synlig. Beroenden, grundimages, pipelines, plattformsanpassningar och säkerhetsuppdateringar behöver hanteras kontinuerligt.

Det betyder att förvaltningens roll behöver stärkas, inte försvagas.

Förvaltningen behöver kunna prioritera tekniskt underhåll, inte bara ny funktionalitet. Den behöver förstå vilka risker som uppstår om images inte byggs om, beroenden inte uppdateras eller pipeline-kontroller kringgås. Den behöver också kunna föra dialog med både verksamhet, utveckling, drift, säkerhet och leverantörer.

I en myndighet är detta särskilt viktigt eftersom IT-stöd ofta lever länge. Ett system som fungerar i dag kan snabbt bli svårt att underhålla om containerplattform, grundimages, bibliotek eller säkerhetskrav förändras runt omkring det.

Förvaltningsfrågan blir därför:

**Har förvaltningen mandat och budget att hålla IT-stödet körbart, säkert och uppdateringsbart över tid?**

Om svaret är nej riskerar containerplattformen att bli en plats där gammal teknisk skuld bara paketeras på ett modernare sätt.

### Ansvarsmodell: från muntlig förståelse till beslutad struktur

En ansvarsmodell beskriver vem som ansvarar för vad, vem som beslutar vad och hur olika roller samverkar.

I en containerbaserad miljö bör ansvarsmodellen inte bara beskriva organisationsrutor. Den bör beskriva ansvar längs leveransflödet.

Exempel på områden som behöver tydliggöras:

| Område | Fråga som behöver besvaras |
|---|---|
| Applikationskod | Vem ansvarar för funktion, kvalitet och kodnära beroenden? |
| Image | Vem ansvarar för hur applikationen paketeras och versioneras? |
| Grundimage | Vem godkänner och underhåller gemensamma baser? |
| Pipeline | Vem äger bygg-, test- och kontrollflödet? |
| Registry | Vem får publicera, godkänna och ta bort images? |
| Plattform | Vem ansvarar för kapacitet, uppgraderingar och gemensamma policies? |
| Produktion | Vem ansvarar för tillgänglighet, incidenter och återställning? |
| Säkerhet | Vem ställer krav, följer upp och beslutar om undantag? |
| Förvaltning | Vem prioriterar livscykel, tekniskt underhåll och långsiktig förvaltningsbarhet? |
| Leverantörer | Vem säkerställer att externa parter följer myndighetens modell? |

Den här typen av ansvarskarta behöver vara begriplig för både ledning och praktiska team. Om den bara finns som ett övergripande styrdokument men inte syns i vardagens arbetsflöden kommer den inte att fungera.

En bra ansvarsmodell ska hjälpa människor att agera rätt även när något går fel.

## Scenario: Myndigheten Nordverk

Nordverk har nu kommit långt i sin containerresa.

De har en containerplattform. Flera team bygger images. Pipelines kör tester och säkerhetskontroller. Ett internt registry används för godkända images. Driftorganisationen har börjat arbeta mer med plattformsdrift än med enskilda servrar.

På pappret ser utvecklingen positiv ut.

Men efter några månader uppstår nya problem.

Ett produktteam anser att plattformsteamet är för långsamt med att införa nya funktioner. Plattformsteamet menar att produktteamen inte följer standarderna. Säkerhetsfunktionen upptäcker att vissa undantag har blivit permanenta. Förvaltningen har svårt att få budget för uppdatering av gamla images eftersom verksamheten hellre prioriterar ny funktionalitet. En leverantör levererar en containeriserad applikation, men den passar dåligt in i myndighetens pipeline och övervakning.

Vid ett ledningsmöte sammanfattar IT-chefen situationen:

“Vi har infört mycket av tekniken, men vi har inte infört en gemensam ansvarskarta.”

Nordverk beslutar därför att ta fram en ansvarsmodell för containerbaserade IT-stöd. Den ska inte bara beskriva roller utan också koppla ansvar till leveransflödet: från kod och image till pipeline, registry, plattform, produktion och förvaltning.

Arbetet leder till tre viktiga beslut:

1. Plattformsteamet får tydligt mandat att sätta gemensamma tekniska standarder.
2. Produktteamen får tydligt ansvar för att deras IT-stöd är byggbara, testbara, övervakningsbara och förvaltningsbara.
3. Förvaltning och säkerhet får tydligare roll i prioritering, livscykelhantering, riskbeslut och uppföljning.

Det löser inte alla konflikter. Men det gör konflikterna synliga och möjliga att styra.

## Påverkan på utveckling, test, förvaltning och drift

### Utveckling

Utveckling påverkas genom att ansvaret breddas från kod till körbar leverans. Utvecklingsteam behöver förstå hur applikationen byggs som image, hur den konfigureras, hur den loggar, hur den testas och hur den beter sig på plattformen.

Det betyder inte att utveckling ska ta över all drift. Men utveckling kan inte längre lämna över en applikation utan att ta ansvar för dess körbarhet.

### Test

Test påverkas genom att test inte längre är en separat fas där “någon annan” försöker verifiera en leverans. Testbarhet behöver byggas in i applikation, pipeline och miljöer.

Testfunktionen behöver därför samverka nära med både produktteam och plattformsteam. Den behöver påverka vilka tester som automatiseras, vilka miljöer som behövs och vilka kvalitetsgrindar som ska finnas före produktion.

### Förvaltning

Förvaltning påverkas genom att livscykelansvaret blir mer tekniskt och mer kontinuerligt. Förvaltningen behöver kunna prioritera uppdateringar av images, beroenden, pipelines och plattformsanpassningar.

Förvaltningens roll blir att hålla ihop funktion, risk, ekonomi, livscykel och förvaltningsbarhet över tid.

### Drift

Drift påverkas genom att rollen delas tydligare mellan plattformsdrift och applikationsdrift.

Plattformsteamet ansvarar för den gemensamma plattformens förmåga. Produktteam eller applikationsansvariga behöver samtidigt förstå och hantera applikationens beteende i produktion.

Den viktiga förändringen är att drift inte längre kan vara en plats där alla otydligheter till sist hamnar.

## Vanliga chefsfällor

### Fälla 1: Att tro att nya roller räcker

Det är vanligt att skapa nya rollnamn: plattformsteam, DevOps-team, produktteam eller cloud team. Men nya namn löser inte otydligt ansvar.

Frågan är inte vad teamet heter. Frågan är vilket mandat teamet har, vilket ansvar det bär och hur det samverkar med andra.

### Fälla 2: Att göra plattformsteamet till ny flaskhals

Om plattformsteamet måste godkänna varje detalj manuellt riskerar organisationen att bygga en modern variant av gammal driftkö.

Plattformsteamets viktigaste uppgift är inte att vara grindvakt i varje enskilt ärende. Det är att skapa standarder, verktyg och kontroller som gör rätt arbetssätt möjligt i stor skala.

### Fälla 3: Att produktteam bara mäts på ny funktionalitet

Om produktteam bara belönas för nya funktioner kommer tekniskt underhåll, säkerhetsuppdateringar, testbarhet och förvaltningsbarhet att prioriteras ned.

Det leder till risker som senare hamnar hos drift, säkerhet eller förvaltning.

### Fälla 4: Att säkerhet kommer in för sent

Om säkerhetsfunktionen bara granskar i slutet kommer den ofta att uppfattas som bromsande. Om säkerhetskrav däremot byggs in i policies, pipelines och gemensamma standarder blir säkerhet en del av leveransförmågan.

### Fälla 5: Att ansvar blir otydligt vid incidenter

Den verkliga prövningen av en ansvarsmodell sker ofta vid incident. Om alla måste börja diskutera vem som äger problemet när produktionen redan är påverkad är modellen för svag.

Ansvar vid incident behöver vara tydligt innan incidenten inträffar.

## Frågor att ställa i den egna organisationen

- Vem äger den gemensamma containerplattformen?
- Har plattformsteamet mandat att sätta standarder, eller bara ansvar att hålla tekniken igång?
- Vem ansvarar för att ett IT-stöd är byggbart, testbart och körbart på plattformen?
- Vem ansvarar för att images uppdateras när grundimages eller beroenden förändras?
- Vem får besluta om undantag från plattforms- eller säkerhetskrav?
- Hur tidsbegränsas och följs undantag upp?
- Vem ansvarar för incidenter där både applikation och plattform kan vara inblandade?
- Hur involveras test, säkerhet och förvaltning i pipeline- och plattformsbeslut?
- Har leverantörer tydliga ansvar i samma modell som interna team?
- Mäter vi team på långsiktig förvaltningsbarhet eller bara på levererad funktionalitet?

## Tecken på att ansvarsmodellen fungerar

En ansvarsmodell fungerar inte för att den är beslutad. Den fungerar när den hjälper organisationen att agera.

Tecken på att modellen börjar fungera är:

- team vet vilka beslut de själva får fatta
- undantag är synliga, tidsbegränsade och ägda
- plattformsteamet kan säga nej med stöd av beslutade standarder
- produktteam förstår sitt ansvar för körbarhet och övervakning
- förvaltning kan prioritera tekniskt underhåll utan att varje gång behöva börja från noll
- säkerhetskrav syns i pipeline och plattform, inte bara i dokument
- incidenter leder till lärande och förbättring av arbetssätt
- leverantörer kravställs på samma sätt som interna team

## Snabb sammanfattning

- Containerteknik gör ansvar mellan utveckling, test, förvaltning, drift och säkerhet mer sammanhängande.
- Plattformsteam behöver mandat att sätta standarder, inte bara ansvar att hålla tekniken igång.
- Produktteam behöver ta ansvar för körbarhet, testbarhet, övervakning och förvaltningsbarhet.
- Säkerhetsfunktionen behöver vara integrerad i arbetssätt och kontroller, inte bara granska i slutet.
- Förvaltning behöver mandat och budget för livscykelhantering och tekniskt underhåll.
- En ansvarsmodell ska beskriva ansvar längs leveransflödet, inte bara i organisationsrutor.
- Otydligt ansvar märks särskilt vid incidenter, undantag, leverantörsleveranser och tekniskt underhåll.

## Nästa steg

I nästa kapitel går vi vidare till upphandling, leverantörer och kravställning.

När roller och ansvar har blivit tydligare kan myndigheten också ställa bättre krav externt. Det räcker inte att en leverantör säger att ett IT-stöd “stödjer containers” eller “kan köras i Kubernetes”. Myndigheten behöver kunna kravställa paketering, pipeline-anpassning, spårbarhet, testbarhet, säkerhetskontroller, förvaltningsbarhet och ansvar över tid.
