

# Installation.

kilde: https://github.com/rwaldron/johnny-five/wiki/Getting-Started#prerequisites

Tjek At du hart python installeret 

I terminalen.
```
python --version
```

## Windows

1. https://visualstudio.microsoft.com/vs/community/

Installer ovenstående.

Herefter åbner vi Visual Studio Installer.
I Studio Installer vælger vi to pakke.

1. Desctop Development with c++
2. Python Development.

Genstart Maskinen.

## Mac

*I vinder denne gang og skal bare gå til næste punkt - hvis phyton er installeret.*

## Windows og Mac -> Installer i projektet

Firmata
```
npm i firmata
```

Node Gyp kan installeres globalt og dermed kun én gang.
```
npm install -g node-gyp
```

Alternativt hvis det giver problemer (*pga skrive-rettigheder*). Så kan det installeres på projektet.
```
npm install node-gyp
```

Og så skulle alt gerne være godt - husk "StandardFirmataPlus" uploadet til din Arduino.


