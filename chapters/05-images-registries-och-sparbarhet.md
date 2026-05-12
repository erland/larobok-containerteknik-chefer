# Kapitel 5: Images, registries och spårbarhet

## Varför detta kapitel finns

I kapitel 4 sorterade vi container-ekosystemets viktigaste delar. Vi såg att Podman, Kubernetes, registry och plattform inte är samma sak, utan olika byggstenar i en större förmåga. Nu går vi djupare i en av de viktigaste byggstenarna för styrning: **container images** och **registries**.

Det kan låta tekniskt. Men för en chef är detta i hög grad en fråga om kontroll.

När en organisation kör ett IT-stöd som container kör den inte bara “applikationen”. Den kör en paketerad version av applikationen, tillsammans med ett antal beroenden, inställningar och tekniska komponenter. Denna paketerade version kallas en **image**. En image hämtas ofta från ett **registry**, det vill säga en plats där images lagras, versioneras och görs tillgängliga.

Det centrala i kapitlet är detta:

> Den image som körs i produktion är ett beslutsobjekt, inte bara en teknisk fil.

Det innebär att organisationen behöver veta vad den kör, varifrån det kommer, vem som byggt det, vilka kontroller som har gjorts och vilken version som faktiskt är i produktion. Utan den spårbarheten riskerar containerteknik att bli ännu ett sätt att snabbt flytta osäkerhet till produktion.

Med rätt styrning blir det tvärtom. Images och registries kan göra leveransen mer kontrollerad, mer reproducerbar och lättare att följa upp.

## Lärandemål

Efter kapitlet ska du kunna:

- förklara varför images är centrala för styrning och spårbarhet
- förstå vad ett registry är och varför det behöver hanteras som en kontrollpunkt
- se skillnaden mellan att “ha en image” och att ha en godkänd, spårbar och förvaltningsbar image
- förstå varför versionshantering, märkning och ursprung spelar roll
- ställa relevanta frågor om vilka images som får byggas, lagras, hämtas och köras i produktion

## Innan vi börjar

Vi bygger vidare på fyra tidigare begrepp:

- **Container:** en isolerad och standardiserad körmiljö där en applikation kan köras tillsammans med de beroenden den behöver.
- **Image:** en paketerad mall som används för att starta containrar.
- **Plattform:** en gemensam teknisk och organisatorisk förmåga för att köra och förvalta applikationer standardiserat.
- **Registry:** en plats där container images lagras, hämtas och kontrolleras.

I kapitel 2 beskrevs en image som en slags mall. Det räcker som första förståelse. I detta kapitel lägger vi till ett ledningsperspektiv: en image är också något som behöver styras, granskas, versioneras och följas genom organisationens leveransflöde.

## Huvudförklaring

### En image är mer än applikationen

När man talar om ett IT-stöd i produktion tänker många på själva applikationen: koden, funktionerna och det användaren ser. Men en fungerande applikation kräver ofta mer än sin egen kod. Den behöver exempelvis:

- ett operativsystemnära grundlager
- bibliotek och programkomponenter
- konfigurationsmöjligheter
- startinstruktioner
- tekniska beroenden
- ibland särskilda verktyg för loggning, certifikat eller kommunikation

En container image paketerar sådant i en form som kan användas för att starta en eller flera containrar. Det är därför images blir viktiga för både utveckling, test, drift och säkerhet.

Om organisationen inte har kontroll över sina images vet den inte fullt ut vad den kör.

Det gäller särskilt i större organisationer, där flera team, leverantörer och plattformar kan vara inblandade. En image kan ha byggts av ett utvecklingsteam, baseras på en grundimage från en extern källa, lagras i ett internt registry, testas i en testmiljö och senare användas i produktion via Kubernetes eller en annan plattform.

Varje steg kan vara välstyrt. Varje steg kan också bli otydligt.

### Registry som lager och kontrollpunkt

Ett registry kan först förstås som ett lager för images. Där kan tekniska team hämta och publicera images. Men för en myndighet bör ett registry också ses som en kontrollpunkt.

Ett kontrollerat registry kan hjälpa organisationen att svara på frågor som:

- Vilka images finns hos oss?
- Vilka är godkända för produktion?
- Vem har byggt dem?
- Vilket IT-stöd hör de till?
- Vilken version är aktuell?
- Vilka images är gamla och bör tas bort?
- Vilka images bygger på sårbara eller föråldrade komponenter?
- Vilka externa källor tillåter vi?

Detta är inte bara tekniska frågor. De rör informationssäkerhet, kontinuitet, regelefterlevnad, leverantörsstyrning och förvaltningsbarhet.

Om varje team hämtar images fritt från olika externa källor får organisationen snabbt många varianter, svag spårbarhet och otydligt ansvar. Om allt däremot går via kontrollerade flöden blir registryt en del av myndighetens styrmodell.

### Versionering: att veta exakt vad som körs

En vanlig chefsfråga vid incidenter är: “Vad ändrades?”

I traditionell drift kan svaret ibland vara svårt att få fram. Någon kan ha installerat ett paket, ändrat en inställning, lagt in en fil eller gjort en manuell justering direkt i miljön. Dokumentationen kanske finns, men den kanske inte motsvarar verkligheten.

Med container images finns möjlighet att göra detta mer styrbart. Varje image kan märkas med en version. Den kan kopplas till kod, byggtidpunkt, testresultat och godkännanden.

Men det sker inte automatiskt bara för att man använder containrar.

En organisation behöver bestämma hur images ska namnges och versioneras. Det behöver finnas regler för vad en versionsbeteckning betyder. Det behöver också finnas en tydlig koppling mellan versionen som testats och versionen som senare körs i produktion.

En risk är att organisationen använder otydliga märkningar som “latest”, “ny”, “test” eller “prod”. Sådana etiketter kan vara praktiska i experiment, men de är svaga som styrmedel. Om “latest” i dag inte är samma sak som “latest” i går kan det bli svårt att veta exakt vad som kördes vid en viss tidpunkt.

För en chef är poängen enkel:

> En produktionssatt image ska kunna identifieras entydigt.

Det ska inte krävas gissningar, personminne eller efterhandsrekonstruktion.

### Ursprung: varifrån kommer det vi kör?

När en image byggs utgår den ofta från en annan image. Det kan exempelvis vara en grundimage med ett visst operativsystemlager eller en färdig miljö för ett visst programspråk. På den grunden lägger organisationen sin egen applikation och sina egna inställningar.

Detta skapar en kedja av beroenden.

För en myndighet är det viktigt att veta varifrån dessa grundkomponenter kommer. Det handlar inte om att varje chef ska granska tekniska lager. Men chefen behöver förstå att “vår applikation” kan innehålla många delar som inte organisationen själv har skrivit.

Därför behöver organisationen ha principer för:

- vilka externa källor som är tillåtna
- vilka grundimages som får användas
- hur ofta grundimages uppdateras
- vem som ansvarar för att sårbarheter åtgärdas
- hur leverantörer ska redovisa vad deras images innehåller
- hur undantag beslutas och dokumenteras

Detta blir särskilt viktigt när containerteknik införs i offentlig sektor, där informationssäkerhet, kontinuitet och spårbarhet ofta är avgörande för förtroendet.

### Från fil till beslut

Det är frestande att tänka på en image som ett tekniskt byggresultat. Utvecklingsteamet bygger en image, plattformen kör den och driften övervakar den.

Men i en styrbar organisation är en image också en bärare av beslut.

En produktionsklar image bör representera att vissa frågor är hanterade:

- Är rätt kod med?
- Är den byggd på godkända komponenter?
- Har automatiska tester körts?
- Har säkerhetskontroller genomförts?
- Är versionen dokumenterad?
- Är image-källan betrodd?
- Är den godkänd för den miljö där den ska köras?
- Finns ansvarig förvaltning?

Det betyder inte att varje image behöver godkännas manuellt av en chef. Tvärtom kan många kontroller automatiseras. Men det behöver vara tydligt vilka kontroller som krävs, var de sker och vem som äger regelverket.

## Scenario: Myndigheten Nordverk

Nordverk har börjat införa containerteknik. I början är arbetet lovande. Utvecklingsteamen kan bygga images, testmiljöerna blir enklare att skapa och plattformsteamet kan köra containeriserade applikationer mer konsekvent än tidigare.

Men efter några månader uppstår nya frågor.

En incident inträffar i ett internt handläggningssystem. Systemet körs som container. När driftledaren frågar vilken version som är i produktion får hon tre olika svar:

- utvecklingsteamet anger versionsnumret i koden
- plattformsteamet ser en annan image-tagg i Kubernetes
- leverantören hänvisar till sin egen leveransbeteckning

Alla menar att de har rätt, men de talar om olika saker.

Samtidigt upptäcker säkerhetsfunktionen att vissa images bygger på äldre grundimages. Ingen kan snabbt svara på vilka system som påverkas. Det visar sig också att några team har hämtat images direkt från externa publika källor under utvecklingsarbetet och att samma mönster delvis följt med in i testmiljö.

Nordverk inser att containerteknik inte bara kräver en plattform. Den kräver en kontrollerad hantering av images.

Myndigheten beslutar därför att införa en enkel men tydlig princip:

> Det som får köras i produktion ska kunna spåras från källa till byggd image, från test till godkännande och från registry till körande container.

För att nå dit börjar Nordverk med fyra åtgärder:

1. **Ett internt registry utses som godkänd källa för produktionsimages.**  
   Plattformen ska inte hämta produktionsimages direkt från okända eller externa platser.

2. **Images ska märkas enligt en gemensam versionsprincip.**  
   Versioner ska kunna kopplas till kod, byggtillfälle och testresultat.

3. **Grundimages standardiseras.**  
   Organisationen tar fram godkända baser som team och leverantörer förväntas använda.

4. **Ägarskap dokumenteras.**  
   Varje image ska kunna kopplas till ett IT-stöd, ett ansvarigt team eller en ansvarig leverantör och en förvaltningsansvarig.

Detta löser inte alla problem direkt. Men det flyttar Nordverk från informell hantering till styrbar hantering.

## Påverkan på utveckling

För utvecklingsteamen innebär styrd image-hantering att de inte längre bara levererar kod. De behöver också bidra till en körbar och spårbar paketering av applikationen.

Det påverkar exempelvis:

- hur applikationen byggs
- vilka grundimages som används
- hur beroenden uppdateras
- hur versioner sätts
- hur byggresultat dokumenteras
- hur images skickas vidare till test och produktion

Detta kan uppfattas som en extra belastning om organisationen inför regler utan stöd. Därför behöver chefer se till att utvecklingsteamen får gemensamma mallar, verktyg och vägledning. Målet är inte att varje team ska uppfinna sin egen metod för image-hantering. Målet är att skapa ett standardiserat leveranssätt.

En viktig ledningsfråga är därför:

> Har vi gjort det enkelt att göra rätt?

Om det är svårt att följa den godkända vägen kommer team och leverantörer att hitta genvägar.

## Påverkan på test

För testarbetet kan images ge stor nytta. Om samma image kan användas i test och produktion minskar risken att testresultatet bygger på en miljö som inte motsvarar verkligheten.

Men det kräver disciplin.

Testorganisationen behöver veta vilken image som testas. Den behöver också kunna koppla testresultat till just den versionen. Om en image testas, men en annan image senare produktionssätts, har spårbarheten brutits.

Det innebär att test inte bara ska svara på frågan “fungerar systemet?”. Test behöver också kunna svara på:

- vilken version testades?
- i vilken miljö testades den?
- vilka kontroller passerade den?
- är detta samma image som senare ska gå vidare?

Detta är grunden för mer tillförlitliga leveransflöden.

## Påverkan på förvaltning

Förvaltningen påverkas kraftigt av image-hantering. En image är inte färdig för all framtid bara för att den fungerar i dag. Den innehåller beroenden som behöver underhållas.

Det kan handla om:

- säkerhetsuppdateringar
- uppdaterade grundimages
- borttagning av gamla versioner
- livscykel för bibliotek och komponenter
- dokumentation av vilka images som hör till vilka IT-stöd
- beslut om när gamla versioner inte längre får användas

I en traditionell förvaltningsmodell kan tekniskt underhåll ibland hamna i skuggan av verksamhetsnära ändringar. Containerteknik gör detta mer synligt. Om gamla images ligger kvar och används länge ökar risken för sårbarheter, driftproblem och otydligt ansvar.

Förvaltningsledningen behöver därför se image-hantering som en del av livscykelansvaret för IT-stödet.

## Påverkan på drift

För driften blir registry och image-spårbarhet en grund för stabilitet och felsökning.

När ett problem uppstår behöver driftorganisationen snabbt kunna se:

- vilken image körs?
- när började den köras?
- vad ersatte den?
- varifrån hämtades den?
- finns samma version i test?
- finns tidigare version att återgå till?
- vilka andra system använder samma grundimage?

Detta förändrar driftens arbete. Mindre tid bör gå åt till att manuellt undersöka vad som finns installerat på en server. Mer tid kan läggas på att förstå plattformens tillstånd, följa standardiserade leveransflöden och hantera avvikelser.

Men det kräver att organisationen har skapat ordning i image-flödet. Annars riskerar driftorganisationen att få ansvar för att reda ut en otydlighet som egentligen uppstod tidigare i leveranskedjan.

## Vanliga chefsfällor

### Fälla 1: Att tro att registry bara är en teknisk lagringsplats

Ett registry är tekniskt sett en plats för images, men organisatoriskt kan det vara en viktig kontrollpunkt. Om ledningen inte ser detta missar man en möjlighet att styra vad som får köras.

**Hur du undviker fällan:**  
Behandla registryt som en del av myndighetens leverans- och säkerhetsstyrning.

### Fälla 2: Att acceptera otydliga versionsnamn

Otydliga taggar och informella versionsnamn gör det svårt att följa vad som faktiskt testats och produktionssatts.

**Hur du undviker fällan:**  
Kräv en versionsprincip som gör produktionssatta images entydigt identifierbara.

### Fälla 3: Att låta varje team välja grundimages fritt

Frihet kan skapa snabbhet i början, men också variation, sårbarheter och ökade förvaltningskostnader.

**Hur du undviker fällan:**  
Inför godkända grundimages och dokumenterade undantag.

### Fälla 4: Att separera image-hantering från förvaltning

Om images bara betraktas som byggresultat missar organisationen livscykelansvaret.

**Hur du undviker fällan:**  
Koppla varje image till IT-stöd, ansvarigt team, leverantör och förvaltningsmodell.

### Fälla 5: Att lita på manuell kontroll i ett snabbt flöde

Manuella kontroller kan vara nödvändiga i vissa beslutspunkter, men de räcker sällan för många återkommande leveranser.

**Hur du undviker fällan:**  
Automatisera återkommande kontroller och använd manuella beslut där mänsklig bedömning faktiskt tillför värde.

## Frågor att ställa i den egna organisationen

### Om kontroll och styrning

1. Var lagras våra container images?
2. Vilka registries är godkända för utveckling, test och produktion?
3. Får produktionsplattformen hämta images direkt från externa källor?
4. Vem beslutar vilka images som får köras i produktion?
5. Hur dokumenteras undantag från standardflödet?

### Om versionering och spårbarhet

1. Kan vi entydigt identifiera vilken image som körs i produktion?
2. Kan vi koppla en produktionsimage till kod, byggtillfälle, testresultat och godkännande?
3. Använder vi versionsnamn som är begripliga men också exakta?
4. Kan vi se historik över vilka images som tidigare körts?
5. Vet vi vilka system som påverkas om en grundimage behöver uppdateras?

### Om ansvar

1. Vem äger organisationens registry-strategi?
2. Vem ansvarar för godkända grundimages?
3. Vem ansvarar för att gamla images tas bort eller spärras?
4. Vem ansvarar för images som levereras av externa leverantörer?
5. Hur kopplas image-hantering till systemförvaltning och informationssäkerhet?

### Om utveckling, test och drift

1. Testar vi samma image som senare går vidare mot produktion?
2. Har utvecklingsteamen stöd för att bygga images på rätt sätt?
3. Kan driften snabbt se vilken image som orsakar ett problem?
4. Finns det en enkel väg tillbaka till tidigare fungerande version?
5. Följs image-hantering upp som en del av leveransförmågan?

## Checklista för ett styrbart image-flöde

En myndighet som vill göra image-hanteringen styrbar bör minst kunna beskriva:

- vilka externa image-källor som är tillåtna
- var interna images lagras
- hur images versioneras
- hur images kopplas till kod och testresultat
- vilka kontroller som krävs innan produktion
- vilka grundimages som är godkända
- vem som ansvarar för uppdatering av grundimages
- hur gamla images hanteras
- hur incidenter kan spåras till rätt image-version
- hur leverantörer ska leverera och dokumentera images

Checklistan behöver inte vara perfekt från början. Det viktiga är att organisationen går från informella vanor till synliga och förbättringsbara arbetssätt.

## Snabb sammanfattning

- En **image** är inte bara en teknisk mall. Den är också ett styrbart leveransobjekt.
- Ett **registry** är inte bara lagring. Det kan vara en central kontrollpunkt.
- Spårbarhet innebär att organisationen kan följa en image från källa och byggtillfälle till test, godkännande och produktion.
- Otydliga versionsnamn skapar risk, särskilt vid incidenter och revision.
- Godkända grundimages och kontrollerade externa källor minskar variation och stärker förvaltningsbarheten.
- Utveckling, test, förvaltning och drift påverkas alla av hur images hanteras.
- Chefer behöver inte kunna bygga images, men de behöver förstå vilka beslut och ansvar som krävs.

## Nästa steg

I detta kapitel har vi fokuserat på images, registries och spårbarhet. Vi har sett hur organisationen kan veta vad den kör och varifrån det kommer.

Nästa kapitel tar steget vidare till **automation, pipelines och vägen till produktion**. Där kopplas image-hanteringen ihop med ett mer sammanhängande leveransflöde: från kodändring till byggd image, test, kontroll och produktionssättning.

Då blir frågan inte bara “vad kör vi?”, utan också:

> Hur rör sig en ändring säkert, spårbart och effektivt hela vägen till produktion?
