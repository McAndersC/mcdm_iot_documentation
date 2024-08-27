```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Node og Johnny-five
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express.
```

## Introduktion.

Nu skal vi tale med vores Arduino fra NodeJS. Det åbner for en række muligheder som for f.eks. at sende data via en server og at tænde og slukke lamper via et interface.

### Men vi starter simpelt.

Man kan sagten lege med dette derhjemme og i vrikeligheden købe sig fattig i sensorer. Og derhjemme og i andre situationer der kan et lille node program være nok. Så lad os start der.

Vi benytter et *node_module* der hedder `johnny-five`. (*jhonny-five er en reference til en gammel film "Short Circuit" hvori der er en robot med serie numme 5, ref: https://en.wikipedia.org/wiki/Short_Circuit_(1986_film)).

Johnny-five Modul:
https://www.npmjs.com/package/johnny-five

Vi benytter dokumentationen fra:
https://johnny-five.io/ og https://github.com/rwaldron/johnny-five/wiki/Getting-Started.

Da vi ønsker at forsøge at holde os til **ES6** javascript så har jeg lavet en lille "getting started".

:bulb: Så husk når i læser dokumentationen på https://www.npmjs.com/package/johnny-five, at noget af koden er lidt *gammel-dags*. Det kan være lidt en udfordring. Så det er også okey at arbejdet med deres eksempler, bare husk at vi tilføjer *"type" : "module"* til vores *package.json* så vi kan benyye * imports* og ikke * require *(commonjs)*. 


### Start med en Arduino.

1. Lav et *Blink* breadboard.
https://docs.arduino.cc/built-in-examples/basics/Blink/

:bulb: Test at alt virker ved at uploade *Blink* sketchen til din Arduino.

Nu skal vi styre vores Arduino fra Node så vi skal uploade en ny firmware sktech til vores Arduino.

Vælg `File / Examples / Firmata / StandardFirmataPlus` sketchen og upload denne til din Arduino.

Nu vil din LED på Arduino´en ikke lyse længere og du kan lukke Arduino IDE´et.

### IOT Projekt(er)
Nu skal du oprette en projekt mappe til vores IOT projekter/opgaver.

I den mappe opretter vi en arduino_node mappe, til denne opgave, og deri en index.js fil.

Forslået struktur.
```
├─> iot
│   ├─> arduino_node
│   │   ├── index.js
```

Åbn `arduino_node` mappen i VisualCode.

Nu har vi et helt nyt projekt, så vi starter med at åbne vores terminal og skrive er kommando for at få vores package.json fil og have adgang til node_modules.

```
npm init -y
```

Nu er er der oprettet en standard `package.json` fil. 

Åbn `package.json` filen og tilføj følgende:

```
"description": "",
"type": "module", <-- Tilføj dette imellem description og main.
"main": "index.js",
```

Nu har vi fortalt vores compiler at vi benytte ES6 *imports* og ikke CommonJS *require*. Vi kunne også omdøbe vores filer til .mjs og dermed fortælle at disse benytter **m**odule som type. 

Ideén med denne lille aplikation er at vi lære hvordan *johnny-five* og *arduino* taler sammen.

Nu kan vi installere *johnny-five* (https://johnny-five.io/) modulet

```
npm install johnny-five
```

Når vi kigger på https://johnny-five.io/examples/ siden så kan vi se et "hello-world" eksempel. Her benyttes *CommonJS* og derfor omskriver vi det til **ES6** således.

```javascript
import five from 'johnny-five';

const board = new five.Board(
    { port : 'COM8' }
);

board.on("ready", () => {

    // Arduino Board Is Ready
    board.info("Board", "Ready");

    let led = new five.Led(13);
    led.blink(500);
    
})
```

Læg godt mærke til `{port : 'COM8'}` - denne port skal svare til den port din Arduino tilgår. Du kan se det enten via `device manager/enhedshåndtering` eller via Arduino IDE `Tools/Port`.

Kig godt på scriptet. Hvad forventer vi?

Lad os afvikle vores script.

Skriv i terminalen:
```
node index
```

Terminale skulle gerne skrive noget ala:

```js
1724535541317 Connected COM8
1724535542998 Repl Initialized
>> Arduino Board Is Ready!
```

Og din :bulb: -> blinker,  overraskende :)

Så *"lidt"* skal der til. Nu kan vi sende kommandoer og modtage fra vores Arduino til og fra node.

```javascript
let led = new five.Led(13);
led.blink(500);
```

Herover opretter vi en variable til at holde på output Led 13.
Her efter sender vi en indbygget kommando 'blink' og fortælle det skal ske med 500ms mellemrum.

Så i stedet for at *uploade* en sketch med et færdigt program kan vi nu lave forskellige "aktioner".

Men lad os kigge lidt på hvad vi mere kan med vores Led.

Læs på denne side, https://johnny-five.io/api/led/ scroll ned til https://johnny-five.io/api/led/#api

Her kan i se at man kan kalde forskellige metoder.

lad os prøve med en timeout at slukke for vores blink efter 5 sekunder, vi benytte jhonny-five "wait" tilføj uden at slette noget:


```javascript
// --- 

// LED
let led = new five.Led(13);
led.blink(500);

// Board Timeout
board.wait(5000, () => {
    board.info("Led", "Stopped blinking");
    led.stop();
    led.off();
});

// --- 
```

:dart: Prøv at få lampen til at blinke og "fade ud" efter 5 sekunder. Læg mærke til at din *Led* ikke nødvendigvis altid er 13. Kig godt på dokumentationen `new five.Led(11)` så skal du flytte din *wire*/ledning.

:bulb: Brug https://johnny-five.io/examples/ siden og kig under LED i venstre side her finder du f.eks. https://johnny-five.io/examples/led-fade/ og den viser også hvordan du (fuldtændig hovedløst) bare smækker led pære direkte i boardet :).

Det er ok til test i denne øvelse men så snart du gerne vil have to ting i sving begynder det at blive problematisk. 
Du sidder heldigvis med en rigtig udgave så du flytte ledningen fra 13 til 11 hvis du benytter fade.

:dart: Opgave.

1. Sæt nu to led lys på dit board.
2. Forbind dem til Led, 9 og 10.
3. Lav en sekvens der skiftevis tænder og slukker de to lamper.

:dart: Opgave.

Lav en eller flere af:

* https://johnny-five.io/examples/photoresistor/
* https://johnny-five.io/examples/potentiometer/
* https://johnny-five.io/examples/led-rgb-anode/

Eller find selv en af de mange eksempler : https://johnny-five.io/examples/


Få en knap til at udskrive i node consollen.


