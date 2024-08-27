```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Arduino.
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express.
```

## Introduktion.

I faget IOT skal vi stifte bekendskab med hvordan "ting" har adgang til internettet og kan reagere ved et klik eller en sensor der registrere at lyset er slukket. 

For at få en forståelse for "elektronikken" i nogle af de dismer vi omgiver os med så arbejder vi med Arduino.

https://www.arduino.cc/en/about
*Arduino designs, manufactures, and supports electronic devices and software, allowing people around the world to easily access advanced technologies that interact with the physical world. Our products are straightforward, simple, and powerful, ready to satisfy users’ needs from students to makers and all the way to professional developers.* 

Man kan tilgå det at lære en "breadboard" og alt om modstand, på flere måder. 

Vi starter på software måden ved først at bruge "ThinkerCad" - "ThinkerCad" er meget mere en bare circut boards og arduinos men jeg linker til det senere i dette dokument. Dette program er stærk til at afprøve sine forsøg inden man rent faktisk tager et fysisk board og indsætter ledninger og dioder. 

Der er kun to *obligatoriske*  opgaver i ThinkerCad i skal udføre, men brug gerne mere tid til at lave flere - der er en ret sjov måde at lære lidt om elektronik, og så er det let at tilpasse og ødelægge uden omkostninger.

Når vi har lavet de opgaver skal vi have fat i et fysisk Arduino BreabBoard og installere lidt software.
Herefter kommer der en række opgaver som lære os at benytte et fysisk board med Arduino ID´et.

Så lad os starte med 'ThinkerCad'.

## 1. ThinkerCad
Det kræver en konto, brug elev mail, herefter skal i finde de to "tutorial" under dette link.
https://www.tinkercad.com/learn/overview/OPRHCXXL20FZS3N?collectionId=O0K87SQL1W5N4P2&type=circuits

Gennemfør.
 
 1. Introducing the Breadboard
 2. Multiple LEDs & Breadboards
 3. Lav gerne flere.

Færdig med "ThinkerCad" for nu, men hold den klar så vi kan se at har gennemført de to tutorials.

## 2. Arduino og Arduino IDE.

1. Installér Arduino IDE.
https://www.arduino.cc/en/software

Tilslut Arduino til din computer og vælg 'tools/ports' i Ardiuno IDE´et og sæt den til den port hvor der står (arduino uno).

Vælg nu `file/examples/01.Basics/Blink` i Ardiuno IDE´et, denne `sketch` skal uploades til arduino´en.
Læg mærke til at der i `sketchen` er et link til tilhørende dokumentation.

Jeg har linket til de to `boards` i skal lave.

Så man laver et board efter anvisninger og uploader `sketchen`, rækkefølgen er lidt underordnet.
Programmet i `sketchen`vil køre indtil du overskriver med en anden `sketch`.

### Udfør
1. Blink.
https://docs.arduino.cc/built-in-examples/basics/Blink/
Når du har lavet dit board som ovenstående link så vil led lyset blinke, hvis du har uploadet din `blink` sketch.

2. Lav "Digital Read Serial" i 01.Basic.
https://docs.arduino.cc/built-in-examples/basics/DigitalReadSerial/ 
Når du har lavet dit board som ovenstående link så vil du via `tools/serial monitor` i Ardiuno IDE´et kunne se det, *stream* der kommer fra output 2. Når du trykke og holder knappen nede får du udelukkende `0` retur - dette viser os, at vi kan kontrollere hvad der skal ske når vi trykker på en knap.

3. Nu er det valgfrit, ikke om du skal lave noget men, vælg en af de sketches du kan finde via `file/examples` i Ardiuno IDE´et. og prøv gerne at arbejde med en sensor.

Nu har du fået en forståelse for hvad det handler om. Vi har muligheden for at manipulere strøm og dermed tænde og slukke systemer og sågar aflæse sensore via `serial monitor`.