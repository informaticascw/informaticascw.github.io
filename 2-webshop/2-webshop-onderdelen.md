# Webshop-onderdelen

```{pull-quote}
We beginnen met drie smurfen.
```

```{figure} scherm1.png
Schermafdruk van webshop aan het begin van dit hoofdstuk.
```
In dit hoofdstuk ga je kleine wijzigingen maken in je webshop, zoals teksten, kleuren en plaatjes aanpassen. Je maakt kennis met alle onderdelen van de webshop en leert hoe die samenwerken.

## Opdracht: Startcode voor je webshop 
In deze opdracht krijgt iedereen uit jouw groepje een ontwikkelomgeving met toegang tot de startcode. Er is één ontwikkelomgeving per persoon en één kopie van de startcode per groepje. De ontwikkelomgeving heet een **codespace**. De map met code heet een **repository**. De repository en de codespace zijn onderdeel van de **GitHub**-website.

```{attention} GitHub account
Tijdens opdracht a) wordt gevraagd om in te loggen op GitHub.

Inloggen op GitHub als je al eerder een GitHub-account op school hebt gemaakt:
: 1. Klik op **sign in**.
: 2. Gebruik je schoolmail en het wachtwoord dat je eerder voor GitHub gekozen hebt. 

Inloggen op GitHub als je nog geen GitHub-account hebt:
: 1. Klik op sign up.
: 2. Gebruik je email adres van school.
: 3. Kies een wachtwoord dat je terug kunt vinden.
: 4. Kies als username je voornaam met je leerlingnummer. Bijvoorbeeld `james112007`
: 5. Bevestig je account door te klikken op de link in de mail die je ontvangt van GitHub.
```

:::{note} Opdracht a)
### Maak een Codespace met startcode
1. De docent deelt een link naar GitHub Classroom waarmee jij je kunt inschrijven voor een opdracht. Na inschrijven krijg je automatisch een repository met startcode voor de opdracht. 
2. Als je in een groepje werkt dan maakt het eerste groepslid die zich inschrijft een team aan. De naam van dat team bestaat uit alle voornamen van de groepsleden gescheiden door een streepje. Bijvoorbeeld `anne-jasmin-noah`. De andere groepsleden joinen bij inschrijven het team dat is aangemaakt.
3. Je maakt je eigen codespace door op de knop `Create Codespace` te klikken. Alle bestanden uit de GitHub repository worden gekopieerd naar jouw codespace. Dit kan enkele minuten duren.
:::

```{hint} Tips
:class: dropdown
- Meer informatie over de ontwikkelomgeving Codespaces vind je op\
  [https://stanislas.informatica.nu/webshop/codespaces/](#webshop-codespaces)
```

:::{note} Opdracht b)
### Run de startcode 
- Start de server (database en api) van je webshop. Gebruikt daarvoor het commando `bash start.sh` in de terminal van je codespace.
- Open een client van je webshop. Klik daarvoor op de link van de webserverer. Die link staat op het tabblad ports (bij de terminal). Je kunt klikken op de wereldbol die verschijnt als je met je muis de link aanwijst. 

Als het gelukt is, dan zie je een webshop met drie smurfen.
:::

```{hint} Tips
:class: dropdown
- Bij de startcode zit een `README.md` bestand. Hierin staat hoe je code kunt starten, stoppen, wijzigingen en opslaan.
- Meer informatie over de ontwikkelomgeving Codespaces vind je op\
  [https://stanislas.informatica.nu/webshop/codespaces/](#webshop-codespaces)
```


## Uitleg: Architectuur
:::{note} Uitleg

### Onderdelen van de webshop
```{figure} 2-architecture.svg
Architectuur van de webshop
```

Als je de webshop bezoekt dan laadt de browser eerst een kale webpagina zonder producten. Daarna worden de artikelen geladen. Dat gaat zo snel, dat je het bijna niet ziet.

### Webpagina laden
Het laden van de kale webpagina gaat met de volgende stappen.
1. Je opent een browser op je client en navigeert naar de webshop.
2. De browser downloadt het index.html bestand van de server. 
3. In het index.html bestand ziet de browser dat hij de bestanden style.css en script.js moet laden.
4. De bestanden index.html en style.css bevatten de startpagina van de webshop, zonder producten. De informatie uit die bestanden wordt door de browser opgeslagen in een Document Object Model (_DOM_). De DOM staat in het geheugen van de browser en bepaalt wat de browser op het scherm toont.

### Producten laden
Het laden van de artikelen gebeurt in de volgende stappen.
1. In script.js staat een JavaScript-programma. De browser voert dat programma uit.
2. De JavaScript-code maakt via een link verbinding met de server.
3. De link is gekoppeld aan een programma op de server. Dit programma is een Application Programming Interface (_API_, spreek uit als ee-pie-aai). De API in deze webshop is geschreven in de programmeertaal Python. 
4. De API vraagt via het SQL-commando `select` informatie over artikelen op uit de database. 
5. Het antwoord van de database wordt door de API omgezet in _JSON_-formaat (spreek uit als djee-sun-formaat) en teruggestuurd naar de client waarop de browser draait. 
6. Het JavaScript-programma in de browser leest het JSON-bestand en voegt elementen toe aan de DOM. Die elementen zijn stukjes HTML met informatie over de artikelen. In die informatie zit ook een link naar het plaatje van het artikel. De browser downloadt de plaatjes en toont alle elementen die aan de DOM zijn toegevoegd op het scherm.

:::

```{seealso} REST 
Het geheel van linken, API, database en JSON dat op de server staat is een _REST_-API. De REST-API zorgt ervoor dat de JavaScript-code in de browser informatie op kan vragen over artikelen uit de webshop. De REST-API wint aan populariteit vanaf ongeveer 2010. Voor die tijd werd vaak gekozen voor een server die complete webpagina’s maakt, inclusief alle informatie over de artikelen. 

Een voordeel van REST ten opzichte van de traditionele aanpak is dat REST interactievere websites mogelijk maakt. Dat komt omdat het laden van extra informatie via een REST-API sneller gaat dan het herladen van de hele webpagina. Een ander voordeel is dat een REST-API gemakkelijk door andere programma's dan browsers gebruikt kan worden. Zo kun je bijvoorbeeld zelf een Python-programma schrijven dat gebruik maakt van de REST-interface van chatgpt. 

Je leert meer over REST in de volgende hoofdstukken.
```

## Opdracht: Je eerste wijzigingen in je webshop 
In deze opdracht ga je de eerste kleine wijzigingen maken in de startcode die je hebt gekregen.

```{attention} Onderwerpen die je kunt kiezen
Voor bezoekers van je webshop is het handig als het onderwerp duidelijk aangeeft welke artikelen je verkoopt. Je mag de smurfen uit de startcode verkopen, maar je mag ook kiezen voor andere artikelen. Om de opdrachten uit de volgende hoofdstukken goed te kunnen maken, moet je met twee dingen rekening houden.
- In hoofdstuk 4 krijgen je artikelen een merk, we gebruiken de merken Smurf Mania en Totally Smurf. Deze twee merken moeten herkenbaar blijven, maar je mag het woord Smurf aanpassen en meer merken toevoegen.
- In hoofdstuk 5 krijgen je artikelen kleuren, we gebruiken rood, geel, blauw en combinaties daarvan. Je mag meer kleuren toevoegen.
```

:::{note} Opdracht a)
### Verander het onderwerp

Start de webshop met het commando `bash start.sh` in de terminal
De webshop verschijnt op je scherm.
Bovenaan de webshoppagina staat de naam van de webshop (Smurfsjop). 

Verzin zelf een naam voor jouw webshop en pas de code aan, zodat jouw naam getoond wordt.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/index.html`.
- Zoek naar de `h1` tag
```

:::{note} Opdracht b)
### Verander de kleur

De webshop gebruikt zwarte letters op een bijna witte achtergrond en witte letters op een smurfblauwe achtergrond. 

Verander de smurfblauwe kleur in een kleur die past bij jouw webshop.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/style.css`.
```

:::{note} Opdracht c)
### Verander de artikelnamen

Bovenaan de plaatjes staan de namen van de artikelen die je verkoopt. 

Verander de namen van artikelen in artikelen die jij wilt verkopen.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/data/init.sql` en pas daar de inhoud van de juiste velden aan.
- Start de webshop opnieuw met het terminal-commando `bash start.sh`. Tijdens het starten wordt de database opnieuw gemaakt met de commando's in het bestand init.sql
```

:::{note} Opdracht d)
### Verander een plaatje

Voeg een nieuw plaatje toe en geef het een naam die past bij het artikel.
:::

```{hint} Tips
:class: dropdown
- Er is [meer uitleg over de ontwikkelomgeving Codespaces](#webshop-codespaces), daarin staat hoe je bestanden kunt uploaden. 
- De bestanden met plaatjes staan in de map `/static/images`.
- De namen van de bestanden staan in de database `/data/init.sql`.
- Na aanpassen van het bestand `/data/init.sql` moet je de database opnieuw maken met het terminal-commando `bash start.sh`.
```
