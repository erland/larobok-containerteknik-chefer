# Kapitel 9: Hur förvaltningen förändras

## Varför detta kapitel finns

När en organisation börjar använda containerteknik förändras inte bara utveckling, test och drift. Även förvaltningen förändras.

I många statliga myndigheter är systemförvaltning organiserad kring förvaltningsobjekt, årsplanering, ändringsärenden, budgetcykler och överenskommelser mellan verksamhet och IT. Det kan skapa stabilitet, ansvar och långsiktighet. Men när applikationer börjar paketeras som container images, testas i pipelines och köras på en gemensam plattform räcker det inte längre att förvaltningen enbart följer funktionella ändringar och incidenter.

Förvaltningen behöver också kunna följa tekniska livscykler. Images blir gamla. Grundimages behöver uppdateras. Beroenden får nya versioner. Säkerhetsbrister upptäcks i komponenter som ingår i applikationen. Plattformen utvecklas. Testkedjan behöver underhållas. Leverantörers leveranser behöver kunna byggas, testas och köras på myndighetens sätt.

Det betyder inte att förvaltningen ska bli ett tekniskt specialistteam. Men den behöver kunna styra, prioritera och följa upp tekniskt underhåll på ett mer kontinuerligt sätt än tidigare.

För en chef är den centrala frågan därför inte: “Vem sköter containrarna?” Den centrala frågan är: “Hur säkerställer vi att våra IT-stöd förblir körbara, säkra, uppdaterbara och förvaltningsbara över tid?”

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förklara varför containerteknik påverkar systemförvaltningens ansvar
- förstå skillnaden mellan funktionell förvaltning och teknisk livscykelhantering
- se hur beroenden, grundimages och pipelines blir förvaltningsfrågor
- identifiera varför gamla förvaltningsmodeller kan skapa risk i containerbaserade miljöer
- formulera frågor som hjälper organisationen att styra tekniskt underhåll mer medvetet

## Innan vi börjar

I tidigare kapitel har vi sett att en container image är en paketerad mall som används för att starta en container. Vi har också sett att images kan lagras i ett registry, att pipelines kan bygga och testa dem, och att testmiljöer kan bli mer reproducerbara.

Detta förändrar förvaltningen. När samma image kan följas från byggande till test och produktion får organisationen bättre spårbarhet. Men den får också ett tydligare ansvar: det som är paketerat behöver underhållas.

En containerbaserad leverans är alltså inte “klar” när den första gången fungerar i produktion. Den behöver förvaltas genom hela sin livscykel.

## Förvaltning i en mer rörlig teknisk miljö

Traditionell systemförvaltning har ofta haft en tydlig uppdelning:

- verksamheten beskriver behov
- utveckling eller leverantör genomför ändringar
- test verifierar funktionen
- drift håller systemet igång
- förvaltningen samordnar planering, budget, ändringar och incidenter

Den modellen kan fortfarande vara användbar, men den behöver kompletteras.

I en containerbaserad miljö finns fler delar som förändras över tid. En applikation består inte bara av verksamhetslogik. Den består också av beroenden, bibliotek, körmiljö, konfiguration, grundimage, bygginstruktioner, tester, pipeline och plattformsanpassningar.

Förvaltningen behöver därför ha kontroll över två typer av förändring:

1. **Verksamhetsdriven förändring**  
   Nya funktioner, regeländringar, förbättringar, rättningar och anpassningar till nya behov.

2. **Teknikdriven förändring**  
   Uppdateringar av images, beroenden, grundimages, säkerhetsrättningar, plattformsversioner, byggkedjor och tekniska standarder.

Den första typen är ofta välkänd för chefer. Den andra typen riskerar att hamna i skymundan, trots att den kan vara avgörande för säkerhet, stabilitet och framtida förändringsförmåga.

## Förvaltningsobjektet blir större än applikationen

Ett vanligt misstag är att se förvaltningsobjektet som “systemet” i snäv mening: funktionerna användarna ser, databasen, några integrationer och kanske en driftmiljö.

Med containerteknik behöver förvaltningsobjektet förstås bredare. Det kan omfatta:

- applikationskod
- container images
- grundimages
- beroenden och bibliotek
- bygginstruktioner
- pipelines
- testdata och testmiljöer
- konfiguration för olika miljöer
- dokumenterade driftsättningsmönster
- övervakning, loggning och larm
- plattformsberoenden
- leverantörers leveransformat

Det betyder inte att samma person ska ansvara för allt praktiskt arbete. Men organisationen behöver veta vem som ansvarar för att varje del hålls aktuell, kontrollerad och användbar.

För chefer blir detta en styrningsfråga. Om förvaltningsobjektet definieras för snävt kommer viktiga delar av den faktiska leveransförmågan att sakna ägare.

## Livscykelhantering

Ett centralt begrepp i detta kapitel är **livscykelhantering**.

Livscykelhantering betyder att organisationen aktivt följer och styr hur tekniska delar föds, används, uppdateras och avvecklas över tid. Det gäller inte bara själva applikationen, utan också de komponenter som gör applikationen körbar.

I containerbaserad förvaltning kan livscykelhantering till exempel handla om att veta:

- vilka image-versioner som finns
- vilka versioner som körs i produktion
- vilka grundimages som används
- när en image behöver byggas om
- vilka beroenden som är för gamla
- vilka tekniska standarder som ändrats
- vilka plattformsversioner applikationen är beroende av
- vilka leveranser som inte längre är godkända att använda

Utan livscykelhantering kan en organisation hamna i ett läge där den har modern containerteknik på ytan, men gammalt personberoende och teknisk skuld under ytan.

## Beroendehantering

Ett annat viktigt begrepp är **beroendehantering**.

En applikation är sällan fristående. Den är beroende av bibliotek, ramverk, operativsystemnära komponenter, databasdrivrutiner, nätverksinställningar, certifikat, API:er och andra tjänster. När applikationen paketeras som en image blir vissa av dessa beroenden tydligare, men de försvinner inte.

Containerteknik kan göra beroenden mer synliga, eftersom de ingår i byggprocessen och i den image som sedan testas och körs. Men det kräver att organisationen faktiskt använder synligheten.

Förvaltningen bör därför kunna svara på frågor som:

- Vilka externa komponenter bygger våra images på?
- Vem följer upp om en komponent behöver uppdateras?
- Hur snabbt kan vi bygga om och testa en image om ett beroende behöver bytas?
- Finns det standardiserade grundimages som minskar variationen?
- Har vi en prioriteringsmodell för tekniskt underhåll?

Om dessa frågor saknar svar finns risken att beroenden bara hanteras när något går sönder eller när en säkerhetsgranskning upptäcker problemet.

## Scenario: Nordverk upptäcker det dolda förvaltningsarbetet

Myndigheten Nordverk har nu genomfört flera steg i sin förändringsresa. Ett av de interna IT-stöden har paketerats som container image. En pipeline bygger och testar imagen. Testmiljöerna är lättare att återskapa än tidigare, och produktionssättningen har blivit mer förutsägbar.

Ledningen börjar därför tala om pilotprojektet som lyckat.

Efter några månader uppstår en ny situation. Plattformsteamet meddelar att en grundimage som flera applikationer bygger på behöver uppdateras. Säkerhetsfunktionen vill veta vilka system som påverkas. Förvaltningen frågar om detta är en driftfråga, ett utvecklingsärende eller ett säkerhetsärende. Leverantören säger att applikationen fortfarande fungerar och att uppdateringen inte ingår i den beställda funktionsutvecklingen.

Ingen motsätter sig uppdateringen, men ingen har heller planerat tid, budget eller ansvar för den.

Nordverk inser då att containerteknik har gjort ett gammalt problem tydligare. Organisationen har länge haft tekniskt underhåll, men det har ofta varit osynligt, personberoende eller inbakat i större förändringspaket. Nu blir underhållet mer konkret: en image behöver byggas om, testas och godkännas.

Detta leder till en viktig ledningsinsikt: containerteknik kräver inte bara en ny teknisk plattform. Den kräver en förvaltningsmodell där tekniskt underhåll är planerat, prioriterat och finansierat.

## Påverkan på utveckling, test, förvaltning och drift

### Utveckling

Utvecklingsteam behöver bygga applikationer så att de kan underhållas över tid. Det räcker inte att en image fungerar vid första leverans. Den måste kunna byggas om, uppdateras och testas igen.

Det påverkar krav på kodstruktur, dokumentation, bygginstruktioner och ansvar för beroenden.

### Test

Test blir en del av förvaltningens livscykel. När en grundimage eller ett beroende ändras behöver organisationen kunna testa att applikationen fortfarande fungerar. Därför behöver automatiserade tester och reproducerbara testmiljöer underhållas även när ingen ny verksamhetsfunktion utvecklas.

### Förvaltning

Förvaltningen behöver planera för både funktionella ändringar och tekniskt underhåll. Det innebär att förvaltningsplanen bör innehålla tid och utrymme för uppdateringar, ombyggnad av images, förbättring av pipelines, testunderhåll och anpassningar till plattformens utveckling.

### Drift

Driftens roll påverkas genom att färre problem bör lösas genom manuell handpåläggning i produktion. I stället behöver drift och plattformsteam kunna ge återkoppling om beteende, resursanvändning, larm, kapacitet och mönster som förvaltningen behöver prioritera.

## Vanliga chefsfällor

### Fälla 1: Att tro att tekniskt underhåll är ett tekniskt sidospår

Tekniskt underhåll konkurrerar ofta med ny funktionalitet. Om ledningen inte ser underhållet som en förvaltningsfråga riskerar det att skjutas upp tills det blir akut.

**Hur man undviker det:**  
Gör tekniskt underhåll synligt i förvaltningsplaner, prioriteringar och uppföljning.

### Fälla 2: Att finansiera plattformen men inte förmågan att använda den

En myndighet kan investera i en containerplattform men sakna budget för att anpassa applikationer, bygga pipelines, underhålla tester och utbilda förvaltningsteam.

**Hur man undviker det:**  
Se plattformen som en del av en bredare förvaltningsförmåga, inte som en isolerad teknisk investering.

### Fälla 3: Att låta gamla ansvarsfördelningar leva kvar oförändrade

Om utveckling, test, förvaltning, drift och säkerhet fortsätter arbeta som separata överlämningsstationer kan containertekniken skapa nya konflikter i stället för bättre flöde.

**Hur man undviker det:**  
Tydliggör ansvar för images, beroenden, grundimages, pipelines, testmiljöer och produktionsberedskap.

### Fälla 4: Att betrakta leverantörens kod som hela leveransen

I en containerbaserad miljö är leveransen inte bara kod. Den behöver vara byggbar, testbar, paketerad, spårbar och möjlig att förvalta på myndighetens plattform.

**Hur man undviker det:**  
Ställ krav på förvaltningsbar leverans, inte bara på funktionell leverans.

### Fälla 5: Att inte avveckla gamla arbetssätt

Om gamla manuella rutiner behålls parallellt med nya containerflöden kan organisationen få dubbel komplexitet: både gammal handpåläggning och ny plattform.

**Hur man undviker det:**  
Bestäm vilka manuella moment som ska ersättas, vilka som ska finnas kvar som kontroller och vilka som ska avvecklas.

## Frågor att ställa i den egna organisationen

1. Vad ingår i vårt förvaltningsobjekt i dag: bara applikationen, eller också images, pipelines, tester, beroenden och plattformsanpassningar?
2. Vem ansvarar för att gamla images, grundimages och beroenden uppdateras?
3. Finns tekniskt underhåll synligt i förvaltningsplan, budget och prioritering?
4. Hur snabbt kan vi bygga om, testa och godkänna en image om ett beroende behöver uppdateras?
5. Har våra leverantörer ansvar för att leverera något som är körbart och förvaltningsbart på vår plattform?
6. Vilka manuella rutiner finns kvar trots att de skulle kunna ersättas av standardiserade flöden?
7. Får drift, test och säkerhet tillräckligt inflytande över förvaltningens prioriteringar?
8. Hur vet vi om ett IT-stöd håller på att bli tekniskt svårt att förvalta?

## Checklista för chefer

En containerbaserad förvaltning bör minst ha kontroll över:

- vilka images som används i produktion
- vilka grundimages som är godkända
- vem som ansvarar för beroenden
- hur images byggs om vid behov
- vilka tester som krävs vid tekniskt underhåll
- hur tekniska uppdateringar prioriteras mot ny funktionalitet
- hur leverantörer ska leverera förvaltningsbara lösningar
- hur plattformens förändringar påverkar applikationerna
- hur manuella undantag dokumenteras och avvecklas

Checklistan är inte en teknisk detaljlista. Den är ett sätt för ledningen att säkerställa att förvaltningen omfattar hela den förmåga som krävs för att hålla IT-stöd fungerande över tid.

## Snabb sammanfattning

- Containerteknik gör förvaltningen bredare, eftersom applikationens körbarhet beror på images, beroenden, grundimages, pipelines, tester och plattform.
- Förvaltningsobjektet bör inte definieras för snävt. Annars riskerar viktiga delar av leveransförmågan att sakna ägare.
- Livscykelhantering handlar om att följa, uppdatera och avveckla tekniska delar över tid.
- Beroendehantering blir mer synlig och mer styrbar när applikationer byggs som images, men bara om organisationen tar ansvar för uppföljningen.
- Tekniskt underhåll behöver planeras, finansieras och prioriteras. Det bör inte ses som ett sidospår.
- Leverantörer behöver kunna leverera lösningar som är byggbara, testbara, spårbara och förvaltningsbara på myndighetens plattform.

## Reflektionsfrågor

1. Vilka delar av våra IT-stöd är viktiga för körbarhet men saknar tydligt förvaltningsansvar?
2. Hur behandlas tekniskt underhåll i våra prioriteringsforum?
3. Har vi någon gemensam bild av vad en förvaltningsbar containerbaserad leverans innebär?
4. Vad skulle hända om en central grundimage behövde uppdateras inom två veckor?
5. Vilka styrsignaler behöver ledningen ge för att tekniskt underhåll inte ska bli osynligt?

## Nästa steg

Detta kapitel har visat hur förvaltningen förändras när IT-stöd paketeras, testas och körs på ett mer standardiserat sätt. Nästa kapitel går vidare till driften.

Där fördjupar vi hur driftrollen förändras från manuell serverhantering till plattformsdrift, övervakning, kapacitetsstyrning och automatiserade driftsmönster. Vi tittar också på varför driftens erfarenhet fortfarande är avgörande, även när färre saker bör göras manuellt i produktion.
