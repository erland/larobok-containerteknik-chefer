# Kapitel 6: Automation, pipelines och vägen till produktion

## Varför detta kapitel finns

I kapitel 5 gick vi igenom varför **images** och **registries** är centrala för spårbarhet och kontroll. Vi såg att den image som körs i produktion inte bara är en teknisk fil, utan ett beslutsobjekt. Den behöver kunna kopplas till kod, test, godkännande och förvaltning.

Nu tar vi nästa steg: hur kommer en image egentligen fram till produktion?

I många organisationer har vägen till produktion länge byggt på manuella överlämningar. Ett utvecklingsteam lämnar något till test. Test lämnar vidare en rapport. Förvaltning samordnar ett införande. Drift följer en checklista. Någon skickar instruktioner i ett ärendehanteringssystem. Någon annan loggar in på en server och gör ändringar.

Det kan fungera länge. Särskilt om organisationen har erfarna personer som kan systemen, vet vilka undantag som gäller och minns vilka steg som brukar behövas. Men det skapar samtidigt tre problem:

1. **Leveransen blir svår att upprepa.**
2. **Kontrollen hamnar hos individer snarare än i ett styrt flöde.**
3. **Det blir svårt att veta exakt vad som testats, godkänts och driftsatts.**

Containerteknik löser inte detta automatiskt. Men containerteknik gör det möjligt att skapa mer standardiserade och automatiserade leveransflöden. Ett sådant flöde kallas ofta en **pipeline**.

En pipeline kan beskrivas som en kontrollerad väg från ändring till produktion. Den kan bygga applikationen, skapa en image, köra tester, utföra säkerhetskontroller, publicera image till ett registry och förbereda eller genomföra driftsättning.

För en chef är poängen inte att kunna skriva pipeline-konfiguration. Poängen är att förstå att pipeline blir en styrmekanism.

> En pipeline är inte bara ett utvecklarverktyg. Den är organisationens praktiska kontrollkedja för hur ändringar blir produktion.

Detta kapitel handlar därför om automation, pipelines och vägen till produktion ur ett ledningsperspektiv.

## Lärandemål

Efter kapitlet ska du kunna:

- förklara vad en pipeline är på chefsnivå
- förstå varför automation är mer än effektivisering
- se hur pipeline, image, registry, test och produktionssättning hänger ihop
- skilja mellan automatisering av teknik och automatisering av beslut
- identifiera vilka manuella steg som bör behållas, förändras eller automatiseras
- ställa relevanta frågor om kontroll, kvalitet och ansvar i vägen till produktion

## Innan vi börjar

Vi bygger vidare på begrepp från tidigare kapitel:

- **Leveransflöde:** kedjan från ändringsbehov till testad och driftsatt funktion.
- **Container:** en standardiserad körmiljö för applikationen.
- **Image:** en paketerad version av applikationen och dess beroenden.
- **Registry:** platsen där images lagras, hämtas och kontrolleras.
- **Spårbarhet:** förmågan att följa vad som byggts, testats, godkänts och körs.

I detta kapitel introduceras tre nya huvudbegrepp:

- **Pipeline:** ett automatiserat eller delvis automatiserat flöde som bygger, testar, kontrollerar och levererar en ändring.
- **Automatiserad testning:** tester som körs maskinellt och återkommande som del av leveransflödet.
- **Kontrollerad produktionssättning:** ett sätt att föra ändringar till produktion där steg, ansvar, kontroller och beslut är tydliga och spårbara.

## Huvudförklaring

### Varför vägen till produktion ofta blir svårstyrd

För att förstå pipelines behöver vi först förstå det problem de försöker lösa.

I en traditionell miljö kan vägen till produktion se ut ungefär så här:

1. En utvecklare gör en ändring.
2. Ändringen byggs på utvecklarens dator eller i en särskild byggmiljö.
3. En fil, ett paket eller en instruktion lämnas vidare.
4. Testmiljön uppdateras manuellt.
5. Testare kontrollerar systemet.
6. Förvaltning samordnar godkännande.
7. Drift får instruktioner.
8. Produktionsmiljön ändras manuellt.
9. Någon dokumenterar vad som gjorts.

Varje steg kan vara begripligt. Problemet uppstår när helheten blir beroende av människor, minne, checklistor, kalenderbokningar och informella överenskommelser.

Då blir det svårt att svara på frågor som:

- Vilken kodändring ingår i den version som nu körs?
- Vilka tester kördes innan produktionssättning?
- Var testet gjort på samma paketering som sedan driftsattes?
- Vem godkände ändringen?
- Vilka manuella avsteg gjordes?
- Går det att återskapa samma leverans?
- Kan vi snabbt gå tillbaka om något går fel?

Det är här pipeline-tänkandet kommer in.

### Vad en pipeline är

En **pipeline** är ett beskrivet och ofta automatiserat flöde för att ta en ändring genom flera steg. I containerbaserade miljöer handlar det ofta om att:

1. hämta kod från versionshantering
2. bygga applikationen
3. köra tester
4. skapa en container image
5. kontrollera image och beroenden
6. publicera image till ett registry
7. förbereda driftsättning
8. driftsätta till test, acceptans eller produktion
9. dokumentera eller logga vad som skett

Ordet pipeline kan låta mekaniskt, men det är ett användbart begrepp. Det signalerar att vägen till produktion inte ska uppfinnas på nytt varje gång. Den ska följa ett känt flöde.

Det betyder inte att allt måste vara helautomatiskt. En pipeline kan innehålla manuella beslutspunkter, till exempel att en ansvarig person måste godkänna produktionssättning. Skillnaden är att beslutspunkten är synlig, dokumenterad och placerad i ett kontrollerat flöde.

### Pipeline som styrmekanism

Det är lätt att se pipeline som något tekniskt. För en utvecklare är det ofta en konfigurationsfil. För en plattformstekniker är det en integration mellan verktyg. För en testare kan det vara platsen där tester körs.

För en chef bör pipeline förstås som något mer:

- ett sätt att styra kvalitet
- ett sätt att minska personberoende
- ett sätt att skapa spårbarhet
- ett sätt att upptäcka fel tidigare
- ett sätt att göra produktionssättning mer förutsägbar
- ett sätt att omsätta policy i praktiken

Om organisationen säger att kod ska testas innan produktion, men testningen sker manuellt och oregelbundet, är kontrollen svag. Om samma kontroll däremot ligger i en pipeline och alltid körs, blir kontrollen starkare.

Om organisationen säger att bara godkända images får användas, men drift manuellt kan hämta valfri image, är styrningen svag. Om pipeline bara publicerar images till ett godkänt registry efter kontroller, blir styrningen tydligare.

En pipeline gör alltså inte bara saker snabbare. Den gör saker mer konsekventa.

### Automation betyder inte att människor försvinner

Ett vanligt missförstånd är att automation betyder att människor inte längre behövs. Det är fel.

Automation tar inte bort behovet av ansvar. Den flyttar ansvar från manuellt utförande till utformning, styrning och uppföljning av flöden.

I en manuell modell kan en erfaren drifttekniker vara den som vet vilka kommandon som ska köras vid produktionssättning. I en automatiserad modell behöver organisationen i stället säkerställa att:

- rätt steg finns i pipeline
- rätt kontroller körs
- rätt personer kan godkänna rätt beslut
- fel stoppar flödet på rätt sätt
- loggar och historik sparas
- avvikelser hanteras strukturerat
- flödet förbättras när problem upptäcks

Det mänskliga arbetet blir inte oviktigt. Det blir mer inriktat på design, prioritering, analys och ansvarstagande.

### Skillnaden mellan automatisering av steg och automatisering av beslut

Det är viktigt att skilja mellan två typer av automation:

1. **Automatisering av steg**
2. **Automatisering av beslut**

Automatisering av steg innebär att återkommande tekniska moment utförs maskinellt. Exempel:

- bygga applikationen
- skapa en image
- köra tester
- kontrollera kodstil
- skanna beroenden
- publicera image till registry
- skapa en testmiljö

Automatisering av beslut innebär att systemet själv avgör om något ska gå vidare. Exempel:

- stoppa leverans om tester misslyckas
- stoppa image om säkerhetskontroll hittar kritiska brister
- tillåta driftsättning om alla kontroller är godkända
- kräva manuellt godkännande vid produktionssättning

Båda behövs. Men de har olika styrningskonsekvenser.

En chef behöver inte bestämma exakt hur varje tekniskt steg ska skrivas. Däremot behöver chefen förstå vilka beslut pipeline får fatta automatiskt, vilka beslut som kräver mänsklig bedömning och vem som ansvarar för reglerna.

### Pipeline och kontrollpunkter

Ett bra sätt att förstå pipeline är att se den som en serie kontrollpunkter.

Exempel på kontrollpunkter kan vara:

| Kontrollpunkt | Fråga som besvaras |
|---|---|
| Kod hämtad från rätt källa | Vet vi vilken ändring som ska levereras? |
| Bygge lyckas | Går applikationen att bygga på ett upprepat sätt? |
| Tester passerar | Har grundläggande funktion kontrollerats? |
| Image skapas | Finns en standardiserad paketering? |
| Image märks | Vet vi vilken version detta är? |
| Säkerhetskontroll körs | Finns kända risker som måste hanteras? |
| Image publiceras till registry | Finns en kontrollerad källa för driftsättning? |
| Godkännande sker | Har rätt ansvarig fattat beslut? |
| Driftsättning loggas | Kan vi följa vad som hänt i efterhand? |

I en manuell organisation kan många av dessa kontroller finnas, men de sker utspritt. Något sker i ett möte, något i ett dokument, något i ett ärende, något i en persons huvud och något i en serverlogg.

Pipeline samlar inte nödvändigtvis allt på ett ställe, men den gör kontrollkedjan mer sammanhängande.

### Pipeline och containers

Containerteknik passar väl ihop med pipeline-tänkande eftersom en image är ett tydligt leveransobjekt.

I stället för att leverera “en uppsättning filer och instruktioner” kan organisationen leverera “denna image, med denna version, byggd från denna kod, testad på detta sätt”.

Det gör det lättare att skilja på:

- vad som byggts
- vad som testats
- vad som godkänts
- vad som körs

När pipeline skapar en image blir den en del av spårbarhetskedjan. När image publiceras till registry blir den tillgänglig för test eller produktion. När plattformen driftsätter image blir det möjligt att följa exakt vilken version som körs.

Detta är en av de stora ledningspoängerna med containerteknik: leveransen får ett tydligare objekt.

### Pipeline och test

Automatiserade tester är en central del av pipeline. Men det är viktigt att förstå vad automatiserade tester kan och inte kan göra.

Automatiserade tester kan till exempel kontrollera att:

- applikationen går att bygga
- centrala funktioner fungerar
- tekniska beroenden finns
- vissa säkerhetskrav uppfylls
- gränssnitt svarar som förväntat
- ändringen inte uppenbart förstör tidigare funktion

Automatiserade tester kan däremot inte ensamma ersätta all verksamhetsbedömning. De kan inte alltid avgöra om en funktion är lämplig, begriplig, rätt prioriterad eller tillräckligt bra ur användarens perspektiv.

Därför bör chefer inte fråga “kan vi automatisera all testning?” som första fråga. En bättre fråga är:

> Vilka kontroller ska alltid ske automatiskt, och vilka bedömningar kräver mänskligt ansvar?

Detta är särskilt viktigt i offentlig sektor där IT-stöd ofta påverkar rättssäkerhet, handläggning, tillgänglighet, arkivering, informationssäkerhet eller samhällsviktig service.

### Pipeline och produktionssättning

Produktionssättning är ofta den punkt där organisationens kultur blir synlig.

I en manuell kultur kan produktionssättning vara något dramatiskt. Många personer samlas. Flera system påverkas. Checklistor följs. Beslut tas sent. Återställning är oklar. Man undviker ändringar nära helger eller semestrar eftersom nyckelpersoner inte är på plats.

I en mer automatiserad och containerbaserad modell bör produktionssättning bli mer förutsägbar. Det betyder inte att den är riskfri. Men den ska bygga på:

- tydlig version
- känd image
- genomförda tester
- dokumenterade kontroller
- förberedd återgång eller korrigering
- tydlig ansvarsfördelning
- synlig status

En viktig poäng är att pipeline inte bara ska stödja snabb leverans. Den ska stödja kontrollerad leverans.

Snabbhet utan kontroll är inte målet. Kontroll utan orimlig tröghet är målet.

### Manuella beslutspunkter kan vara rätt

Ibland beskrivs moderna leveransflöden som om allt ska gå automatiskt hela vägen till produktion. Det är inte alltid rätt mål för en statlig myndighet.

Det kan finnas goda skäl att behålla manuella beslutspunkter, till exempel:

- verksamhetsgodkännande
- säkerhetsbedömning
- juridisk bedömning
- ändringsbeslut
- samordning med andra myndigheter
- beslut vid särskilt känsliga system
- beslut vid större förändringar i användargränssnitt eller handläggningsprocess

Men manuella beslutspunkter ska inte vara otydliga stopp där ärenden blir liggande. De bör vara definierade steg med tydligt syfte.

En bra manuell beslutspunkt har:

- tydligt ansvar
- tydligt beslutsunderlag
- tydlig tidsram
- tydliga kriterier
- dokumenterat utfall

Då blir den en del av styrningen, inte ett dolt hinder.

### Vanliga former av pipeline i en myndighet

En myndighet kan ha flera typer av pipelines. Några vanliga exempel är:

#### Byggpipeline

Bygger applikationen och kontrollerar att koden kan sammanställas eller paketeras.

#### Testpipeline

Kör automatiserade tester, exempelvis enhetstester, integrationstester eller tekniska kontroller.

#### Image-pipeline

Skapar container image, märker den med version och publicerar den till registry.

#### Säkerhetspipeline

Kontrollerar beroenden, kända sårbarheter, hemligheter i kod, policybrott eller otillåtna komponenter.

#### Deploy-pipeline

Förbereder eller genomför driftsättning till test, acceptans eller produktion.

I mindre organisationer kan flera av dessa delar ligga i samma pipeline. I större organisationer kan de vara uppdelade. Det viktiga är inte exakt verktygsstruktur. Det viktiga är att ansvar och kontrollkedja är begripliga.

### Pipeline är också dokumentation

I många organisationer finns produktionsinstruktioner i dokument. Problemet är att dokument lätt blir inaktuella. Någon ändrar ett kommando, men inte instruktionen. Någon hittar ett undantag, men skriver inte ner det. Någon gör en manuell korrigering, men bara de närvarande känner till den.

En pipeline kan fungera som levande dokumentation. Den visar vilka steg som faktiskt körs.

Det betyder inte att all dokumentation försvinner. Det behövs fortfarande förklaringar, beslutsunderlag, arkitektur, riskbedömningar och rutiner. Men pipeline minskar gapet mellan “så här säger vi att vi gör” och “så här gör vi faktiskt”.

För en chef är detta viktigt. Styrning bygger inte bara på policy. Styrning kräver att policy omsätts i vardagligt arbetssätt.

### Pipeline och avvikelser

Ett moget leveransflöde måste hantera avvikelser.

Exempel:

- ett test misslyckas
- en image får inte publiceras
- en sårbarhet upptäcks
- en produktionssättning stoppas
- ett manuellt godkännande saknas
- en leverantör följer inte standarden
- en akut incident kräver snabb rättning

Om varje avvikelse leder till improvisation är organisationen fortfarande personberoende. Målet är inte att avvikelser aldrig ska inträffa. Målet är att de ska hanteras på ett styrt sätt.

Det kan innebära:

- tydliga regler för när pipeline får brytas
- dokumenterade undantag
- tidsbegränsade avsteg
- krav på efteranalys
- synlighet för ansvariga chefer
- förbättring av pipeline efter återkommande problem

En viktig ledningsfråga är därför:

> Hur hanterar vi undantag utan att undantagen blir den nya normalprocessen?

### Pipeline, ansvar och kultur

När en organisation inför pipelines förändras ofta relationen mellan utveckling, test, förvaltning och drift.

Utveckling kan inte längre säga: “Vi levererar kod, resten är driftens ansvar.”

Drift kan inte längre säga: “Vi installerar det vi får, men vet inte vad som ingår.”

Test kan inte längre vara en sen kontrollstation som först mot slutet upptäcker grundläggande problem.

Förvaltning kan inte bara samordna ärenden utan att förstå leveransflödets tekniska och organisatoriska beroenden.

Pipeline gör beroenden synliga. Det är bra, men det kan också skapa friktion. Gamla gränser utmanas. Ansvar behöver förtydligas. Vissa roller behöver ny kompetens. Vissa beslut behöver flyttas tidigare i flödet.

Därför är pipeline-införande inte bara en teknisk förbättring. Det är en förändring av arbetssätt.

## Scenario: Myndigheten Nordverk

Nordverk har länge haft en etablerad produktionsprocess. Den är dokumenterad, men mycket av den praktiska kunskapen finns hos ett fåtal personer.

När ett av myndighetens viktigaste IT-stöd ska uppdateras sker ungefär följande:

- Utveckling lämnar en leveransnot.
- Test får instruktioner om vad som ska installeras.
- Förvaltning samordnar testresultat och godkännande.
- Drift får en checklista för produktionssättning.
- En erfaren tekniker gör flera manuella steg.
- Ett möte hålls efteråt för att bekräfta att allt verkar fungera.

Processen har fungerat, men den är långsam. Den är också känslig. Om rätt personer inte är tillgängliga skjuts produktionssättning upp. När fel uppstår är det svårt att veta om felet ligger i koden, miljön, installationssteget eller ett manuellt avsteg.

Efter diskussionerna om containerplattformen beslutar Nordverk att införa en första pipeline för ett mindre men viktigt IT-stöd.

Målet är inte att gå direkt till helautomatisk produktionssättning. Målet är att skapa en mer kontrollerad väg.

Den första pipelinen gör fem saker:

1. Hämtar kod från versionshantering.
2. Bygger applikationen.
3. Kör grundläggande automatiserade tester.
4. Skapar en container image.
5. Publicerar image till ett internt registry om kontrollerna lyckas.

Produktionssättningen är fortfarande manuell, men den manuella delen förändras. Drift ska inte längre bygga eller modifiera leveransen. Drift ska hämta en godkänd image från registry och driftsätta enligt plattformens standard.

Efter några månader märker Nordverk flera effekter:

- Färre fel beror på skillnader mellan miljöer.
- Det blir lättare att se vilken version som testats.
- Testteamet hittar vissa fel tidigare.
- Förvaltningen får bättre underlag för godkännande.
- Drift behöver färre manuella instruktioner.
- Diskussionen flyttas från “vem kan göra detta?” till “vilka kontroller ska flödet innehålla?”

Samtidigt uppstår nya frågor:

- Vem äger pipelinen?
- Vem får ändra kontrollstegen?
- Vem beslutar om ett test är obligatoriskt?
- Hur hanteras akuta rättningar?
- Vad gör man när en leverantör inte kan leverera på detta sätt?

Nordverks ledning inser att pipeline inte är ett sidospår. Det är en central del av förändringsresan.

## Påverkan på utveckling, test, förvaltning och drift

### Utveckling

För utvecklingsteam innebär pipeline att leveransen behöver vara byggbar och testbar på ett standardiserat sätt.

Det räcker inte att koden fungerar på en utvecklares dator. Koden behöver kunna byggas i ett gemensamt flöde. Det innebär ofta krav på:

- tydlig versionshantering
- automatiserbara byggsteg
- hanterade beroenden
- testbar struktur
- tydlig konfiguration
- containeranpassad paketering

Utvecklingens ansvar flyttas alltså närmare körbarhet. Teamet behöver tänka på hur applikationen byggs, testas, paketeras och överlämnas till plattformen.

### Test

För testfunktionen innebär pipeline både möjlighet och krav.

Möjligheten är att fler tester kan köras tidigare och oftare. Det gör att fel upptäcks när de är billigare att åtgärda.

Kravet är att teststrategin behöver bli tydligare. Organisationen behöver bestämma:

- vilka tester som ska köras vid varje kodändring
- vilka tester som ska köras innan image publiceras
- vilka tester som krävs inför produktionssättning
- vilka tester som fortfarande behöver manuell bedömning
- hur testresultat ska sparas och följas upp

Test blir mindre av en sen fas och mer av en återkommande kontroll genom hela leveransflödet.

### Förvaltning

Förvaltningens roll påverkas kraftigt.

I en traditionell modell kan förvaltning ofta fokusera på ärenden, releaseplanering, användarbehov och samordning mellan parter. I en containerbaserad modell behöver förvaltningen också förstå livscykeln för images, beroenden och pipeline-kontroller.

Förvaltningen behöver kunna svara på frågor som:

- Vilken version är godkänd för produktion?
- Vilka tekniska beroenden ingår?
- Vilka kontroller krävs för ändring?
- Hur prioriteras underhåll av pipeline och test?
- Hur hanteras säkerhetsuppdateringar i grundimages?
- Hur påverkar leveransflödet förvaltningsplanen?

Det betyder inte att förvaltningsledare ska bli tekniker. Men de behöver förstå att förvaltningsbarhet numera också sitter i leveransflödet.

### Drift

För drift innebär pipeline att manuella installationsmoment bör minska.

Driftens fokus flyttas från att utföra unika produktionssteg till att säkerställa att plattformen, kontrollpunkterna och driftsättningsmönstren fungerar.

Det kan innebära:

- mindre handpåläggning på enskilda servrar
- mer fokus på standardiserad driftsättning
- mer samarbete med plattformsteam
- tydligare krav på loggning och övervakning
- bättre förberedelse för återstart, skalning och återställning
- mindre acceptans för informella produktionsändringar

Drift blir inte mindre viktig. Driftens uppgift blir mer plattformsorienterad och mer kopplad till robusta flöden.

## Vanliga chefsfällor

### Fälla 1: Att tro att pipeline bara är en teknisk detalj

En pipeline avgör i praktiken hur ändringar kontrolleras innan de når produktion. Om ledningen inte förstår detta riskerar viktiga styrningsbeslut att hamna osynligt hos enskilda teknikteam.

**Hur man undviker det:**  
Be att få pipeline-flödet beskrivet på verksamhetsnivå. Fråga vilka kontroller som finns, vem som äger dem och vilka beslut som är manuella.

### Fälla 2: Att automatisera ett dåligt flöde

Om dagens process är otydlig kan automation göra otydligheten snabbare, inte bättre.

**Hur man undviker det:**  
Kartlägg först nuvarande leveransflöde. Identifiera flaskhalsar, onödiga steg och oklara ansvar innan ni automatiserar.

### Fälla 3: Att ta bort manuella godkännanden utan att ersätta dem med tydliga kontroller

Snabbare produktionssättning är inte ett självändamål. Vissa beslut behöver fortfarande mänsklig bedömning.

**Hur man undviker det:**  
Skilj på kontroller som kan automatiseras och beslut som kräver ansvarig person. Gör båda synliga i flödet.

### Fälla 4: Att låta varje team skapa sin egen pipeline-standard

Om varje team bygger sin egen väg till produktion kan organisationen få nya silos. Det blir svårt att följa upp, säkra och förvalta helheten.

**Hur man undviker det:**  
Skapa gemensamma minimikrav för pipelines, men tillåt anpassning där det finns goda skäl.

### Fälla 5: Att mäta framgång enbart i hastighet

En snabb pipeline är inte automatiskt en bra pipeline. Om den saknar tester, spårbarhet eller säkerhetskontroller kan den öka risk.

**Hur man undviker det:**  
Mät både ledtid och kontroll: testtäckning, fel som stoppas tidigt, återställningsförmåga, spårbarhet och antal manuella avsteg.

### Fälla 6: Att glömma leverantörerna

Om myndigheten har externa leverantörer måste de kunna passa in i leveransflödet. Annars blir pipeline bara intern teori.

**Hur man undviker det:**  
Ställ krav på byggbarhet, testbarhet, containerpaketering, dokumenterade beroenden och integration med myndighetens leveransflöde.

## Frågor att ställa i den egna organisationen

### Om nuläget

1. Hur ser vägen från kodändring till produktion ut i dag?
2. Vilka steg är manuella?
3. Vilka steg är dokumenterade men inte automatiserade?
4. Var uppstår väntetider?
5. Var finns personberoende?
6. Vilka kontroller sker alltid, och vilka sker bara ibland?

### Om pipeline och automation

1. Har vi en definierad pipeline för varje viktigt IT-stöd?
2. Vilka steg i pipeline är obligatoriska?
3. Vem äger pipeline-flödet?
4. Vem får ändra pipeline-regler?
5. Hur loggas resultat från byggen, tester och driftsättningar?
6. Finns det gemensamma minimikrav för pipelines?

### Om test och kvalitet

1. Vilka tester körs automatiskt innan något når testmiljö?
2. Vilka tester krävs innan en image får publiceras till registry?
3. Vilka tester krävs innan produktionssättning?
4. Hur hanteras test som misslyckas?
5. Vilka manuella tester eller bedömningar behöver fortfarande finnas kvar?
6. Hur följs återkommande testproblem upp?

### Om produktion och beslut

1. Vad krävs för att något ska få gå till produktion?
2. Vilka beslut är automatiserade?
3. Vilka beslut kräver mänskligt godkännande?
4. Vem kan stoppa en produktionssättning?
5. Hur hanteras akuta rättningar?
6. Finns en tydlig väg tillbaka om något går fel?

### Om leverantörer

1. Kan våra leverantörer leverera på ett sätt som passar vår pipeline?
2. Kräver vi att leverantörer tillhandahåller automatiserbara tester?
3. Kräver vi container images som kan spåras till kod och version?
4. Vem ansvarar för att leverantörens leverans fungerar i vårt flöde?
5. Hur hanteras leverantörsavvikelser?

## Ledningsbeslut som ofta behöver fattas

När en myndighet börjar använda pipelines behöver flera beslut lyftas till rätt nivå.

### Beslut 1: Vilka kontroller är obligatoriska?

Organisationen behöver bestämma vilka kontroller som alltid ska ske innan en ändring går vidare. Det kan handla om tester, säkerhet, versionsmärkning, godkännanden och dokumentation.

### Beslut 2: Vad får automatiseras?

Allt som kan automatiseras bör inte automatiseras direkt. Beslutet bör utgå från risk, mognad, systemets känslighet och organisationens förmåga att följa upp.

### Beslut 3: Vem äger pipeline-standarden?

Om ingen äger standarden kommer varje team att skapa egna lösningar. Om standarden är för centraliserad kan den bli trög och svår att använda. Organisationen behöver hitta en balans.

### Beslut 4: Hur hanteras undantag?

Undantag kommer att behövas, särskilt i början. Men de måste vara synliga, tidsbegränsade och följas upp.

### Beslut 5: Hur kopplas pipeline till förvaltningsstyrning?

Pipeline ska inte leva vid sidan av förvaltningsmodellen. Den behöver kopplas till releaseplanering, ändringshantering, riskbedömning och uppföljning.

## En enkel mognadstrappa för pipeline

En myndighet behöver inte börja med allt. Ett stegvis införande kan se ut så här:

### Steg 1: Synliggör leveransflödet

Kartlägg hur ändringar går till produktion i dag. Identifiera manuella steg, väntetider och personberoenden.

### Steg 2: Automatisera bygg och grundläggande test

Säkerställ att applikationen kan byggas och testas på ett upprepat sätt.

### Steg 3: Skapa och publicera images kontrollerat

Låt pipeline skapa container images och publicera dem till ett godkänt registry efter kontroller.

### Steg 4: Koppla pipeline till testmiljöer

Gör det enkelt att driftsätta samma image till testmiljöer och köra återkommande tester.

### Steg 5: Inför tydliga produktionsbeslut

Lägg in manuella eller automatiserade beslutspunkter inför produktion, med tydliga kriterier.

### Steg 6: Följ upp och förbättra

Mät ledtid, fel, avvikelser, testresultat och återkommande problem. Använd resultaten för att förbättra flödet.

Denna trappa är inte en teknisk standard. Den är ett sätt att tänka kring förändringsledning.

## Tecken på att organisationen är på rätt väg

En organisation som börjar få kontroll över pipeline och automation kan ofta se följande tecken:

- Fler fel upptäcks före produktion.
- Färre produktionssättningar kräver unik handpåläggning.
- Det är tydligare vilken version som körs.
- Testresultat är lättare att hitta.
- Drift får färre oklara instruktioner.
- Förvaltning har bättre beslutsunderlag.
- Leverantörer får tydligare krav.
- Ledningen kan följa leveransförmåga utan att fråga enskilda specialister.
- Diskussionen handlar mer om flöde, kontroll och ansvar än om enskilda kommandon.

## Tecken på risk

Det finns också varningssignaler:

- Pipeline finns, men ingen vet vem som äger den.
- Tester misslyckas ofta men ignoreras.
- Manuella avsteg görs utan dokumentation.
- Olika team har helt olika regler.
- Produktionssättning kräver fortfarande informella kontakter.
- Images byggs utanför det godkända flödet.
- Leverantörer skickar leveranser som inte går att bygga eller testa automatiskt.
- Ledningen mäter bara antal leveranser, inte kvalitet eller kontroll.

Dessa tecken betyder inte att förändringen har misslyckats. De visar var styrningen behöver stärkas.

## Snabb sammanfattning

- En pipeline är ett kontrollerat flöde från ändring till testad, paketerad och potentiellt driftsatt version.
- Pipeline är inte bara ett tekniskt verktyg utan en styrmekanism.
- Automation handlar inte bara om snabbhet, utan om upprepbarhet, spårbarhet och kvalitet.
- Containerteknik passar väl ihop med pipelines eftersom en image blir ett tydligt leveransobjekt.
- Automatiserade tester kan stärka kvaliteten, men de ersätter inte all mänsklig bedömning.
- Manuella beslutspunkter kan vara rätt, men de ska vara tydliga, dokumenterade och placerade i flödet.
- Pipeline påverkar utveckling, test, förvaltning och drift samtidigt.
- Organisationen behöver besluta vilka kontroller som är obligatoriska, vem som äger pipeline-standarden och hur undantag hanteras.
- Målet är inte maximal hastighet, utan styrbar och förutsägbar leverans.

## Nästa steg

Nu har vi gått igenom hur containerteknik, images, registries och pipelines tillsammans kan skapa en mer kontrollerad väg till produktion.

I nästa kapitel flyttar vi fokus till utvecklingsarbetet. Vi ska titta på hur utvecklingsteamens ansvar förändras när applikationer inte bara ska skrivas, utan också byggas, testas, paketeras och levereras på ett sätt som passar en containerplattform.

Nästa kapitel heter:

**Kapitel 7: Hur utvecklingsarbetet förändras**
