# Inlämningsuppgift 2
Du ska ta fram en modell på en databas för bostadsföretag som äger och administrerar olika bostadsrättsföreningar.
Följande data om bostadsrättsföreningarna är nödvändiga för administrationen, och ska lagras i en egen databas.

Företaget äger många bostadsrättsföreningar.
För varje bostadsrättsförening ska det finnas uppgifter om:

- Föreningens namn
- Namn
- Adress
- Antal hus
- År som föreningens bildades

Företaget har ett medlemsregister över samtliga andelsägare i bostadsrättsföreningarna.
För varje medlem registreras uppgifter om:

- Personnummer
- För- och efternamn
- Adress
- Telefonnummer

I varje bostadsrättsförening finns det MINST ett hus, men förening kan ha hur många hus som helst. För varje hus ska uppgifter om:

- Husets adress
- Antal våning
- Antal lägenhet

Varje hus innehåller i sin tur minst en lägenhet. Lägenheterna beskrivs med hjälp av:

- Antal rum
- Totalyta
- Vilken våning lägenheten finns på
- Lägenhetsnummer

En andelsägare kan bara äga en lägenhet i varje bostadsrättsförening. En lägenhet har alltid en andelsägare.

## Uppgift 1–3 – Tabeller

Bostadsrättsförening:

- id_forening, PK
- namn_forening
- adress_forening
- hus_antal
- ar_etablerat

Kandidatnycklar:
Bostadsrättsföreningens namn är troligen unikt, men det är inte garanterat.
Bostadsrättsföreningens adress är inte nödvändigtvis unik. Teoretiskt sett kan det finnas flera bostadsrättsföreningar på samma adress.

Primärnyckel:
Därför är det lämpligt att införa en surrogatnyckel som primärnyckel, därav id_forening.

Främmande nycklar:

---

Andelsägare:

- id_person, PK
- personnummer
- fornamn
- efternamn
- adress_person
- telefonnummer

Kandidatnycklar:
Personnummer är unikt och skulle därmed kunna användas som primärnyckel. Men alla har inte ett svenskt personnummer (och saknar då de fyra sista siffrorna).
Telefonnummer fungerar inte heller, eftersom alla inte har ett telefonnummer.

Primärnyckel:
Därför behövs en surrogatnyckel som primärnyckel, därav id_person.

Främmande nycklar:

---

Hus:

- id_hus, PK
- hus_adress
- vaning_antal
- lagenhet_antal
- id_forening*, FK

Kandidatnycklar:

Primärnyckel:
Utifrån uppgifterna i beskrivningen behövs ytterligare information i tabellen Hus. Därför införs surrogatnyckeln id_hus som primärnyckel.

Främmande nyckel:
Enligt beskrivningen ska ett hus alltid tillhöra en bostadsrättsförening. Därför finns id_forening med i tabellen som främmande nyckel.

---

Lägenhet:

- id_lagenhet, PK
- lagenhetsnummer
- rum_antal
- yta_total
- vaning
- id_hus*, FK
- id_forening*, FK
- id_person*, FK

Kandidatnycklar:
Lägenhetsnummer är inte nödvändigtvis unikt. Två bostadsrättsföreningar skulle kunna ha exakt samma uppsättning lägenhetsnummer (1001, 1101, 1201 osv.).

Primärnyckel:
Därför behövs en surrogatnyckel, därav id_lagenhet.

Främmande nycklar:
Utifrån uppgifterna i beskrivningen behövs följande främmande nycklar i tabellen Lägenhet: id_hus, id_forening, id_person.

---

Bostadsrättsförening - Andelsägare:

- id_forening_person, PK
- id_forening*, FK
- id_person*, FK

En bostadsrättsförening kan ha flera medlemmar (ett-till-många).

---

Bostadsrättsförening - Hus

- id_forening_hus, PK
- id_forening*, FK
- id_hus*, FK

En bostadsrättsförening kan ha flera hus (ett-till-många).

---

Hus - Lägenhet

- id_hus_lagenhet, PK
- id_hus*, FK
- id_lagenhet*, FK

Ett hus kan ha flera lägenheter (ett-till-många).

---

## Inlämning

### Uppgift 1: Tabeller

Bostadsrättsförening(föreningID, föreningNamn, föreningAdress, antalHus, etableringsÅr)

Andelsägare(ägareID, personNummer, förNamn, efterNamn, ägareAdress, ägareTelefonNummer)

Hus(husID, husAdress, antalVångningar, antalLägenheter)

Lägenhet(lägenhetID, lägenhetNummer, antalRum, totalYta, våning)

Medlemskap(föreningID, ägareID)

### Uppgift 2: Primärnycklar

Bostadsrättförening(<u>föreningID</u>, föreningNamn, föreningAdress, antalHus, etableringsÅr)

- föreningID införs som en surrogatnyckel då de ursprungliga kolumnerna inte är tillräckligt unika

Andelsägare(<u>ägareID</u>, personNummer, förNamn, efterNamn, ägareAdress, ägareTelefonNummer)

- ägareID införs som en surrogatnyckel då de ursprungliga kolumnerna inte är tillräckligt unika. Teoretiskt sett så skulle personnummer vara unikt men det förekommer personer som saknar svenskt personnummer (de 4 sista siffrorna) och då är födelsedatumet inte tillräckligt unikt

Hus(<u>husID</u>, husAdress, antalVåningar, antalLägenheter)

- husID införs som en surrogatnyckel då de ursprungliga kolumnerna inte är tillräckligt unika

Lägenhet(<u>lägenhetID</u>, lägenhetNummer, antalRum, totalYta, våning)

- lägenhetID införs som en surrogatnyckel då de ursprungliga kolumnerna inte är tillräckligt unika. Samma uppsättning av lägenhetsnummer kan förekomma i andra huas och bostadsrättsförening

Medlemskap(<u>föreningID</u>, <u>ägareID</u>)

- Både föreningID och ägareID införs för att skapa en kompositnyckel, och den är tänkt för att användas som en primärnyckel

### Uppgift 3: Främmande nyckel

Bostadsrättförening(<u>föreningID</u>, föreningNamn, föreningAdress, antalHus, etableringsÅr)

Andelsägare(<u>ägareID</u>, personNummer, förNamn, efterNamn, ägareAdress, ägareTelefonNummer)

Hus(<u>husID</u>, husAdress, antalVåningar, antalLägenheter, föreningID*)

- föreningID införs till tabellen för beskriva kopplingen mellan hus och bostadsrättsförening. Utan den så vet man inte vilken bostadsrättsförening huset tillhör
- En bostadsrättsförening kan ha flera hus (ett-till-många)

Lägenhet(<u>lägenhetID</u>, lägenhetNummer, antalRum, totalYta, våning, husID*, ägareID*)

- husID och ägareID införs till tabellen för att beskriva kopplingarna mellan lägenhet, hus, och andelsägare
- Ett hus kan ha flera lägenheter (ett-till-många)
- En lägenhet kan endast ha en andelsägare (ett-till-ett)
- En andelsägare kan ha flera lägenheter i olika föreningar men aldrig mer än en lägenhet i en förening

Medlemskap(<u>föreningID</u>*, <u>ägareID</u>\*)

- Både föreningID och ägareID är främmande nycklar från andra tabeller (Bostadsrättsförening och Andelsägare)
- En bostadsrättsförening kan ha flera ägare (ett-till-många)
- En ägare kan vara medlem i flera bostadsrättsföreningar (ett-till-många)
  - Sambandet blir därför många-till-många (sammanfattat från de två ovanstående punkterna/sambanden)
- Denna tabell beskriver ENDAST relationen mellan bostadsrättsförening och andelsägare, inte om andelsägare äger en lägenhet i en bostadsrättsförening
