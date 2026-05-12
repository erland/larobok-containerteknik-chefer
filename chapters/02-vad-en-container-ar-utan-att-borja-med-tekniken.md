# Kapitel 2: Vad en container är – utan att börja med tekniken

## Varför detta kapitel finns

I förra kapitlet såg vi hur personberoende drift och manuella produktionsmoment gör IT-leveranser svåra att styra. Problemet är sällan att människor gör ett dåligt arbete. Problemet är att organisationens förmåga ofta sitter i personers erfarenhet, lokala rutiner och miljöspecifika speciallösningar.

Det här kapitlet introducerar containerbegreppet på chefsnivå. Målet är inte att du ska kunna bygga en container själv. Målet är att du ska förstå varför containrar förändrar hur IT-stöd utvecklas, testas, driftsätts och förvaltas.

En container kan beskrivas som ett standardiserat sätt att paketera och köra en applikation tillsammans med det den behöver för att fungera. Den viktigaste poängen för en chef är inte själva tekniken, utan att paketeringen gör leveransen mer upprepningsbar, mer flyttbar och lättare att styra.

## Lärandemål

Efter kapitlet ska du kunna:

- förklara vad en container är på en övergripande nivå
- skilja mellan en applikation, en image och en körande container
- förstå varför containrar kan minska skillnader mellan utveckling, test och produktion
- se hur containerteknik påverkar ansvar mellan utveckling, test, förvaltning och drift
- ställa relevanta frågor om paketering, miljöer och körbarhet i den egna organisationen

## Innan vi börjar

Vi bygger vidare på fyra begrepp från kapitel 1:

- **Manuell produktionsdrift:** när viktiga moment utförs för hand.
- **Personberoende:** när organisationen är beroende av specifika individers kunskap.
- **Leveransflöde:** kedjan från ändring till testad och driftsatt funktion.
- **Styrbar leverans:** ett leveranssätt som kan följas, kontrolleras, upprepas och förbättras.

Containerteknik är ett av flera sätt att göra leveransflödet mer styrbart. Det löser inte alla problem, men det förändrar förutsättningarna.

## Ett vanligt nuläge: “det fungerade i test”

Många organisationer känner igen situationen:

1. Ett utvecklingsteam gör en ändring.
2. Ändringen fungerar i utvecklingsmiljön.
3. Den fungerar också i test, åtminstone efter några justeringar.
4. Vid produktionssättning uppstår problem.
5. Felsökningen visar att produktionsmiljön inte riktigt motsvarar testmiljön.

Skillnaden kan vara liten: en annan version av ett bibliotek, en annorlunda systeminställning, en saknad miljövariabel, en annan katalogstruktur eller ett manuellt moment som råkade göras i test men inte i produktion.

Ur ett chefsperspektiv är det viktiga inte exakt vilken teknisk detalj som skiljer sig. Det viktiga är att organisationen har en leveransmodell där samma IT-stöd kan bete sig olika i olika miljöer.

Det skapar flera problem:

- Testresultat blir mindre pålitliga.
- Produktionssättning kräver mer handpåläggning.
- Felsökning blir personberoende.
- Ansvar blir otydligt: var felet i koden, miljön, installationen, dokumentationen eller överlämningen?
- Ledtiden från färdig ändring till fungerande produktion ökar.

Containrar försöker minska just den typen av variation.

## Vad är en container?

En **container** är en isolerad körmiljö där en applikation kan köras tillsammans med de beroenden den behöver.

Ett enklare sätt att säga det:

> En container är ett standardiserat paket för att köra ett IT-stöd på ett mer förutsägbart sätt.

Paketet innehåller inte hela servern. Det innehåller det som behövs för att applikationen ska kunna starta och fungera på ett kontrollerat sätt. Containern körs ovanpå en teknisk plattform som tillhandahåller grundläggande resurser som processor, minne, nätverk och lagring.

För en chef är tre saker särskilt viktiga:

1. **Containern gör körningen mer upprepningsbar.**  
   Samma paketering kan användas i flera miljöer.

2. **Containern gör ansvar tydligare.**  
   Det blir lättare att fråga: vem ansvarar för att applikationen är korrekt paketerad och körbar?

3. **Containern flyttar fokus från installation till leverans.**  
   I stället för att manuellt installera ett system i varje miljö kan organisationen bygga ett paket som sedan körs på ett standardiserat sätt.

## En analogi: instruktion, paket och servering

Tänk dig en myndighetsrestaurang som ska servera samma lunch på flera orter. Ett traditionellt arbetssätt kan vara att varje ort får ett recept och sedan tolkar det lokalt. Resultatet blir beroende av lokala råvaror, lokala köksrutiner och kockarnas erfarenhet.

En containerliknande modell är mer som ett förberett måltidspaket: ingredienserna är samlade, instruktionerna är tydliga och paketet är gjort för att tillagas på samma sätt på olika platser.

Det betyder inte att allt blir automatiskt perfekt. Köket behöver fortfarande fungera. Det måste finnas el, hygien, utrustning och personal. Men variationen minskar eftersom mer av det viktiga följer med paketet.

På samma sätt betyder containerteknik inte att organisationen slipper plattform, säkerhet, övervakning eller ansvar. Men den minskar beroendet av att varje miljö byggs upp manuellt på exakt rätt sätt.

## Applikation, image och container

För att kunna styra containerbaserade leveranser behöver chefer förstå tre ord.

### Applikation

**Applikationen** är själva IT-stödet eller den del av IT-stödet som ska köras. Det kan vara en webbtjänst, ett API, en batchfunktion eller en annan komponent.

Applikationen är det verksamheten oftast bryr sig om: fungerar tjänsten, hanteras ärenden, kan användare logga in, går informationen att hämta?

### Image

En **image** är en paketerad mall. Den innehåller applikationen och de delar som behövs för att kunna starta den som en container.

Man kan tänka på en image som ett godkänt paket eller en fryst version. När organisationen säger “det här är version 2.4.1 av tjänsten” bör det gå att koppla den versionen till en specifik image.

Image är därför viktig för spårbarhet:

- Vilken version byggdes?
- När byggdes den?
- Från vilken kod?
- Med vilka beroenden?
- Har den testats?
- Är den godkänd att köras?

Vi kommer tillbaka till images, registries och spårbarhet i kapitel 5. Här räcker det att förstå att imagen är mallen eller paketet.

### Container

En **container** är en körande instans av en image.

Om imagen är paketet är containern det som faktiskt körs.

Samma image kan startas flera gånger. Då får man flera containrar som bygger på samma paketerade version. Det är en viktig skillnad mot många äldre arbetssätt där installationen i varje miljö kan bli lite olika.

## Varför containrar påverkar fler än driftorganisationen

Det är lätt att tro att containrar främst är en driftfråga. Det är begripligt, eftersom containrar handlar om hur applikationer körs. Men konsekvenserna börjar mycket tidigare i leveransflödet.

### Utveckling påverkas

Utvecklingsteam behöver tänka på hur applikationen ska paketeras, startas, konfigureras och fungera i en standardiserad körmiljö. Det räcker inte alltid att “koden fungerar på utvecklarens dator”.

Frågan blir: kan applikationen byggas och paketeras på ett sätt som organisationen kan upprepa och kontrollera?

### Test påverkas

Test blir mer värdefullt när testmiljön liknar produktionsmiljön. Om samma image kan användas genom flera steg i leveransflödet blir det lättare att lita på testresultaten.

Frågan blir: testar vi samma paketerade version som vi senare avser att köra i produktion?

### Förvaltning påverkas

Förvaltningen behöver följa inte bara funktionella ändringar utan också paketering, beroenden, tekniska versioner och livscykel. En gammal image kan innehålla gamla komponenter även om applikationen fortfarande fungerar.

Frågan blir: vem ansvarar för att paketerade versioner hålls aktuella, säkra och förvaltningsbara?

### Drift påverkas

Driften går från att installera och justera enskilda miljöer till att tillhandahålla en standardiserad plattform där containrar kan köras, övervakas och hanteras.

Frågan blir: hur skapar vi en plattform där applikationer kan köras konsekvent utan att varje produktionssättning blir ett specialfall?

## Scenario: Nordverk möter containerbegreppet

På Myndigheten Nordverk har ett viktigt ärendehanteringssystem länge varit svårt att produktionssätta. Inför varje större ändring hålls ett möte där utveckling, test, förvaltning och drift går igenom checklistor.

Alla är överens om att processen är dokumenterad. Ändå uppstår ofta frågor:

- Vilken version av systemkomponenten ligger egentligen i test?
- Är samma bibliotek installerat i produktion?
- Vem gjorde den manuella justeringen i acceptanstestmiljön?
- Behöver driftgruppen upprepa samma ändring vid produktionssättning?
- Varför uppstod felet först efter driftsättning?

En arkitekt föreslår att Nordverk ska börja paketera vissa delar av systemet som containrar. Först uppstår osäkerhet i ledningsgruppen. Är det här ännu ett tekniskt verktyg? Ska myndigheten byta hela driftmodellen? Är Kubernetes ett krav redan från början?

Efter en första genomgång blir diskussionen mer konkret. Containerteknik presenteras inte som en magisk lösning, utan som ett sätt att minska skillnader mellan miljöer och göra leveranser mer upprepningsbara.

Ledningen formulerar tre första mål:

1. Det som testas ska i högre grad vara samma paketerade version som senare körs.
2. Det ska gå att spåra vilken version som körs i varje miljö.
3. Produktionssättning ska kräva färre manuella, miljöspecifika moment.

Det är fortfarande tidigt. Nordverk har ännu inte beslutat om plattform, organisationsmodell eller leverantörskrav. Men myndigheten har börjat förstå att containerteknik handlar om styrbarhet, inte bara teknik.

## Vad containrar inte löser

Det är viktigt att inte översälja containerteknik. En container gör inte automatiskt ett IT-stöd modernt, säkert eller lättförvaltat.

Containrar löser inte i sig:

- otydligt ansvar
- bristande teststrategi
- svag informationssäkerhetsstyrning
- gamla applikationer med dålig arkitektur
- brist på kompetens
- otydliga leverantörsavtal
- avsaknad av prioritering för tekniskt underhåll

En dåligt byggd applikation kan paketeras i en container och fortfarande vara dåligt byggd. En osäker komponent kan följa med i en image. En otydlig organisation kan använda modern teknik och ändå skapa nya former av otydlighet.

Chefsfrågan är därför inte “ska vi använda containrar?” i största allmänhet. En bättre fråga är:

> Vilka problem i vårt leveransflöde ska containerteknik hjälpa oss att minska, och vilka organisatoriska beslut krävs för att det ska fungera?

## Vanliga chefsfällor

### Fälla 1: Att se containrar som enbart en driftfråga

**Varför det händer:**  
Containrar körs i tekniska miljöer, och därför hamnar frågan ofta hos drift eller infrastruktur.

**Hur man undviker det:**  
Be om en beskrivning av hela leveransflödet: utveckling, test, paketering, godkännande, produktionssättning och förvaltning. Containerteknik påverkar alla dessa delar.

### Fälla 2: Att tro att containerteknik automatiskt skapar ordning

**Varför det händer:**  
Tekniken förknippas ofta med automation, standardisering och modernisering.

**Hur man undviker det:**  
Skilj på teknisk möjlighet och faktisk styrning. Fråga vilka regler, ansvar och kontroller som ska gälla.

### Fälla 3: Att börja med produktnamn

**Varför det händer:**  
Diskussionen går snabbt till Podman, Docker, Kubernetes, OpenShift och olika molntjänster.

**Hur man undviker det:**  
Börja med målbilden: vad ska bli mer repeterbart, spårbart, säkert och förvaltningsbart? Produktval kommer senare.

### Fälla 4: Att glömma förvaltningen

**Varför det händer:**  
Containerinitiativ startar ofta i utveckling eller plattformsteam, medan förvaltning kommer in senare.

**Hur man undviker det:**  
Ställ tidigt frågan om livscykelansvar: vem uppdaterar, följer upp och avvecklar images och beroenden över tid?

## Frågor att ställa i den egna organisationen

Använd frågorna för att undersöka nuläget och förbereda dialogen med IT-ledning, arkitekter, säkerhetsfunktioner, utvecklingsteam, test, drift och leverantörer.

### Om miljöer

- Hur stora skillnader finns mellan utveckling, test och produktion?
- Vilka fel beror på miljöskillnader snarare än på verksamhetsfunktion?
- Kan vi återskapa en testmiljö på ett kontrollerat sätt?

### Om paketering

- Hur paketeras våra applikationer i dag?
- Är paketeringen dokumenterad, automatiserad och repeterbar?
- Vet vi exakt vad som ingår i en levererad version?

### Om ansvar

- Vem ansvarar för att applikationen är körbar i standardiserad miljö?
- Vem ansvarar för beroenden som följer med applikationen?
- Vem beslutar vilka paketeringssätt som är godkända?

### Om test och produktion

- Testar vi samma paketerade version som senare ska köras i produktion?
- Vilka manuella ändringar sker efter test men före produktion?
- Hur upptäcker vi om produktion avviker från det som testats?

## Snabb sammanfattning

- En container är en standardiserad körmiljö för en applikation och dess beroenden.
- En image är den paketerade mallen; en container är en körande instans av den mallen.
- Containerteknik kan minska skillnader mellan utveckling, test och produktion.
- Effekten är organisatorisk, inte bara teknisk.
- Utveckling, test, förvaltning och drift påverkas alla av hur applikationer paketeras och körs.
- Containerteknik skapar inte automatiskt styrning; styrningen måste beslutas, införas och följas upp.

## Nästa steg

I det här kapitlet har vi fokuserat på containern som paketering och körmiljö. Nästa kapitel lyfter blicken från enskilda containrar till den miljö där de ska köras.

Då går vi från frågan:

> Hur paketerar vi ett IT-stöd så att det kan köras mer förutsägbart?

till frågan:

> Hur går organisationen från att tänka i servrar till att tänka i gemensamma plattformar?
