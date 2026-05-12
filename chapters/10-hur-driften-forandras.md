# Kapitel 10: Hur driften förändras

## Varför detta kapitel finns

När en organisation börjar använda containerteknik förändras driftens uppdrag. Det betyder inte att drift blir mindre viktig. Tvärtom blir driftens roll ofta mer strategisk, men på ett annat sätt än tidigare.

I en traditionell miljö har drift ofta handlat om servrar, installationer, patchning, kapacitet, behörigheter, schemalagda körningar, manuella kontroller, felsökning och incidenthantering. Mycket av arbetet har varit nära kopplat till enskilda system och deras specifika miljöer. I en myndighet med lång historik kan det finnas många olika tekniska mönster, speciallösningar och undantag.

Med containerteknik flyttas en del av fokus. Driften handlar inte längre bara om att hålla enskilda servrar och system igång. Den handlar också om att hålla en gemensam plattform stabil, säker, övervakad, skalbar och användbar för många IT-stöd. Därmed förändras också relationen mellan drift, utveckling, test, förvaltning, säkerhet och leverantörer.

En containerplattform kan starta om containrar, placera dem på lämpliga noder, rulla ut nya versioner och skapa mer standardiserade driftsmönster. Men den gör inte organisationen automatiskt mogen. Den kräver nya arbetssätt, nya kontroller, bättre gemensamma standarder och tydligare ansvar.

För en chef är den viktiga frågan därför inte: “Behöver vi fortfarande drift?” Den viktiga frågan är: “Vilken typ av driftförmåga behöver vi när fler IT-stöd körs på en gemensam containerplattform?”

Detta kapitel handlar om hur driften förändras från manuell serverhantering till plattformsdrift, automatisering, övervakning, kapacitetsstyrning och tydligare samspel med applikationsteam.

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förklara hur driftrollen förändras när organisationen går mot containerplattformar
- skilja mellan applikationsdrift och plattformsdrift
- förstå varför övervakning, loggning och larm behöver utvecklas
- se varför automation inte tar bort ansvar, utan förändrar var ansvaret ligger
- identifiera chefsfrågor om incidenthantering, kapacitet, tillgänglighet och ansvarsfördelning

## Innan vi börjar

I tidigare kapitel har vi sett att containrar gör applikationer mer standardiserat paketerade. Vi har sett att images kan lagras i registries, att pipelines kan bygga och testa dem, och att förvaltningen behöver följa tekniska livscykler över tid.

Nu flyttar vi fokus till produktion.

Produktion är där myndighetens IT-stöd faktiskt används. Det är där verksamheten är beroende av att systemen fungerar. Det är också där brister i ansvar, övervakning, test, förvaltning och säkerhet till slut blir synliga.

Containerteknik kan göra produktionsdrift mer förutsägbar, men bara om organisationen förstår vad som förändras. Om gamla manuella arbetssätt bara flyttas in i en ny teknisk plattform riskerar myndigheten att få både ny komplexitet och gamla problem.

## Från serverdrift till plattformsdrift

Ett vanligt sätt att beskriva förändringen är att drift går från serverdrift till plattformsdrift.

**Serverdrift** innebär att driftorganisationen ofta arbetar nära enskilda servrar, operativsystem, installationer och systemmiljöer. Varje IT-stöd kan ha egna lösningar, egna instruktioner och egna undantag. Felsökning kan innebära att någon loggar in på en server, granskar filer, startar om tjänster eller gör manuella ändringar.

**Plattformsdrift** innebär att driftorganisationen i stället ansvarar för en gemensam förmåga där många applikationer kan köras enligt standardiserade mönster. Fokus flyttas till plattformens hälsa, kapacitet, säkerhet, uppgraderingar, standarder, behörigheter, övervakning och automatiserade processer.

Det betyder inte att servrar försvinner. Containerplattformar kör fortfarande på fysisk eller virtuell infrastruktur. Men chefer behöver förstå att den operativa styrningen förändras. Den enskilda servern blir mindre central som styrningsobjekt. Plattformen och dess tjänster blir viktigare.

Det kan jämföras med skillnaden mellan att förvalta varje enskild vägsträcka separat och att förvalta ett helt vägnät med gemensamma regler, skyltning, underhållsplanering och trafikövervakning. Vägarna finns kvar, men styrningen behöver ske på systemnivå.

## Vad plattformsdrift omfattar

Plattformsdrift kan omfatta flera olika ansvarsområden. Exakt fördelning beror på organisationens storlek, säkerhetskrav, leverantörsmodell och tekniska val. Men på chefsnivå är följande områden viktiga att förstå.

### Plattformens tillgänglighet

Plattformen behöver vara tillgänglig för de IT-stöd som körs där. Om plattformen påverkas kan flera system påverkas samtidigt. Därför blir plattformen en gemensam kritisk förmåga.

Det kräver beslut om:

- tillgänglighetsmål
- redundans
- driftfönster
- uppgraderingsrutiner
- incidentprocesser
- beroenden till nätverk, lagring, identitetstjänster och övervakning

En chef behöver förstå att en gemensam plattform kan ge bättre standardisering, men också koncentrera ansvar och risk. Det är inte ett argument mot plattformar. Det är ett argument för tydlig styrning.

### Plattformens kapacitet

I en serverbaserad modell kan kapacitet ofta diskuteras system för system. I en containerplattform behöver kapacitet också hanteras gemensamt. Många applikationer delar på resurser som processorkraft, minne, nätverk och lagring.

Det väcker nya frågor:

- Hur vet vi att plattformen har tillräcklig kapacitet?
- Hur fördelas resurser mellan olika IT-stöd?
- Vilka system får prioritet vid belastning?
- Hur planeras kapacitet vid nya leveranser?
- Vem betalar för överkapacitet eller expansionsbehov?

Om dessa frågor inte hanteras kan plattformen bli en ny flaskhals. Organisationen kanske har automatiserade leveranser, men saknar kapacitetsstyrning.

### Plattformens standarder

Plattformsdrift handlar också om att hålla gemensamma standarder levande. Det kan handla om hur applikationer ska logga, hur hälsokontroller ska definieras, hur konfiguration hanteras, vilka grundimages som får användas, hur nätverkspolicyer utformas och hur behörigheter ges.

Standarder är viktiga för drift därför att de gör applikationer mer lika att hantera. Om varje team gör på sitt eget sätt blir plattformen svårare att övervaka, felsöka och säkra.

För en chef är detta en central styrningsfråga. En plattform utan standarder riskerar att bli en teknisk gemensam yta där gamla olikheter fortsätter att växa.

### Plattformens uppgraderingar

En containerplattform behöver själv förvaltas. Plattformskomponenter uppdateras, säkerhetsbrister åtgärdas, integrationer förändras och nya funktioner införs. Detta behöver planeras och testas.

Det är lätt att underskatta detta. Många organisationer fokuserar på att “införa Kubernetes” eller “införa containerplattform”, men glömmer att plattformen därefter blir ett långsiktigt förvaltningsobjekt.

Frågan är inte bara hur plattformen byggs. Frågan är hur den hålls aktuell, säker och användbar år efter år.

## Applikationsdrift och plattformsdrift

När containerteknik införs blir det viktigt att skilja mellan applikationsdrift och plattformsdrift.

**Applikationsdrift** handlar om att ett visst IT-stöd fungerar som det ska. Det omfattar exempelvis applikationens tillgänglighet, svarstider, fel, loggar, integrationer, konfiguration, versioner och användarpåverkan.

**Plattformsdrift** handlar om att den gemensamma containerplattformen fungerar. Det omfattar exempelvis klusterhälsa, noder, nätverk, lagring, resursfördelning, behörigheter, policyer, plattformskomponenter och gemensamma övervakningslösningar.

I en enkel bild:

| Fråga | Applikationsdrift | Plattformsdrift |
|---|---|---|
| Vad är fokus? | Ett specifikt IT-stöd | Den gemensamma körplattformen |
| Vem påverkas? | Användare av ett system | Flera team och system |
| Typiska problem | Fel i applikation, integration, konfiguration eller data | Kapacitet, noder, nätverk, plattformskomponenter eller policy |
| Typiska aktörer | Applikationsteam, förvaltning, leverantör | Plattformsteam, drift, infrastruktur, säkerhet |
| Chefsfråga | Vem ansvarar för att systemet fungerar för verksamheten? | Vem ansvarar för att plattformen är stabil, säker och användbar? |

Denna uppdelning låter enkel, men i praktiken kan gränsen vara svår. Ett applikationsfel kan bero på plattformskonfiguration. Ett plattformsproblem kan synas först som ett applikationsproblem. En felaktig image kan se ut som ett driftproblem. En bristande pipeline kan orsaka incidenter i produktion.

Därför behöver organisationen inte bara teknisk övervakning, utan även tydliga samverkansformer.

## Driftens nya kompetensprofil

När driften förändras behöver även kompetensen utvecklas. Det betyder inte att all tidigare driftkompetens blir obsolet. Mycket av den är fortsatt värdefull: förståelse för produktion, stabilitet, incidenter, säkerhet, kapacitet, nätverk, operativsystem, beroenden och verksamhetskritiska system.

Men kompetensen behöver kompletteras.

Driftorganisationen behöver ofta mer kunskap om:

- containerplattformar
- deklarativ konfiguration
- automation
- pipelines
- loggning och mätvärden
- plattformsövervakning
- policybaserad styrning
- infrastruktur som kod
- samarbete med utvecklings- och applikationsteam

För chefer är detta en kompetens- och förändringsledningsfråga. Det räcker inte att köpa en plattform eller anlita en leverantör. Organisationen behöver förstå vilken intern förmåga som måste finnas kvar för att kunna styra, följa upp och fatta beslut.

En myndighet kan lägga ut delar av tekniken på leverantörer, men den kan inte lägga ut hela ansvaret för styrbarhet.

## Automation förändrar vad drift gör

Ett vanligt missförstånd är att automation betyder att drift inte längre behövs. Det stämmer inte. Automation betyder att vissa återkommande moment utförs av system i stället för av människor. Men människor behöver fortfarande bestämma vad som ska automatiseras, hur det ska kontrolleras, hur undantag hanteras och hur resultat följs upp.

I en traditionell miljö kan drift ha lagt mycket tid på manuella åtgärder:

- starta om tjänster
- kontrollera loggar
- genomföra installationer
- flytta filer
- ändra konfiguration
- kontrollera checklistor
- övervaka batchkörningar
- göra återställningar

I en mer automatiserad containerbaserad miljö bör många sådana moment ersättas eller minskas. Men nya uppgifter tillkommer:

- definiera önskat läge
- övervaka att plattformen når önskat läge
- hantera automatiska larm
- analysera mönster i incidenter
- förbättra standarder
- underhålla plattformskomponenter
- stötta team i rätt användning av plattformen
- säkerställa att automationen är kontrollerad

Automation flyttar alltså arbetet från enskilda manuella ingrepp till styrning av regler, flöden och plattformens beteende.

Det är en viktig förändring för chefer. Produktivitet ska inte bara mätas i hur många ärenden drift löser manuellt. Den bör också mätas i hur många återkommande fel som byggs bort, hur stabila standarderna är och hur väl plattformen stödjer kontrollerade leveranser.

## Självläkning är inte samma sak som ansvarsfrihet

Containerplattformar kan ofta återstarta containrar som kraschar, flytta arbetslaster eller försöka upprätthålla ett definierat önskat läge. Detta beskrivs ibland som självläkning.

Begreppet kan vara användbart, men det behöver förstås rätt. Självläkning betyder inte att problemen försvinner. Det betyder att plattformen kan hantera vissa typer av fel automatiskt.

Om en container kraschar och startas om kan användarna kanske inte märka något. Men organisationen behöver fortfarande förstå varför den kraschar. Annars riskerar felet att döljas tills det blir större.

Självläkning kan därför skapa både trygghet och blindhet.

Tryggheten ligger i att vissa fel kan hanteras snabbare och mer konsekvent än vid manuell hantering. Blindheten uppstår om organisationen tolkar automatiska återstarter som att allt fungerar.

En chef bör därför fråga:

- Följer vi upp automatiska återstarter?
- Vet vi vilka fel plattformen hanterar utan manuell åtgärd?
- Finns larm när återkommande självläkning döljer ett underliggande problem?
- Vem analyserar mönster i plattformens automatiska åtgärder?

Självläkning är ett tekniskt stöd. Det är inte en ersättning för ansvar, analys eller långsiktig förbättring.

## Observability: att kunna förstå vad som händer

När system körs på en containerplattform blir traditionell övervakning ofta otillräcklig. Det räcker inte att veta om en server är uppe eller nere. Organisationen behöver förstå vad som händer i applikationen, i plattformen och i samspelet mellan dem.

Ett viktigt begrepp är **observability**. På svenska kan det förklaras som förmågan att förstå ett systems tillstånd utifrån de signaler systemet lämnar ifrån sig. De vanligaste signalerna är loggar, mätvärden och spårning.

**Loggar** beskriver händelser. De kan visa fel, varningar, informationsmeddelanden och tekniska detaljer om vad applikationen gör.

**Mätvärden** visar kvantitativa signaler över tid, till exempel svarstider, antal fel, minnesanvändning, processorbelastning eller antal begäranden.

**Spårning** hjälper organisationen att följa ett anrop eller en transaktion genom flera tjänster och komponenter.

För chefer är poängen inte att kunna konfigurera dessa verktyg. Poängen är att förstå att modern drift kräver bättre insyn. Om ett IT-stöd består av flera containrar, integrationer, beroenden och plattformstjänster behöver organisationen kunna se helheten.

Annars blir felsökningen personberoende på nytt, bara i en modernare teknisk miljö.

## Loggning som styrningsfråga

Loggning kan låta som en teknisk detalj, men i en containerbaserad miljö blir den en styrningsfråga.

I äldre miljöer kan loggar ha legat på en specifik server. Någon med rätt behörighet kunde logga in och läsa dem. I en containerplattform är containrar mer flyttbara och tillfälliga. De kan startas om, ersättas eller flyttas. Därför behöver loggar samlas, struktureras och göras tillgängliga på ett kontrollerat sätt.

Det väcker flera chefsfrågor:

- Vilka loggar behöver sparas?
- Hur länge ska de sparas?
- Vem får läsa dem?
- Innehåller loggar personuppgifter eller känslig information?
- Kan loggar användas vid incidentanalys?
- Kan applikationsteam och plattformsteam se samma information?
- Finns standarder för hur applikationer ska logga?

Utan gemensam logghantering kan containerplattformen bli svår att drifta. Med rätt logghantering kan organisationen däremot få bättre spårbarhet och snabbare felsökning än tidigare.

## Larm och incidenter

När driften förändras behöver även larm och incidentprocesser förändras.

I en traditionell miljö kan larm ofta ha varit kopplade till servrar, diskar, processer eller tjänster. I en containerplattform behöver larm också spegla applikationernas tillstånd, plattformens hälsa, resursproblem, misslyckade utrullningar, återkommande omstarter och beroenden mellan tjänster.

Det är lätt att skapa för många larm. Då uppstår larmtrötthet. Människor slutar reagera, eller så blir incidentprocessen fylld av brus.

Det är också lätt att skapa för få larm. Då upptäcks fel först när användare hör av sig.

Bra larm behöver vara kopplade till ansvar och åtgärd. Ett larm som ingen äger är inte ett styrmedel. Det är bara ljud.

För chefer är det därför viktigt att fråga:

- Vilka larm är verksamhetskritiska?
- Vem tar emot larm?
- Vilka larm kräver omedelbar åtgärd?
- Vilka larm ska leda till förbättringsarbete snarare än akut insats?
- Hur skiljer vi mellan applikationsproblem och plattformsproblem?
- Hur följer vi upp återkommande incidenter?

Containerteknik kan ge bättre signaler, men bara om organisationen omsätter signalerna i ansvar och lärande.

## Kapacitetsstyrning i en delad plattform

En containerplattform gör det möjligt för flera IT-stöd att dela resurser. Det kan ge bättre resursutnyttjande och mer flexibel kapacitet. Men det kräver också tydligare styrning.

Om alla team begär mer resurser än de behöver kan plattformen bli dyr och svårplanerad. Om team får för lite resurser kan applikationerna fungera dåligt. Om prioriteringar saknas kan mindre viktiga system påverka mer samhällsviktiga system.

Kapacitetsstyrning blir därför både teknisk och organisatorisk.

Organisationen behöver kunna svara på frågor som:

- Vilka IT-stöd är mest kritiska?
- Vilka resurser har varje applikation rätt att använda?
- Hur hanteras toppbelastningar?
- Hur planeras kapacitet inför nya system och större förändringar?
- Vem ser helheten när många team använder samma plattform?
- Hur kopplas kostnader till faktisk användning?

Detta är särskilt viktigt i offentlig sektor, där stabilitet, kostnadskontroll och ansvar inför medborgare och tillsyn kan vara lika viktiga som snabb leverans.

## Produktionssättning förändras

I en containerbaserad miljö bör produktionssättning bli mer standardiserad. I stället för att någon manuellt installerar eller ändrar på en server bör organisationen sträva efter att samma paketerade image som testats också är den som körs i produktion.

Men produktionssättning blir inte automatiskt säker bara för att den är automatiserad. Automatisering kan göra fel snabbare om kontroller saknas.

Därför behöver produktionssättning ha tydliga principer:

- rätt version ska vara identifierad
- rätt tester ska vara genomförda
- rätt kontroller ska vara godkända
- rätt ansvariga ska vara informerade
- återställning eller omdirigering ska vara planerad
- påverkan på verksamheten ska vara förstådd
- drift och support ska veta vad som förändras

I en mogen organisation är produktionssättning inte ett hantverk som uppfinns på nytt varje gång. Det är ett styrt flöde där teknik, ansvar och beslut hänger ihop.

## Driftens relation till utveckling

När containerteknik införs kommer drift och utveckling närmare varandra. Det beror på att många driftaspekter behöver hanteras redan när applikationen byggs.

Exempel:

- Applikationen behöver kunna logga på ett standardiserat sätt.
- Den behöver kunna visa om den är frisk eller inte.
- Den behöver hantera konfiguration på ett säkert sätt.
- Den behöver kunna starta, stoppa och uppdateras utan onödiga manuella moment.
- Den behöver kunna övervakas i produktion.
- Den behöver fungera med plattformens standarder.

Detta betyder att driftkrav inte bör komma som överraskningar i slutet av ett projekt. De bör vara en del av utvecklingsarbetet.

För chefer innebär det att utveckling och drift inte kan styras som helt separata världar. Även om organisatoriska roller finns kvar behöver flödet vara sammanhängande.

En bra fråga är: “När upptäcker vi driftproblem?” Om svaret är “vid produktionssättning” är förändringsresan inte klar.

## Driftens relation till test

Test och drift hänger också närmare ihop. Om testmiljöer liknar produktion blir tester mer tillförlitliga. Om loggning, larm och hälsokontroller finns redan i test kan organisationen upptäcka driftproblem tidigare.

Det innebär att test inte bara ska verifiera funktion. Test bör också bidra till att verifiera driftsättningsbarhet och driftbarhet.

Exempel på frågor:

- Kan applikationen startas om utan att tappa viktig information?
- Fungerar loggning och larm innan produktion?
- Klarar applikationen förväntad belastning?
- Vad händer när ett beroende inte svarar?
- Går det att rulla tillbaka eller byta version kontrollerat?
- Är övervakningen begriplig för dem som ska hantera incidenter?

När sådana frågor flyttas tidigare i flödet minskar risken att driftorganisationen får bära konsekvenserna av beslut som fattats långt tidigare.

## Driftens relation till förvaltning

Förvaltningen behöver förstå driftens nya roll. Om plattformen och applikationerna ska hållas stabila över tid behöver förvaltningen planera för tekniskt underhåll, kapacitet, uppgraderingar, säkerhetsåtgärder och ändrade standarder.

Drift kan inte ensam bära ansvaret för allt som händer i produktion. Om en applikation bygger på gammal teknik, saknar bra loggar eller har otydligt ägarskap är det inte bara ett driftproblem. Det är ett förvaltningsproblem.

Förvaltningen behöver därför följa upp:

- återkommande incidenter
- teknisk skuld
- föråldrade images
- bristande standardefterlevnad
- kapacitetsproblem
- manuell handpåläggning
- beroenden som saknar ägare

När driftens observationer används i förvaltningsstyrningen kan organisationen gå från reaktiv felhantering till planerad förbättring.

## Scenario: Nordverk förändrar driftens uppdrag

Myndigheten Nordverk har länge haft en erfaren driftgrupp. Gruppen kan systemen väl. De vet vilka tjänster som brukar behöva startas om, vilka loggar som är viktiga och vilka produktionssättningar som brukar vara riskfyllda.

Det finns en stolthet i gruppen. De har räddat många situationer. När ett samhällsviktigt IT-stöd krånglar vet andra i organisationen vilka personer de ska ringa.

Men samma styrka är också en risk.

När Nordverk börjar införa containerteknik märker driftgruppen att gamla arbetssätt inte räcker. Det går inte att behandla varje container som en liten server. Det går inte att logga in överallt och felsöka manuellt som tidigare. Det går inte heller att låta varje utvecklingsteam själv hitta på loggning, larm och driftsättningsmönster.

I början uppstår irritation. Utvecklingsteamen tycker att drift bromsar. Drift tycker att utvecklingsteamen levererar applikationer som inte går att övervaka ordentligt. Förvaltningen vill veta vem som egentligen ansvarar för incidenter. Säkerhetsfunktionen vill förstå hur behörigheter och loggar hanteras.

Efter flera workshops formulerar Nordverk en ny driftmodell.

Den bygger på tre tydliga delar:

1. **Plattformsteamet ansvarar för containerplattformen.**  
   Teamet ansvarar för plattformens hälsa, kapacitet, uppgraderingar, standarder och gemensamma övervakningslösningar.

2. **Applikationsteamen ansvarar för att deras IT-stöd är driftbara.**  
   Det innebär bland annat loggning, hälsokontroller, rätt paketering, konfiguration och samarbete vid incidenter.

3. **Förvaltningen ansvarar för långsiktig prioritering och uppföljning.**  
   Förvaltningen följer upp teknisk skuld, återkommande incidenter, uppgraderingsbehov och avvikelser från standard.

Nordverk märker att driftens uppdrag inte blir mindre. Det blir tydligare. Driftgruppen går från att vara sista linjens problemlösare till att bli en nyckelaktör i plattformsstyrning, standardisering och förbättring.

## Påverkan på utveckling, test, förvaltning och drift

### Utveckling

Utveckling behöver bygga applikationer som kan drivas på plattformen. Det innebär att driftbarhet blir ett utvecklingskrav. Loggning, hälsokontroller, konfiguration, beroenden och startbeteende behöver hanteras redan från början.

### Test

Test behöver inkludera driftrelaterade frågor. Det räcker inte att funktionen fungerar. Organisationen behöver också testa om applikationen går att starta, stoppa, övervaka, felsöka och uppdatera kontrollerat.

### Förvaltning

Förvaltning behöver använda driftens signaler för prioritering. Återkommande incidenter, teknisk skuld, gamla beroenden och svag övervakning behöver bli en del av förvaltningsplanen.

### Drift

Drift går från manuell hantering av enskilda servrar till ansvar för plattform, automation, standarder, övervakning, incidentprocesser och samarbete med applikationsteam.

## Vanliga chefsfällor

### Fälla 1: Att tro att plattformen ersätter drift

En containerplattform kan automatisera vissa moment, men den ersätter inte behovet av driftkompetens. Den förändrar driftens fokus.

**Hur man undviker det:**  
Beskriv driftens nya uppdrag tydligt och planera kompetensutveckling.

### Fälla 2: Att låta varje team skapa egna driftsmönster

Om varje team väljer egen loggning, larmstruktur, konfiguration och driftsättningsmetod blir plattformen svår att hantera.

**Hur man undviker det:**  
Inför gemensamma minimistandarder för driftbarhet.

### Fälla 3: Att mäta drift på gamla sätt

Om drift bara mäts på antal lösta ärenden kan organisationen missa värdet av automation, förebyggande arbete och förbättrade standarder.

**Hur man undviker det:**  
Mät även återkommande fel, automatiseringsgrad, återställningstid, standardefterlevnad och förbättringsarbete.

### Fälla 4: Att underskatta plattformens egen livscykel

Plattformen behöver underhållas, uppgraderas och säkras. Det är inte ett engångsprojekt.

**Hur man undviker det:**  
Behandla plattformen som ett eget förvaltningsobjekt med budget, ansvar och plan.

### Fälla 5: Att sakna gemensam incidentmodell

När applikation och plattform hänger ihop kan incidenter hamna mellan team.

**Hur man undviker det:**  
Definiera ansvar, eskalering och samverkan mellan applikationsteam, plattformsteam, förvaltning och säkerhet.

## Frågor att ställa i den egna organisationen

- Loggar vi fortfarande in manuellt på produktionsmiljöer för att lösa återkommande problem?
- Vilka delar av driftens arbete bör automatiseras, och vilka kräver mänsklig bedömning?
- Har vi tydlig skillnad mellan applikationsdrift och plattformsdrift?
- Vem ansvarar för plattformens kapacitet, tillgänglighet och uppgraderingar?
- Har varje applikation tydliga krav på loggning, larm och hälsokontroller?
- Kan vi upptäcka fel innan användarna gör det?
- Kan vi skilja mellan applikationsfel och plattformsfel?
- Följer vi upp automatiska omstarter och andra självläkande åtgärder?
- Används driftens erfarenheter i förvaltningsplaneringen?
- Har vi en incidentmodell som fungerar när flera team och leverantörer är inblandade?
- Vet vi vilka IT-stöd som är mest kritiska på plattformen?
- Har vi standarder som gör det lättare att drifta många applikationer på samma sätt?

## Snabb sammanfattning

- Containerteknik gör inte drift mindre viktig. Den förändrar driftens uppdrag.
- Fokus flyttas från enskilda servrar till gemensam plattform, standarder, automation och övervakning.
- Applikationsdrift och plattformsdrift behöver skiljas åt, men också samverka.
- Automation tar inte bort ansvar. Den flyttar ansvar till regler, flöden, kontroller och uppföljning.
- Självläkning kan hantera vissa fel automatiskt, men återkommande automatiska åtgärder behöver analyseras.
- Observability, loggning, mätvärden och larm blir centrala för att förstå produktion.
- Förvaltningen behöver använda driftens signaler för att prioritera tekniskt underhåll och förbättringar.
- Chefer behöver styra driftförmågan som en del av hela förändringsresan, inte som en separat teknisk funktion.

## Quiz/reflektionsfrågor

1. Vad är den viktigaste skillnaden mellan serverdrift och plattformsdrift?
2. Varför kan en gemensam containerplattform både minska variation och koncentrera risk?
3. Vad är skillnaden mellan applikationsdrift och plattformsdrift?
4. Varför är självläkning inte samma sak som att problemen är lösta?
5. Vilka driftkrav bör utvecklingsteam känna till redan innan ett IT-stöd når produktion?
6. Hur kan driftens observationer användas i förvaltningsstyrningen?
7. Vilka larm i er organisation leder till faktisk åtgärd, och vilka skapar mest brus?

## Nästa steg

Driftens förändring leder vidare till en central fråga: hur säkerställer myndigheten kontroll, säkerhet och regelefterlevnad när leveransflöden blir mer automatiserade och plattformen används av många team?

Nästa kapitel handlar därför om säkerhet, regelefterlevnad och kontroll. Där ser vi hur containerteknik påverkar riskhantering, spårbarhet, policyer och styrning i en statlig myndighet.
