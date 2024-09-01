```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Arbejde Externt med Vite.
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express, Deploy
```


# Sidste Stint!

Denne opgave er en opsummering af vores pil igennem lagene i at tale frem og tilbage imellem enheder.

Vi tilføjer dog idenne omgang at jeres opgave skal placeres på vores Raspberry Pi´es og afvikles derfra.

Formålet er at i får erfaring med at benytte Linux til f.eks at håndtere en node server og samtidigt lære i hvordan man navigere på sådan en maskine. Både til hjemmebrug men især til at benytte skyen (cloud services) og alle dennes muligheder. Som sagt er skyen "en anden computer på internettet" som du kan have fuldstændig råderet over. 

Men du kan også "bare" købe plads på en server "Cloud Applications" og slippe (betale) for bøvlet med at håndtere en server selv.

Men det gælder altid at det hele ofte ender i en kombination. Og det handler om produkt, omfang osv osv.

Men en Raspberry Pi er en god maskine at øve/teste på - og man kan med fordel skifte sd-kort og teste vidt og bredt.

## Men først!

Vi skal have lavet en "johnny-five" kopi. Men denne skal være din egen.

Du skal lave en client og en server.

Det hele skal navngives [dit-alias]-five-['client/server'] => f.eks -> `mcandersc-five-server`, `mcandersc-five-client`

### Client

Du skal lave et interface hvor man nydeligt kan stye din "johnny". Her må du ikke kopiere designet men skal lave dit eget - det skal være brugbart på vores to touch skærme.

#### 1. Forside / Control Panel

Der må gerne være flere features og ikke alle behøver at tænde noget nyt som sådan - der må gerne være knapper der får én pære til f.eks at blinke med forskellige intervaller (1sek) (2sek). 

#### 2. Infoside

Der skal være en info side med billede(r) af, hvordan man bygger din "Arduino" hvem der har lavet den, hvordan man får det i sving. 

#### Formål
:dart: Målet er at andre skal kunne se din info side, bygge din "Johnny", og bruge dit interface til at styre den.

### Server

Du kan kopiere `johnnyfive_server` og gøre den til din egen. Du må meget gerne lave ændringer men det er også okey at benytte den som den er, især til at starte med. Men brug gerne det du lavede i opgaven `johnnyfive`.

Husk det kræver en fysisk arduino.

### Generelt

* Start med en simpel udgave som vi kan deploye og derefter udvide.
    * Få lavet dit design og struktur.
    * Brug et dummy billede osv.
    * Tænk over at andre skal kunne ituitivt kunne hoppe fra din infoskærm til dit control panel.
    * Det må gerne være split-view/dashboard.
* Du bestemmer selv opbygning af din side.
* Der skal ikke være database tilknyttet.
* Der kan komme yderligere instrukser undervejs.
* Både klient og server skal afleveres via git.
    * vi laver et fork og i kan slette dem igen hvis i ikke ønsker dem længere.
    * I kan godt holde det privat (det taler vi om).
* En uge er afsat, MEN!
    * Forvent tid til at "deploye".
    * Forvent undervisning i at "deploye".


## Prototype

Du udarbejder din prototyper af client og server på din egen maskine i første omgang.

Du skal teste din client ved at benytte:

```
npm run build
```

Det opretter en `dist` mappe i dit projekt og hvis vi skriver:

```
npm run preview
```

Så starter vi en ny server til se det optimale statiske version af din applikation.

Hver gang vi skal "deploye" vores side skal vi lave et nyt `build`.

## Deploy.

Der er både en server og en client vi skal have deployet. 

Serveren skal deployes som den er og klienten er det indholdet af dist mappen vi skal bruge.

Vi skal benytte to(tre) metoder til at tilgå vores Raspberry Pi´s.

* FTP - File Transfer Protocol, via FileZilla
* SSH - Secure Shell, via Terminal
* RDT - Remote Desktop

Vi gør dette for at få et indblik i hvordan de forskellige metoder kan benyttes. Vi gør det med Raspberry Pi´s så vi ikke behøver at være nervøse og fordi det er en fordel at kunne benytte disse metoder når man skal begå sig i skyen af services.

Dokumentationen for hvordan vi gør afventer lige lidt teknisk afklaring men det forventes at I vil release og teste jeres applikation flere gange. Men vi starter lokalt med vores egen maskine.  

### Server.

... *dokumentation på vej - afventer*

### Client.

... *dokumentation på vej - afventer* 