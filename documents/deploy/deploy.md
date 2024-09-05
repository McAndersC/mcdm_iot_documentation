```
Ophav       :   WEB - Viborg Media College.
Fag         :   IOT - Internet of  things.
Emne        :   Deploy - Værktøjer.
Omfavner    :   javascript, html, css, http sockets, Arduino, ReactJS, api, Serverside og ClientSide, Express.
```

Nu skal vi have vores client og vores server ud af vores local miljø og over på raspberry pi´s.

Vi gør dette for at lære tre virkelig brugbare værktøjer og i læsre at gøre det på den manuelle måde.
Det er klart at man i mange tilfælde vil benytte Git-Actions, Vercel eller andre tjenester til at  "git-push" er alt der skal til.

Men det giver mening at kendskab til disse værktøjer alligevel. Der er f.eks ikke lige en git-push til simply.com - det kan man så lave via github actions men man kan også bare uploade sine filer med FTP.

Det er alt sammen afhæmgig af opgaves art, hvor mange arbejder på projektet - har vi live, preview og dev server osv. 

I mange tilfælde kan en ftp og ssh adgang spare dig for en masse besvær - og har du købt en viruel maskine på nettet så kan man i mange tilfælde styre den med remote desktop - altså fjern skrivebord.

# Tungen lige i munden.

Vi har 2 projekter.

En **server** og en **klient**.

Vi starter med vores server så kan vi stadig teste den med vores lokale klient.

1. Din server skal være på github i public tilstand. Vi skal bruge http linket så vi kan klone den på raspbarry pi.

2. Det kan være en fordel at flytte sin PORT værdi ud i .env filerne. Prøv at kigge på hvordan *SERVER_PORT* i .en filen bliver benyttet så kunne du lave en ARDUINO_PORT i din .env/..env.local fil og benytte den i scriptet der tilgår Arduino.

Så skal vi finde en Raspberry Pi IP adresse.

NB: Lige nu har vi to maskiner vi kan ligge det på den "blå" og den "røde" vælg en hvor der ikke sidder for mange Arduinos til, fordel jer. Kig på skærmen *(her kommer et link)* og notér IP adressen.

# SSH

[Vi starter med SSH via terminalen](ssh.md).


