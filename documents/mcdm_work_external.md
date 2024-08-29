```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Arbejde Externt med Vite.
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express.
```


# Arbejde Eksternt.

For at arbejde "eksternt" skal du kende din IP-Adresse.

I en terminal skriv:

## Windows:
```
ipconfig
```

Resultat ala:
```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . : localdomain
   IPv4 Address. . . . . . . . . . . : 192.168.0.55
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Default Gateway . . . . . . . . . : 192.168.1.1
```

En lokal ip adresse vil næste altid state med 192.168 - de næste to tal afgøre din maskines placering på det interne netværk.

I mit tilfælde 192.168.0.55.

## Macbook
```
ipconfig getifaddr en0
```

Resultat:
```
192.168.0.55
```

Denne ip adresse skal vi udskitfe vores "localhost" med et par steder i projekterne.

## Client.

Åbn settings.js og øndre server adressen til din ip f.eks.

```javascript
export const serverPath = "http://192.168.0.55:3042"
```

Nu skal man huske at starte sin client med "dev extern". Enten vi NPM Scripts eller ved at skrive

```javascript
npm run "dev extern"
```

## Server

Ændre ALLE env filer så de benytter DIN IP.

F.eks.
```
# Secret Variables for use in Server Application.
NODE_ENV=development

SERVER_PORT=3042
SERVER_HOST=http://192.168.0.XX:3042
```

Så skulle du gerne have adgang fra mobilen eller andre computere på netværket.

HUSK at benytte ip adressen i browseren: 
Client -> http://192.168.0.XX:5173
Server -> http://192.168.0.XX:3042

:bulb: Husk det er **DIN IP ADRESSE** og ikke det som er her i dokumentet.