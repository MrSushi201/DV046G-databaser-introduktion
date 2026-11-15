# Lektion 2

## Inledning

Den vanligaste tolkningen är att en databas baserad på relationsmodellen består av relationer (tabeller) och relationerna (sambanden) mellan data i olika tabeller.
En annan tolkning är att en relationsdatabas måste stödja jämförelseoperatorer som "större än" och "mindre än". 
Både dessa tolkningar är felaktiga.

## Relationsmodellen

Relationsmodellen beskrevs första gången 1970 av Edward F. Codd i hans artikel "A Relational Model of Data for Large Shared Data Banks".
Codd arbetade vid IBM på deras forskningslaboratorium i San Jose, Kalifornien.

Relationsmodellen är ett sätt att se på data, ett slags recept för hur man representera data och hur man manipulera denna representation.
Modellen bygger på matematiska begrepp, som utgör den teoretiska grunden för att skapa relationsdatabaser.

I relationsmodellen talar man om tre huvudsakliga delar:

- Datastruktur
- Dataintegritet
- Datamanipulation

Dessa delar beskriver hur data ska organiseras, hur integriteten av data ska säkerställas samt olika metoder för att manipulera data.

## Datastruktur

Grundkonceptet i relationsdatabaser är relationen.
Ordet relation har här en matematisk betydelse som är relaterad till matematiska mängder.
En mängd är en samling datavärden som kan vara enkla eller komplexa värden.
Inget av värdena får förekomma mer än en gång i mängden, och värdena är inte ordnade på något särskilt sätt.

Vi kan beskriva en relation på följande sätt:

- En relation (tabell) består av datatyper, ett huvud och en kropp
- Huvudet består av ett begränsat antal attribut (kolumner). Till varje attribut knyts en domän med tillåtna värden. Antalet attribut och dess domän ändras normalt inte med tiden
- Kroppen består av ett antal tupler (rader) där både innehållet och antalet kan variera med tiden. Varje tupel i en relation representerar ett samband mellan en mängd värden
- Varje cell i en tupel ges värden av en bestämd datatyp. Datatypen anger vilken domän dessa värden tillhör. Några vanliga domäner i en relationsdatabas är:
  - Tal, text, datum, flagga
    - Ett tal kan vara ett heltal eller flyttal. Flyttal används vid beräkningar av stora tal elelr små tal med många decimaler
    - Text har antingen en obestämd längd (varchar) eller består av ett visst antal tecken (char). Det är vanligt att ange det maximala antalet tecken för en text
    - En flagga har värdet "ja" eller "nej" (True/False). Till exempel kan vi ha ett attribut som anger om en student är registrerad på heltiddstudier eller inte

På många sätt påminner en relation en vanlig tabell som består av kolumner och rader.
Men ordet tabell är egentligen inte tillräckligt bra att använda ur ett teoretiskt perspektiv.
En tabell har nämligen ingen exakt matematisk definition och dessutom har en relation också några andra egenskaper som en tabell inte har.
Det finns inga tupler som är lika, tupler och attribut är inte ordnade på något särskilt sätt och alla attributvärden är icke sammansatta värden-

### Inga tupler är lika

En mängd (matematisk) innehåller per definition inga dubbletter.
En mämngd består av ett antal element (som inte behöver vara tal utan kan vara vad som helst).
En mängd M som innehåller talen 1, 2, 3 skriver man: M = {1, 2, 3}.
Om vi nu skulle lägga till talet 3 till mängden M så innehåller M fortfarande bara tre tal, {3, 1, 2, 3} = {1, 2, 3}.
Eftersom kroppen av en relation definieras som en mängd av tupler kommer det därför aldrig att existera tupler med samma innehåll.
En viktig konsekvens av detta är att en relation alltid har en unik primärnyckel för varje tupel (mer om detta senare).

### Tupler och attribut är inte ordnade

I en matematisk mängd spelar det ingen roll i vilken ordning man skriver elementen.
Mängden M = {1, 2, 3} är samman som mängden {3, 1, 2}.
Tupler och attribut i en relation är därför inte heller ordnade eller sorterade på något sätt speciellt sätt (kroppen är en mängd av tupler och huvudet är en mängd av attribut).

### Alla attributvärden är icke sammansatta värden

Alla värden som hör till relationen ska vara atomära värden eller icke sammansatta värden.
Vad som egentligen menas med detta kan man se lite olika tolkningar på.
Ett atomärt värde i en databas är ett värde som man betraktar som odelbart, och inte delar upp eller titar på delar av.
Ett namn som "Bertil Andersson" kan vi säga är delbart.
Ett namn består av ett för- och efternamn, och vi kan vara intresserad av att titta på dessa delar var för sig.
Vi bör därför dela upp namn till förnamn och efternamn.

Andra menar på att det räcker att se ett atomärt värde som exakt ett värde, aldrig en uppsättning eller mängd av värden.
Det vill säga att i ett attribut kan vi lagra ett namn "Bertil Andersson", men aldrig flera namn samtidigt som "Bertil Andersson, Sara Svensson".
En relation som uppfyller detta krav anses vara normaliserad.

### Dataintegritet

Integritetsvillkor består av regler som garanterar att databasen alltid existerar som en oskadad enhet.
Med detta menas att databasen till exempel inte innehåller motstridiga uppgifter (en anställds lön lagras på två ställen med två olika värden).
I en relationsdatabas finns framför allt två vanliga typer av integritetsvillkor:

- Entitetsintegritet (primärnycklar)
- Referensintegritet (främmande nycklar)

Dessa är generella regler som betraktas som meta-regler, det vill säga regler om att det måste finnas regler.
Utöver dessa generella regler kommer det även att finnas mer specifika regler, som representerar så kallade verksamhetsregler.
Det kan vara en regel om att en anställd måste ha en e-postadress eller att en avdelning identifieras med tre bokstäver.

### Entitetsintegritet

Entitetsintegritet innebär att inget attribut i basrelationens primärnyckel kan vara null (sakna värde).
En basrelation är en relation som inte sammanställts med hjälp av andra relationer utan är den relation som faktskt innehåller den data som lagras i databasen.
För att förstå vad denna regel egentligen betyder behöver vi veta lite mer om nycklar.

#### Kandidatnycklar

En kandidatnyckel är ett attribut, eller en kombination av flera attribut, som alltid har ett unikt värde för varje tupel i relationen.
I en relation kan det finnas flera kandidatnycklar och utifrån dessa kandidatnycklar väljs en som relationens primärnyckel.

#### Primärnyckel

Utifrån de kandidatnycklar som identifierats i en relation väljs en som relationens primärnyckel.
Primärnycklar är avgörande för relationsmodellen eftersom de representerar den enda mekanismen att unikt identifiera varje tupel i en relation.
Entitetsintegritetsregeln kräver att inget värde som ingår i en primärnyckel får vara utan värde.
Om en del av en primärnyckel saknar värde, det vill säga innehåller NULL, betyder det att vi inte kan identifiera de olika tuplerna i en relation.
Baserat på förståelse av en databas är detta nästan självklart eftersom hela grejen med en databas är att söka efter data, och hur ska vi göra det om vi inte kan identifiera den data vi är ute efter.
Detta är även nära besläktad med den verkliga världen.
Alla entiteter (objekt) kan separeras från varandra, de har på ett eller annat sätt en unik identifiering.
På samma sätt säkerställer primärnycklar den unika identifieringen i relationsmodellen.

En kandidatnyckel får innehålla NULL, vilket som sagt en primärnyckel inte får. Av den anledningen använder vi _id som primärnyckel.

#### Alternativ nyckel

De kandidatnycklar som inte väljs som primärnyckel kallas för alternativa nycklar.
Altenativa nycklar tillåts ha NULL-värden.
När en primärnyckel valts kommer den att vara en viktig referens för en så kallad främmande nyckel.
De alternativa nycklarna ska inte användas som referens för främmande nycklar.
Date hävdar att om någon är av en annan åsikt, är det ett tecken på en dålig databasdesign.

#### Sammansatt nyckel

Väldigt ofta räcker det inte med att bara ett attribut i en primärnyckel för att unikt kunna identifiera en tupel.
Använder vi flera attribut i en primärnyckel har vi en sammansatt nyckel.
För sammansatta nycklar gäller fortfarande regeln att ingen del av nyckeln får innehålla NULL.

#### Surrogatnyckel

Ibland kan det vara svårt att finna en lämplig primärnyckel i en relation eller så består primärnyckeln av väldigt många sammansatta attribut.
I dessa fall föreslår Date en lösning där en så kallad surrogatnyckel används.
En surrogatnyckel är ett nytt attribut som lagts till i relationen och vars enda syfte är att vara unik identifierare för en tupel.

Att införa en surrogatnyckel är alla gånger inte en bra lösning.
Det som kännetecknar en surrogatnyckel är att den saknar betydelse och inte har någon anknytning till övriga attribut i relationen.
Date hävdar att surrogatnyckelns värden, förutom att vara meningslösa, ska genereras av databashanteraren själv och döljas helt från slutanvändarna.
Alla databashanterare stödjer detta genom att ha infört "räknare" som en datatyp som kan användas för ett attribut.

I en databas stöter vi ofta på ofta sammansatta nycklar i relationer på grund av referenser till andra relationer.
En sammansatt nyckel kan bestå av attribut som återfinns bland primärnycklar i andra relationer, det vill säga det finns överlappning mellan primärnyckel och främmande nycklar.
Även i sådana fall kan det vara nyttigt att införa surrogatnycklar i stället för den sammansatta primärnyckeln.
Användning av surrogatnycklar eller inte är inte en fråga om antingen - eller, utan om när.
Den person som designar databasen måste bestämma när det kan vara lämpligt att införa surrogatnycklar, och när det verkligen inte bidrar med något positivt.

### Referensintegritet

Referensintegritet säkerställer integriteten mellan relationer i en relationsdatabas med hjälp något som kallas främmande nycklar.
En relationsdatabas innehåller normalt ett stort antal olika relationer som på olika sätt relaterar till varandra, det finns samband mellan de olika relationerna i en datbas.
Det är främmande nyckelns uppgift att knyta samman de relationer som har ett samband med varandra.
Främmande nyckeln i en relation knyts till primärnyckeln i en annan relation.
En främmande nyckel utgör på så sätt "limmet" som binder samman alla data i en databas.

Regeln för referensintegritet säger att om en basrelation R2 innehåller en främmande nyckel som motsvarar primärnyckeln i en annan basrelation R1, måste varje värde i främmande nyckeln i R2 antingen återfinnas bland värdena i primärnyckeln i R1, eller vara utan värde NULL.
Med andra ord, en databas får inte innehålla främmande nycklar som inte refererar till befintliga värden i en primärnyckel.

En främmande nyckel är således ett attribut eller en kombination av attribut som refererar till en primärnyckel i en annan relation.
En grundläggande utgångspunkt för referensintegriteten är att det inte kan hänvisa till något som inte finns.
Därav att värdet i en främmande nyckel måste återfinnas bland primärnyckelns värden.
Till skillnad från en primärnyckel är det tillåtet att en främmande nyckel innehåller NULL.

### NULL-värden

Vi har tidigare nämnt NULL-värden utan att ge någon närmare förklaring på vad det innebär.
Ett NULL-värde innebär helt enkelt att ett värde saknas.
Det kan finnas olika anledningar till att ett värde saknas och NULL-värdet kan därför ha olika betydelser.

- Den vanligaste användningen av NULL är när vi inte har tillräckligt med information om det vi vill lagra. Ett attribut som i det här fallet innehåller NULL har ett värde, men det är just nu för oss okänt
- Vi använder också NULL när värdet inte existerar. Det är till exempel tillfället när utlandsstudenter saknar svenskt personnummer
- NULL används också när vi inte har några giltiga värden att lagra, när vi vet att värdet i fråga är fel
- En annan användning av NULL kan vara någon nekar till att lämna uppgifter

Dessa är de olika typerna av NULL-värden Date nämner kan finnas i en basrelation. Alla dessa sätt att få ett NULL-värde i ett attribut kan få konsekvenser för de generella integritetsvillkoren (entitets- och referensintegritet).

### Datamanipulation

Att kunna manipulera data i en databas är en mycket viktig egenskap i alla typer av databaser.
Syftet med att manipulera data är inte bara att hämta data, utan även kunna skapa relationerna och förändra befintliga data i databasen.
I relationsmodellen finns två likvärdiga metoder för att manipulera data: relationsalgebra (relational algebra) och relationskalkyl (relational calculus).

Relationsalgebra, som är procedurell, används för att lösa ett givet problem med vissa bestämda operatorer.
Där anges vilka operatorer som ska användas och i vilken ordning de olika operatorerna ska användas för att lösa det givna problemet.

Med relationskalkyl, som är deklarativ, anger vi i stället vad problemet är. Det är viktigt att notera att relationsalgebra och relatiosnkalkyl är helt likvärdiga med ett ett-till-ett-förhållande mellan uttrycken i de båda metoderna.
Det som kan uttryckas med relationsalgebra kan uttryckas i relationskalkyl, och tvärtom.

#### Relationsalgebra

I vanliga algebra använder vi tal tillsammans med operatorer som addition, subtraktion, multiplikation och division för att beräkna uttryck av olika slag.
De olika variablerna i uttrycket består av tal och resultatet av uttrycket är ett annat tal.
Detta tal kan vi i sin tur använda som en variabel i ett annat uttryck.

Relationsalgebra fungerar på samman sätt, men i stället för att räkna med tal räknar vi med relationer.
I relationsalgebra består varje variabel av en relation som appliceras på en relationsoperator.
Resultatet av ett uttryck i relationsalgebra är en ny relation.
Precis som i vanliga algebra kan denna nya relation användas som en variabel i ett nytt uttryck.

I relationsalgebran finns det nio olika uttryck kan vi använda för att manipulera en databas.
Dessa operatorer är:

- Selektion (selection)
- Projektion (projection)
- Kartesisk produkt (product)
- Union (union)
- Differens (difference)
- Omdöpning (rename)
- Snitt (intersection)
- Sammanslagning (join)
- Kvot (division)

De sex första operatorerna är så kallade primitiva operatorer.
Med hjälp av dessa oepratorer kan de tre sista operatorerna definieras.
Produkt, union, snitt och differens är vanliga mängdoperatorer (från matematiken) men med vissa justeringar för relationer.
De övriga operatorerna speciella för relationsalgebra.
En operator används på en eller två relationer och ger som sagt en ny relation som resultat.

När vi manipulerar data i en databas är det sällan relationsalgebra används direkt utan i stället använder man ett frågespråk av något slag.
SQL är det mest använda frågespråket och allt som går att uttrycka i relationsalgebran går att uttrycka i SQL.
I den här lektionen används därför SQL för att visa hur de olika operatorerna i relationsalgebran fungerar och används.
En del av SQL-frågorna blir en aning komplexa, men du behöver inte förstå de till fullo i den här lektionen.

#### Selektion

Operatorn selektion används på en relation och skapar en ny relation som endast innehåller de tupler som uppfyller ett visst villkor.

'''sql
SELECT *
FROM databas.schema.tabell
WHERE 1 = 1;
'''

I SQL är det nyckelordet WHERE som utför selektionen.

#### Projektion

Operatorn projektion används på en relation och skapar en ny relation som endast innehåller vissa utvalda attribut, överiga attribut utesluts.
För att skapa en ny relation som endast innehåller attributet kurskod skriver man följande SQL-fråga.

'''sql
SELECT attribut1
FROM databas.schema.tabell;
'''

I SQL är det nyckelordet SELECT som utför projektion.
Efter SELECT skriver vi en kommaseparerad lista med alla attribut vi vill välja ut.
För att välja ut alla attribut kan vi använda tecknet *.

#### Kartesisk produkt

Operatorn kartesisk produkt använder två relationer och skapar en ny relation där varje tupel i den första relationen kombineras med varje tupel i den andra relationen.

I SQL är det nyckelordet FROM som utför kartesisk produkt.
Efter FROM skriver vi i en kommaspearerad lista alla relationer som ska ingå i den kartesiska produkten.
Exempelvis, relationen X innehåller 4 attribut och 6 tupler, och relation Y innehåller 3 attribut och 10 tupler så kommer den nya relationen X*Y bestå av 7 (4 + 3) attribut och 60 tupler (6 x 10).

#### Union

Operatorn union används på två relationer och skapar en ny relation med tupler från de både relationerna, men där eventuella dubbletter tas bort.
De relationer union används på måste vara unionskompatibla.
Med detta menas att de både relationerna måste ha lika många attribut och att motsvarande attribut i de båda relationerna har samma domän.

'''sql
SELECT *
FROM databas.schema.tabell1
UNION
SELECT *
FORM databas.schema.tabell2;
'''

I SQL är det nyckelordet UNION som utför unionen.
Notera att den eller de tupler som finns i både relationer bara återfinns en gång i den nya relationen. Detta är givetvis självklart eftersom det i en relation inte kan finnas några tupler som är lika.

#### Snitt

Operatorn snitt (intersection) används på två relationer och skapar en ny relation med tupler som återfinns i båda dessa relationer.
Precis som för union måste relationerna snitt används på vara unionskompatibla.

'''sql
SELECT *
FROM databas.schema.tabell1
WHERE kolumn1 IN (
    SELECT kolumn1
    FROM databas.schema.tabell2
);
'''

För att åstadkomma ett med SQL använder vi en nästlad SELECT och IN.

#### Differens

Operatorn differens används även den på två unionskompatibla relationer och skapar en ny relation med tupler som återfinns i den första relationen men som inte återfinns i den andra relationen.

För att skapa en ny relation med tupler som finns i tabell1 men inte i tabell2 så skriver vi följande SQL-fråga:

'''sql
SELECT *
FROM databas.schema.tabell1
WHERE kolumn1 NOT IN (
    SELECT kolumn1
    FROM databas.schema.tabell2
);
'''

Som man ser påminner SQL-frågan väldigt mycket om SQL-frågan för snitt.
Skillnaden är att man använder NOT IN framför den inre SELECT.
Vi väljer alltså återigen ut alla kolumn1 från tabell1 och därefter väljer man ut alla tupler från tabell2 vars kolumn1 inte finns bland (NOT IN) i tabell1.

#### Omdöpning

En relation vi får som resultat av ett uttryck i relationssalgebran har inget namn.
Med operatorn omdöpning (rename) kan vi ge dessa relationer ett namn.
Det är även möjligt att ge enskilda attribut i den nya relationen nya namn med operatorn omdöpning.
I SQL används nycketordet AS för att döpa om attribut och relationer.

'''sql
SELECT
    kolumn1 AS kolumn2
FROM databas.schema.tabell1 AS tabell2;
'''

#### Kvot

Operatorn kvot är användbar för att ställa frågor som "välj alla X som har alla Y".
Operatorn används två relationer, vilka har minst ett gemensamt attribut, och väljs ut alla attribut som förekommer i första relationen men som inte finns i den andra relationen.
De tupler som kommer med i resultatet är alla tupler i första relationen som är relaterade till den andra relationen (via de gemensamma attributen).

Kvot är ganska besvärlig att förklara och den SQL-fråga vi måste skriva för att utföra kvot är väldigt komplex.

'''sql
SELECT DISTINCT t1.kolumn1
FROM databas.schema.tabell1 AS t1
WHERE NOT EXISTS (
    SELECT *
    FROM databas.schema.tabell2 AS t2
    WHERE NOT EXISTS (
        SELECT *
        FROM databas.schema.tabell3 AS t3
        WHERE t1.kolumn1 = t2.kolumn1
        AND t2.kolumn2 = t3.kolumn2
    )
);
'''

#### Join

Operatorn join skapar en ny relation genom att lägga ihop tupler från två relationer via ett gemensamt attribut (primärnyckel - främmande nyckel) där varje tupel uppfyller ett givet villkor.
Denna relationsoperator uttrycks genom tre andra relationsoperatorer: projektion (SELECT), kartesisk produkt (FROM med mer än två relationer) och selektion (WHERE).

'''sql
SELECT *
FROM databas.schema.tabell1, databas.schema.tabell2
WHERE databas.schema.tabell1.kolumn1 = databas.schema.tabell2.kolumn1;
'''

### Sammanfattning

Syftet med dessa relationsoperatorer är att skapa ett språk som kan användas för att manipulera relationer.
Det finns inget krav att alla nio operatorer ska finnas i en relationsdatabas och bara sec av de är primitiva operatorer.
De resterande kan utföras med hjälp av de primitiva operatorerna, men i praktiken är de andra tre (särskilt join) så användbara att det är meningsfullt att definiera dem som egna operatorer.

## Vad är då en relationsdatabas?

Hur kan man då veta om man har att göra med en relationsdatabas?
Codd säger att ett system är relationellt om och endast om det har åtminstone följande två egenskaper:

- Systemet måste ha databaser som består av, vad användaren kan uppfatta som, tabeller och ingenting annat än tabeller
- Det måste finnas stöd för relationsoperatorerna selektion, projektion och join

Ett annat problem för relationsdatabaser är att systemet måste klara av att optimera utförandet av relationsoperatorerna så att det blir tillräckligt effektiv.
Görs detta på ett alltför eneklt sätt riskterar prestandan att bli dålig.
Kraven på optimering är så stora att det inte är ett lätt jobb att skapa ett system som utnyttjar potentialen i relationsmodellen.
