# Wat is Physical Computing?

## Inleiding
% bron: https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4889676

Bij physical computing draait het om computersystemen die gebruik maken van sensoren (om iets waar te nemen) en actuatoren (om iets in gang te zetten). Een relatief simpel voorbeeld is de thermostaat die je in de meeste huizen vindt. De thermostaat meet de temperatuur met één of meerdere temperatuursensoren in huis. Als de temperatuur te laag is, zet het systeem de verwarming aan. De verwarming is een actuator.

Ook een sporthorloge hoort bij physical computing. Een veel complexer systeem is een zelfrijdende auto. Of een robotchirurg. En zo zijn er duizenden toepassingen. In de volgende paragrafen geven we nog enkele voorbeelden van physical computing. Bepaal samen met je docent welke voorbeelden je gaat bekijken.

In de rest van de module zul je natuurlijk ook allerlei toepassingen vinden van physical computing.

```{exercise} Opdracht: verken een toepassing van physical computing en bereid een presentatie voor
:label: opdracht1verken

Je merkt al, het aantal toepassingen van physical computing is onzettend groot. Voor deze opdracht werk je in twee- of drietallen. Kies samen een toepassing binnen physical computing. Bedenk eerst binnen welk domein je gaat zoeken:

- Zorg
- Transport / vervoer / mobiliteit
- Kunst
- Veiligheid
- Comfort in en om het huis
- Sport
- ...

Kies samen één toepassing en verken deze toepassing. Zoek zelf naar informatie. Bereid vervolgens een presentatie voor waarin jullie een review geven van de toepassing. Ga in ieder geval in op de volgende vragen:

- Wat kun je er mee?
- Hoe werkt het?
- Welke sensoren en actuatoren worden gebruikt?
- Wat zijn beperkingen van het systeem? Wanneer werkt het niet of niet goed?
- Wat kost het?
```

## Voorbeeld: Robotchirurg
% bron: https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4855421
% Cobots verwijderd, want die link zit nu achter een paywall

Bekijk de twee video’s in het volgende artikel over robotchirurgie.

[Opereren met robots gaat grote vlucht nemen](https://www.1limburg.nl/opereren-met-robots-gaat-grote-vlucht-nemen)

```{exercise} Robotchirurg
:label: opdracht1chirurgie
1. Welke sensoren en actuatoren heeft de robot die in het filmpje over robotchirurgie wordt gebruikt?
2. Wat zijn de uitdagingen in de verdere ontwikkeling van deze chirurgie-robots?
3. Vergelijk mensen en computers/robots met elkaar als het gaat om het chirurgie. Waar zijn mensen op dit moment beter in en waar zijn robots/computers beter in?
```

## Voorbeeld: Stofzuigerrobot
% bron : https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4855424

Een stofzuigerrobot maakt je kamer schoon terwijl je zelf op school zit of aan het werk bent. Er zijn diverse stofzuigerrobots verkrijgbaar. In het filmpje hieronder zie je een korte review van de iRobot Roomba 980. Deze stofzuigerrobot is in staat te bepalen of er een object in de weg staat. Als de stofzuiger naar beneden dreigt te vallen, bijvoorbeeld van de trap, draait hij zich om. Hij laadt zichzelf op bij het basisstation.

iRobot Roomba 980 review

```{exercise} Stofzuigerrobot
:label: opdracht1stofzuiger
1. Beschrijf de sensoren van deze stofzuigerrobot (de iRobot Roomba 980)
2. Actuatoren zijn onderdelen die een robot in staat stelt de wereld om zich heen te beïnvloeden of de robot te laten bewegen. Welke actuatoren heeft deze stofzuigerrobot?
````

```{solution} opdracht1stofzuiger
:class: dropdown
**Uitleg**

1) In ieder geval:

Objectsensor om te bepalen of er een object of muur voor de robot is.
Afstandssensor om de afstand tot de grond te bepalen, zodat een 'afgrond' kan worden gedetecteerd. In het filmpje wordt gesproken over een camera.
Batterijstatussensor, om te bepalen of de stofzuiger moet worden opgeladen.
Hier niet genoemd is het vermogen van de stofzuiger om te bepalen of er meer of minder stof ligt. Het is niet helemaal duidelijk hoe dat werkt.
Verder is het goed mogelijk dat de stofzuiger meet welke afstand steeds wordt afgelegd (bijvoorbeeld door het aantal omwentelingen van de wielen te meten).
Sommige stofzuigersrobots kunnen ook meten wat de afstand tot de muur is om een inschatting te maken van de grootte van de ruimte.
Daarnaast, voor de gebruikersinterface gebruikt de robot Wifi, en er zitten ook enkele knopjes op de robot zelf om deze aan te sturen.
Op How Stuff Works (zie: https://electronics.howstuffworks.com/gadgets/home/robotic-vacuum1.htm) staan foto's van de boven- en onderkant van een (verouderde) Roomba. Daar zie je onder meer een bumper die detecteert als de robot ergens tegenaan rijdt.

2) In ieder geval:

Twee motoren, één voor elk van de wielen
Een motor voor de stofzuiger
Eén of twee motoren voor de borstels aan de onderkant
```

## Voorbeeld: Weerstation
% bron: https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4855426

Hieronder zie je de display en overige onderdelen van een uitgebreid weerstation.


```{figure} 2-weerstation.png
```

```{exercise} Weerstation
:label: opdracht1weerstation
Bekijk de afbeeldingen van het weerstation zorgvuldig en geef aan wat voor sensoren dit weerstation gebruikt. Geef ook aan waarvoor het weerstation deze sensoren gebruikt.
```

```{solution} opdracht1weerstation
:class: dropdown
**Uitleg**
- Luchtdruksensor/Barometer (luchtdruk)
- Lichtsensor (UV en lichtsterkte)
- 2 x Temperatuursensor/thermometer (binnen / buiten)
- 2 x Luchtvochtigheidsmeter/hygrometer (binnen / buiten)
- Windsnelheid-sensor/anemometer (windsnelheid)
- Windrichting-sensor
- Regensensor
```

## Voorbeeld: Exoskelet
% bron: https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4855427

Studenten van de TU-Delft werken aan de ontwikkeling van een exoskelet, de March II. Een exoskelet maakt het mogelijk voor mensen met een dwarslaesie om te kunnen lopen. 

Bekijk het filmpje, de website van project MARCH en lees eventueel het artikel.
```{iframe} https://www.youtube.com/embed/Bsr-42pyRIs
:width:100%
Cybathlon Aftermovie 2018 - Project MARCH
```

[Project MARCH](https://www.projectmarch.nl/)

[Dwarslaesiepatiënt zet eerste stappen met exoskelet van studenten](https://tweakers.net/nieuws/129067/dwarslaesiepatient-zet-eerste-stappen-met-exoskelet-van-studenten.html)

```{exercise} Exo-skelet
:label: opdracht1skelet
Beschrijf welke ontwikkeling(en) het tegenwoordig mogelijk maken om een dergelijk exoskelet te kunnen bouwen.
```

```{solution} opdracht1skelet
:class: dropdown
**Uitleg**

Een belangrijke ontwikkeling hier is de kwaliteit van de accu, de motoren en het materiaal. Bijvoorbeeld: hoe lichter de accu, hoe makkelijker het is om een dergelijk skelet te bouwen. Echter, de accu moet wel voldoende vermogen kunnen leveren. Iets soortgelijks geldt voor de motoren (de actuatoren): hoe kleiner de motor, hoe beter. Tegelijk moeten ze wel sterk genoeg zijn. De kosten van dergelijke onderdelen en materialen spelen ook een rol.

Verder wordt het exoskelet aangestuurd door software. Die bepaalde op basis van de bewegingen van de persoon in het exoskelet, met behulp van sensoren, wat er moet gebeuren. Deze software wordt steeds beter doordat teams zoals de studenten van de TU Delft, steeds beter worden om deze software te maken.
```

## Zintuigen en sensoren
% TODO: fix de linkjes, want die in het SLO materiaal zijn gebroken
% TODO: dit gaat alleen over sensoren, er zouden ook een paragraaf over actuatoren in moeten

Hier komt ooit nog wat, je mag het nu overslaan.

## Onderdelen physical computing
% bron https://maken.wikiwijs.nl/135425/Physical_Computing___Inleiding#!page-4855368

Physical Computing gaat altijd over systemen die via sensoren en actuatoren met de wereld eromheen interacteren.

```{figure} 2-onderdelen.png
Onderdelen physical computing: sensoren, actuatoren en regelaar 
```

Neem bijvoorbeeld een systeem dat automatisch een plant water geeft. Het systeem meet hoe vochtig de aarde is. Als de aarde te droog wordt, zal het systeem met behulp van een pompje water toevoegen.

- De omgeving is de plant en de aarde waar de plant in staat.
- Het systeem bestaat uit een sensor voor het meten van de vochtigheid van de aarde, en misschien een lichtsensor om te meten hoeveel licht de plant ontvangt.
- De waterpomp om de plant water te kunnen geven is een actuator.
- De regelaar zelf bestaat onder meer uit een kleine computer en de bijbehorende software.

Die kleine computer is vaak een microcontroller. Zo'n microcontroller bevat een processor, geheugen en aansluitingen om sensoren en actuatoren op te kunnen aansluiten. Een microcontroller is meestal veel kleiner en goedkoper dan een PC of laptop. Ook gebruikt zo'n microcontroller minder energie. Meestal zit er geen beeldscherm en toetsenbord of muis bij. In deze module gebruiken we bijvoorbeeld een Micro:bit, Arduino of Lego Mindstorms als microcontroller.

Met de software kun je bepalen wat het gedrag van het systeem moet zijn. Bijvoorbeeld: hoe vochtig mag de aarde nog zijn voordat de waterpomp wordt aangezet?

Daarnaast is er vaak ook een gebruikersinterface waarmee iemand het systeem kan aansturen en informatie vanuit het systeem krijgt. Deze interface kan bestaan uit een schermpje waarop de status van het systeem is te zien: is het systeem actief? Hoe vochtig is de aarde? Hoeveel water is er tot nu toe aan de plant gegeven? En wellicht kun je met knopjes of een touchscreen het systeem bedienen (aan- en uitzetten bijvoorbeeld).

```{exercise} Wasmachine
:label: opdracht1wasmachine
Beschrijf voor een wasmachine: de omgeving, de sensoren, de actuatoren, de regelaar en de gebruikersinterface.
```

```{solution} opdracht1wasmachine
:class: dropdown
**Uitleg**
- De omgeving bestaat uit de wastrommel met daarin de was en de waterkraan.
- Sensoren voor het meten van de temperatuur van het water, de hoeveelheid water in de trommel, het gewicht van de was, etc.
- Actuatoren zoals een motor om de trommel te laten draaien, een verwarmingselement om het water op te warmen, een pomp, het slot op de deur, etc
- De regelaar bestaat uit een microcontroller en de software die daarop is geïnstalleerd.
- De gebruikersinterface bestaat uit het bedieningspaneel waarmee de gebruiker de wasmachine kan bedienen en kan zien wat de status is (Is de was klaar? Is er een storing? etc).
``