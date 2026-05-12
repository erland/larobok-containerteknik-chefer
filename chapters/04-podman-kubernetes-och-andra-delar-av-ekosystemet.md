# Kapitel 4: Podman, Kubernetes och andra delar av ekosystemet

## Varför detta kapitel finns

I kapitel 3 flyttade vi fokus från enskilda servrar till plattformar. Det är ett viktigt steg för att förstå containerteknik på chefsnivå. Men när en organisation börjar diskutera containerplattformar dyker snabbt många namn upp: Podman, Docker, Kubernetes, OpenShift, registry, runtime, cluster, pipeline och ibland även begrepp som GitOps, service mesh och platform engineering.

För en chef kan det låta som en samling konkurrerande produkter. I praktiken är det bättre att se dem som olika delar av ett ekosystem.

Det här kapitlet hjälper dig att förstå de viktigaste byggstenarna utan att behöva kunna installera eller konfigurera dem. Målet är inte att du ska bli teknisk specialist. Målet är att du ska kunna förstå vad som diskuteras, skilja mellan olika typer av beslut och ställa rätt frågor till specialister, leverantörer och interna team.

Den viktigaste insikten i kapitlet är denna:

> En containerplattform är inte ett enda verktyg. Den är en samverkan mellan verktyg, standarder, ansvar, arbetssätt och styrning.

När en myndighet säger “vi ska införa Kubernetes” eller “vi ska använda Podman” är det därför bara början på diskussionen. Den större frågan är: vilken förmåga vill organisationen bygga, vem ska ansvara för den och hur ska den användas i utveckling, test, förvaltning och drift?

## Lärandemål

Efter kapitlet ska du kunna:

- förstå skillnaden mellan ett verktyg som kör containrar och en plattform som orkestrerar många containrar
- förklara Podman och Kubernetes på en övergripande chefsnivå
- känna igen centrala delar i ett containerbaserat ekosystem
- skilja mellan produktnamn, tekniska funktioner och organisatoriska beslut
- ställa relevanta frågor om ansvar, verktygsval, standarder och förvaltningsmodell

## Innan vi börjar

Vi bygger vidare på begreppen från tidigare kapitel:

- **Container:** en isolerad och standardiserad körmiljö där en applikation kan köras tillsammans med sina beroenden.
- **Image:** en paketerad mall som används för att starta containrar.
- **Plattform:** en gemensam teknisk och organisatorisk förmåga för att köra och förvalta applikationer på ett standardiserat sätt.
- **Standardisering:** gemensamma regler, mönster och lösningar som minskar variation och personberoende.
- **Driftmodell:** hur ansvar, arbetssätt, verktyg och beslut organiseras för att hålla IT-stöd fungerande över tid.

I det här kapitlet introduceras tre nya huvudbegrepp:

- **Container runtime:** den del som faktiskt startar och kör containrar på en maskin.
- **Orchestration:** samordning av många containrar, till exempel var de ska köras, hur de ska uppdateras och hur de ska återstartas vid fel.
- **Kubernetes:** en vanlig plattform för att orkestrera containeriserade applikationer i större miljöer.

## Verktyg, plattform och ekosystem

Ett vanligt misstag är att prata om containerteknik som om allt vore samma sak. Det är förståeligt, eftersom begreppen ofta används samtidigt. Men för att kunna fatta bra beslut behöver man skilja mellan nivåerna.

Ett förenklat sätt att se ekosystemet är:

| Nivå | Vad nivån gör | Exempel på begrepp |
|---|---|---|
| Paketering | Gör applikationen körbar som container | Image, Containerfile, Dockerfile |
| Körning | Startar och kör containern | Container runtime, Podman, Docker |
| Lagring och distribution | Lagrar och tillhandahåller images | Registry |
| Orkestrering | Samordnar många containrar | Kubernetes |
| Plattform | Ger organisationen en styrd förmåga | Containerplattform, OpenShift, plattformsteam |
| Leveransflöde | Bygger, testar och godkänner förändringar | Pipeline, automatiserade kontroller |
| Styrning | Bestämmer ansvar, krav och regler | Policy, roller, förvaltningsmodell |

Det här är inte en fullständig teknisk karta. Den är avsedd att hjälpa dig som chef att sortera diskussionen.

När en tekniker säger “vi behöver Podman” kan det handla om lokal utveckling, byggande av images eller körning av containrar på en enskild maskin. När någon säger “vi behöver Kubernetes” handlar det oftare om hur många containeriserade applikationer ska köras och styras över tid. När någon säger “vi behöver en plattform” handlar det både om teknik och om organisatorisk förmåga.

## Podman: att bygga och köra containrar

Podman är ett verktyg för att arbeta med containrar och container images. Det kan användas för att bygga, hämta, starta, stoppa och hantera containrar. För en chef är det viktigast att förstå Podman som ett verktyg nära utvecklare, tekniker och plattformsnära team.

Podman används ofta i sammanhang där man vill kunna arbeta med containrar utan att först ha en fullskalig containerplattform. Ett utvecklingsteam kan till exempel använda Podman för att testa att en applikation kan byggas och köras som container innan den går vidare till test eller produktion.

En enkel analogi är att Podman är som en verkstadsbänk. Där kan teamet bygga, prova och inspektera en container. Kubernetes är mer som en trafikledning eller produktionsmiljö där många containrar ska samordnas, övervakas och hållas igång.

Det betyder inte att Podman är oviktigt. Tvärtom kan ett sådant verktyg vara centralt för att skapa bra leveransflöden. Om utvecklingsteam, testare och plattformsteam kan arbeta med samma typ av images minskar risken att problem upptäcks sent.

För en myndighet som Nordverk kan Podman vara relevant i flera situationer:

- utvecklingsteam bygger och testar applikationer lokalt
- leverantörer visar att deras applikation går att köra som container
- tekniker analyserar en image innan den godkänns
- plattformsteam skapar standardiserade exempel för hur applikationer ska paketeras
- testmiljöer använder samma paketering som senare ska användas i produktion

Chefsfrågan är alltså inte bara “ska vi använda Podman?” Den mer användbara frågan är: “Vilka verktyg ska våra team använda för att bygga och verifiera containeriserade leveranser innan de når plattformen?”

## Kubernetes: att samordna många containrar

Kubernetes är en plattform för att orkestrera containeriserade applikationer. Orkestrering betyder i det här sammanhanget att många containrar samordnas så att de körs på rätt plats, i rätt antal, med rätt konfiguration och med möjlighet att återstartas, uppdateras och övervakas.

Det går att köra en container manuellt. Men i en större organisation räcker det inte. Ett samhällsviktigt IT-stöd kan bestå av flera komponenter. Det kan behöva skalas upp vid hög belastning, uppdateras utan onödigt långa avbrott, övervakas kontinuerligt och återstartas om något går fel. Flera IT-stöd kan dessutom dela samma plattform.

Det är här Kubernetes kommer in.

På chefsnivå kan Kubernetes förstås som ett styrsystem för containeriserade applikationer. Det håller reda på vilket önskat läge organisationen har beskrivit och försöker få den tekniska miljön att motsvara det läget.

Exempel:

- “Den här applikationen ska köras i tre instanser.”
- “Den ska bara använda denna godkända image.”
- “Den ska ha vissa resursgränser.”
- “Den ska exponeras på ett kontrollerat sätt.”
- “Om en instans faller bort ska en ny startas.”

Det här skiljer sig från manuell drift. I en traditionell modell kanske någon loggar in på en server, installerar programvara, ändrar konfiguration och startar om tjänster. I en Kubernetes-baserad modell beskriver organisationen i stället hur applikationen ska köras, och plattformen arbetar för att uppnå det läget.

Det betyder inte att allt blir automatiskt bra. Kubernetes är kraftfullt, men också komplext. Det kräver kompetens, styrning, säkerhetskontroller, standarder och en fungerande driftmodell. En myndighet som inför Kubernetes utan tydligt ägarskap riskerar att flytta komplexiteten från serverrummet till plattformen.

## Orchestration: varför samordning behövs

Orchestration, eller orkestrering, är ett av de viktigaste begreppen i kapitlet. Ordet kan låta abstrakt, men idén är enkel: när många containrar ska köras samtidigt behöver någon eller något samordna dem.

I en liten miljö kan en tekniker starta en container för hand. I en större miljö uppstår snabbt frågor:

- På vilken maskin ska containern köras?
- Vad händer om maskinen går sönder?
- Hur många instanser behövs?
- Hur gör vi en uppdatering utan att skapa onödigt driftstopp?
- Hur hittar olika delar av applikationen varandra?
- Hur begränsas resurser så att ett system inte påverkar andra?
- Hur vet vi vilket läge som är godkänt?

Orkestrering handlar om att hantera sådana frågor på ett mer standardiserat sätt.

För en chef är det viktigt att förstå att orkestrering inte bara är teknisk bekvämlighet. Den påverkar organisationens förmåga att hantera incidenter, införa ändringar, skala kapacitet och minska personberoende.

Men orkestrering skapar också nya frågor:

- Vem får ändra det önskade läget?
- Vem granskar konfigurationer?
- Vem ansvarar när applikationen fungerar men plattformen inte gör det?
- Vem ansvarar när plattformen fungerar men applikationen är felkonfigurerad?
- Hur dokumenteras beslut och undantag?

Det är därför containerplattformar kräver både teknisk och organisatorisk mognad.

## Registry: platsen där images hämtas och kontrolleras

I kapitel 2 introducerades begreppet image. I kapitel 5 kommer vi att gå djupare in i images, registries och spårbarhet. Men redan här behöver vi förstå rollen som ett registry spelar i ekosystemet.

Ett registry är en plats där container images lagras och hämtas. Man kan se det som ett kontrollerat bibliotek för applikationspaket.

För en statlig myndighet är detta inte en detalj. Om organisationen inte vet varifrån images kommer, vem som byggt dem, vilka versioner som är godkända och vilka säkerhetskontroller som gjorts, blir containerteknik snabbt en ny riskkälla.

Ett registry bör därför inte bara ses som teknisk lagring. Det är en del av myndighetens kontrollkedja.

Frågor som hör hemma här är:

- Vilka images får användas?
- Vem får publicera images?
- Hur länge får gamla images finnas kvar?
- Hur kopplas en image till kod, testresultat och godkännanden?
- Hur hanteras images från externa leverantörer?

Det här är exempel på hur ett tekniskt begrepp snabbt blir en ledningsfråga.

## OpenShift och andra distributionsplattformar

I många organisationer möter chefer inte bara Kubernetes som öppen källkod, utan även paketerade plattformar och produkter som bygger på eller använder Kubernetes. Ett vanligt exempel är OpenShift.

En sådan plattform kan innehålla Kubernetes, men också ytterligare funktioner, verktyg, säkerhetsinställningar, administrationsgränssnitt, stöd för utvecklingsflöden och leverantörssupport. Det kan vara relevant i organisationer som vill ha en mer sammanhållen plattformsprodukt i stället för att själva sätta ihop alla delar.

Det viktiga för en chef är att inte fastna i produktnamnet. Frågan är inte bara vilken produkt som väljs, utan vilken förmåga organisationen behöver.

Exempel på beslutsfrågor:

- Behöver vi en egen plattform, en köpt tjänst eller en kombination?
- Vilken kompetens ska finnas internt?
- Vilken del ansvarar leverantören för?
- Hur undviker vi inlåsning i lösningar som vi inte förstår?
- Hur säkerställer vi att plattformen stödjer våra arbetssätt, krav och säkerhetsbehov?

En plattform kan minska vissa tekniska bördor, men den tar inte bort behovet av styrning. Även om en leverantör driver delar av plattformen måste myndigheten förstå sitt ansvar för informationssäkerhet, kravställning, förvaltningsmodell och beslut.

## Myndigheten Nordverk: när begreppen börjar blandas ihop

På Nordverk har ledningen beslutat att utreda containerteknik. Ganska snabbt börjar olika grupper använda olika ord.

Utvecklingsteamet säger:

> “Vi behöver Podman eller Docker för att bygga och testa våra containrar.”

Driftorganisationen säger:

> “Vi behöver veta om produktion ska ligga på Kubernetes, OpenShift eller något annat.”

Säkerhetsfunktionen säger:

> “Vi behöver kontroll över vilka images som får köras.”

Förvaltningen säger:

> “Vi behöver veta vem som ansvarar när en container behöver uppdateras.”

Upphandlingsenheten säger:

> “Vi behöver formulera krav på leverantörer.”

Alla har rätt, men de pratar om olika delar av samma ekosystem. Problemet är inte att organisationen saknar teknikord. Problemet är att det saknas en gemensam karta.

Nordverk tar därför fram en enkel översikt:

- Utveckling och leverantörer ska kunna bygga och testa container images.
- Godkända images ska lagras i ett kontrollerat registry.
- Produktionskörning ska ske på en styrd containerplattform.
- Plattformen ska ha tydligt ägarskap.
- Säkerhetskontroller ska finnas i leveransflödet.
- Förvaltningen ska veta vem som ansvarar för uppdateringar, beroenden och incidenter.
- Ledningen ska följa upp förändringen som en organisatorisk förmåga, inte som ett isolerat teknikprojekt.

Det är först när Nordverk gör denna karta som diskussionen blir möjlig att styra.

## Påverkan på utveckling

För utvecklingsteam innebär containerteknik att det inte längre räcker att skriva kod som “fungerar på utvecklarens dator”. Teamet behöver också förstå hur applikationen paketeras, vilka beroenden den har och hur den ska startas i en standardiserad miljö.

Det betyder inte att alla utvecklare måste bli plattformsexperter. Men utvecklingsteam behöver ta större ansvar för körbarhet.

Exempel på förändringar:

- Applikationen behöver byggas som en image.
- Konfiguration behöver hanteras på ett kontrollerat sätt.
- Lokala tester bör likna senare miljöer.
- Leveransen bör fungera i pipeline och på plattform.
- Teamet behöver förstå grundläggande krav från plattformen.

För chefer innebär det att utvecklingsuppdrag och leverantörsavtal behöver omfatta mer än funktionalitet. De behöver också omfatta paketering, testbarhet, driftsättbarhet och förvaltningsbarhet.

## Påverkan på test

För testverksamheten kan containerteknik ge bättre möjligheter att skapa liknande miljöer och köra tester mer automatiserat. Men det kräver att test inte behandlas som en separat fas som börjar först när allt annat är färdigt.

När images används som leveransobjekt kan samma image testas i flera steg. Det stärker spårbarheten: det som går vidare mot produktion är inte en ny installation som någon satt ihop för hand, utan samma paketerade leverans som kontrollerats tidigare.

Samtidigt behöver teststrategin utvecklas. Det räcker inte att fråga om applikationen fungerar funktionellt. Organisationen behöver även testa sådant som start, stopp, konfiguration, loggning, beroenden, uppdatering och felhantering.

För chefer innebär det att testkapacitet och testansvar behöver ses som en del av förändringsresan.

## Påverkan på förvaltning

Förvaltningen påverkas eftersom containerteknik gör beroenden och versioner tydligare, men också mer kontinuerliga. En image är inte något som kan glömmas bort när systemet väl är i produktion. Den innehåller komponenter som kan behöva uppdateras av säkerhets-, stabilitets- eller kompatibilitetsskäl.

Förvaltningen behöver därför kunna svara på frågor som:

- Vilka images ingår i förvaltningsobjektet?
- Vem ansvarar för att de hålls uppdaterade?
- Hur hanteras sårbarheter i beroenden?
- Hur prioriteras tekniskt underhåll mot ny funktionalitet?
- Hur dokumenteras godkända versioner?

Detta innebär att containerteknik kan göra förvaltningen mer transparent, men bara om ansvar och arbetssätt följer med.

## Påverkan på drift

Driften påverkas kanske mest synligt. I en traditionell modell har drift ofta handlat om servrar, installationer, patchning, manuella kontroller och felsökning direkt i miljöer. I en containerplattform blir driften mer inriktad på plattformens hälsa, kapacitet, standarder, övervakning och automatiserade mönster.

Det innebär inte att driftkompetens blir mindre viktig. Den förändras.

Driftorganisationen behöver förstå:

- hur plattformen kör workloads
- hur resurser fördelas
- hur loggar och mätvärden samlas in
- hur incidenter analyseras
- hur uppdateringar av plattformen påverkar applikationerna
- hur ansvar delas mellan plattformsteam och applikationsteam

En vanlig risk är att organisationen tror att Kubernetes “tar hand om driften”. Det gör den inte. Kubernetes kan automatisera vissa uppgifter, men någon måste fortfarande utforma, förvalta, säkra och övervaka helheten.

## Vanliga chefsfällor

### Fälla 1: Att tro att ett produktval är samma sak som en strategi

Det är lätt att fråga: “Ska vi välja Kubernetes, OpenShift eller något annat?” Det är en relevant fråga, men den kommer för tidigt om organisationen inte först vet vilken förmåga som ska byggas.

**Hur man undviker det:**  
Börja med målbild, ansvar, säkerhetskrav, kompetens och leveransflöde. Låt produktvalet stödja strategin, inte ersätta den.

### Fälla 2: Att underskatta komplexiteten i Kubernetes

Kubernetes kan ge stora möjligheter, men det är inte en enkel genväg. Plattformen behöver designas, säkras, driftas och förvaltas.

**Hur man undviker det:**  
Be om en realistisk bedömning av kompetensbehov, driftmodell, support, säkerhetskontroller och förvaltning innan beslut fattas.

### Fälla 3: Att låta varje team välja egna verktyg utan styrning

Lokal frihet kan kännas effektivt i början. Men om varje team väljer egna byggmönster, registries, konfigurationer och driftsättningssätt ökar variationen snabbt.

**Hur man undviker det:**  
Skapa gemensamma standarder, men gör dem praktiskt användbara. Standardisering ska hjälpa teamen, inte bara begränsa dem.

### Fälla 4: Att se registry och images som tekniska detaljer

Om organisationen saknar kontroll över images saknar den kontroll över vad som faktiskt körs.

**Hur man undviker det:**  
Behandla registry, imageflöde och godkännanden som en del av myndighetens styrning och säkerhetsarbete.

### Fälla 5: Att glömma leverantörerna

Många myndigheter är beroende av externa leverantörer. Om leverantörerna fortsätter leverera enligt gamla mönster kommer organisationen inte få full effekt av containerplattformen.

**Hur man undviker det:**  
Inför krav på paketering, testbarhet, dokumentation, uppdateringsansvar och anpassning till myndighetens plattform.

## Frågor att ställa i den egna organisationen

1. Vilka containerverktyg används redan i dag, formellt eller informellt?
2. Har vi en gemensam karta över container-ekosystemet, eller används begreppen olika i olika grupper?
3. Ska vi själva drifta containerplattformen, köpa den som tjänst eller använda en kombination?
4. Vem äger beslutet om vilka images som får användas?
5. Var ska godkända images lagras?
6. Vilka krav ställer vi på leverantörer som ska leverera containeriserade applikationer?
7. Har vi kompetens att drifta och säkra Kubernetes, eller behöver vi en annan modell?
8. Hur ska ansvar fördelas mellan utvecklingsteam, plattformsteam, förvaltning, drift och säkerhet?
9. Vilka tekniska val är strategiska, och vilka bör standardiseras för att minska variation?
10. Hur säkerställer vi att plattformen blir en gemensam förmåga och inte bara ett nytt teknikprojekt?

## Snabb sammanfattning

- Containerteknik består av flera delar: paketering, körning, registry, orkestrering, plattform, leveransflöde och styrning.
- Podman är ett verktyg för att bygga, köra och hantera containrar och images.
- Kubernetes används för att orkestrera många containeriserade applikationer i större miljöer.
- Orchestration handlar om att samordna containrar, önskat läge, uppdateringar, återstarter, resurser och tillgänglighet.
- Ett registry är en central del av kontrollkedjan eftersom det hanterar vilka images som finns och kan användas.
- Produktval är inte samma sak som strategi.
- För chefer är den centrala frågan vilken organisatorisk och teknisk förmåga myndigheten behöver bygga.
- Containerplattformar påverkar utveckling, test, förvaltning och drift samtidigt.
- Utan tydligt ansvar riskerar organisationen att ersätta gammalt personberoende med ny plattformskomplexitet.

## Nästa steg

Nu har vi placerat Podman, Kubernetes och andra delar i ett begripligt ekosystem. Nästa kapitel går djupare in i en av de viktigaste kontrollpunkterna: **images, registries och spårbarhet**.

Där kommer vi att titta närmare på hur myndigheten kan veta vad som faktiskt körs, var det kommer ifrån, vem som godkänt det och hur det kan följas genom hela leveransflödet.
