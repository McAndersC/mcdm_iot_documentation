```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Socket.io og Express server
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express. 
```

## Introduktion

Nu har vi fået kendskab til hvordan vi taler med en "dims" via NodJS. Der findes en væld af måder at kommunikere med "dimser" og benytte NodeJS, frem for pyhton, giver mest mening når vi vil arbejde med resultaterne via web.

Vi har også den fordel at vi beholder alt vores kodning i JavaScript og dermed lettere kan integrere det i f.eks React, Vue, Angular osv.

Så nu vender vi Arduino ryggen for en stund og skal arbejde lidt med en smule backend og frontend.

Jeg har lavet to templates som vi tager udgangspunkt i. Der er vejledning til installation i *readme.md* filerne i hver projekt - men jeg beskriver i dette dokument det væsentlige indhold i Server og Klient.

1. En server (En klasssik node/express)
Fork eller zip følgnede repositorie, læs projektets *readme.md* for installation.
!TODO indsæt link

1. En Klient/Frontend (En klasssik vite-react)
Fork eller zip følgnede repositorie, læs projektets *readme.md* for installation.
!TODO indsæt link

## Server.

Serveren er en forholdsvis standard Express Server.
Den store forskel er at vi har tilknyttet [socket.io ](https://socket.io/).

https://socket.io/docs/v4/
>What Socket.IO is
Socket.IO is a library that enables low-latency, bidirectional and event-based communication between a client and a server.

Vi har installeret 
```
npm i socket.io
```

og det giver os mulighed for at skabe en "kanal" imellem server og klient.

I `server.js` tilknytter vi io (socket.io) og åbner for crossdomain trafik. :

```javascript
const io = new Server(server,{
  cors: {
    origin: "*",
  }
});
```

Dernæst sætter vi i funktionen `server.run` følgende op:

```javascript
// Manage socket connections.
io.on('connection', (socket) => {
    
    console.log('A client connected');

    socket.on('clientMessage', (data) => {

        io.emit('post', data);

    });

});
```

1. Her lytter vi efter en Klient der kontakter vores server `io.on('connection' ...`.

2. Når en klient får en "connection" så lytter vi efter om klienten sender (emitter) en "clientMessage".

3. Hvis klienten sender en "clientMessage" så sender (emitter) serveren en "post" tilbage.

Så man benytter `emit` til at sende en `event` -> `io.emit('post', data);` - hvor "data" kan være json stringify´et.

Og man lytter ligeledes på en event `socket.on('clientMessage', (data)` med `.on` og her modtager man ligeledes data.

Det er klart at dette er et forsimplet eksempel og jeg vil anbefale at læse på socket.io dokumentationen og bruge denne server template som udgangspunkt - der er et væld af tutorials derude og problemet er ofte først at få hul igennem, det har i via denne template. Vi kommer til at lave mere med denne server senere men i denne omgang skal vi bare lade den køre og starter vores klient projekt.

## Klient

Vores klient er en "standard" (mediacollege)-vite-react template. Ikke at vi laver de store forskelle fra den oprindelige men der er tilføjet lidt struktur for at vi holder en genkendelighed.

:bulb: Sti til serveren, i `services/settings.js` filen, er der en variable til *socket-server* serveren. hvis du ikke har ændret noget burde alt være godt!.

**Start** 
Hvis du har startet serveren (socket) og klient så vil du på forsiden af klienten kunne tilføje en besked. Hvis du åbner endnu et browser vindue og skriver en besked, med et andet brugernavn - så er der gang i chatten.

Alt funktionalitet er i `SocketExample.jsx` så åbn den og kig den godt igennem og læs kommentare.

1. Prøv nu at kigge på server koden og se hvordan vi emitter en post fra vores server og modtager den i klienten.
2. Men vi emitter også fra klienten til serveren.
```javascript
socket.emit('clientMessage', JSON.stringify({
    'author' : author.value,
    'message' : message.value
}));
```

Og her sender vi et object med som indeholder navn og besked fra formen.

Vi bruger lidt primitivt, *navnet* til at gøre det unikt!.

Så rundkredsen er fuldendt når klienten har sendt en besked til serveren og serveren sender beskeden tilbage. Så putter vi beskeden i vores array og loop´er over det.

Vi modtager beskeden.
```javascript
socket.on('post', (post) => {

    post = JSON.parse(post);

    setThread(
        [
            ...thread,
            post
        ]
    )

});
```

Vi loop´er over alle beskeder vi har modtaget.

```javascript
{thread.map( (post, index) => {

    // Sætter vores style afhængig af om vi selv er Author.
    let commentStyle = post.author !== author ? iStyles.fromServer : iStyles.fromClient

    return <p key={index} className={commentStyle}><span>{post.author} skriver</span>{post.message}</p>

})}
```

Nu har vi fået forståelse for hvordan vi kan sende data via socket forbindelser. Dette er ikke lavet til store mængder data - men det giver mening i mange andre sammenhænge. Live aktie kurser, Service-Chat, spil osv.

Der findes selvfølgelig services man kan købe til dette og der findes også andre metoder. socket.io er open-source og et meget anvendt bibliotek - men som altid, så findes der professionelle løsninger som gør det let at håndtere tusindvis af brugere osv. Feks. https://www.pubnub.com/ men man kunne også benytte `firebase` databaser osv.

:dart: Opgave

1. Tilføj en mulighed for at give sin bobbel en unik farve.
2. Tilføj så sidens baggrundsfarve matcher den seneste bobbel.
2.B *frivillig* - Hvordan undgår vi at Author navnet skal være unikt

3. Jeg har ladet mig kraftigt inspirere at tale bobble design herfra: https://freefrontend.com/css-speech-bubbles/              
Lav nu dit egen komponent der udskriver beskeder løbende som f.eks. https://codepen.io/quadbaup/pen/rKOKQv eller https://codepen.io/Kosai106/pen/eZvJwY, men du bestmmer selv og du bestemmer selv omfang.

:bulb: Det åbner en massse muligheder og det er klart at vi nu kunne arbejde med at gemme vores brugere, og threads, lave individuelle chat-rum osv. osv.

Der findes en masse tutorials til dette og jeg vil anbefale at starte med at læse socket.io og bnytte deres tutorials og eksempler. Disse to templates giver muligheden for at arbejde med tutorials - med det samme!

I næste opgave arbejder vi med en ny server og en ny klient men de er bygget på samme prinzip og så tilføjer vi Arduino og benytter på Socket og Endpoints til at tale med vores Arduino.

God fornøjelse.
