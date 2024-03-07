# Data loggen

## Lokaal op de Raspberry Pi

Volg deze stappen
1. Data uitlezen (zonder kleuren sensor) https://projects.raspberrypi.org/en/projects/sense-hat-data-logger/1
1. Data wegschrijven naar file https://projects.raspberrypi.org/en/projects/sense-hat-data-logger/2
1. Kolommen maken in CSV https://projects.raspberrypi.org/en/projects/sense-hat-data-logger/3
1. Data loggen met vaste intervallen https://projects.raspberrypi.org/en/projects/sense-hat-data-logger/4

## Meetgegevens beschikbaar maken voor Prometheus

We gaan nu de gemeten data beschikbaar stellen in een dashboard systeem waar je grafieken kunt tekenen.

In Thonny installeer de package `prometheus-client`. (Tools -> Manage packages...)

Met de prometheus client kun je getallen beschikbaar stellen die door het dashboard systeem dat we zo gaan opzetten kunt uitlezen. Lees de documentatie (https://github.com/prometheus/client_python) en pas je programma aan om de getallen beschikbaar te stellen je kunt her het beste per meetwaarde een 'Gauge' voor anbieden in prometeus. Je moet hiervoor een 'custom collector' maken. Gebruik als naam voor de gauage de klom namen uit de csv file.

De getallen moeten er ongeveer zo uit zien in je browser
```
# HELP sense_hat Sense HAT sensor values
# TYPE sense_hat gauge
sense_hat{temp="temp"} 36.055355072021484 1709809791422
sense_hat{pres="pres"} 1027.023681640625 1709809791422
sense_hat{hum="hum"} 39.34347152709961 1709809791422
sense_hat{yaw="yaw"} 144.47365030534877 1709809791422
sense_hat{pitch="pitch"} 359.98630578420915 1709809791422
sense_hat{roll="roll"} 358.1242919560272 1709809791422
sense_hat{mag_x="mag_x"} -69.1010971069336 1709809791422
sense_hat{mag_y="mag_y"} -49.47803497314453 1709809791422
sense_hat{mag_z="mag_z"} 20.4950008392334 1709809791422
sense_hat{acc_x="acc_x"} -0.0 1709809791422
sense_hat{acc_y="acc_y"} -0.03666633740067482 1709809791422
sense_hat{acc_z="acc_z"} 0.9991570711135864 1709809791422
sense_hat{gyro_x="gyro_x"} 0.005473993718624115 1709809791422
sense_hat{gyro_y="gyro_y"} 0.0029010882135480642 1709809791422
sense_hat{gyro_z="gyro_z"} -0.004732053726911545 1709809791422
sense_hat{datetime="datetime"} 1.709809791422743e+09 1709809791422

```

## Grafana en Prometeus opzetten
[Grafana](https://grafana.com/docs/) is een tool om dashboards voor monitoring mee te maken.
[Prometheus](https://prometheus.io/) is een tool om telemetrie mee te verzamelen in een database.
[Dockcer](https://www.docker.com/) is een tool om virtuele servers binnen je computer te draaien.

Je gaar nu Prometeus en Grafana op je laptop opzetten zodat Prometeus de meetgegevens van de Raspberry Pi kan verzamelen. Vervolgens ga je in Grafana een dashboard maken die een grafiek tekent van de meetgegevens.

1. Installeer Docker desktop op je laptop. https://www.docker.com/get-started/
1. Installeer Git op je laptop. https://git-scm.com/download/win
1. Installeer Visual Studio Code op je laptop. https://code.visualstudio.com/
1. Clone deze repository naar je laptop door in de terminal op je laptop dit commando te draaien. `git clone https://github.com/erikhh/measure-sense-control.git`
1. Ga naar de directory in `cd meaure-sense-control`
1. Open deze directory in Visual Studio Code. Bestudeer alles in deze directory en probeer het te begrijpen.
1. Pas de file `prometeus/prometeus.yml` regel 12 aan zodat naar het ip address van de Raspberry PI.
1. Zorg dat je sense programma altijd automatisch opstart als de Pi opstart. https://projects.raspberrypi.org/en/projects/sense-hat-data-logger/5
1. Draai in een terminal in de `measure-sense-control` directory het commando `docker compose up`
1. Ga in een browser naar http://localhost:3000 en log in met gebruiker admin en wachtwoord grafana.
1. Klink aan de linker kan op de Explore knop.
1. Probeer eerst maar eens alles te tekenen in een lijn grafiek.
1. Draai bevoorbeeld de rapberry pi om en zie hoe de meetwaardes veranderen.
1. Probeer nu onder dashboards een dashboard te maken die temperature, humidity en pressure weer geeft.
1. Kun je een alert genereren als de temperatuur boven de 34 graden komt?
1. Je kunt de temperatuur verhogen door op de Raspberry Pi het commando `s-tui` te gebruiken.

# Tijd over

Probeer een mooie flistende en flikkerende disco vloer te maken met de lampjes
https://magpi.raspberrypi.com/articles/make-a-sense-hat-rainbow-display-for-your-window

Of een spelletje
https://projects.raspberrypi.org/en/projects/sense-hat-pong
