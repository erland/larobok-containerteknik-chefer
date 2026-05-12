# Kapitel 7: Hur utvecklingsarbetet förändras

## Varför detta kapitel finns

När en organisation börjar använda containerteknik förändras inte bara driften. Utvecklingsarbetet förändras också.

Det är lätt att tänka att containrar främst är en fråga för tekniska specialister: någon bygger en image, någon annan kör den på en plattform, och verksamheten märker förhoppningsvis bara att leveranserna går snabbare. I praktiken är förändringen bredare än så. Utvecklingsteam behöver förstå mer om hur deras applikationer ska paketeras, startas, konfigureras, testas, uppdateras och överlämnas till produktion.

För en chef är den viktiga frågan därför inte: “Ska utvecklarna lära sig Kubernetes?” Den viktiga frågan är snarare: “Hur behöver vårt utvecklingsarbete förändras för att våra IT-stöd ska bli körbara, testbara, säkra och förvaltningsbara på en modern plattform?”

I tidigare kapitel har vi sett hur containrar ger en mer standardiserad körmiljö, hur images kan hanteras i registries och hur pipelines kan göra vägen till produktion mer styrbar. I detta kapitel flyttar vi fokus till utvecklingens vardag. Vad innebär det när applikationen inte längre bara är kod, utan något som ska kunna byggas, paketeras och köras på ett upprepat sätt?

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förklara varför containerteknik påverkar utvecklingsarbetet, inte bara driften
- förstå skillnaden mellan att leverera kod och att leverera något som faktiskt är körbart
- se varför utvecklingsteam behöver arbeta närmare test, förvaltning, säkerhet och plattformsdrift
- identifiera nya krav på interna team och externa leverantörer
- ställa chefsfrågor om byggbarhet, paketering, beroenden och ansvar

## Innan vi börjar

Vi bygger vidare på fyra begrepp från tidigare kapitel:

- **Container**: en standardiserad körmiljö för applikationen.
- **Image**: den paketerade mall som används för att starta containern.
- **Registry**: platsen där images lagras, hämtas och kontrolleras.
- **Pipeline**: flödet som bygger, testar, kontrollerar och levererar ändringar.

I detta kapitel introducerar vi tre nya huvudbegrepp:

- **Byggbarhet**
- **Standardiserad applikationspaketering**
- **DevOps-samarbete**

Begreppen är tekniska till ytan, men de är också organisatoriska. De påverkar beställning, ansvar, kompetens, leverantörsstyrning och förvaltningsbarhet.

## Från kodleverans till körbar leverans

I många organisationer har utvecklingsarbetet historiskt kunnat avslutas med att utvecklingsteamet lämnar över kod, installationspaket eller instruktioner till någon annan. Därefter har test, förvaltning eller drift behövt få systemet att fungera i respektive miljö.

Detta kan fungera när förändringstakten är låg, miljöerna är få och organisationen har personer som kan alla speciallösningar. Men det skapar ofta problem:

- utvecklingsteamet vet inte alltid exakt hur systemet installeras i produktion
- driftorganisationen behöver tolka installationsinstruktioner
- testmiljön blir inte identisk med produktionsmiljön
- överlämningar blir beroende av personliga relationer
- fel upptäcks sent, ibland först vid produktionssättning
- ansvaret för “att det fungerar” blir otydligt

Containerteknik pressar fram en annan logik. Det räcker inte att koden finns. Den behöver kunna byggas till en image, kontrolleras, testas och startas på ett förutsägbart sätt.

Det betyder inte att varje utvecklare måste bli plattformsexpert. Men utvecklingsarbetet behöver ta ansvar för att applikationen kan bli en fungerande och förvaltningsbar leverans.

En enkel jämförelse:

| Traditionellt synsätt | Containerbaserat synsätt |
|---|---|
| Utveckling levererar kod eller installationsunderlag. | Utveckling bidrar till en körbar, testbar och paketerad applikation. |
| Drift får ofta lösa miljöskillnader. | Miljöskillnader minskas genom standardiserad paketering. |
| Installation kan vara ett separat hantverk. | Bygge och paketering blir del av leveransflödet. |
| Fel kan uppstå sent i överlämningen. | Fel bör upptäckas tidigare i pipeline och test. |
| Ansvar hamnar mellan organisatoriska stuprör. | Ansvar behöver tydliggöras längs hela flödet. |

För chefer är detta en viktig förändring. Det handlar inte bara om nya verktyg. Det handlar om vad organisationen menar med “klart”.

## Begrepp 1: Byggbarhet

**Byggbarhet** betyder att applikationen kan byggas på ett upprepat, begripligt och kontrollerat sätt.

Det ska inte krävas att en viss person har rätt filer på sin dator, känner till en hemlig inställning eller minns en särskild ordning på manuella steg. En annan person, eller helst en pipeline, ska kunna bygga samma applikation med samma resultat.

Byggbarhet är en grundförutsättning för containerbaserad leverans. Om organisationen inte kan bygga applikationen på ett upprepat sätt blir det svårt att skapa en tillförlitlig image. Om imagen inte är tillförlitlig blir test, spårbarhet och produktion också svagare.

För en chef kan byggbarhet översättas till en styrningsfråga:

> Kan organisationen återskapa det som körs i produktion utan att vara beroende av enskilda personers lokala kunskap?

Tecken på låg byggbarhet kan vara:

- byggsteg finns bara dokumenterade i äldre instruktioner
- leverantören skickar färdiga paket men inte tydlig information om hur de skapats
- olika utvecklare får olika resultat när de bygger samma system
- det finns beroenden till gamla verktyg som ingen längre äger
- testmiljön byggs på ett annat sätt än produktionen
- det saknas koppling mellan kodversion, image-version och godkänd release

Byggbarhet är alltså inte en detaljfråga för utvecklare. Den avgör om myndigheten kan ha kontroll över sina IT-stöd över tid.

## Begrepp 2: Standardiserad applikationspaketering

I kapitel 5 såg vi att en image är en paketerad mall för att starta en container. För utvecklingsarbetet innebär det att applikationen behöver paketeras enligt gemensamma regler.

**Standardiserad applikationspaketering** betyder att organisationen har ett gemensamt sätt att beskriva hur applikationer byggs, vilka grundimages som får användas, hur konfiguration hanteras, hur loggar skrivs, hur applikationen startas och hur den ska kunna övervakas.

Standardisering kan låta begränsande, men för en större organisation är den ofta en förutsättning för tempo. Om varje system har sitt eget unika sätt att paketeras, startas och felsökas blir organisationen långsam även om tekniken i sig är modern.

Standardiserad paketering hjälper organisationen att svara på frågor som:

- Vilken grundimage får användas?
- Var hämtas beroenden ifrån?
- Hur startas applikationen?
- Hur skickar applikationen loggar?
- Hur exponeras hälsokontroller?
- Hur hanteras konfiguration mellan miljöer?
- Vad måste finnas för att applikationen ska kunna testas automatiskt?
- Hur vet plattformen om applikationen fungerar?

En chef behöver inte kunna skriva instruktionerna själv. Men chefen behöver förstå att sådana regler måste finnas, ägas och följas.

Utan standardiserad paketering finns risken att organisationen bara flyttar gamla problem in i en ny teknik. Man får containrar, men behåller otydliga installationer, svårtestade leveranser och speciallösningar.

## Begrepp 3: DevOps-samarbete

**DevOps-samarbete** betyder i den här boken inte en viss organisationsmodell eller ett modeord. Det betyder att utveckling, test, förvaltning, säkerhet och drift behöver samarbeta tidigare och mer kontinuerligt kring hur IT-stöd byggs och levereras.

Containerteknik gör gränserna mellan roller tydligare på vissa sätt och mer sammanhängande på andra sätt.

Utvecklingsteamet behöver förstå hur applikationen ska köras. Plattformsteamet behöver förstå vilka krav applikationerna ställer. Säkerhetsfunktionen behöver komma in tidigt med regler för images, beroenden och behörigheter. Test behöver kunna påverka hur applikationen görs testbar. Förvaltningen behöver säkerställa att leveransen går att underhålla över tid.

Det betyder inte att alla gör allt. Det betyder att ingen del av kedjan kan behandlas som helt frikopplad.

Ett praktiskt sätt att uttrycka detta är:

> Containerteknik fungerar bäst när ansvar delas tydligt, inte när ansvar skickas vidare otydligt.

För chefer är detta centralt. Om organisationen inför containerteknik men behåller gamla stuprör kan resultatet bli frustration. Utveckling tycker att plattformen bromsar. Drift tycker att utveckling levererar ofärdiga applikationer. Säkerhet tycker att kontroller kommer in för sent. Förvaltning tycker att livscykelansvaret är oklart.

DevOps-samarbete handlar därför inte bara om samarbetskultur. Det handlar om att skapa ett leveransflöde där rollerna möts vid rätt tidpunkt och där ansvar är uttalat.

## Scenario: Myndigheten Nordverk

Nordverk har nyligen börjat arbeta med en gemensam containerplattform. De första tekniska försöken ser lovande ut. Ett internt utvecklingsteam har lyckats paketera en mindre applikation som en container image och köra den i en testmiljö.

Ledningen får en positiv rapport: “Tekniken fungerar.”

Men några veckor senare blir bilden mer komplicerad.

När teamet ska göra samma sak med ett större förvaltningsobjekt uppstår problem. Applikationen har flera gamla beroenden. Bygget fungerar bara på en särskild utvecklares arbetsstation. Installationsinstruktionen hänvisar till manuella steg som inte längre är aktuella. Testteamet kan inte enkelt starta en egen testmiljö. Driftorganisationen frågar hur loggar och larm ska fungera, men utvecklingsteamet har inte fått några tydliga riktlinjer.

Säkerhetsfunktionen ställer dessutom frågor:

- Vilken grundimage används?
- Varifrån hämtas beroenden?
- Vem godkänner imagen?
- Hur vet vi att det som testas är samma sak som ska till produktion?

Det blir tydligt att Nordverk inte bara behöver en plattform. De behöver förändra hur utvecklingsarbetet definierar en leverans.

I ett möte mellan utveckling, test, förvaltning, drift och säkerhet formulerar Nordverk en ny princip:

> Ett IT-stöd är inte leveransklart bara för att koden är färdig. Det är leveransklart när det kan byggas, paketeras, testas, kontrolleras och förvaltas på ett spårbart sätt.

Detta blir en vändpunkt. Containerplattformen är fortfarande viktig, men fokus flyttas från “vilket verktyg ska vi använda?” till “hur ska vi arbeta för att få styrbara leveranser?”

## Vad förändras i utvecklingsteamens vardag?

För utvecklingsteam innebär containerteknik flera konkreta förändringar.

### 1. Applikationen behöver kunna startas förutsägbart

En container ska kunna startas på ett standardiserat sätt. Det innebär att applikationen inte bör kräva manuella justeringar efter start eller specialkunskap som bara finns hos en person.

Utvecklingsteam behöver därför tänka på startbeteende:

- Vad krävs för att applikationen ska starta?
- Vad händer om ett beroende saknas?
- Hur visas fel vid uppstart?
- Kan plattformen avgöra om applikationen är frisk?
- Finns det tydliga loggar?

För chefer är detta inte en teknisk detalj utan en fråga om driftsäkerhet. En applikation som bara fungerar när någon tolkar felmeddelanden manuellt är svår att automatisera.

### 2. Konfiguration behöver skiljas från applikationen

I traditionella miljöer kan inställningar ibland vara inbyggda i installationen eller ligga i filer som ändras manuellt i varje miljö. I containerbaserade arbetssätt behöver organisationen vara tydligare med vad som är applikation och vad som är miljöspecifik konfiguration.

Det som testas bör vara samma image som senare kan gå vidare mot produktion. Skillnader mellan miljöer bör i första hand hanteras genom kontrollerad konfiguration, inte genom att imagen byggs om på olika sätt för varje miljö.

Chefsfrågan blir:

> Har vi en tydlig princip för vad som paketeras i imagen och vad som tillförs som miljöspecifik konfiguration?

Om svaret är nej riskerar organisationen att förlora mycket av värdet med containrar.

### 3. Beroenden behöver bli synliga

Moderna applikationer bygger ofta på många beroenden: bibliotek, ramverk, grundimages, externa tjänster, databaser och integrationer. Containerteknik gör det möjligt att paketera mycket av detta tydligare, men den tar inte bort ansvaret för beroendehantering.

Tvärtom blir beroenden mer synliga. Det är positivt, men det kan också blottlägga gamla problem.

Utvecklingsteam behöver kunna svara på:

- Vilka beroenden ingår?
- Varifrån kommer de?
- Hur uppdateras de?
- Vem ansvarar när ett beroende får en säkerhetsbrist?
- Hur påverkas applikationen om grundimagen uppdateras?

För myndigheter är detta särskilt viktigt eftersom lång livslängd, krav på kontroll och beroende av externa leverantörer ofta går hand i hand.

### 4. Testbarhet behöver byggas in

En applikation som körs som container bör kunna testas tidigt och ofta. Det kräver att utvecklingsteamet bygger applikationen så att den går att starta, testa och observera på ett konsekvent sätt.

Testbarhet är inte något som testorganisationen ensam kan lägga till i efterhand. Den påverkas av hur applikationen är byggd.

Exempel på frågor:

- Kan applikationen startas i en testmiljö utan omfattande handpåläggning?
- Går det att skapa testdata på ett kontrollerat sätt?
- Är beroenden mot andra system hanterade så att tester kan köras?
- Finns det automatiserade tester som ger rimlig trygghet?
- Kan fel analyseras med loggar och mätvärden?

Detta förbereder boken för nästa kapitel, där testarbetet behandlas mer fördjupat.

### 5. Leveransen behöver dokumenteras i flödet

I en manuell miljö kan mycket dokumentation finnas vid sidan av: instruktioner, mötesanteckningar, checklistor eller e-post. I ett containerbaserat leveransflöde bör mer av kunskapen finnas i själva flödet: i byggdefinitioner, pipeline-steg, versionsmärkning, godkännanden och kontroller.

Det betyder inte att traditionell dokumentation blir oviktig. Men den bör komplettera flödet, inte ersätta det.

En organisation bör kunna se:

- vilken kodversion som byggts
- vilken image som skapats
- vilka tester som körts
- vilka kontroller som passerats
- vem som godkänt nästa steg
- var imagen körs

För utvecklingsteam innebär detta att leveransen inte bara består av funktionalitet. Den består också av bevis på att funktionaliteten byggts och kontrollerats på rätt sätt.

## Vad behöver chefer vara uppmärksamma på?

När utvecklingsarbetet förändras finns några återkommande risker.

### Risk 1: Containerisering behandlas som efterarbete

En vanlig fälla är att utvecklingsteamet bygger applikationen som tidigare och sedan försöker “lägga den i en container” i slutet.

Det kan fungera för enkla applikationer, men det blir ofta problem när applikationen har gamla antaganden om filsystem, nätverk, konfiguration, sessionshantering eller installation.

Chefsfråga:

> Är containeranpassning en del av utvecklingsarbetet från början, eller något som görs sent i leveransen?

### Risk 2: Plattformsteamet får bära utvecklingsproblem

Om applikationer inte är byggbara, testbara eller paketerade enligt gemensamma regler hamnar problemen ofta hos plattformsteamet eller driftorganisationen. Då kan plattformen felaktigt uppfattas som långsam eller krånglig, trots att grundproblemet är bristande leveranskvalitet.

Chefsfråga:

> Skiljer vi mellan problem i plattformen och problem i applikationens paketering?

### Risk 3: Leverantörer fortsätter leverera enligt gamla mönster

Många myndigheter är beroende av externa leverantörer. Om avtalen och kraven inte förändras kan leverantörer fortsätta leverera kod, installationspaket eller dokumentation enligt gamla arbetssätt.

Då får myndigheten bära integrations- och paketeringsansvaret själv.

Chefsfråga:

> Kräver vi att leverantörer levererar på ett sätt som passar vår containerplattform och våra pipeline-krav?

Detta återkommer mer utförligt i kapitel 13 om upphandling och kravställning.

### Risk 4: Utveckling får ansvar utan stöd

Det motsatta problemet kan också uppstå. Organisationen säger till utvecklingsteam att de ska “ta ansvar för containrar”, men ger dem inte standarder, verktyg, utbildning eller stöd från plattformsteam och säkerhet.

Då blir resultatet ofta många lokala lösningar. Varje team hittar sitt eget sätt, vilket minskar styrbarheten.

Chefsfråga:

> Har utvecklingsteamen fått både ansvar och praktiska förutsättningar?

### Risk 5: Man underskattar befintliga system

Nya applikationer kan ofta anpassas relativt enkelt till containerbaserade arbetssätt. Äldre system kan vara svårare. De kan ha antaganden om operativsystem, filkataloger, installation, licenser, nätverk, databaser eller schemalagda jobb.

Chefsfråga:

> Har vi bedömt vilka system som är lämpliga att containerisera tidigt och vilka som kräver mer analys?

Alla system behöver inte flyttas samtidigt. Förändringsresan bör vara styrd, inte symbolisk.

## Påverkan på utveckling, test, förvaltning och drift

Även om detta kapitel fokuserar på utveckling påverkas hela kedjan.

## Utveckling

Utveckling behöver ta större ansvar för att applikationen är byggbar, paketerbar och testbar. Teamen behöver förstå de standarder som gäller för images, konfiguration, loggning, beroenden och hälsokontroller.

## Test

Test får bättre förutsättningar när applikationer kan startas på ett mer reproducerbart sätt. Men testbarhet måste byggas in tidigt. Testorganisationen behöver vara med och definiera vad som krävs för att automatiska och manuella tester ska bli meningsfulla.

## Förvaltning

Förvaltningen får ett tydligare tekniskt livscykelansvar. Det räcker inte att följa verksamhetsändringar och incidenter. Förvaltningen behöver även förstå när grundimages, beroenden och pipeline-steg behöver uppdateras.

## Drift

Driftens arbete påverkas av hur väl applikationen är byggd för plattformen. Om applikationen loggar rätt, startar förutsägbart och exponerar hälsosignaler blir drift och incidenthantering enklare. Om den inte gör det blir plattformen svårare att utnyttja.

## Säkerhet

Säkerhet behöver komma in tidigare i utvecklingsflödet. Krav på godkända grundimages, beroenden, sårbarhetsskanning, behörigheter och spårbarhet behöver vara inbyggda i arbetssättet, inte bara kontrollerade i slutet.

## Vanliga chefsfällor

### Fälla 1: “Det där är en utvecklarfråga”

Det är sant att utvecklare behöver hantera många praktiska detaljer. Men resultatet påverkar styrning, förvaltning, säkerhet och leveransförmåga. Därför är det också en ledningsfråga.

### Fälla 2: “När plattformen finns löser resten sig”

En plattform skapar möjligheter, men den förändrar inte automatiskt hur applikationer byggs. Utan förändrat utvecklingsarbete riskerar plattformen att bli underutnyttjad.

### Fälla 3: “Vi börjar med tekniken och tar ansvar senare”

Ansvar bör utformas tidigt. Annars skapas informella lösningar som är svåra att ändra när fler system börjar använda plattformen.

### Fälla 4: “Alla system ska containeriseras på samma sätt och samtidigt”

Olika system har olika förutsättningar. En klok förändringsresa börjar med lämpliga kandidater, lär av dem och bygger sedan vidare.

### Fälla 5: “Leverantören får lösa det”

Leverantörer kan bidra med viktig kompetens, men myndigheten behöver äga sina principer, standarder och krav. Annars riskerar varje leverantör att skapa sin egen modell.

## Frågor att ställa i den egna organisationen

### Om byggbarhet

1. Kan vi bygga våra viktigaste applikationer på ett upprepat och dokumenterat sätt?
2. Kräver bygget särskilda personer, lokala datorer eller informell kunskap?
3. Kan vi koppla en produktionssatt version till kod, image, testresultat och godkännande?

### Om paketering

4. Har vi gemensamma regler för hur applikationer ska paketeras som images?
5. Vet teamen vilka grundimages som är godkända?
6. Är det tydligt vad som ska ligga i imagen och vad som ska vara miljöspecifik konfiguration?

### Om ansvar

7. Vem ansvarar för att applikationen är körbar på plattformen?
8. Vem ansvarar för att pipeline, test och säkerhetskontroller fungerar?
9. Hur samverkar utveckling, test, förvaltning, drift och säkerhet innan något närmar sig produktion?

### Om leverantörer

10. Kräver vi att leverantörer levererar containeranpassade och testbara applikationer?
11. Ingår byggbarhet, paketering och spårbarhet i våra leveranskrav?
12. Kan vi själva förstå och följa hur leverantörens image har skapats?

### Om förändringsledning

13. Vilka utvecklingsteam är redo att arbeta på detta sätt?
14. Vilka behöver utbildning, stöd eller tydligare standarder?
15. Vilket system är en rimlig kandidat för nästa steg i förändringsresan?

## Mini-checklista för chefer

Innan ett utvecklingsteam eller en leverantör börjar leverera till en containerplattform bör organisationen kunna svara på följande:

- Det finns en tydlig standard för applikationspaketering.
- Det finns godkända grundimages eller principer för val av grundimage.
- Det är tydligt hur applikationer ska byggas i pipeline.
- Det är tydligt hur images ska versioneras och lagras.
- Det är tydligt hur konfiguration hanteras mellan miljöer.
- Det finns krav på loggning, hälsokontroller och observerbarhet.
- Det finns en ansvarsfördelning mellan utveckling, plattform, test, säkerhet och förvaltning.
- Leverantörskrav stödjer det nya arbetssättet.

## Snabb sammanfattning

- Containerteknik förändrar utvecklingsarbetet eftersom applikationen behöver vara byggbar, paketerbar, testbar och körbar på ett standardiserat sätt.
- Utvecklingsteam levererar inte längre bara kod; de bidrar till en kontrollerad och spårbar leverans.
- Byggbarhet minskar personberoende och gör det möjligt att återskapa det som körs i produktion.
- Standardiserad applikationspaketering gör att organisationen kan skala arbetssättet över flera system och team.
- DevOps-samarbete innebär tydligare och tidigare samverkan mellan utveckling, test, förvaltning, drift, säkerhet och plattform.
- Chefer behöver säkerställa att ansvar, krav, stöd och standarder utvecklas samtidigt som den tekniska plattformen.

## Reflektionsfrågor

1. Vad betyder “klart” i vår organisation: färdig kod, godkänd test eller körbar och förvaltningsbar leverans?
2. Vilka delar av vårt utvecklingsarbete bygger fortfarande på informell kunskap?
3. Vilka system skulle avslöja flest svagheter om vi försökte bygga och paketera dem helt automatiserat?
4. Har våra utvecklingsteam tillräckligt stöd för att ta ansvar för containerbaserad leverans?
5. Vilka krav behöver vi börja ställa redan i nya utvecklingsinitiativ?

## Nästa steg

Detta kapitel har visat hur utvecklingsarbetet påverkas när IT-stöd ska byggas och levereras som containrar. Nästa kapitel går vidare till testarbetet.

Där fördjupar vi frågan om hur containerteknik kan göra testmiljöer mer reproducerbara, hur automatiserad testning får större betydelse och varför “det fungerade i test” inte längre bör vara en ursäkt när skillnader mellan miljöer kan minskas.
