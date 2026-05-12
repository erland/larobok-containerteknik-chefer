# Kapitel 8: Hur testarbetet förändras

## Varför detta kapitel finns

När en organisation börjar använda containerteknik förändras inte bara hur applikationer byggs och driftsätts. Testarbetet förändras också.

I många organisationer har test länge varit ett separat steg mellan utveckling och produktion. Utvecklingsteamet gör en ändring, någon paketerar eller installerar den i en testmiljö, testare genomför planerade tester och först därefter kan organisationen börja tala om produktionssättning. Det kan fungera, men det bygger ofta på att testmiljöer hålls vid liv manuellt, att installationssteg upprepas korrekt och att alla förstår vilka skillnader som finns mellan test och produktion.

Containerteknik ändrar förutsättningarna. När applikationen paketeras på ett standardiserat sätt kan samma image testas i flera steg. Testmiljöer kan skapas mer förutsägbart. Automatiserade tester kan köras tidigare och oftare. Skillnader mellan utveckling, test och produktion kan minska.

Men det sker inte automatiskt. En containerplattform gör inte testarbetet moget av sig själv. Om organisationen bara flyttar gamla manuella testmönster till en ny teknisk plattform kan resultatet bli samma osäkerhet, men med fler tekniska begrepp.

För chefer är den viktiga frågan därför inte: “Kan vi köra tester i containrar?” Den viktiga frågan är: “Hur behöver vårt testarbetet förändras för att vi snabbare och säkrare ska veta om ett IT-stöd är redo att gå vidare?”

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förklara varför containerteknik påverkar teststrategi och testmiljöer
- förstå begreppen reproducerbar testmiljö, testautomation och miljöparitet
- se kopplingen mellan pipeline, image, test och produktionssättning
- identifiera risker med manuella och personberoende testmiljöer
- ställa chefsfrågor om testbarhet, kvalitet, ansvar och beslutsunderlag

## Innan vi börjar

Vi bygger vidare på begrepp från tidigare kapitel:

- **Container**: en standardiserad körmiljö för applikationen.
- **Image**: den paketerade mall som används för att starta containern.
- **Miljöparitet**: strävan efter att utveckling, test och produktion ska vara tillräckligt lika för att testresultat ska vara trovärdiga.
- **Pipeline**: flödet som bygger, testar, kontrollerar och levererar ändringar.
- **Byggbarhet**: förmågan att bygga applikationen på ett upprepat och kontrollerat sätt.

I detta kapitel introducerar vi tre huvudbegrepp:

- **Reproducerbar testmiljö**
- **Testautomation**
- **Teststrategi**

## Varför traditionella testmiljöer ofta blir osäkra

En testmiljö ska ge organisationen kunskap. Den ska hjälpa oss att förstå om en ändring fungerar, om den påverkar andra delar av systemet och om den kan gå vidare mot produktion.

Problemet är att testmiljön ibland blir en egen verklighet.

Den kan ha andra versioner av beroenden än produktion. Den kan ha andra inställningar. Den kan vara uppsatt för hand för länge sedan. Den kan ha testdata som inte längre motsvarar verkligheten. Den kan ha undantag som alla känner till men ingen riktigt äger. Den kan dessutom vara beroende av en person som “vet hur man får igång den”.

Då blir testresultatet svagare. Ett godkänt test betyder inte längre säkert att ändringen fungerar i produktion. Det betyder bara att ändringen fungerade i just den testmiljö som användes vid just det tillfället.

För en chef är detta en styrningsfråga. Om testmiljön inte är pålitlig blir även beslutsunderlaget inför produktionssättning svagt.

Vanliga tecken på osäkra testmiljöer är:

- testmiljöer skiljer sig kraftigt från produktion
- testmiljöer skapas och underhålls manuellt
- det är oklart vilken version som testas
- testresultat kan inte kopplas tydligt till en image eller ändring
- tester upprepas inte på samma sätt varje gång
- fel avfärdas med “det fungerar nog i produktion”
- produktionssättningar kräver extra manuell kontroll eftersom testmiljön inte anses tillräckligt trovärdig

Containerteknik kan minska flera av dessa problem, men bara om organisationen använder tekniken för att stärka testprocessen.

## Reproducerbar testmiljö

En **reproducerbar testmiljö** är en testmiljö som kan återskapas på ett förutsägbart sätt.

Det betyder inte att alla testmiljöer måste vara identiska med produktion i varje detalj. Det betyder att organisationen vet hur miljön skapas, vilka versioner som används, vilka beroenden som ingår och vilka skillnader mot produktion som är accepterade.

I en traditionell miljö kan testmiljön vara något som “finns där”. Den har byggts upp över tid, ändrats av olika personer och justerats när problem har uppstått. I en containerbaserad miljö bör testmiljön i högre grad vara något som kan beskrivas, skapas, användas och vid behov kastas bort och återskapas.

Det är en stor skillnad.

En reproducerbar testmiljö ger organisationen bättre kontroll över frågor som:

- Vilken applikationsversion testades?
- Vilken image användes?
- Vilka beroenden ingick?
- Vilken konfiguration användes?
- Vilka tester kördes?
- Kan vi återskapa samma förutsättningar om vi behöver felsöka?

För chefer är detta viktigt eftersom reproducerbarhet minskar personberoende. Det blir mindre viktigt vem som råkade sätta upp testmiljön, och mer viktigt att organisationen har ett definierat sätt att skapa den.

## Miljöparitet: tillräckligt lika för att vara meningsfullt

I kapitel 2 introducerades begreppet **miljöparitet**. Det handlar om att utveckling, test och produktion ska vara tillräckligt lika för att testresultat ska vara användbara.

Containerteknik bidrar till miljöparitet genom att samma image kan följa med genom flera steg. Applikationen paketeras inte om manuellt för varje miljö. Det som testas kan i högre grad vara samma tekniska artefakt som senare körs i produktion.

Det betyder inte att alla miljöer ska vara exakt likadana. Produktion har ofta andra volymer, andra säkerhetskrav, annan åtkomst, andra integrationspunkter och annan övervakning. Men skillnaderna ska vara kända och medvetna.

En bra chefsfråga är därför:

> Vilka skillnader mellan test och produktion är avsiktliga, dokumenterade och accepterade?

Om svaret är oklart finns en risk att organisationen testar något annat än det den senare ska driftsätta.

## Testautomation

**Testautomation** betyder att tester körs maskinellt, återkommande och på ett förutsägbart sätt.

Det betyder inte att alla tester ska automatiseras. Vissa tester kräver mänsklig bedömning, särskilt användbarhet, verksamhetsnära granskning och vissa typer av acceptanstest. Men många tekniska kontroller bör inte behöva göras manuellt varje gång.

Exempel på tester och kontroller som ofta kan automatiseras är:

- att applikationen går att bygga
- att grundläggande funktioner fungerar
- att API:er svarar som förväntat
- att kända fel inte återkommer
- att image kan starta
- att nödvändiga konfigurationsvärden finns
- att beroenden inte bryter mot definierade regler
- att kod- eller image-kontroller passerar fastställda gränser

För en chef är poängen inte att kunna skriva testerna. Poängen är att förstå vad automatiserade tester gör med styrningen.

När tester körs automatiskt kan organisationen få tidigare signaler. Fel upptäcks innan de har gått långt i leveransflödet. Beslut kan baseras på upprepbara kontroller, inte bara på muntliga besked. Produktionssättning kan bli mindre dramatisk eftersom fler saker redan har kontrollerats på vägen.

Men testautomation kräver investering. Den behöver prioriteras, förvaltas och följas upp. Tester som ingen äger blir snabbt inaktuella. Automatisering utan ansvar blir bara ännu ett tekniskt lager.

## Teststrategi: mer än att ha många tester

Det är lätt att tro att bättre testning betyder fler tester. Ibland stämmer det. Men ofta är den viktigare frågan vilka tester som behövs, när de ska köras och vilket beslut de ska stödja.

En **teststrategi** beskriver hur organisationen får tillräcklig kunskap om kvalitet, risk och produktionsberedskap.

I en containerbaserad leverans bör teststrategin svara på frågor som:

- Vilka tester ska köras innan en image får publiceras till registry?
- Vilka tester ska köras innan en image får gå vidare till en gemensam testmiljö?
- Vilka kontroller krävs innan produktionssättning?
- Vilka tester är automatiserade, och vilka kräver mänsklig bedömning?
- Vem äger testdata, testmiljöer och testresultat?
- Hur kopplas testresultat till spårbarhet och godkännande?

Teststrategin behöver alltså hänga ihop med pipeline, registry, plattform och förvaltningsmodell. Den kan inte vara ett fristående dokument som lever bredvid leveransflödet.

## Scenario: Nordverk och testmiljön som inte längre gick att lita på

Myndigheten Nordverk har länge haft en etablerad testprocess. När en ny version av ett IT-stöd ska testas beställer förvaltningen en uppdatering av testmiljön. Driftgruppen installerar versionen enligt instruktioner. Testgruppen genomför planerade tester. Om testerna går bra förbereds produktionssättning.

På papperet ser processen tydlig ut. I praktiken finns flera problem.

Testmiljön är gammal. Den har uppdaterats stegvis under många år. Vissa inställningar skiljer sig från produktion. Några beroenden har andra versioner. Testdata är ofullständig. När installationen misslyckas finns det två personer som brukar veta vilka manuella justeringar som krävs.

När Nordverk börjar arbeta med containrar upptäcker man att detta inte bara är ett tekniskt problem. Det är ett ledningsproblem.

Ledningen har tidigare fått rapporter om att “test är godkänt”. Men ingen har ställt följdfrågan: “Vad betyder godkänt, givet hur testmiljön faktiskt ser ut?”

I den nya målbilden ska Nordverk kunna göra följande:

1. Bygga en image i pipeline.
2. Köra grundläggande automatiserade tester.
3. Publicera image till ett kontrollerat registry.
4. Starta samma image i en testmiljö.
5. Köra både automatiserade och verksamhetsnära tester.
6. Koppla testresultatet till exakt image-version.
7. Fatta beslut om vidare steg baserat på spårbara resultat.

Det löser inte alla problem, men det ändrar styrningen. Test blir inte längre bara en aktivitet efter utveckling. Test blir en integrerad del av leveransflödet.

## Påverkan på utveckling

För utvecklingsteam innebär förändringen att testbarhet behöver byggas in tidigare.

Applikationen behöver kunna startas på ett förutsägbart sätt. Den behöver kunna konfigureras utan manuella specialsteg. Den behöver ge tydliga felmeddelanden när något saknas. Den behöver fungera med automatiserade tester i pipeline.

Det innebär att utvecklingsteam inte bara kan fråga: “Fungerar koden på min dator?” De behöver också fråga:

- Kan applikationen byggas till en image varje gång?
- Kan den startas i en ren testmiljö?
- Kan grundläggande tester köras automatiskt?
- Är beroenden tydliga?
- Är testdata och konfiguration hanterbara?
- Går fel att felsöka utan informell kunskap?

För chefer innebär detta att testbarhet bör vara ett krav på utvecklingsarbete, inte en efterhandsfråga för testorganisationen.

## Påverkan på test

För testfunktionen förändras rollen från att enbart genomföra tester till att också bidra till hur kvalitet byggs in i leveransflödet.

Det kan innebära att testare behöver arbeta närmare utveckling och plattformsteam. De behöver påverka vilka tester som automatiseras, hur testdata hanteras och hur testresultat ska presenteras för beslut.

Test blir mer kontinuerligt. Vissa tester körs tidigt och ofta. Andra tester sker senare och mer verksamhetsnära. Det viktiga är att organisationen förstår skillnaden mellan olika typer av tester.

En enkel indelning kan vara:

| Testtyp | Syfte | Typisk plats i flödet |
|---|---|---|
| Bygg- och startkontroll | Kontrollera att applikationen kan byggas och startas. | Tidigt i pipeline. |
| Funktionella automatiserade tester | Kontrollera att centrala funktioner fungerar. | Pipeline eller testmiljö. |
| Integrationstester | Kontrollera samspel med andra system. | Särskild testmiljö. |
| Säkerhets- och policykontroller | Kontrollera definierade tekniska och säkerhetsmässiga krav. | Pipeline och registry-flöde. |
| Verksamhetsnära tester | Bedöma om lösningen stödjer verkligt arbetssätt. | Test- eller acceptansmiljö. |

Poängen är inte att denna tabell ska bli en fast modell för alla. Poängen är att test behöver delas upp efter vilket beslut det ska stödja.

## Påverkan på förvaltning

Förvaltningen påverkas eftersom testresultat blir en viktig del av systemets livscykel.

Om en image behöver uppdateras på grund av ett säkerhetsproblem räcker det inte att fråga om uppdateringen tekniskt går att göra. Förvaltningen behöver veta vilka tester som krävs för att våga släppa den nya versionen. Om en beroende komponent byts ut behöver förvaltningen förstå hur detta verifieras.

Det innebär att förvaltningens ansvar blir mer kontinuerligt. Teststrategin är inte bara relevant vid stora releaser. Den är relevant vid mindre ändringar, tekniska uppdateringar, akuta rättningar och plattformsförändringar.

Chefer bör därför se testförmåga som en förvaltningsförmåga. En organisation som inte kan testa effektivt får svårt att uppdatera säkert.

## Påverkan på drift och plattform

Drift och plattformsteam påverkas eftersom testmiljöer i högre grad behöver skapas och drivas på samma sätt som andra miljöer.

Det betyder inte att testmiljöer ska ha samma kapacitet eller säkerhetsnivå som produktion. Men de bör bygga på samma grundläggande mönster där det är möjligt.

Plattformsteam kan behöva erbjuda:

- standardiserade sätt att starta applikationer i test
- stöd för loggning och felsökning
- hantering av testnamespace eller motsvarande avgränsade miljöer
- gemensamma regler för konfiguration och åtkomst
- möjlighet att skapa och ta bort testmiljöer på kontrollerat sätt

Detta förändrar driftens roll. Testmiljöer blir inte bara “något lägre prioriterat vid sidan av”. De blir en del av organisationens leveransförmåga.

## Vanliga chefsfällor

### Fälla 1: Att tro att containrar automatiskt ger bra test

Containrar kan göra test mer förutsägbart, men de ersätter inte teststrategi, testdata, ansvar eller kvalitetsarbete.

**Hur man undviker fällan:**  
Ställ frågor om vilka tester som körs, när de körs, vem som äger dem och vilket beslut de stödjer.

### Fälla 2: Att mäta testmognad i antal automatiserade tester

Många tester är inte alltid bättre. Tester kan vara långsamma, irrelevanta eller svåra att underhålla.

**Hur man undviker fällan:**  
Fokusera på risk, täckning, beslutsvärde och återkopplingstid. Fråga vad organisationen lär sig av testerna.

### Fälla 3: Att låta testmiljöer fortsätta vara manuella undantag

Om testmiljöer fortfarande skapas och justeras manuellt försvinner mycket av värdet med standardiserad paketering.

**Hur man undviker fällan:**  
Kravställ reproducerbarhet. Organisationen bör veta hur testmiljöer skapas, konfigureras och återställs.

### Fälla 4: Att separera test från förvaltning

Test ses ibland som något som hör till projekt eller utveckling. Men i en containerbaserad miljö behövs testförmåga löpande, även vid tekniska uppdateringar och säkerhetsåtgärder.

**Hur man undviker fällan:**  
Behandla testautomation, testdata och testmiljöer som delar av långsiktig förvaltningsförmåga.

### Fälla 5: Att acceptera otydliga testbesked

Besked som “det är testat” eller “det fungerar i test” är inte tillräckliga om det är oklart vad som testats.

**Hur man undviker fällan:**  
Koppla testbesked till image-version, testmiljö, testomfattning och eventuella kända avvikelser.

## Frågor att ställa i den egna organisationen

### Om testmiljöer

- Hur skapas våra testmiljöer i dag?
- Vilka delar är automatiserade och vilka är manuella?
- Kan vi återskapa en testmiljö från grunden?
- Vet vi vilka skillnader som finns mellan test och produktion?
- Är skillnaderna avsiktliga, dokumenterade och accepterade?

### Om testautomation

- Vilka tester körs automatiskt i pipeline?
- Vilka tester görs fortfarande manuellt av vana snarare än behov?
- Hur ofta går automatiserade tester sönder av andra skäl än verkliga fel?
- Vem ansvarar för att tester hålls aktuella?
- Hur snabbt får utvecklingsteam återkoppling när något går fel?

### Om beslut och styrning

- Vad betyder “godkänt test” hos oss?
- Kan ett testresultat kopplas till exakt image-version?
- Vilka testresultat krävs för produktionssättning?
- Vilka risker accepteras när tester saknas eller hoppas över?
- Får ledningen tillräckligt tydligt beslutsunderlag inför större förändringar?

### Om organisation och ansvar

- Vem äger teststrategin?
- Hur samverkar utveckling, test, förvaltning, säkerhet och plattform kring test?
- Har förvaltningen budget och mandat att underhålla testautomation?
- Har leverantörer tydliga krav på testbarhet och automatiserade kontroller?
- Behandlas testmiljöer som strategisk leveransförmåga eller som tekniska sidomiljöer?

## Mini-checklista för chefer

En organisation är på rätt väg när den kan svara ja på följande:

- Vi vet vilken image som har testats.
- Vi kan återskapa viktiga testmiljöer.
- Vi har definierat vilka skillnader som finns mellan test och produktion.
- Vi kör centrala tester automatiskt i leveransflödet.
- Vi vet vilka manuella tester som fortfarande behövs och varför.
- Vi kopplar testresultat till beslut om vidare leverans.
- Vi har ägarskap för testautomation, testdata och testmiljöer.
- Vi ser testförmåga som en del av förvaltningen, inte bara som en projektaktivitet.

## Snabb sammanfattning

- Containerteknik kan göra testarbetet mer förutsägbart, men bara om organisationen samtidigt utvecklar sin teststrategi.
- En reproducerbar testmiljö kan återskapas på ett kontrollerat sätt och minskar personberoende.
- Miljöparitet handlar om att test och produktion ska vara tillräckligt lika för att testresultat ska vara trovärdiga.
- Testautomation ger snabbare och mer upprepbar återkoppling, men behöver ägarskap och underhåll.
- Testresultat bör kopplas till exakt image-version, testmiljö och beslut.
- För chefer är test inte bara en kvalitetsfråga. Det är en styrningsfråga, en riskfråga och en förvaltningsfråga.

## Nästa steg

I nästa kapitel går vi vidare till förvaltningen. När applikationer paketeras som images, testas i pipelines och körs på en plattform förändras också vad det innebär att långsiktigt förvalta ett IT-stöd.

Förvaltning handlar då inte bara om ärenden, ändringar och årsplaner. Den behöver också hantera livscykler för images, beroenden, grundimages, plattformsanpassningar, testförmåga och kontinuerliga säkerhetsuppdateringar.
