# Kapitel 11: Säkerhet, regelefterlevnad och kontroll

## Varför detta kapitel finns

När containerteknik införs i en myndighet uppstår ofta två motsatta reaktioner.

Den ena reaktionen är oro: “Går det inte för fort nu? Tappar vi kontrollen när utvecklingsteam kan bygga och leverera oftare?” Den andra reaktionen är övertro: “När allt ligger i containrar och pipelines blir säkerheten automatiskt bättre.”

Båda reaktionerna missar något viktigt.

Containerteknik kan ge bättre kontroll än många traditionella arbetssätt, men bara om organisationen bygger in kontrollen i själva leveransflödet. Om images byggs på okända baser, hämtas från okontrollerade källor, körs med för höga rättigheter eller släpps igenom utan spårbarhet, kan riskerna i stället öka. Det som tidigare var manuellt och långsamt kan bli snabbt men otydligt. Det är inte målet.

För en statlig myndighet är frågan därför inte om containerteknik är “säker” eller “osäker” i sig. Frågan är om myndigheten har förmåga att styra hela kedjan: från kod och beroenden, via byggande och test, till godkänd image, kontrollerad körning och uppföljning i produktion.

I tidigare kapitel har vi sett hur containerteknik påverkar utveckling, test, förvaltning och drift. I detta kapitel kopplar vi ihop dessa delar med säkerhet, regelefterlevnad och kontroll.

Kapitlets huvudbudskap är:

**Säkerhet i containerbaserade miljöer skapas inte främst genom en sista manuell granskning före produktion. Den skapas genom tydliga regler, automatiserade kontroller, spårbarhet och ansvar i hela leveranskedjan.**

## Lärandemål

Efter kapitlet ska läsaren kunna:

- förstå varför containerteknik förändrar säkerhets- och kontrollarbetet
- förklara vad supply chain-säkerhet betyder på chefsnivå
- se hur policies och kontrollpunkter kan byggas in i leveransflödet
- ställa frågor om images, beroenden, behörigheter, loggning och godkännande
- förstå varför regelefterlevnad kräver både teknik, arbetssätt och ansvarsfördelning

## Innan vi börjar

Vi återanvänder flera begrepp från tidigare kapitel:

- **Image**: den paketerade mall som används för att starta en container.
- **Registry**: platsen där images lagras och hämtas.
- **Pipeline**: flödet som bygger, testar, kontrollerar och levererar en ändring.
- **Spårbarhet**: förmågan att följa en leverans från källa till produktion.
- **Plattform**: den gemensamma tekniska och organisatoriska förmågan att köra IT-stöd standardiserat.
- **Plattformsdrift**: drift av den gemensamma miljö där många IT-stöd körs.

I detta kapitel lägger vi till tre huvudbegrepp:

- **Supply chain-säkerhet**
- **Policy**
- **Säkerhetsgrind**

De låter tekniska, men chefsfrågan bakom dem är enkel:

**Hur vet vi att det vi kör i produktion är det vi avsåg att köra, att det har kontrollerats på rätt sätt och att det körs inom beslutade ramar?**

## Huvudförklaring

### Säkerhet flyttar tidigare i flödet

I en traditionell leveransmodell kan säkerhet ofta uppfattas som något som sker sent: en granskning före produktionssättning, en checklista, ett godkännande eller ett möte där någon bekräftar att allt är klart.

Det kan fortfarande finnas behov av formella beslut och manuella godkännanden. Men i en containerbaserad leveransmodell räcker det inte att titta sent i processen. Många viktiga säkerhetsfrågor avgörs tidigare:

- Vilken grundimage används?
- Varifrån kommer beroenden och bibliotek?
- Vem får bygga en image?
- Vilka tester och skanningar körs?
- Vem får publicera till organisationens registry?
- Vilka images får köras i plattformen?
- Vilka rättigheter får en container ha i produktion?
- Hur upptäcks sårbarheter efter att en image redan har driftsatts?

Säkerheten behöver därför flytta från “kontroll i slutet” till “kontroll genom hela flödet”.

Det betyder inte att allt ska automatiseras utan mänskligt omdöme. Det betyder att människor inte ska behöva försöka kompensera för ett otydligt flöde med sena manuella kontroller.

### Supply chain-säkerhet: säkerhet i hela leveranskedjan

Begreppet **supply chain-säkerhet** betyder säkerhet i den kedja av komponenter, verktyg, personer, beslut och system som tillsammans skapar det som körs i produktion.

För en chef kan begreppet förklaras så här:

**Supply chain-säkerhet handlar om att ha kontroll över varifrån programvara kommer, hur den byggs, hur den kontrolleras, vem som får ändra den och hur den till slut blir en produktionssatt tjänst.**

I en containerbaserad miljö omfattar kedjan bland annat:

- källkod
- externa bibliotek och beroenden
- grundimages
- byggverktyg
- pipelineverktyg
- testresultat
- sårbarhetsskanning
- signering eller godkännande av images
- registry
- plattformens regler för vad som får köras
- loggar och spårbarhet i produktion

För en myndighet är detta särskilt viktigt eftersom IT-stöd ofta kan vara verksamhetskritiska, innehålla känslig information eller vara beroende av externa leverantörer. Om myndigheten inte vet hur programvaran har byggts och kontrollerats blir det svårt att visa att risker hanteras på ett styrt sätt.

### Policy: beslut som tekniken kan följa

En **policy** är en regel eller styrande princip. I vardagligt chefsspråk kan policy betyda ett dokument. I containerplattformar kan policy också betyda regler som tekniken faktiskt kan kontrollera.

Exempel på policybeslut kan vara:

- Endast images från myndighetens godkända registry får köras.
- Images måste vara byggda via godkänd pipeline.
- Images får inte köras som administratör om det inte finns särskilt beslut.
- Vissa typer av sårbarheter måste vara hanterade innan produktionssättning.
- Hemligheter, som lösenord och nycklar, får inte ligga inbyggda i images.
- Alla produktionssatta images ska kunna kopplas till ett ärende, en kodändring eller ett godkännande.

Skillnaden mellan en dokumenterad policy och en fungerande policy är viktig.

En dokumenterad policy säger vad organisationen vill. En fungerande policy påverkar faktiskt vad som kan byggas, godkännas och köras.

Målet är inte att ersätta styrning med teknik. Målet är att göra styrningen möjlig att följa, mäta och upprätthålla.

### Säkerhetsgrindar: kontrollpunkter som stoppar fel i tid

En **säkerhetsgrind** är en kontrollpunkt i leveransflödet där något måste vara uppfyllt innan arbetet får gå vidare.

Exempel:

- Pipeline får inte publicera en image om tester misslyckas.
- Registry får bara ta emot images från godkända byggflöden.
- Plattformen får bara köra images från godkända källor.
- En produktionsmiljö får inte acceptera en konfiguration som bryter mot säkerhetsregler.
- En ändring med hög risk kräver särskilt godkännande innan driftsättning.

Säkerhetsgrindar ska inte utformas för att bromsa allt. De ska utformas för att stoppa det som organisationen faktiskt har beslutat att den inte vill acceptera.

Det är en viktig chefsfråga. Om säkerhetsgrindarna är för svaga blir de symboliska. Om de är för hårda och dåligt förankrade kan de skapa skuggvägar, manuella undantag och frustration. Rätt nivå kräver samarbete mellan säkerhet, utveckling, test, drift, förvaltning och ledning.

### Kontroll är inte samma sak som långsamhet

I organisationer med stark manuell tradition kan kontroll ofta förknippas med möten, signaturer, väntan och personliga godkännanden. Containerteknik gör det möjligt att skilja kontroll från långsamhet.

En automatiserad kontroll kan vara både snabbare och mer konsekvent än en manuell kontroll. Den kan köras varje gång, på samma sätt, och ge spårbara resultat.

Exempel:

- Varje image skannas för kända sårbarheter.
- Varje ändring kopplas till en versionshistorik.
- Varje produktionssättning loggas.
- Varje avvikelse från policy kan följas upp.
- Varje container körs med definierade rättigheter.

Det betyder inte att automatiserade kontroller alltid är tillräckliga. Vissa beslut kräver fortfarande mänsklig bedömning. Men mänsklig bedömning bör användas där den gör mest nytta: vid riskavvägning, undantag, prioriteringar och ansvarstagande, inte för att gång på gång kontrollera sådant som tekniken kan kontrollera bättre.

### Regelefterlevnad kräver bevisbarhet

Regelefterlevnad handlar inte bara om att organisationen säger att den följer regler. Den behöver också kunna visa det.

I containerbaserade miljöer kan god spårbarhet göra detta lättare:

- Vilken image kördes vid ett visst tillfälle?
- Vilken version av koden byggde imagen på?
- Vilka tester passerade?
- Vilka sårbarheter var kända vid produktionssättning?
- Vem eller vilket flöde godkände leveransen?
- Vilka ändringar gjordes efter en incident?
- Vilka undantag beslutades, av vem och med vilken giltighetstid?

Detta är särskilt relevant i offentlig sektor, där krav på dokumentation, informationssäkerhet, ansvar, revision och långsiktig förvaltning ofta är höga.

En mogen containerplattform bör därför inte bara stödja teknisk körning. Den bör också stödja bevisbar styrning.

## Scenario: Myndigheten Nordverk

Nordverk har kommit långt i sin förändringsresa. De har börjat använda containrar, infört ett internt registry och byggt pipelines för några prioriterade IT-stöd. Testmiljöerna är mer reproducerbara än tidigare, och driftorganisationen börjar gå från serverhantering till plattformsdrift.

Men säkerhetschefen är inte helt nöjd.

På ett ledningsmöte säger hon:

“Vi har blivit snabbare, men jag vill veta om vi också har blivit mer styrbara. Kan vi visa vilka images som får köras, vilka kontroller de passerat och vem som ansvarar för undantag?”

Frågan blir startpunkten för ett gemensamt arbete mellan säkerhet, utveckling, test, förvaltning och drift.

### Det första problemet: olika team gör olika

Nordverk upptäcker att olika utvecklingsteam har gjort olika val.

Ett team bygger images från en godkänd grundimage. Ett annat team använder en image från en publik källa eftersom den var enkel att komma igång med. Ett tredje team har lagt in vissa inställningar direkt i imagen, trots att de egentligen borde hanteras som miljöspecifik konfiguration.

Alla team har försökt lösa praktiska problem. Men ur ett myndighetsperspektiv blir variationen en risk.

Ledningen inser att frågan inte bara är teknisk. Den handlar om gemensamma regler:

- Vilka grundimages är godkända?
- Vem förvaltar dem?
- Hur hanteras undantag?
- Hur säkerställs att leverantörer följer samma regler?
- Hur syns detta i uppföljning och revision?

### Det andra problemet: säkerhetskontroller sker för sent

Nordverk har sårbarhetsskanning, men den körs sent. Ibland upptäcks problem först när en release nästan är klar. Då uppstår press att göra undantag, skjuta upp åtgärder eller släppa ändå.

Utvecklingsteamen upplever säkerhet som ett hinder. Säkerhetsfunktionen upplever att teamen inte tar ansvar. Förvaltningen hamnar i mitten och får väga verksamhetens behov mot tekniska risker.

Efter en genomgång beslutar Nordverk att flera kontroller ska flyttas tidigare:

- grundimages ska kontrolleras innan de används brett
- sårbarhetsskanning ska köras redan i pipeline
- kritiska avvikelser ska synas tidigt
- undantag ska ha ägare och slutdatum
- produktionssättning ska bygga på samma kontrollresultat som tidigare steg

Det leder inte till att alla problem försvinner, men det förändrar samtalet. Säkerhet blir mindre av en slutgrind och mer av ett löpande ansvar.

### Det tredje problemet: plattformen accepterar för mycket

När plattformsteamet granskar produktionsmiljön upptäcker de att plattformen tekniskt sett kan köra mer än vad myndighetens policy egentligen borde tillåta.

Det går att köra images från fel registry. Vissa containrar körs med mer behörighet än de behöver. Nätverksregler är inte konsekvent definierade. Vissa loggar finns, men de används inte systematiskt för uppföljning.

Här blir en viktig insikt tydlig:

**Om plattformen accepterar sådant som organisationen inte vill tillåta, finns det ett glapp mellan styrning och faktisk kontroll.**

Nordverk börjar därför formulera tekniska policyregler som stödjer ledningens beslut. Det handlar inte om att chefer ska skriva teknisk konfiguration, utan om att chefer ska fatta tydliga beslut om risknivå, ansvar och uppföljning.

## Påverkan på utveckling, test, förvaltning och drift

### Utveckling

Utveckling påverkas genom att säkerhetskrav behöver bli en del av det normala byggflödet.

Utvecklingsteam behöver förstå:

- vilka grundimages som ska användas
- vilka beroenden som är tillåtna
- hur sårbarheter ska hanteras
- hur hemligheter och konfiguration ska separeras från image
- vilka krav som gäller innan en image får publiceras

Det betyder inte att varje utvecklare ska bli säkerhetsspecialist. Men teamet behöver arbeta inom tydliga ramar och få snabb återkoppling när något bryter mot ramarna.

### Test

Testarbetet påverkas genom att säkerhet blir en del av teststrategin.

Det handlar inte bara om funktionella tester, alltså om systemet gör rätt saker. Det handlar också om kontroller som visar att leveransen uppfyller organisationens tekniska och säkerhetsmässiga krav.

Exempel:

- test av konfiguration
- kontroll av att container inte kräver onödiga rättigheter
- kontroll av att image kommer från rätt registry
- kontroll av att sårbarhetsskanning har körts
- kontroll av att loggning och övervakning fungerar

Test blir därmed både kvalitetsarbete och kontrollarbete.

### Förvaltning

Förvaltningen påverkas eftersom säkerhet inte är avslutad vid produktionssättning.

En image som var acceptabel vid driftsättning kan senare visa sig innehålla en sårbar komponent. Ett beroende kan behöva uppdateras. En grundimage kan behöva bytas. En policy kan ändras. Ett undantag kan löpa ut.

Förvaltningen behöver därför ha processer för:

- uppföljning av kända sårbarheter
- prioritering av tekniskt underhåll
- ansvar för uppdateringar
- livscykelhantering av images och beroenden
- dokumentation av undantag
- koppling mellan säkerhetsrisk och verksamhetsrisk

Detta är en av de viktigaste chefsfrågorna i kapitlet. Containerteknik gör det lättare att paketera och leverera, men den tar inte bort behovet av aktiv förvaltning.

### Drift

Driften påverkas genom att plattformen blir en central kontrollpunkt.

Plattformsdriften behöver hantera:

- åtkomst till plattformen
- regler för vad som får köras
- nätverksstyrning
- loggning och övervakning
- incidentberedskap
- kapacitet och isolering mellan IT-stöd
- tekniska policyer

Det är här skillnaden mellan gammal och ny drift blir tydlig. I en manuell servermodell kunde drift ofta kontrollera genom att själv utföra många moment. I en containerplattform behöver drift i stället kontrollera genom standarder, plattformsregler, automation och uppföljning.

## Vanliga chefsfällor

### Fälla 1: Att tro att snabbare leverans betyder svagare kontroll

Snabbare leverans kan ge svagare kontroll om organisationen bara tar bort manuella steg utan att ersätta dem med tydligare regler och automatiserade kontroller.

Men snabbare leverans kan också ge starkare kontroll om varje ändring byggs, testas, skannas, loggas och spåras på samma sätt.

Chefsfrågan är inte om det går snabbt. Frågan är om flödet är styrt.

### Fälla 2: Att låta säkerhet bli ett separat sidospår

Om säkerhet hanteras som ett separat spår bredvid utveckling, test, förvaltning och drift kommer säkerhetsarbetet ofta in för sent.

I containerbaserade arbetssätt behöver säkerhet vara inbyggt i:

- kravställning
- utvecklingsflöde
- pipeline
- test
- registry
- plattform
- förvaltning
- incidenthantering

Säkerhetsfunktionen behöver därför vara med och utforma arbetssätt, inte bara granska resultat.

### Fälla 3: Att ha policyer som ingen teknisk kontroll stödjer

Många organisationer har bra styrdokument. Problemet är att styrdokumenten inte alltid syns i vardagens verktyg och flöden.

Om policyn säger att bara godkända images får köras, men plattformen ändå accepterar images från andra källor, finns ett kontrollglapp.

Chefer bör därför fråga:

“Vilka av våra viktiga regler kan tekniken faktiskt kontrollera?”

### Fälla 4: Att underskatta beroenden

En container image innehåller ofta mer än organisationens egen kod. Den kan innehålla operativsystemnära lager, bibliotek, paket och konfiguration. Dessutom används byggverktyg, pipelinekomponenter och externa källor.

Om organisationen bara granskar den egna koden missar den en stor del av risken.

### Fälla 5: Att göra undantag permanenta

Alla organisationer behöver ibland undantag. Det kan finnas verksamhetsskäl, akuta produktionsbehov eller tekniska övergångsproblem.

Problemet uppstår när undantag inte har ägare, slutdatum eller uppföljning.

I en containerplattform bör undantag behandlas som styrda riskbeslut, inte som informella genvägar.

## Frågor att ställa i den egna organisationen

### Om images och beroenden

- Vilka grundimages är godkända?
- Vem ansvarar för att grundimages uppdateras?
- Får team använda images från publika källor?
- Kan vi se vilka beroenden som ingår i en produktionssatt image?
- Hur hanterar vi sårbarheter som upptäcks efter produktionssättning?

### Om pipeline och kontrollpunkter

- Vilka säkerhetskontroller körs automatiskt i pipeline?
- Vad stoppar en leverans från att gå vidare?
- Vilka kontroller är rådgivande och vilka är blockerande?
- Var krävs mänskligt godkännande?
- Loggas kontrollresultat så att de kan följas upp?

### Om registry och godkännande

- Vem får publicera images till vårt registry?
- Är registry en teknisk lagringsplats eller också en styrpunkt?
- Kan vi skilja mellan utvecklingsimages, testade images och produktionsgodkända images?
- Kan en image tas bort, spärras eller återkallas vid behov?

### Om plattform och produktion

- Får plattformen bara köra images från godkända källor?
- Vilka rättigheter får containrar ha?
- Finns regler för nätverkstrafik mellan olika IT-stöd?
- Hur hanteras hemligheter som lösenord, nycklar och certifikat?
- Vilka säkerhetshändelser loggas och följs upp?

### Om regelefterlevnad och ansvar

- Kan vi visa hur en produktionssatt version godkändes?
- Kan vi visa vilka tester och kontroller som genomfördes?
- Vem beslutar om undantag?
- Hur länge gäller ett undantag?
- Hur rapporteras containerrelaterade risker till rätt ledningsnivå?

## Beslutsstöd: tre nivåer av kontroll

Ett praktiskt sätt att tänka är att dela upp kontrollen i tre nivåer.

### Nivå 1: Dokumenterad kontroll

Organisationen har beslutat hur det ska fungera.

Exempel:

- riktlinjer för images
- krav på registry
- ansvarsfördelning
- godkännandeprocess
- regler för undantag

Detta är nödvändigt, men inte tillräckligt.

### Nivå 2: Inbyggd kontroll

Organisationens tekniska flöden stödjer besluten.

Exempel:

- pipeline stoppar vissa fel
- registry kräver rätt behörighet
- plattformen accepterar bara godkända images
- säkerhetskontroller körs automatiskt
- loggar skapas konsekvent

Detta minskar beroendet av manuell kontroll.

### Nivå 3: Uppföljd kontroll

Organisationen följer upp att reglerna fungerar över tid.

Exempel:

- rapporter över sårbarheter
- uppföljning av undantag
- revision av åtkomst
- analys av incidenter
- mätning av hur snabbt risker åtgärdas

Detta är ofta den nivå där ledningen behöver vara mest aktiv. En kontroll som inte följs upp riskerar att förlora kraft.

## Vad chefen behöver besluta

Chefen behöver inte besluta exakt hur varje teknisk kontroll ska konfigureras. Men chefen behöver se till att vissa beslut faktiskt fattas.

Exempel på ledningsbeslut:

1. **Vilken risknivå accepterar vi?**  
   Alla sårbarheter är inte lika allvarliga, men organisationen behöver en tydlig modell för prioritering.

2. **Vilka källor litar vi på?**  
   Det måste vara tydligt varifrån images, grundimages och beroenden får komma.

3. **Vilka kontroller är obligatoriska?**  
   Organisationen behöver veta vilka kontroller som är krav och vilka som är rådgivande.

4. **Vem får besluta om undantag?**  
   Undantag ska vara synliga, tidsbegränsade och ägda.

5. **Hur kopplas tekniska risker till verksamhetsrisker?**  
   En sårbar komponent är inte bara en teknisk fråga. Den kan påverka verksamhet, rättssäkerhet, tillgänglighet och förtroende.

6. **Hur följer vi upp att modellen fungerar?**  
   Ledningen behöver indikatorer som visar om säkerhetsarbetet faktiskt blir bättre.

## Kort checklista för ledningsgruppen

En ledningsgrupp behöver inte kunna tekniken i detalj, men bör kunna få tydliga svar på följande:

- Vi vet vilka images som körs i produktion.
- Vi vet varifrån de kommer.
- Vi vet hur de har byggts.
- Vi vet vilka tester och kontroller de passerat.
- Vi vet vilka sårbarheter som är kända och hur de hanteras.
- Vi vet vem som ansvarar för undantag.
- Vi vet vilka regler plattformen själv upprätthåller.
- Vi vet hur containerrelaterade risker rapporteras och följs upp.

Om flera av dessa punkter inte går att besvara är organisationen sannolikt inte redo att betrakta containerplattformen som fullt styrd, även om den tekniskt fungerar.

## Snabb sammanfattning

- Containerteknik gör inte säkerheten bättre automatiskt.
- Den kan däremot göra säkerhet och kontroll mer spårbar, konsekvent och inbyggd.
- Supply chain-säkerhet handlar om kontroll över hela kedjan från kod och beroenden till produktionssatt IT-stöd.
- Policyer behöver omsättas till fungerande regler i pipeline, registry och plattform.
- Säkerhetsgrindar ska stoppa rätt saker vid rätt tidpunkt.
- Regelefterlevnad kräver bevisbarhet: organisationen behöver kunna visa vad som körs, hur det godkändes och vilka risker som hanteras.
- Undantag behöver vara synliga, tidsbegränsade och ägda.
- Chefer behöver inte konfigurera tekniken, men de behöver säkerställa att risknivå, ansvar och uppföljning är tydliga.

## Reflektionsfrågor

1. Var i vår leveranskedja har vi i dag störst kontrollglapp?
2. Vilka säkerhetskontroller sker för sent?
3. Vilka policyer finns bara som dokument, men inte som fungerande teknisk kontroll?
4. Vilka undantag har blivit permanenta?
5. Kan vi visa, i efterhand, exakt vad som kördes i produktion och hur det godkändes?
6. Hur rapporteras tekniska säkerhetsrisker till ledningen?
7. Vem äger helheten för supply chain-säkerhet i vår organisation?

## Nästa steg

Säkerhet, regelefterlevnad och kontroll visar att containerteknik inte kan införas som en isolerad teknikfråga. Den påverkar ansvar, roller och beslutsvägar.

Nästa kapitel handlar därför om **roller, ansvar och organisation**. Där går vi vidare från kontrollfrågan till organisationsfrågan: vem ska göra vad när utveckling, test, säkerhet, förvaltning och drift blir mer sammanlänkade?
