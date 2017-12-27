

```python
# Dependencies
import requests as req
import json
import datetime
import matplotlib.pyplot as plt
from citipy import citipy 
from matplotlib.dates import DateFormatter
import openweathermapy.core as ow
import random
import sys
import math
from collections import Counter
import csv
import pandas as pd
import numpy as np
import os
import time
def pretty_print_json(obj):
    print(json.dumps(obj, indent=4, sort_keys=True))
```


```python
#getting coordinates for 600 cities
unique_cities = []
unique_city_num=0
cities=[]
while len(unique_cities) < 600:
    lat=random.uniform(-91, 91)
    lon = random.uniform(-180, 180)
    cities.append(citipy.nearest_city(lat,lon).city_name)
    for city in cities:
        if city not in unique_cities:
            unique_cities.append(city)
            unique_city_num += 1
unique_cities[9]
```




    'taolanaro'




```python
api_key = "d9574ab3601b961626f2e9c15bccdc43"
url = "http://api.openweathermap.org/data/2.5/weather?"
query_url = url + "appid=" + api_key + "&q=" 
```


```python
weather_data=[]
for city in unique_cities:
    text = "Now retrieving " + str(city)+ "" + str (query_url) + str(city)
    print(text)
    f = open("HW7retrieved_data.txt","w") #opens file with name of "test.txt"
    f.write(text)
    f.close()
    weather_response = req.get(query_url +city)
    weather_json = weather_response.json()
    weather_data.append(weather_json)
weather_data[0]
```

    Now retrieving lagoahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lagoa
    Now retrieving vuktylhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vuktyl
    Now retrieving saint-philippehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint-philippe
    Now retrieving torbayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=torbay
    Now retrieving gigmotohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gigmoto
    Now retrieving hutchinsonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hutchinson
    Now retrieving grand river south easthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=grand river south east
    Now retrieving bredasdorphttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bredasdorp
    Now retrieving flindershttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=flinders
    Now retrieving taolanarohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=taolanaro
    Now retrieving hithadhoohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hithadhoo
    Now retrieving bluffhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bluff
    Now retrieving atuonahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=atuona
    Now retrieving cazajehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cazaje
    Now retrieving matarahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=matara
    Now retrieving pacificahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pacifica
    Now retrieving kapaahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kapaa
    Now retrieving puerto ayorahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=puerto ayora
    Now retrieving inhambanehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=inhambane
    Now retrieving yellowknifehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yellowknife
    Now retrieving zarcerohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=zarcero
    Now retrieving wanakahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=wanaka
    Now retrieving samalaeuluhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=samalaeulu
    Now retrieving vainihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vaini
    Now retrieving punta arenashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=punta arenas
    Now retrieving butaritarihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=butaritari
    Now retrieving port alfredhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port alfred
    Now retrieving hilohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hilo
    Now retrieving honiarahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=honiara
    Now retrieving kaduyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kaduy
    Now retrieving louisbourghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=louisbourg
    Now retrieving tiksihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tiksi
    Now retrieving iqaluithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=iqaluit
    Now retrieving nuukhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nuuk
    Now retrieving lebuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lebu
    Now retrieving baijiantanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=baijiantan
    Now retrieving ijakihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ijaki
    Now retrieving mortkahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mortka
    Now retrieving salymhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=salym
    Now retrieving palasahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=palasa
    Now retrieving heinolahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=heinola
    Now retrieving ushuaiahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ushuaia
    Now retrieving kosonsoyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kosonsoy
    Now retrieving fortunahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=fortuna
    Now retrieving tuktoyaktukhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tuktoyaktuk
    Now retrieving preobrazheniyehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=preobrazheniye
    Now retrieving van burenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=van buren
    Now retrieving leningradskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=leningradskiy
    Now retrieving busseltonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=busselton
    Now retrieving guajara-mirimhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=guajara-mirim
    Now retrieving serenjehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=serenje
    Now retrieving hermanushttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hermanus
    Now retrieving illoqqortoormiuthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=illoqqortoormiut
    Now retrieving souillachttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=souillac
    Now retrieving mahadday weynehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mahadday weyne
    Now retrieving mataurahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mataura
    Now retrieving avaruahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=avarua
    Now retrieving snezhnogorskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=snezhnogorsk
    Now retrieving saldanhahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saldanha
    Now retrieving tolaga bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tolaga bay
    Now retrieving rosaritohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rosarito
    Now retrieving hobarthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hobart
    Now retrieving gorno-chuyskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gorno-chuyskiy
    Now retrieving terrellhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=terrell
    Now retrieving tautirahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tautira
    Now retrieving sambavahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sambava
    Now retrieving sentyabrskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sentyabrskiy
    Now retrieving shimodahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=shimoda
    Now retrieving aklavikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=aklavik
    Now retrieving port blairhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port blair
    Now retrieving loluahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lolua
    Now retrieving daruhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=daru
    Now retrieving diksonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dikson
    Now retrieving norman wellshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=norman wells
    Now retrieving rikiteahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rikitea
    Now retrieving adrarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=adrar
    Now retrieving kodiakhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kodiak
    Now retrieving iskateleyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=iskateley
    Now retrieving groningenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=groningen
    Now retrieving jaluhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=jalu
    Now retrieving georgetownhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=georgetown
    Now retrieving cidreirahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cidreira
    Now retrieving albanyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=albany
    Now retrieving castrohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=castro
    Now retrieving byron bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=byron bay
    Now retrieving duncanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=duncan
    Now retrieving santa cruz del nortehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=santa cruz del norte
    Now retrieving port huenemehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port hueneme
    Now retrieving tamandarehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tamandare
    Now retrieving comodoro rivadaviahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=comodoro rivadavia
    Now retrieving tsihombehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tsihombe
    Now retrieving kahuluihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kahului
    Now retrieving mys shmidtahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mys shmidta
    Now retrieving qaanaaqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=qaanaaq
    Now retrieving yularahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yulara
    Now retrieving narsaqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=narsaq
    Now retrieving barrowhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=barrow
    Now retrieving mount isahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mount isa
    Now retrieving lorengauhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lorengau
    Now retrieving collipullihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=collipulli
    Now retrieving ngukurrhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ngukurr
    Now retrieving salinopolishttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=salinopolis
    Now retrieving trincomaleehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=trincomalee
    Now retrieving rio gallegoshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rio gallegos
    Now retrieving seshekehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sesheke
    Now retrieving lagoshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lagos
    Now retrieving saskylakhhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saskylakh
    Now retrieving likuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=liku
    Now retrieving longyearbyenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=longyearbyen
    Now retrieving zlatoustovskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=zlatoustovsk
    Now retrieving barentsburghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=barentsburg
    Now retrieving ribeira grandehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ribeira grande
    Now retrieving cape townhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cape town
    Now retrieving havre-saint-pierrehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=havre-saint-pierre
    Now retrieving chagdahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chagda
    Now retrieving bethelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bethel
    Now retrieving sharhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=shar
    Now retrieving baykithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=baykit
    Now retrieving new norfolkhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=new norfolk
    Now retrieving sibolgahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sibolga
    Now retrieving derzhavinskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=derzhavinsk
    Now retrieving bismarckhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bismarck
    Now retrieving solnechnyyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=solnechnyy
    Now retrieving esperancehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=esperance
    Now retrieving flin flonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=flin flon
    Now retrieving cabo san lucashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cabo san lucas
    Now retrieving amdermahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=amderma
    Now retrieving manokwarihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=manokwari
    Now retrieving namibehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=namibe
    Now retrieving turahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tura
    Now retrieving druzhbahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=druzhba
    Now retrieving victoriahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=victoria
    Now retrieving san patriciohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san patricio
    Now retrieving port angeleshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port angeles
    Now retrieving rokytnehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rokytne
    Now retrieving nemurohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nemuro
    Now retrieving komsomolskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=komsomolskiy
    Now retrieving waipawahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=waipawa
    Now retrieving port elizabethhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port elizabeth
    Now retrieving bathshebahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bathsheba
    Now retrieving bengkuluhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bengkulu
    Now retrieving sabratahhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sabratah
    Now retrieving noshirohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=noshiro
    Now retrieving villa corzohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=villa corzo
    Now retrieving nazehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=naze
    Now retrieving provideniyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=provideniya
    Now retrieving camopihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=camopi
    Now retrieving port hardyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port hardy
    Now retrieving cherskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cherskiy
    Now retrieving pangnirtunghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pangnirtung
    Now retrieving jamestownhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=jamestown
    Now retrieving arraial do cabohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=arraial do cabo
    Now retrieving vestmannaeyjarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vestmannaeyjar
    Now retrieving tawkarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tawkar
    Now retrieving la rongehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=la ronge
    Now retrieving kietahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kieta
    Now retrieving severo-kurilskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=severo-kurilsk
    Now retrieving halifaxhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=halifax
    Now retrieving manacapuruhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=manacapuru
    Now retrieving les cayeshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=les cayes
    Now retrieving tasiilaqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tasiilaq
    Now retrieving goundamhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=goundam
    Now retrieving mogadishuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mogadishu
    Now retrieving matreihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=matrei
    Now retrieving attawapiskathttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=attawapiskat
    Now retrieving east londonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=east london
    Now retrieving lasahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lasa
    Now retrieving calamahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=calama
    Now retrieving bambous virieuxhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bambous virieux
    Now retrieving airaihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=airai
    Now retrieving nantuckethttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nantucket
    Now retrieving nomehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nome
    Now retrieving berlevaghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=berlevag
    Now retrieving kathahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=katha
    Now retrieving tabiaueahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tabiauea
    Now retrieving marconahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=marcona
    Now retrieving antoninyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=antoniny
    Now retrieving kruisfonteinhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kruisfontein
    Now retrieving murgabhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=murgab
    Now retrieving surhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sur
    Now retrieving talnakhhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=talnakh
    Now retrieving yuanpinghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yuanping
    Now retrieving petropavlovsk-kamchatskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=petropavlovsk-kamchatskiy
    Now retrieving kwinanahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kwinana
    Now retrieving groahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=groa
    Now retrieving nizhneyanskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nizhneyansk
    Now retrieving sitkahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sitka
    Now retrieving ulladullahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ulladulla
    Now retrieving cabedelohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cabedelo
    Now retrieving upernavikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=upernavik
    Now retrieving chazutahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chazuta
    Now retrieving rochahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rocha
    Now retrieving portlandhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=portland
    Now retrieving geraldtonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=geraldton
    Now retrieving haines junctionhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=haines junction
    Now retrieving atambuahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=atambua
    Now retrieving isangelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=isangel
    Now retrieving eurekahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=eureka
    Now retrieving mount gambierhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mount gambier
    Now retrieving nchelengehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nchelenge
    Now retrieving narasannapetahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=narasannapeta
    Now retrieving hilton head islandhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hilton head island
    Now retrieving brezovica pri ljubljanihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=brezovica pri ljubljani
    Now retrieving vaitupuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vaitupu
    Now retrieving atarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=atar
    Now retrieving mareebahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mareeba
    Now retrieving carnarvonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=carnarvon
    Now retrieving lompochttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lompoc
    Now retrieving galganihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=galgani
    Now retrieving ogahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=oga
    Now retrieving atasuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=atasu
    Now retrieving villa bruzualhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=villa bruzual
    Now retrieving gamahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gama
    Now retrieving belohahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beloha
    Now retrieving masvingohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=masvingo
    Now retrieving lithakiahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lithakia
    Now retrieving saint anthonyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint anthony
    Now retrieving ormarahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ormara
    Now retrieving thompsonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=thompson
    Now retrieving palmerhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=palmer
    Now retrieving mar del platahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mar del plata
    Now retrieving udachnyyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=udachnyy
    Now retrieving burns lakehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=burns lake
    Now retrieving sabanghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sabang
    Now retrieving magadanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=magadan
    Now retrieving krasnoselkuphttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=krasnoselkup
    Now retrieving hammerfesthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hammerfest
    Now retrieving bonavistahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bonavista
    Now retrieving dohahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=doha
    Now retrieving hamiltonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hamilton
    Now retrieving altayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=altay
    Now retrieving bulembuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bulembu
    Now retrieving lagunahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=laguna
    Now retrieving rawsonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rawson
    Now retrieving rio tubahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rio tuba
    Now retrieving guymonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=guymon
    Now retrieving muroshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=muros
    Now retrieving mrirthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mrirt
    Now retrieving katherinehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=katherine
    Now retrieving barra do garcashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=barra do garcas
    Now retrieving mocubahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mocuba
    Now retrieving waddanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=waddan
    Now retrieving quesnelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=quesnel
    Now retrieving andeneshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=andenes
    Now retrieving mnogovershinnyyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mnogovershinnyy
    Now retrieving mitsamioulihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mitsamiouli
    Now retrieving peleduyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=peleduy
    Now retrieving sao paulo de olivencahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sao paulo de olivenca
    Now retrieving gayahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gaya
    Now retrieving abonnemahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=abonnema
    Now retrieving ayapelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ayapel
    Now retrieving aukihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=auki
    Now retrieving viligilihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=viligili
    Now retrieving collegehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=college
    Now retrieving murray bridgehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=murray bridge
    Now retrieving luderitzhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=luderitz
    Now retrieving edeahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=edea
    Now retrieving saint-francoishttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint-francois
    Now retrieving hambantotahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hambantota
    Now retrieving kloulklubedhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kloulklubed
    Now retrieving batemans bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=batemans bay
    Now retrieving manavalakurichihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=manavalakurichi
    Now retrieving nesebarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nesebar
    Now retrieving rio grandehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rio grande
    Now retrieving jumlahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=jumla
    Now retrieving alofihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=alofi
    Now retrieving haapitihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=haapiti
    Now retrieving sisimiuthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sisimiut
    Now retrieving nanortalikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nanortalik
    Now retrieving ilulissathttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ilulissat
    Now retrieving alekseyevskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=alekseyevsk
    Now retrieving superiorhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=superior
    Now retrieving matahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mata
    Now retrieving khatangahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=khatanga
    Now retrieving chlorakashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chlorakas
    Now retrieving dinglehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dingle
    Now retrieving mongohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mongo
    Now retrieving pathalgaonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pathalgaon
    Now retrieving maceiohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=maceio
    Now retrieving yantalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yantal
    Now retrieving morgan cityhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=morgan city
    Now retrieving pevekhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pevek
    Now retrieving upatahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=upata
    Now retrieving lakhdenpokhyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lakhdenpokhya
    Now retrieving dwarkahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dwarka
    Now retrieving ambilobehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ambilobe
    Now retrieving podorhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=podor
    Now retrieving beyneuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beyneu
    Now retrieving kaitangatahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kaitangata
    Now retrieving yar-salehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yar-sale
    Now retrieving mersinghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mersing
    Now retrieving condehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=conde
    Now retrieving dunedinhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dunedin
    Now retrieving onegahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=onega
    Now retrieving general rocahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=general roca
    Now retrieving budhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bud
    Now retrieving leshukonskoyehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=leshukonskoye
    Now retrieving nikolskoyehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nikolskoye
    Now retrieving denpasarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=denpasar
    Now retrieving invernesshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=inverness
    Now retrieving dolbeauhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dolbeau
    Now retrieving chimoiohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chimoio
    Now retrieving vila velhahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vila velha
    Now retrieving touroshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=touros
    Now retrieving morwellhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=morwell
    Now retrieving kangaatsiaqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kangaatsiaq
    Now retrieving razdolinskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=razdolinsk
    Now retrieving tommothttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tommot
    Now retrieving bubaquehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bubaque
    Now retrieving rinconhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rincon
    Now retrieving ahiparahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ahipara
    Now retrieving braehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=brae
    Now retrieving liverpoolhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=liverpool
    Now retrieving caxitohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=caxito
    Now retrieving getahovithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=getahovit
    Now retrieving abu dhabihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=abu dhabi
    Now retrieving sassandrahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sassandra
    Now retrieving richards bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=richards bay
    Now retrieving winchesterhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=winchester
    Now retrieving torithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=torit
    Now retrieving san cristobalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san cristobal
    Now retrieving hobyohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hobyo
    Now retrieving dalvikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dalvik
    Now retrieving hildburghausenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hildburghausen
    Now retrieving khanihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=khani
    Now retrieving betare oyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=betare oya
    Now retrieving maragogihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=maragogi
    Now retrieving katsuurahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=katsuura
    Now retrieving marquettehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=marquette
    Now retrieving mahajangahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mahajanga
    Now retrieving eylhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=eyl
    Now retrieving rexburghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rexburg
    Now retrieving sergeyevkahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sergeyevka
    Now retrieving dalihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dali
    Now retrieving labuhanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=labuhan
    Now retrieving yucca valleyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yucca valley
    Now retrieving mwinilungahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mwinilunga
    Now retrieving belmontehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=belmonte
    Now retrieving kroyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kroya
    Now retrieving grotonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=groton
    Now retrieving oriximinahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=oriximina
    Now retrieving luauhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=luau
    Now retrieving tumannyyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tumannyy
    Now retrieving beredahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bereda
    Now retrieving windhoekhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=windhoek
    Now retrieving saint josephhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint joseph
    Now retrieving grindavikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=grindavik
    Now retrieving keti bandarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=keti bandar
    Now retrieving kununurrahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kununurra
    Now retrieving dangarahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dangara
    Now retrieving sherlovaya gorahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sherlovaya gora
    Now retrieving champericohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=champerico
    Now retrieving belushya gubahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=belushya guba
    Now retrieving high levelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=high level
    Now retrieving constitucionhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=constitucion
    Now retrieving matlihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=matli
    Now retrieving kavienghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kavieng
    Now retrieving palabuhanratuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=palabuhanratu
    Now retrieving chokurdakhhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chokurdakh
    Now retrieving nimbaherahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nimbahera
    Now retrieving cajatihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cajati
    Now retrieving angochehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=angoche
    Now retrieving saint-pierrehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint-pierre
    Now retrieving batticaloahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=batticaloa
    Now retrieving hollisterhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hollister
    Now retrieving tres picoshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tres picos
    Now retrieving gambahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gamba
    Now retrieving santa maria da vitoriahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=santa maria da vitoria
    Now retrieving alice springshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=alice springs
    Now retrieving mugur-aksyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mugur-aksy
    Now retrieving san rafaelhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san rafael
    Now retrieving yumenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yumen
    Now retrieving sao filipehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sao filipe
    Now retrieving maracajuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=maracaju
    Now retrieving serra talhadahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=serra talhada
    Now retrieving nadorhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nador
    Now retrieving nazarovohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nazarovo
    Now retrieving itaremahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=itarema
    Now retrieving columbushttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=columbus
    Now retrieving salalahhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=salalah
    Now retrieving katiolahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=katiola
    Now retrieving macabobonihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=macaboboni
    Now retrieving ostrovnoyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ostrovnoy
    Now retrieving marawihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=marawi
    Now retrieving moreehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=moree
    Now retrieving tabouhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tabou
    Now retrieving hasakihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hasaki
    Now retrieving almeirimhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=almeirim
    Now retrieving ginirhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ginir
    Now retrieving sandnessjoenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sandnessjoen
    Now retrieving sant feliu de guixolshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sant feliu de guixols
    Now retrieving charters towershttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=charters towers
    Now retrieving pangkalanbuunhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pangkalanbuun
    Now retrieving sinnamaryhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sinnamary
    Now retrieving santa cruzhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=santa cruz
    Now retrieving vaohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vao
    Now retrieving te anauhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=te anau
    Now retrieving kenaihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kenai
    Now retrieving northamhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=northam
    Now retrieving caravelashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=caravelas
    Now retrieving galesburghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=galesburg
    Now retrieving catamarcahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=catamarca
    Now retrieving nazashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nazas
    Now retrieving olindahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=olinda
    Now retrieving magadihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=magadi
    Now retrieving zhiganskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=zhigansk
    Now retrieving mashhadhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mashhad
    Now retrieving belyy yarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=belyy yar
    Now retrieving deputatskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=deputatskiy
    Now retrieving beidaohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beidao
    Now retrieving latahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lata
    Now retrieving broomehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=broome
    Now retrieving nouadhibouhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nouadhibou
    Now retrieving japurahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=japura
    Now retrieving praia da vitoriahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=praia da vitoria
    Now retrieving opuwohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=opuwo
    Now retrieving tahouahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tahoua
    Now retrieving bairikihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bairiki
    Now retrieving crib pointhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=crib point
    Now retrieving natalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=natal
    Now retrieving baturajahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=baturaja
    Now retrieving guerrero negrohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=guerrero negro
    Now retrieving san ramonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san ramon
    Now retrieving sempornahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=semporna
    Now retrieving felidhoohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=felidhoo
    Now retrieving mahebourghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mahebourg
    Now retrieving anadyrhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=anadyr
    Now retrieving umzimvubuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=umzimvubu
    Now retrieving beianhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beian
    Now retrieving pitiquitohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pitiquito
    Now retrieving amarante do maranhaohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=amarante do maranhao
    Now retrieving padanghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=padang
    Now retrieving kirandohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kirando
    Now retrieving da lathttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=da lat
    Now retrieving virbalishttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=virbalis
    Now retrieving mian channunhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mian channun
    Now retrieving amparaihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=amparai
    Now retrieving erattupettahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=erattupetta
    Now retrieving palmashttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=palmas
    Now retrieving phalodihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=phalodi
    Now retrieving pskenthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pskent
    Now retrieving teknafhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=teknaf
    Now retrieving tibirihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tibiri
    Now retrieving san vicentehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san vicente
    Now retrieving cedar cityhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cedar city
    Now retrieving brownsvillehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=brownsville
    Now retrieving tunduruhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tunduru
    Now retrieving piscohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=pisco
    Now retrieving nguiuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nguiu
    Now retrieving asauhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=asau
    Now retrieving lanzhouhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lanzhou
    Now retrieving clyde riverhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=clyde river
    Now retrieving ponta do solhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ponta do sol
    Now retrieving zeyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=zeya
    Now retrieving biakhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=biak
    Now retrieving timminshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=timmins
    Now retrieving dakarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=dakar
    Now retrieving roroshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=roros
    Now retrieving verkhnedneprovskiyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=verkhnedneprovskiy
    Now retrieving chibombohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chibombo
    Now retrieving cap malheureuxhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cap malheureux
    Now retrieving fayahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=faya
    Now retrieving bairnsdalehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bairnsdale
    Now retrieving kailihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kaili
    Now retrieving kuitohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kuito
    Now retrieving marsa matruhhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=marsa matruh
    Now retrieving meccahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mecca
    Now retrieving lushunkouhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lushunkou
    Now retrieving matamoroshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=matamoros
    Now retrieving taoudennihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=taoudenni
    Now retrieving san pedrohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=san pedro
    Now retrieving bagdarinhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bagdarin
    Now retrieving bongorhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bongor
    Now retrieving walvis bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=walvis bay
    Now retrieving westporthttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=westport
    Now retrieving ozinkihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ozinki
    Now retrieving ancudhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ancud
    Now retrieving srednekolymskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=srednekolymsk
    Now retrieving rettikhovkahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=rettikhovka
    Now retrieving ponta delgadahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ponta delgada
    Now retrieving semaranghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=semarang
    Now retrieving siwanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=siwan
    Now retrieving korlahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=korla
    Now retrieving strezhevoyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=strezhevoy
    Now retrieving yerbogachenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yerbogachen
    Now retrieving mbandakahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mbandaka
    Now retrieving mentokhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mentok
    Now retrieving taharahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tahara
    Now retrieving olahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ola
    Now retrieving yininghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=yining
    Now retrieving mirabadhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mirabad
    Now retrieving kalabohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kalabo
    Now retrieving sicamoushttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sicamous
    Now retrieving camargohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=camargo
    Now retrieving bogovinahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bogovina
    Now retrieving buon me thuothttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=buon me thuot
    Now retrieving praiahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=praia
    Now retrieving hofnhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hofn
    Now retrieving haskovohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=haskovo
    Now retrieving ayanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ayan
    Now retrieving skalistyyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=skalistyy
    Now retrieving tomatlanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tomatlan
    Now retrieving potamhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=potam
    Now retrieving barawehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=barawe
    Now retrieving zafrahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=zafra
    Now retrieving garowehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=garowe
    Now retrieving samanahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=samana
    Now retrieving prieskahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=prieska
    Now retrieving uribiahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=uribia
    Now retrieving lumsdenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lumsden
    Now retrieving bolungarvikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=bolungarvik
    Now retrieving qaqortoqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=qaqortoq
    Now retrieving beisfjordhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beisfjord
    Now retrieving tuataperehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tuatapere
    Now retrieving alyangulahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=alyangula
    Now retrieving kendarihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kendari
    Now retrieving nueva guineahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nueva guinea
    Now retrieving caragahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=caraga
    Now retrieving morroshttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=morros
    Now retrieving south yuba cityhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=south yuba city
    Now retrieving gbarngahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gbarnga
    Now retrieving teguldethttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=teguldet
    Now retrieving poronayskhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=poronaysk
    Now retrieving gathttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gat
    Now retrieving mbekenyerahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mbekenyera
    Now retrieving karaulhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=karaul
    Now retrieving paracuruhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=paracuru
    Now retrieving abu kamalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=abu kamal
    Now retrieving sardarpurhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sardarpur
    Now retrieving stralsundhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=stralsund
    Now retrieving chinsalihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chinsali
    Now retrieving bebotohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=beboto
    Now retrieving kutumhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kutum
    Now retrieving manahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mana
    Now retrieving sao jose da coroa grandehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sao jose da coroa grande
    Now retrieving arroyohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=arroyo
    Now retrieving khonuuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=khonuu
    Now retrieving santa vitoria do palmarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=santa vitoria do palmar
    Now retrieving panoramahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=panorama
    Now retrieving sao joao da barrahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sao joao da barra
    Now retrieving saleaulahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saleaula
    Now retrieving dokahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=doka
    Now retrieving kommunarhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kommunar
    Now retrieving tashtyphttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tashtyp
    Now retrieving son lahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=son la
    Now retrieving ternuvatehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ternuvate
    Now retrieving cabrahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=cabra
    Now retrieving adrehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=adre
    Now retrieving vilahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vila
    Now retrieving ontariohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ontario
    Now retrieving hovdhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hovd
    Now retrieving arlithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=arlit
    Now retrieving amapahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=amapa
    Now retrieving hualmayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hualmay
    Now retrieving klaksvikhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=klaksvik
    Now retrieving road townhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=road town
    Now retrieving tlahualilohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tlahualilo
    Now retrieving sechurahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sechura
    Now retrieving henties bayhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=henties bay
    Now retrieving kikwithttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kikwit
    Now retrieving kidalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=kidal
    Now retrieving afluhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=aflu
    Now retrieving gunjurhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gunjur
    Now retrieving itomanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=itoman
    Now retrieving hamihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=hami
    Now retrieving charlestownhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=charlestown
    Now retrieving ha gianghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ha giang
    Now retrieving jaenhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=jaen
    Now retrieving awjilahhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=awjilah
    Now retrieving sydneyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sydney
    Now retrieving taunggyihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=taunggyi
    Now retrieving carutaperahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=carutapera
    Now retrieving nushkihttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=nushki
    Now retrieving labuttahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=labutta
    Now retrieving vila franca do campohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=vila franca do campo
    Now retrieving la troncalhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=la troncal
    Now retrieving ternatehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ternate
    Now retrieving moronhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=moron
    Now retrieving le moulehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=le moule
    Now retrieving phu lyhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=phu ly
    Now retrieving port lincolnhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=port lincoln
    Now retrieving samusuhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=samusu
    Now retrieving chilchotlahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=chilchotla
    Now retrieving soyohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=soyo
    Now retrieving lavrentiyahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=lavrentiya
    Now retrieving semenyihhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=semenyih
    Now retrieving saint-augustinhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=saint-augustin
    Now retrieving taizhouhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=taizhou
    Now retrieving sharjahhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=sharjah
    Now retrieving ondorhaanhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ondorhaan
    Now retrieving mogochahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=mogocha
    Now retrieving maumerehttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=maumere
    Now retrieving ardatovhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ardatov
    Now retrieving alolenghttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=aloleng
    Now retrieving tubruqhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=tubruq
    Now retrieving imeni poliny osipenkohttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=imeni poliny osipenko
    Now retrieving gulshathttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=gulshat
    Now retrieving codringtonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=codrington
    Now retrieving aytonhttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ayton
    Now retrieving ballinahttp://api.openweathermap.org/data/2.5/weather?appid=d9574ab3601b961626f2e9c15bccdc43&q=ballina





    {'base': 'stations',
     'clouds': {'all': 75},
     'cod': 200,
     'coord': {'lat': 37.14, 'lon': -8.45},
     'dt': 1514354400,
     'id': 2267254,
     'main': {'humidity': 87,
      'pressure': 1017,
      'temp': 289.15,
      'temp_max': 289.15,
      'temp_min': 289.15},
     'name': 'Lagoa',
     'sys': {'country': 'PT',
      'id': 5948,
      'message': 0.004,
      'sunrise': 1514360780,
      'sunset': 1514395434,
      'type': 1},
     'visibility': 10000,
     'weather': [{'description': 'broken clouds',
       'icon': '04n',
       'id': 803,
       'main': 'Clouds'}],
     'wind': {'deg': 270, 'speed': 11.8}}




```python
weather_data[0]
```




    {'base': 'stations',
     'clouds': {'all': 75},
     'cod': 200,
     'coord': {'lat': 37.14, 'lon': -8.45},
     'dt': 1514354400,
     'id': 2267254,
     'main': {'humidity': 87,
      'pressure': 1017,
      'temp': 289.15,
      'temp_max': 289.15,
      'temp_min': 289.15},
     'name': 'Lagoa',
     'sys': {'country': 'PT',
      'id': 5948,
      'message': 0.004,
      'sunrise': 1514360780,
      'sunset': 1514395434,
      'type': 1},
     'visibility': 10000,
     'weather': [{'description': 'broken clouds',
       'icon': '04n',
       'id': 803,
       'main': 'Clouds'}],
     'wind': {'deg': 270, 'speed': 11.8}}




```python
lat=[]
lon=[]
country=[]
temp=[]
name=[]
cloud=[]
wind=[]
hum=[]
date=[]
for x in weather_data:
    if(x["cod"])!="404":
        lat.append(x["coord"]["lat"])
        lon.append(x["coord"]["lon"])
        country.append(x["sys"]["country"])
        temp.append(x["main"]["temp_max"])
        name.append(x["name"])
        cloud.append(x["clouds"]["all"])
        wind.append(x["wind"]["speed"])
        hum.append(x["main"]["humidity"])
        date.append(x["dt"])
   
        
len(lon)       
```




    533




```python
weather_df = pd.DataFrame({"Temperature (F)": temp,"Humidity (%)":hum, 
              "Cloudiness (%)":cloud, "Wind Speed (mph)":wind, 
                           "Latitude":lat, "Longitude":lon, "Date":date, 
                           "City":name,"Country":country })

weather_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness (%)</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity (%)</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Temperature (F)</th>
      <th>Wind Speed (mph)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lagoa</td>
      <td>75</td>
      <td>PT</td>
      <td>1514354400</td>
      <td>87</td>
      <td>37.14</td>
      <td>-8.45</td>
      <td>289.150</td>
      <td>11.80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Vuktyl</td>
      <td>56</td>
      <td>RU</td>
      <td>1514355308</td>
      <td>75</td>
      <td>63.86</td>
      <td>57.31</td>
      <td>258.131</td>
      <td>1.71</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Saint-Philippe</td>
      <td>1</td>
      <td>CA</td>
      <td>1514354100</td>
      <td>59</td>
      <td>45.36</td>
      <td>-73.48</td>
      <td>256.150</td>
      <td>4.31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Torbay</td>
      <td>90</td>
      <td>CA</td>
      <td>1514354400</td>
      <td>54</td>
      <td>47.66</td>
      <td>-52.73</td>
      <td>271.150</td>
      <td>17.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Gigmoto</td>
      <td>80</td>
      <td>PH</td>
      <td>1514355310</td>
      <td>100</td>
      <td>13.78</td>
      <td>124.39</td>
      <td>299.956</td>
      <td>6.76</td>
    </tr>
  </tbody>
</table>
</div>




```python
weather_df.to_csv("Weather.csv")

```


```python
def scatterplot(x_data, y_data,color, marker):
    plt.scatter(x_data, y_data, color=colors[color_index],marker=markers[marker_index])
                
colors = ['g','r','b','y']
markers=["^","s","d","o"]
color_index = 0
marker_index=0
#xlabel="Time (Days)"
scatterplot(x_data = weather_df["Latitude"]
            , y_data = weather_df['Temperature (F)']
            ,color = colors[color_index],marker=markers[marker_index])  
color_index += 1
marker_index +=1
date = time.strftime("%m/%d/%Y")
plt.title(f"City Latitude vs. Max Temp (F) {date}")
plt.xlabel("Latitude")
plt.ylabel("Max Temp (F)")
plt.legend(loc="best")
plt.grid(True, linestyle='dotted')
plt.savefig("City Latitude vs. Max Temp (F).png")

plt.show()
```


![png](output_8_0.png)



```python
def scatterplot(x_data, y_data,color, marker):
    plt.scatter(x_data, y_data, color=colors[color_index],marker=markers[marker_index])
                
colors = ['r','b','y']
markers=["s","d","o"]
color_index = 0
marker_index=0
#xlabel="Time (Days)"
scatterplot(x_data = weather_df["Latitude"]
            , y_data = weather_df['Humidity (%)']
            ,color = colors[color_index],marker=markers[marker_index])  
color_index += 1
marker_index +=1
date = time.strftime("%m/%d/%Y")
plt.title(f"City Latitude vs. Humidity (%){date}")
plt.xlabel("Latitude")
plt.ylabel("Humidity (%)")
plt.legend(loc="best")
plt.grid(True, linestyle='dotted')
plt.savefig("City Latitude vs. Humidity(%).png")

plt.show()


```


![png](output_9_0.png)



```python
def scatterplot(x_data, y_data,color, marker):
    plt.scatter(x_data, y_data, color=colors[color_index],marker=markers[marker_index])
                
colors = ['b','y']
markers=["d","o"]
color_index = 0
marker_index=0
#xlabel="Time (Days)"
scatterplot(x_data = weather_df["Latitude"]
            , y_data = weather_df['Cloudiness (%)']
            ,color = colors[color_index],marker=markers[marker_index])  
color_index += 1
marker_index +=1
date = time.strftime("%m/%d/%Y")
plt.title(f"City Latitude vs. Cloudiness  (%) {date}")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness(%)")
plt.legend(loc="best")
plt.grid(True, linestyle='dotted')
plt.savefig("City Latitude vs. Cloudiness(%).png")

plt.show()

```


![png](output_10_0.png)



```python
def scatterplot(x_data, y_data,color, marker):
    plt.scatter(x_data, y_data, color=colors[color_index],marker=markers[marker_index])
                
colors = ['y']
markers=["o"]
color_index = 0
marker_index=0
#xlabel="Time (Days)"
scatterplot(x_data = weather_df["Latitude"]
            , y_data = weather_df['Wind Speed (mph)']
            ,color = colors[color_index],marker=markers[marker_index])  
color_index += 1
marker_index +=1
date = time.strftime("%m/%d/%Y")
plt.title(f"City Latitude vs. Wind Speed (mph) {date}")
plt.xlabel("Latitude")
plt.ylabel("Wind Speed (mph)")
plt.legend(loc="best")
plt.grid(True, linestyle='dotted')
plt.savefig("City Latitude vs. Wind Speed (mph).png")

plt.show()

```


![png](output_11_0.png)

