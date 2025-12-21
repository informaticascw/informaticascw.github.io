# Codespaces

## Begrippen

Codespace
: is een tijdelijke computer bij Microsoft waar je code kunt wijzigen en uitvoeren via je browser.

VS Code
: is een uitgebreide editor die gebruikt wordt in de codespace, het is de gebruikersinterface van de codespace.

GitHub
: is een website waar je code kunt bewaren en delen.

Repository
: is een map in GitHub met alle code van één project.

## Starten met een project in een codespace

Je start met een project. Daarvoor moet je een codespace met startcode maken. Volg de stappen hieronder.

### Maak een account in GitHub
1. Ga naar https://www.github.com/ (gebruik bij voorkeur Chrome).
2. Klik op sign-up.
3. Gebruik je email adres van school.
4. Kies een wachtwoord dat je terug kunt vinden.
5. Kies als username je voornaam met de eerste letter van je achternaam, als die al bezet is voeg je een nummer toe. Bijvoorbeeld jamesb007
6. Bevestig je account door te klikken op de link in de mail die je ontvangt van GitHub.

### Maak een codespace met startcode voor je opdracht
1. De docent deelt een link naar GitHub Classroom waarmee jij je kunt inschrijven voor een opdracht. Na inschrijven krijg je automatisch een repository met startcode voor de opdracht. 
2. Als je in een groepje werkt dan maakt het eerste groepslid die zich inschrijft een team aan. De naam van dat team bestaat uit alle voornamen van de groepsleden gescheiden door een streepje. Bijvoorbeeld anne-jasmin-noah. De andere groepsleden joinen bij inschrijven het team dat is aangemaakt.
3. Je maakt je eigen codespace door op de knop "Create Codespace te klikken". Alle bestanden uit de GitHub repository worden gekopieerd naar jouw codespace. Dit kan enkele minuten duren.

## Werken aan je project in een codespace

Elke les gebruik je je codespace om aan je project te werken. Je volgt steeds de stappen hieronder.

### Codespace starten

Als je een Codespace start, dan zie je het scherm van VS Code in je browser.


```{figure} ../10-help/vscode.png
:label: vscode
:alt: Schermafdruk van VS Code
:align: center
Schermafdruk van VS Code met de volgende onderdelen:
- (A) Activity Bar, klik op het bovenste icoon (Explorer) om je mappen en bestanden te zien, klik op het derde icoon (Source Control) van boven om te werken met GitHub
- (C) Editor Groups, hier verschijnen de bestanden die je opent.
- (D) Panel, hierin zit onder andere de Terminal. De terminal geeft toegang tot de virtuele computer, je kunt er commando's intypen.
```

### Code wijzigen
1. Dubbelklik op een bestand, bijvoorbeeld `index.html` of `main.py`. Het bestand wordt geopend in de editor. 
2. Je kunt nu het bestand aanpassen.

### Code uitvoeren
Het hangt van de programmeertaal af hoe je kunt bekijken wat je code voor resultaat geeft. In het `README.md` bestand van de startcode staat beschreven hoe dit moet. Voor een aantal veelgebruikte programmeertalen vind je hier een korte samenvattig

#### html:
1. Start een webserver in de Codespace, bij de meeste startcode gebeurt dit automatisch als je de Codespace start. De webserver zorgt ervoor dat de html-bestanden uit de Codespace door een browser op je computer kunne worden geladen.
2. Open een browser-venster met het `index.html` bestand uit je Codespace. Klik hiervoor op Ports, klik daarna op de link met het adres van de webserver.

#### python:
1. Type in de terminal `python main.py`, het programma start<br>
2. Als het programma lang duurt, stop het dan met de toetsen `[CRTL]+[C]`
3. Start het programma opnieuw met de toets `[PIJL OMHOOG]`<br>

#### python met pygame:
1. Type in de terminal `python main.py`, het programma start<br>
2. Open een browser-venster dat is verbonden met het grafische scherm (GUI) van je codespace. Klik hiervoor op Ports, klik daarna op de link met het adres van de GUI.

### Wijzigingen bewaren
1. Klik in de activity bar op het Source Control icoon.
2. Voer een beschrijving van de wijziging in
3. Druk op de groen knop "Commit & Sync". Je wijzigingen worden nu bewaard in GitHub. Je kunt controleren op github.com of het is gelukt.

### Samenwerken

```{figure} ../10-help/samenwerken.png
:label: codespace
:alt: Schematische weergave van samenwerken in Codespaces
:align: center
Schematische weergave van samenwerken in Codespaces
```

#### Jouw wijzigingen opslaan
Klik in je codespace op "Commit & Sync" om je wijzigingen op te slaan:
- Bestanden die door jouw maatje gewijzigd zijn worden van GitHub naar jouw codespace gekopieerd
- Bestanden die jij hebt gewijzigd worden van jouw codespace naar GitHub gekopieerd. 
- Als jij en je maatje in hetzelfde bestand wijzigingen hebben gedaan, dan wordt de laatste versie (jouw bestand) bewaard.

#### Wijzigingen van jou en je maatje samenvoegen
Wijzigingen van je maatje die jij hebt overschreven kun je terughalen:
- Klik in de activity bar op het Source Control icoon.
- Klik onder GRAPH op de wijziging van je maatje, de lijst met bestanden die je maatje veranderd heeft verschijnen
- Klik bij het bestand waarvan je wijzigingen wilt herstellen op het icoontje links van de M, het bestand opent (als je rode en groene regels ziet dan heb je op de naam van het bestand geklikt in plaats van het icoontje)
- Knip en plak de wijzigingen uit de versie van je maatje naar de versie van jou
- Sla je wijzigingen op in GitHub met "Commit & Sync"

```{attention}
:class: dropdown
## Opmerkingen voor ervaren git-gebruikers
Ben je een ervaren git-gebruiker? Lees dan deze paragraaf waarin wordt uitgelegd welke aanpassingen aan de instellingen van git zijn gemaakt in de configuratie van de codespaces die voor projecten worden gebruikt.

Commit & Sync
: De "Commit & Sync" knop doet vier dingen met één klik: Stage all changes, Commit, Pull en Push

Merge (en Pull)
: Bij pull en merge wordt gekeken per bestand (dus niet per regel). De versie van het laatste gewijzigde bestand (ours) wordt bewaard. Op deze manier ontstaan geen merge-conflicten, dat maakt het werken met git voor leerlingen een stuk eenvoudiger. Deze manier van werken is niet heel git-like, maar het zorgt ervoor dat leerlingen altijd hun werk snel kunnen opslaan. Parallele commits van teamgenoten die daarbij mogelijk worden overschreven, kunnen weer hersteld worden door gewijzigde delen code te knippen uit de oude versie en te plakken in de nieuwe versie.

Branches
: Gemiddelde projecten van leerlingen zijn tientallen uren. In de praktijk blijkt dat dat zonder branches goed werkt. Als je met groepen van vier of meer personen werkt aan projecten van meer dan honderd uur, dan kun je het gebruik van branches overwegen.
```

## Veelgestelde vragen

### Werken met codespaces en repositories

```{tip} Hoe open ik mijn laatste Codespace?
:class: dropdown
1. Open GitHub en login.
2. Klik op de drie streepjes links bovenin. Een menu opent.
3. Klik in het menu op Codespaces. Er wordt een lijst al je Codespaces getoond
4. Klik op de Codespace die je wilt openen. Het openen duurt één a twee minuten.
```

```{tip} Hoe maak ik een nieuwe Codespace?
:class: dropdown
1. Open GitHub en login. Ga naar je repository.
2. Klik op de groen knop "Code", een popup menu verschijnt.
3. Kies het tabje "Codespaces" in het menu.
4. Klik op de groen knop "Create Codespace" (die zie je als je nog geen Codespace van deze repository hebt), klik op "+" als je die knop er niet is.
5. De nieuwe Codespace wordt gemaakt en al je code uit GitHub wordt naar de Codespace gekopieerd. Dit duurt één a twee minuten.
```

```{tip} Waar staat mijn repository?
:class: dropdown
1. Open GitHub en login
2. Links in het scherm staan de repo's die je recent en vaak gebruikt hebt. Door op een repo te klikken wordt deze geladen. De link van de repo staat bovenin je browser.
3. Als je in een team aan een repo werkt, klik dan links op het team, daarna bovenin je scherm op repositories
```

```{tip} Lijst met commits bekijken
:class: dropdown
1. Open GitHub, ga naar de pagina met je repository.
2. Een lijst met de laatste wijzigingen krijg je door te klikken op het aantal commits, onder de groene knop met "Code". Van elke commit kun je zien wat er is gewijzigd, klik daarvoor op het nummer van de commit aan het einde van de regel.
```

```{tip} Oude versie van je repository bekijken
:class: dropdown
1. Open GitHub, ga naar de pagina met je repository.
2. Een lijst met de laatste wijzigingen krijg je door te klikken op het aantal commits, onder de groene knop met "Code". 
3. Klik op `<>` achter een commit naar keuze. Je ziet nu de versie van de repository op het moment van de commit.
```
### Werken met hestanden en mappen

```{tip} Bestanden bekijken
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Als je dubbelklikt op een bestand, dan wordt het geopend. 
4. Als je met je rechtermuisknop op een bestand of map klikt, dan verschijnt er een drop-down menu waarin je meer met het bestand of de map kunt doen.
```

```{tip} Nieuw bestand of map maken
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Als je muis op de lijst met bestanden staat, dan zie je vlak boven de lijst twee icoontjes met een +. Als je op de linker klikt, dan maak je een nieuw bestand. Als je op de rechter klikt, dan maak je een nieuwe map.
```

```{tip} Naam van bestand of map wijzigen
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Klik met de rechtmuisknop op een bestand of map. Er verschijnt een drop-down menu. Kies "Rename..." in het pull-down menu. Pas de naam aan en druk op Enter.
```

```{tip} Bestanden verplaatsen
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Sleep het bestand van de ene naar de andere map.
```

```{tip} Bestand uploaden naar Codespaces
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Sleep een bestand van je bureaublad naar het lijstje bestanden in Codespaces.<br>
Als stap 3 niet werkt, probeer dan stap 4.
4. Ga op een map staan, klik op de rechtermuisknop, een pull-down menu verschijnt, kies "Upload..." in het pull-down menu.
```

```{tip} Bestand downloaden uit Codespaces
:class: dropdown
1. Open Codespaces.
2. In de kolom met iconen links op je scherm zie je bovenaan een icoontje met twee velletjes papier. Klik daarop. Je ziet nu een lijst met al je bestanden en mappen. Mappen kun je uitklappen. 
3. Ga op een bestand staan, klik op de rechtermuisknop, een pull-down menu verschijnt, kies "Download..." in het pull-down menu.
```

```{tip} Alle bestanden downloaden
:class: dropdown
1. Open GitHub, ga naar de pagina met je repository.
2. Klik op de groene knop "Code" en kies in het menu dat verschijnt voor "Download ZIP".
3. Dubbelklik op het gedownloade zip-bestand om alle bestanden uit te pakken.
```

### Versiebeheer en samenwerken

```{tip} Oude wijzigingen terughalen
:class: dropdown

*Er zijn oude wijzigingen overschreven, hoe kan ik die terug halen?*

- Open je Codespace
- Klik in de activity bar op het Source Control icoon.
- Klik onder GRAPH op een oude versie, de lijst met bestanden die in die versie gewijzigd zijn verschijnt
- Klik bij het bestand waarvan je wijzigingen wilt herstellen op het icoontje links van de M, het bestand opent (als je rode en groene regels ziet dan heb je op de naam van het bestand geklikt in plaats van het icoontje)
- Knip de wijzigingen uit de oude versie en plak ze in de laatste versie 
- Sla je wijzigingen in de laatste versie op met "Commit & Sync"
```

```{tip} Merge conflict oplossen
:class: dropdown

*Ik heb een merge conflict, hoe los ik dat op?*

Kijk deze video, daarin wordt uitgelegd hoe je een merge conflict in Codespaces oplost.<br>
[https://www.youtube.com/watch?v=HosPml1qkrg](https://www.youtube.com/watch?v=HosPml1qkrg)

Als je er met de video niet uitkomt en er is niemand in de buurt die je kan helpen, dan kun je het volgende doen.
- Maak een nieuwe Codespace. In de nieuwe Codespace wordt de laatste versie van de code van GitHub ingelezen. 
- Knip en plak de wijzigingen van je oude Codespace naar je nieuwe Codespace. 
- Test of je code het doet, haal de fouten eruit. 
- Bewaar je wijzigingen in GitHub door in je nieuwe Codespace op Commit en Sync te klikken.
```

```{tip} Scherm delen
:class: dropdown
*Ik wil mijn scherm delen met iemand anders, hoe doe ik dat?*

In de iconenbalk links op je scherm zie een soort gebogen pijl. Dit is de extension "live-share". Hiermee kun je je scherm delen met andere GitHub gebruikers. 

Deze functie is bedoeld om samen snel een klein probleem op te lossen. Gebruik hem niet meer dan een paar minuten per les. Echte programmeurs verdelen het werk, maken elk hun eigen stuk code in hun eigen Codespace en delen het dan via GitHub. Dat moet jij ook leren.
```

### Overige vragen en problemen

```{tip} GitHub 404 fout oplossen
:class: dropdown

*Ik heb via email een link ontvangen om toegang te krijgen tot een repo, maar als ik op de link druk dan krijg ik een 404 fout. Wat moet ik doen?*

Login op GitHub en druk daarna nogmaals op de link.
```

```{tip} Automatisch inspringen
:class: dropdown

1. Open een bestand in VS Code
2. Klik in het bestand op de rechtermuisknop. Er verschijnt een pop-up menu.
3. Klik in het menu op Format Document. Het document wordt aangepast zodat de code netjes inspringt.
```

```{tip} Hoeveel gratis usage heb ik nog?
:class: dropdown
Per maand krijg je gratis usage voor allerlei dingen, de belangrijkste voor jou zijn:
- Aantal repositories in GitHub: onbeperkt
- Hoeveelheid opslag in GitHub: onbeperkt
- Aantal uren gebruik van Codespaces: 60 per maand (bij de standaard configuratie met 2 vCPU)
- Hoeveelheid opslag gemiddeld per maand in Codespaces: 15 GB (één Codespace neemt 1 à 2 GB in beslag)

Je kunt zien hoeveel usage je nog hebt op:
[https://github.com/settings/billing/summary](https://github.com/settings/billing/summary)

Om onnodige usage te voorkomen is GitHub als volgt ingesteld:
- Een Codespace die je een half uur open hebt staan zonder dat je erin werkt wordt automatisch gesloten (niet gewist).
- Een Codespace die je twee weken niet opent wordt automatische gewist.
```

```{tip} Mijn gratis usage is op
:class: dropdown
Je kunt 3 dingen doen:
- Een tweede account aanmaken, je docent kan dat account toeveogen als collaborator aan de repo waarin je werkte.
- Bijbetalen, dit is vooral handig voor docenten. Je moet een creditcard invoeren en kunt een maximum bedrag per maand instellen.
- Verder werken in een lokaal geïnstalleerde VS Code met Docker, hiervoor heb je een PC of laptop nodig en moet je handig zijn met VS Code en Docker.
```

### Documentatie

```{seealso} Documentatie over VS Code
:class: dropdown
- [https://code.visualstudio.com/docs/getstarted/userinterface](https://code.visualstudio.com/docs/getstarted/userinterface)
```
