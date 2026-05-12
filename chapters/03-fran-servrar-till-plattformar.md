# Kapitel 3: Från servrar till plattformar

## Varför detta kapitel finns

I kapitel 2 såg vi att en container gör det möjligt att paketera en applikation och dess beroenden på ett mer standardiserat sätt. Det gör leveransen mer upprepningsbar. Men en container löser inte i sig frågan om hur många applikationer ska köras, övervakas, uppdateras, skyddas och styras i en större myndighetsmiljö.

Det är här plattformstänkandet kommer in.

Många organisationer har länge utgått från servrar. Ett nytt IT-stöd behöver en server, eller flera servrar. Någon beställer miljöer, någon installerar programvara, någon dokumenterar inställningar och någon ansvarar för att allt fungerar i produktion. Det kan fungera när miljön är liten och förändringstakten låg. Men när antalet system, beroenden, säkerhetskrav och leveranser växer blir server-för-server-modellen svår att styra.

En containerplattform innebär att organisationen flyttar fokus från enskilda servrar till en gemensam förmåga: ett standardiserat sätt att köra, uppdatera, övervaka och styra applikationer.

För en chef är den viktiga frågan därför inte bara: “Ska vi använda containrar?” Den viktigare frågan är: “Vilken gemensam plattformsförmåga behöver myndigheten för att kunna leverera IT-stöd säkert, spårbart och långsiktigt?”

## Lärandemål

Efter kapitlet ska du kunna:

- förklara skillnaden mellan serverfokus och plattformsfokus
- förstå varför standardisering är central för styrbar IT-leverans
- se hur plattformstänkandet påverkar utveckling, test, förvaltning och drift
- identifiera varför en containerplattform behöver ett tydligt organisatoriskt ägarskap
- ställa relevanta frågor om ansvar, standarder och plattformsbeslut

## Innan vi börjar

Vi bygger vidare på begreppen från de två första kapitlen:

- **Styrbar leverans:** organisationen kan följa, kontrollera, upprepa och förbättra vägen till produktion.
- **Container:** en standardiserad körmiljö där en applikation kan köras tillsammans med sina beroenden.
- **Image:** en paketerad mall som används för att starta containrar.
- **Miljöparitet:** strävan efter att utveckling, test och produktion ska vara tillräckligt lika för att testresultat ska vara tillförlitliga.

I det här kapitlet introduceras tre nya huvudbegrepp:

- **Plattform:** en gemensam teknisk och organisatorisk förmåga som gör det möjligt att köra och förvalta applikationer på ett standardiserat sätt.
- **Standardisering:** gemensamma regler, mönster och lösningar som minskar variation och personberoende.
- **Driftmodell:** hur ansvar, arbetssätt, verktyg och beslut är organiserade för att hålla IT-stöd fungerande över tid.

## Serverfokus: när varje IT-stöd blir ett eget undantag

I många organisationer har ett nytt IT-stöd historiskt inneburit en ny miljö. Den miljön kan bestå av virtuella servrar, databaser, nätverksregler, övervakning, säkerhetsinställningar, integrationslösningar och manuella rutiner. Ofta har varje system fått sin egen uppsättning lösningar.

Det kan börja rimligt:

- Ett verksamhetsområde behöver ett nytt system.
- Projektet beställer test- och produktionsmiljö.
- Driftorganisationen skapar servrar och installerar nödvändig programvara.
- Leverantören eller utvecklingsteamet beskriver hur applikationen ska installeras.
- Förvaltningen tar emot dokumentation och ansvar.

Problemet är att detta lätt leder till variation. Ett system installeras på ett sätt, ett annat på ett annat sätt. En leverantör använder en viss struktur, en annan leverantör använder en annan. Över tid får myndigheten många miljöer som liknar varandra på ytan, men som i praktiken kräver olika kunskap, olika rutiner och olika felsökningssätt.

Det skapar en tyst komplexitet. Den syns kanske inte i ett enskilt projekt, men den märks i förvaltning, säkerhetsarbete, incidenthantering och uppgraderingar.

Vanliga symptom är:

- Det är svårt att veta vilka system som kör vilken teknisk grund.
- Produktionssättning kräver systemunik handpåläggning.
- Testmiljöer och produktionsmiljöer skiljer sig åt.
- Uppdateringar blir dyra eftersom varje system behöver analyseras separat.
- Driftorganisationen behöver minnas undantag.
- Leverantörsbyten blir riskfyllda eftersom mycket kunskap ligger i lösningens historik.

Ur ett chefsperspektiv är problemet inte att servrar är “fel”. Problemet är att styrningen ofta sker per system och per miljö, i stället för genom gemensamma mönster.

## Plattformsfokus: en gemensam förmåga

En plattform är inte bara en teknisk produkt. I den här boken använder vi ordet plattform som en kombination av teknik, standarder, arbetssätt och ansvar.

En containerplattform kan till exempel erbjuda gemensamma sätt att:

- köra containrar
- hantera kapacitet
- styra nätverk och åtkomst
- samla loggar
- övervaka applikationer
- hantera uppdateringar
- använda godkända images
- automatisera leveranser
- skapa test- och produktionsmiljöer mer konsekvent

Det viktiga är att varje IT-stöd inte behöver uppfinna allt detta själv. Plattformen blir en gemensam grund.

En enkel jämförelse:

| Serverfokus | Plattformsfokus |
|---|---|
| Varje system får egna miljöer | Flera system använder gemensamma plattformsförmågor |
| Mycket löses system för system | Återkommande behov standardiseras |
| Driftkunskap blir ofta miljöspecifik | Driftkunskap samlas i gemensamma mönster |
| Produktionssättning kan bli unik per system | Leveransflöden kan bli mer likartade |
| Undantag växer över tid | Undantag behöver motiveras och styras |
| Ansvar följer ofta historiska gränser | Ansvar behöver definieras runt plattform, applikation och leveransflöde |

En plattform innebär alltså inte att alla system blir identiska. Men den innebär att organisationen väljer vilka delar som ska vara gemensamma.

## Varför standardisering är en ledningsfråga

Standardisering kan låta som en teknisk detalj. Det är det inte.

När en myndighet standardiserar hur IT-stöd paketeras, testas, körs och övervakas påverkar det flera ledningsfrågor:

- kostnad
- risk
- säkerhet
- kompetensförsörjning
- leverantörsstyrning
- förvaltningsbarhet
- incidenthantering
- möjlighet att förändra system över tid

Utan standardisering måste organisationen hantera många specialfall. Varje specialfall kan vara begripligt för den grupp som skapade det, men tillsammans bildar de en miljö som blir svår att överblicka.

Med standardisering blir det lättare att ställa gemensamma frågor:

- Hur ska en applikation paketeras?
- Var ska images lagras?
- Vilka kontroller måste vara godkända innan produktion?
- Hur ska loggar och larm hanteras?
- Hur ska ansvar delas mellan applikationsteam och plattformsteam?
- Vad krävs av en leverantör för att ett IT-stöd ska kunna förvaltas långsiktigt?

För en chef handlar standardisering därför inte om att begränsa professionella team i onödan. Det handlar om att skapa en gemensam spelplan där frihet och ansvar kan fungera tillsammans.

## Scenario: Nordverk börjar tänka plattform

Myndigheten Nordverk har under många år beställt tekniska miljöer system för system. Ett ärendehanteringssystem har sin struktur. Ett beslutsstöd har sin. Ett integrationsflöde har en tredje lösning. Flera system är välfungerande var för sig, men helheten är svår att styra.

När Nordverk börjar undersöka containerteknik märker ledningen snabbt att frågan inte bara gäller om en enskild applikation kan köras som container.

Flera frågor dyker upp:

- Ska varje projekt själv välja hur containrar byggs och körs?
- Ska varje leverantör ha egna rutiner för images?
- Ska testmiljöer skapas på olika sätt i olika projekt?
- Ska övervakning och loggning lösas separat för varje system?
- Vem ansvarar för att plattformen är säker, uppdaterad och tillgänglig?

Nordverks IT-chef inser att myndigheten står inför ett vägval.

Det ena alternativet är att låta containerteknik införas lokalt i enskilda projekt. Det kan ge snabb start, men riskerar att skapa en ny generation av speciallösningar.

Det andra alternativet är att etablera en gemensam plattformsförmåga med tydliga standarder, ansvar och införanderegler. Det kräver mer styrning i början, men kan ge bättre kontroll och förvaltningsbarhet över tid.

Ledningen behöver därför fatta ett principiellt beslut: containerteknik ska inte införas som en samling fristående teknikinitiativ, utan som en del av myndighetens långsiktiga leverans- och förvaltningsmodell.

## Hur utvecklingsarbetet påverkas

När organisationen går från serverfokus till plattformsfokus förändras utvecklingens arbete.

I en serverorienterad modell kan utvecklingsteam ibland lämna över kod och installationsinstruktioner, medan andra delar av organisationen ansvarar för att få applikationen att fungera i miljön. I en plattformsmodell blir det viktigare att applikationen från början är byggd för att köras på ett standardiserat sätt.

Det innebär att utvecklingsteam behöver förstå:

- hur applikationen paketeras som image
- vilka inställningar som ska vara miljöberoende
- hur loggar ska skrivas så att plattformen kan samla in dem
- hur applikationen visar om den är frisk eller har problem
- vilka resurser applikationen behöver
- vilka beroenden som måste vara tydliga och kontrollerade

Det betyder inte att varje utvecklare ska bli plattformsadministratör. Men det betyder att utveckling inte längre kan ses som helt skild från körbarhet och driftbarhet.

För chefer blir den centrala frågan: har våra team och leverantörer förmåga att leverera applikationer som fungerar i vår gemensamma plattformsmodell?

## Hur testarbetet påverkas

Plattformsfokus kan göra test mer konsekvent, men bara om organisationen använder plattformen medvetet.

Om testmiljöer kan skapas med samma grundläggande mönster som produktion blir det lättare att lita på testresultat. Det minskar risken för att “det fungerade i test” men inte i produktion.

Men en plattform gör inte automatiskt teststrategin bra. Organisationen behöver fortfarande bestämma:

- vilka tester som ska köras innan en ändring går vidare
- när testmiljöer ska skapas och rivas
- vilka testdata som får användas
- hur integrationer ska hanteras i test
- hur prestanda, säkerhet och tillgänglighet ska prövas
- vem som godkänner att en version är redo för nästa steg

För en chef är poängen att plattformen kan ge bättre tekniska förutsättningar för test, men bara om test blir en del av leveransflödet och inte en separat aktivitet i slutet.

## Hur förvaltningen påverkas

I en plattformsmodell förändras också förvaltningens fokus.

Förvaltning handlar inte bara om att hantera ärenden, fel och verksamhetsförändringar. Den behöver också omfatta teknisk livscykelhantering: images, beroenden, plattformsstandarder, säkerhetsuppdateringar och krav på fortsatt körbarhet.

När flera IT-stöd delar samma plattformsförmåga uppstår nya frågor:

- Vilka system följer aktuell standard?
- Vilka system använder gamla images eller gamla tekniska mönster?
- Hur snabbt måste ett system anpassas när plattformen uppdateras?
- Vem finansierar nödvändiga tekniska anpassningar?
- Hur hanteras undantag från standarden?
- När blir ett undantag en accepterad risk?

Det här är särskilt viktigt i offentlig sektor, där IT-stöd ofta har lång livslängd. Ett system kan vara verksamhetskritiskt i många år. Om det inte förvaltas enligt plattformens utveckling riskerar det att bli teknisk skuld, även om det fortfarande fungerar för användarna.

## Hur driften påverkas

För driftorganisationen innebär plattformsfokus en tydlig förändring.

I en traditionell modell kan drift ofta vara starkt kopplad till servrar, operativsystem, installationer och manuella åtgärder. I en plattformsmodell flyttas fokus mot att hålla den gemensamma plattformen stabil, säker och användbar.

Driftens uppgifter kan då handla mer om att:

- säkerställa plattformens tillgänglighet
- hantera kapacitet
- övervaka gemensamma komponenter
- definiera driftsmönster
- stödja applikationsteam
- hantera incidenter utifrån gemensam observability
- uppdatera plattformen kontrollerat
- se till att standarder efterlevs

Det betyder inte att drift blir mindre viktig. Tvärtom. Driftens kunskap blir central, men den används på ett annat sätt. Mindre tid bör gå till återkommande handpåläggning, och mer tid till att bygga robusta, upprepningsbara driftsförmågor.

## Det organisatoriska ägarskapet

En containerplattform behöver ett tydligt ägarskap. Annars riskerar den att hamna mellan stolarna.

Om plattformen ses som ett rent driftverktyg kan utveckling och förvaltning uppleva att den är något som “någon annan” ansvarar för. Om den ses som ett utvecklarverktyg kan säkerhet, drift och långsiktig förvaltning komma in för sent. Om den ses som ett projekt kan organisationen missa att plattformen behöver finansieras, styras och utvecklas över tid.

Ett tydligt ägarskap behöver svara på frågor som:

- Vem äger plattformens målbild?
- Vem beslutar om standarder?
- Vem prioriterar förbättringar?
- Vem hanterar kostnader?
- Vem följer upp användning och efterlevnad?
- Vem ansvarar för dialogen med applikationsteam och leverantörer?
- Vem beslutar om undantag?

En vanlig chefsfälla är att tro att plattformen är “införd” när tekniken är installerad. I praktiken är plattformen först införd när organisationen använder den på ett gemensamt, styrt och förvaltningsbart sätt.

## Vanliga chefsfällor

### Fälla 1: Att tro att plattform betyder produkt

En plattform kan innehålla produkter och verktyg, men den är mer än så. Den omfattar även arbetssätt, ansvar, standarder, kompetens och styrning.

**Hur man undviker det:**  
Be inte bara om en teknisk målarkitektur. Be också om en driftmodell, ansvarsfördelning och införandeplan.

### Fälla 2: Att låta varje projekt skapa sin egen containerlösning

Lokala initiativ kan ge snabb erfarenhet, men utan gemensam styrning kan de skapa ny variation och nya beroenden.

**Hur man undviker det:**  
Tillåt lärande och piloter, men koppla dem till en gemensam målbild och ett beslut om vilka delar som ska standardiseras.

### Fälla 3: Att standardisera utan att förklara varför

Om standarder upplevs som hinder kommer team och leverantörer att försöka gå runt dem.

**Hur man undviker det:**  
Koppla standarder till riskminskning, snabbare leverans, bättre testbarhet, säkrare förvaltning och tydligare ansvar.

### Fälla 4: Att underskatta förvaltningen av plattformen

En plattform behöver utvecklas, uppdateras, säkras, dokumenteras och stödjas.

**Hur man undviker det:**  
Behandla plattformen som en långsiktig förmåga, inte som ett avslutat införandeprojekt.

### Fälla 5: Att glömma befintliga IT-stöd

Nya system kan ofta anpassas lättare till en plattform än gamla system. Men myndighetens risker finns ofta i befintliga samhällsviktiga IT-stöd.

**Hur man undviker det:**  
Skapa en plan både för nya leveranser och för successiv hantering av befintliga system.

## Frågor att ställa i den egna organisationen

### Om nuläget

1. Beställer vi fortfarande tekniska miljöer system för system?
2. Hur många olika sätt har vi att installera, övervaka och förvalta IT-stöd?
3. Vilka undantag är dokumenterade, och vilka lever bara som erfarenhet hos enskilda personer?
4. Var finns störst skillnad mellan test och produktion?
5. Vilka system är svårast att flytta, uppdatera eller återställa?

### Om målbilden

1. Vad ska vara gemensamt i vår framtida plattformsmodell?
2. Vilken frihet ska applikationsteam och leverantörer ha?
3. Vilka standarder måste vara obligatoriska?
4. Hur ska undantag beslutas, dokumenteras och följas upp?
5. Hur vet vi att plattformen faktiskt förbättrar styrbarhet och inte bara inför ny teknik?

### Om ansvar

1. Vem äger plattformen?
2. Vem äger applikationens körbarhet?
3. Vem ansvarar för tekniska standarder?
4. Vem ansvarar för finansiering av plattformsförmågan?
5. Vem följer upp att utveckling, test, förvaltning och drift arbetar enligt samma modell?

## Snabb sammanfattning

- Containerteknik leder ofta till ett behov av plattformstänkande.
- Serverfokus innebär att varje IT-stöd lätt får egna miljöer, rutiner och undantag.
- Plattformsfokus innebär att organisationen bygger en gemensam förmåga för att köra och förvalta applikationer mer standardiserat.
- Standardisering är en ledningsfråga eftersom den påverkar kostnad, risk, säkerhet, kompetens och förvaltningsbarhet.
- En containerplattform är inte bara teknik. Den kräver ansvar, driftmodell, standarder, finansiering och löpande förvaltning.
- Utveckling, test, förvaltning och drift påverkas alla när organisationen går från serverfokus till plattformsfokus.
- En plattform är inte införd förrän den används som en gemensam och styrd organisatorisk förmåga.

## Nästa steg

Nu har vi gått från personberoende drift, via containerbegreppet, till plattformsfokus. Nästa kapitel placerar in Podman, Kubernetes och andra vanliga delar av containerekosystemet.

Målet är inte att gå djupt i tekniska detaljer, utan att ge dig som chef en karta: vilka delar finns, vad används de till och vilka frågor bör du ställa när organisationen diskuterar verktyg, produkter och plattformsval?
