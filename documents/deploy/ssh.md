```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Deploy - Værktøjer.
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express.
```

# SSH Via terminalen.

Vi skal have vores server på raspberri pi.

Jeg har valgt at mine projekter skal ligge på "blå", IP´en kan forandre sig, så den jeg skriver er bare fiktiv, brug den rigtige ip.

Åbn en terminal på din computer og skriv (husk den rigtige ip i dit tilfælde)

```
ssh web@192.168.1.142 
```

Vi skriver **web** fordi det er brugernavnet på alle vores Raspberry Pi´s. og vi skriver **192.168.1.142** fordi det er ip-adressen på den "blå" RP.

Du skal svare på om du stoler på den maskine du forsøger at indtage og hertil skriver du **yes** og trykker enter.

Brugernavn: **web**
Password: **web1234**

Det kan være lidt forskelligt om man bliver bedt om burgernavn og password igen - men du skal bare benytte ovenstående i alle tilfælde.

Men nu er vi inde på maskinen i konsollen vil du se noget ligende

```
Last login: Wed Sep  4 10:08:11 2024 from 192.168.0.55
web@raspberrypi:~ $ 
```

Så er vi klar til at kigge på vores filer.

De vigtigste Kommando´er

| Command           | Action     
| -------------     |:-------------:| 
| ls                | list indhold af mappe       
| ls -a             | list indhold af mappe også skjulte filer       
| cd *mappe-navn*   | Gå ind i mappe       
| cd ..             | Gå en mappe tilbage  
| touch test.txt    | opret test.txt fil  
| mkdir test        | opret test mappe 
| rm test.txt       | remove test.txt / sletter filen
| rm -r test        | slet test mappen og alt den indhold.
          
Derudover er det

```
git clone [dit repositoire]
```
## Oprette din projekt mappe.

Lad os starte med at skrive 

```
ls
```

og trukke enter nu vil du få liste alle filer i "home" mappen på en raspberry pi. Det vil se nogen lunde sådan ud.

```javascript
Bookshelf  Desktop  Documents  Downloads  Music  Pictures  Public  Templates  thinclient_drives  Videos  Web
web@raspberrypi:~ $
```

Som du kan se har vi en række mapper. Vi er kun interreseret i "Web" mappen.

Så vi skriver :

```javascript
cd Web
```

og derefter 

```javascript
ls
```

For lige at se hvad der er i Web mappen.

```javascript
www
web@raspberrypi:~/Web $
```

Den indeholder bare en "www" mappe så den hopper vi ind i

```javascript
cd www
```

og derefter 

```javascript
ls
```

Her kan resultatet være forskelligt men du skulle gerne kunne se en mappe der hedder "iot-projects" gå ind i denne mappe og list (ls) indholdet.

Dette er projekt mappen og her skal du oprette en mappe med dit alias.

Skriv 

```
mkdir [DIT-ALIAS]
```

Feks `mkdir mcandersc` vil oprette en mappe med navnet mcandersc.

Skriv nu `ls` og se din nye mappe og derefter `cd DinNyeMappe`.

Nu har du en tom mappe og du er klar til at oprette to nye mapper i denne mappe.

Opret en `client` og en `server` mappe.

Da vi starter med serveren skriver du `cd server`.

Nu står vi i en tom server mappe og dt vil se nogenlunde således ud

```javascript
web@raspberrypi:~/Web/www/iot-projects/mcandersc/server $
```

## Server Mappen.

Nu skal vi have clonet vores server ned i denne mappe.

```
git clone [dit https link til repositoriet fra github]
```

Her efter skal vi som på vores egen maskine installer node_modules.

```
npm install
```

Nu mangler vi to vigtige filer som ikke ligger på vores github. `.env` og `.env.local`

Den kunne se sådan ud:
```
SERVER_PORT=3042
SERVER_HOST=http://localhost:3042
ARDUINO_PORT='COM10'
```

Vi skal have oprettet to filer med vores .env indhold. vi benytter localhost fordi nu er "raspberry-pi" vores localhost. Men vi skal have en ny **PORT**.

I terminalen skriv:

```
pm2 list
```

Nu vil du se en liste med "applikationer" alle med et port navn

```
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 2  │ Monitor:3043       │ fork     │ 0    │ online    │ 0%       │ 61.5mb   │
│ 4  │ mathias-c:3050     │ fork     │ 16   │ online    │ 0%       │ 25.5mb   │
│ 5  │ mathias-s:3051     │ fork     │ 2    │ online    │ 0%       │ 68.9mb   │
```

Her vil det være oplagt at du vælger port 3060 og 61 eller 40, 41 til din server og client. Men det kan godt være vi lige skal snakke sammen på tværs hvis andre er igang samtidigt - vi kan være maks 4 på hver arduino. Jeg vælger her 60, 61 til client og server.

Så min env data ser nu sådan ud
```
SERVER_PORT=3061
SERVER_HOST=http://localhost:3061
ARDUINO_PORT='/dev/ttyACM1'
```

Bemærk porten til min Arduino. Dette er ikke længere "COM10" nu er vi på en raspberry-os og portene har andre navne. 

:bulb:**HER!** - bliver det lidt *tricky*. Vi har jo flere arduinos på samme Raspberry Pi så vi skal finde ud af hvilket nummer din Arduino sidder på. Prøv som hovedregle at se hvor mange der sidder i allerede `/dev/ttyACM0`, `/dev/ttyACM1`, `/dev/ttyACM2`, `/dev/ttyACM3`

**MEN** Det kan stadig drille, så *kald på assistance*, så kan vi være fælles om *ikke* at forstå hvorfor.

Nu skal vi have oprettet de to filer og lagt indholdet ind.

Skriv følgende for at oprette `.env` filen.

```
touch .env
```

og skriv

```
touch .env.local
```

så har du oprettet de to env filer. Kopier nu dit env indhold så du kan *paste* det ind i dokumenterne.

skriv
```
nano .env
```

Nu åbner der en "mikro editor" i din terminal og du kan med pile taster navigere dig rundt.

Paste nu (ctrl+v) env data´en ind og tryk (ctrl+s) og (ctrl+x) for at gemme og afslutte.

Skriv

```
cat .env
```

For at se om indholdet af filen er korrekt. `cat` kommandoen benyttes til at læse en fil med.

Hvis det er godt så gentag denne procedure for .env.local filen.

## Så er vi på plads og klar til at prøve at starte vores server.

Vi tester ved at skrive

```
node index
```

I terminalen vil du se noget ligende, hvis alt går godt.

```
1725465608854 Connected /dev/ttyACM1

---------------------
Starter Server -> development localhost:3061

---------------------
Serveren lytter på port 3061
1725465610562 Repl Initialized
```

Så køre din server på følgende adresse

```
http://192.168.1.142:3061
```

Husk denne IP er bare fiktiv benyt den rigtige. 

Nu kan du teste om din Arduino og backend og klient stadig snakker sammen ved at benytte din lokale klient på din mac/pc men nu med den nye server adresse i dine .env filer. Gør det.!

Hvis alt er godt har du hu via SSH oprettet en server på en "computer" i "skyen".

Det sidste du skal gøre i forbindelse med dette, er at tilføje denne applikation, til vores manager så vi kan se dig i listen. Men først stop din server med `ctrl+c`.

Herefter skriv, men udskif mit alias med dit og porten med din port.
```
pm2 start index.js --name mcandersc-s:3061
```

Nu kan du se din applikation i listen med en grøn status af "online" så skriver du 

```
pm2 save
```

Nu vil serveren starte selvom vi slukker og tænder vores raspberry pi.


Nu er det tid til en bette pause men vi bliver i terminalen lidt endnu. Du kan godt lukke den og bare huske hvordan man logger ind på den igen med `ssh bruger-navn@ip-adresse`


## Klienten og en lille smule mere i terminalen.

Og *lige nu* tag fat i McAndersC.




