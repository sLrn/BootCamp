
# Analysis
Observed Trend 1 - The latitude vs. temperature plot shows that the highest temperatures are closest to the equator.
Observed Trend 2 - The latitude vs. humidity plot shows that humidity increases near the equator.
Observed Trend 3 - The data does not suggest a strong relationship between latitude and cloudiness or wind speed.


```python
import matplotlib.pyplot as plt
import openweathermapy as ow
import pandas as pd
from citipy import citipy
from pprint import pprint
from random import random
import numpy as np
import requests
import datetime
from config import api_key
```

# Generate Cities List


```python
cities = []

for x in range(0,2000):
    ran_lat = np.random.uniform(-90,90)
    ran_lng = np.random.uniform(-180,180)
    
    city = citipy.nearest_city(ran_lat,ran_lng)

    name = city.city_name
    if name not in cities:
        cities.append(name)
        
len(cities)
```




    758



# Perform API Calls


```python
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

query_url = f"{url}appid={api_key}&units={units}&q="

shortened_city_list = []
temperature = []
humidity = []
latitude = []
longitude = []
cloudiness = []
wind_speed = []
count = 1

for city in cities:
    city_with_plus = city.replace(" ","+")
    print(city_with_plus)
    response = requests.get(query_url + city_with_plus).json()
    if response['cod'] != "404":
        shortened_city_list.append(city)
        temperature.append(response["main"]["temp"])
        humidity.append(response["main"]["humidity"])
        latitude.append(response["coord"]["lat"])
        longitude.append(response["coord"]["lon"])
        cloudiness.append(response["clouds"]["all"])
        wind_speed.append(response["wind"]["speed"])
        print("Processing Record " + str(count) + " " + city + " " + query_url + city_with_plus)
        count = count + 1
```

    arraial+do+cabo
    Processing Record 1 arraial do cabo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arraial+do+cabo
    hermanus
    Processing Record 2 hermanus http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hermanus
    suruc
    Processing Record 3 suruc http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=suruc
    sarkand
    Processing Record 4 sarkand http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sarkand
    chita
    Processing Record 5 chita http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chita
    punta+arenas
    Processing Record 6 punta arenas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=punta+arenas
    hithadhoo
    Processing Record 7 hithadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hithadhoo
    yelizovo
    Processing Record 8 yelizovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yelizovo
    louisbourg
    kapaa
    Processing Record 9 kapaa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kapaa
    cape+town
    Processing Record 10 cape town http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cape+town
    saint+george
    Processing Record 11 saint george http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint+george
    baruun-urt
    Processing Record 12 baruun-urt http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baruun-urt
    ushuaia
    Processing Record 13 ushuaia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ushuaia
    tasiilaq
    Processing Record 14 tasiilaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tasiilaq
    port-gentil
    Processing Record 15 port-gentil http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port-gentil
    victoria
    Processing Record 16 victoria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=victoria
    richards+bay
    Processing Record 17 richards bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=richards+bay
    ilulissat
    Processing Record 18 ilulissat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ilulissat
    jamestown
    Processing Record 19 jamestown http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jamestown
    polewali
    Processing Record 20 polewali http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=polewali
    busselton
    Processing Record 21 busselton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=busselton
    hervey+bay
    Processing Record 22 hervey bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hervey+bay
    bac+lieu
    mahebourg
    Processing Record 23 mahebourg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mahebourg
    inegol
    palembang
    Processing Record 24 palembang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palembang
    pokrovsk
    Processing Record 25 pokrovsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pokrovsk
    hasaki
    Processing Record 26 hasaki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hasaki
    lang+suan
    Processing Record 27 lang suan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lang+suan
    airai
    Processing Record 28 airai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=airai
    mount+gambier
    Processing Record 29 mount gambier http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mount+gambier
    saint+anthony
    Processing Record 30 saint anthony http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint+anthony
    tubuala
    Processing Record 31 tubuala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tubuala
    grindavik
    Processing Record 32 grindavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grindavik
    ponta+do+sol
    Processing Record 33 ponta do sol http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ponta+do+sol
    minna
    Processing Record 34 minna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=minna
    antalaha
    Processing Record 35 antalaha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=antalaha
    saryozek
    Processing Record 36 saryozek http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saryozek
    mar+del+plata
    Processing Record 37 mar del plata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mar+del+plata
    vaini
    Processing Record 38 vaini http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vaini
    dikson
    Processing Record 39 dikson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dikson
    castro
    Processing Record 40 castro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=castro
    mataura
    Processing Record 41 mataura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mataura
    samfya
    Processing Record 42 samfya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=samfya
    vilhena
    Processing Record 43 vilhena http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vilhena
    monrovia
    Processing Record 44 monrovia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=monrovia
    khatanga
    Processing Record 45 khatanga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khatanga
    port+elizabeth
    Processing Record 46 port elizabeth http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+elizabeth
    kaitangata
    Processing Record 47 kaitangata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kaitangata
    rikitea
    Processing Record 48 rikitea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rikitea
    ixtapa
    Processing Record 49 ixtapa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ixtapa
    kodiak
    Processing Record 50 kodiak http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kodiak
    illoqqortoormiut
    attawapiskat
    bethel
    Processing Record 51 bethel http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bethel
    adrar
    Processing Record 52 adrar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=adrar
    lata
    Processing Record 53 lata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lata
    qaanaaq
    Processing Record 54 qaanaaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=qaanaaq
    avarua
    Processing Record 55 avarua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=avarua
    palabuhanratu
    taolanaro
    pevek
    Processing Record 56 pevek http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pevek
    albany
    Processing Record 57 albany http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=albany
    murgeni
    Processing Record 58 murgeni http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=murgeni
    vila+velha
    Processing Record 59 vila velha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila+velha
    rabo+de+peixe
    Processing Record 60 rabo de peixe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rabo+de+peixe
    barrow
    Processing Record 61 barrow http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barrow
    sentyabrskiy
    baudh
    Processing Record 62 baudh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baudh
    hobart
    Processing Record 63 hobart http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hobart
    tuktoyaktuk
    Processing Record 64 tuktoyaktuk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tuktoyaktuk
    birobidzhan
    Processing Record 65 birobidzhan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=birobidzhan
    east+london
    Processing Record 66 east london http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=east+london
    bredasdorp
    Processing Record 67 bredasdorp http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bredasdorp
    new+norfolk
    Processing Record 68 new norfolk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=new+norfolk
    hobyo
    Processing Record 69 hobyo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hobyo
    lebu
    Processing Record 70 lebu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lebu
    walvis+bay
    Processing Record 71 walvis bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=walvis+bay
    vila+franca+do+campo
    Processing Record 72 vila franca do campo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila+franca+do+campo
    tsihombe
    nikolskoye
    Processing Record 73 nikolskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nikolskoye
    los+llanos+de+aridane
    Processing Record 74 los llanos de aridane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=los+llanos+de+aridane
    jega
    Processing Record 75 jega http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jega
    yellowknife
    Processing Record 76 yellowknife http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yellowknife
    valdivia
    Processing Record 77 valdivia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=valdivia
    sinnamary
    Processing Record 78 sinnamary http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sinnamary
    itupiranga
    Processing Record 79 itupiranga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=itupiranga
    saint-philippe
    Processing Record 80 saint-philippe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-philippe
    yar-sale
    Processing Record 81 yar-sale http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yar-sale
    arman
    Processing Record 82 arman http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arman
    tumannyy
    leningradskiy
    Processing Record 83 leningradskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=leningradskiy
    atuona
    Processing Record 84 atuona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atuona
    payo
    Processing Record 85 payo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=payo
    marcona
    kahului
    Processing Record 86 kahului http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kahului
    san+patricio
    Processing Record 87 san patricio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+patricio
    saint-pierre
    Processing Record 88 saint-pierre http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-pierre
    belushya+guba
    sitka
    Processing Record 89 sitka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sitka
    chapais
    Processing Record 90 chapais http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chapais
    saleaula
    alofi
    Processing Record 91 alofi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alofi
    jamsa
    Processing Record 92 jamsa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jamsa
    bluff
    Processing Record 93 bluff http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bluff
    north+las+vegas
    Processing Record 94 north las vegas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=north+las+vegas
    cortez
    Processing Record 95 cortez http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cortez
    mys+shmidta
    chokurdakh
    Processing Record 96 chokurdakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chokurdakh
    vysokogornyy
    Processing Record 97 vysokogornyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vysokogornyy
    tuatapere
    Processing Record 98 tuatapere http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tuatapere
    clyde+river
    Processing Record 99 clyde river http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=clyde+river
    teneguiban
    high+rock
    Processing Record 100 high rock http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=high+rock
    bonthe
    Processing Record 101 bonthe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bonthe
    esperance
    Processing Record 102 esperance http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=esperance
    huarmey
    Processing Record 103 huarmey http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=huarmey
    iwanai
    Processing Record 104 iwanai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=iwanai
    asau
    provideniya
    Processing Record 105 provideniya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=provideniya
    faya
    Processing Record 106 faya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=faya
    ancud
    Processing Record 107 ancud http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ancud
    longyearbyen
    Processing Record 108 longyearbyen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=longyearbyen
    grand+river+south+east
    maraa
    Processing Record 109 maraa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maraa
    port+alfred
    Processing Record 110 port alfred http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+alfred
    nanortalik
    Processing Record 111 nanortalik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nanortalik
    hami
    Processing Record 112 hami http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hami
    coihaique
    Processing Record 113 coihaique http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coihaique
    chiang+klang
    Processing Record 114 chiang klang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chiang+klang
    bambous+virieux
    Processing Record 115 bambous virieux http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bambous+virieux
    ilhabela
    Processing Record 116 ilhabela http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ilhabela
    christchurch
    Processing Record 117 christchurch http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=christchurch
    bergerac
    Processing Record 118 bergerac http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bergerac
    soyo
    Processing Record 119 soyo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=soyo
    portland
    Processing Record 120 portland http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=portland
    butaritari
    Processing Record 121 butaritari http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=butaritari
    thompson
    Processing Record 122 thompson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thompson
    mega
    Processing Record 123 mega http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mega
    inhambane
    Processing Record 124 inhambane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=inhambane
    araouane
    Processing Record 125 araouane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=araouane
    upernavik
    Processing Record 126 upernavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=upernavik
    palana
    Processing Record 127 palana http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palana
    vanavara
    Processing Record 128 vanavara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vanavara
    sao+filipe
    Processing Record 129 sao filipe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+filipe
    inderborskiy
    manzanillo
    Processing Record 130 manzanillo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=manzanillo
    vryburg
    Processing Record 131 vryburg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vryburg
    nantucket
    Processing Record 132 nantucket http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nantucket
    lorengau
    Processing Record 133 lorengau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lorengau
    cabo+san+lucas
    Processing Record 134 cabo san lucas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cabo+san+lucas
    qandala
    Processing Record 135 qandala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=qandala
    thanh+hoa
    Processing Record 136 thanh hoa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thanh+hoa
    tilichiki
    Processing Record 137 tilichiki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tilichiki
    vostok
    Processing Record 138 vostok http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vostok
    namibe
    Processing Record 139 namibe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=namibe
    am+timan
    Processing Record 140 am timan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=am+timan
    kidal
    Processing Record 141 kidal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kidal
    sfantu+gheorghe
    Processing Record 142 sfantu gheorghe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sfantu+gheorghe
    newport
    Processing Record 143 newport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=newport
    viligili
    nicoya
    Processing Record 144 nicoya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nicoya
    deer+lake
    Processing Record 145 deer lake http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=deer+lake
    seymchan
    Processing Record 146 seymchan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=seymchan
    namatanai
    Processing Record 147 namatanai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=namatanai
    yangambi
    Processing Record 148 yangambi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yangambi
    norman+wells
    Processing Record 149 norman wells http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=norman+wells
    pangnirtung
    Processing Record 150 pangnirtung http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pangnirtung
    salalah
    Processing Record 151 salalah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=salalah
    ambilobe
    Processing Record 152 ambilobe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ambilobe
    santa+isabel+do+rio+negro
    Processing Record 153 santa isabel do rio negro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+isabel+do+rio+negro
    luderitz
    Processing Record 154 luderitz http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=luderitz
    kyra
    waipawa
    Processing Record 155 waipawa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=waipawa
    tir+pol
    aberdare
    Processing Record 156 aberdare http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aberdare
    buraydah
    Processing Record 157 buraydah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=buraydah
    sur
    Processing Record 158 sur http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sur
    san+lucas
    Processing Record 159 san lucas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+lucas
    nizhneyansk
    mayo
    Processing Record 160 mayo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mayo
    beberibe
    Processing Record 161 beberibe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=beberibe
    carnarvon
    Processing Record 162 carnarvon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=carnarvon
    zhigansk
    Processing Record 163 zhigansk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zhigansk
    george
    Processing Record 164 george http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=george
    ballina
    Processing Record 165 ballina http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ballina
    bengkulu
    carballo
    Processing Record 166 carballo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=carballo
    pamanukan
    Processing Record 167 pamanukan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pamanukan
    lensk
    Processing Record 168 lensk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lensk
    ribeira+grande
    Processing Record 169 ribeira grande http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ribeira+grande
    praya
    Processing Record 170 praya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=praya
    devonport
    Processing Record 171 devonport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=devonport
    malanje
    Processing Record 172 malanje http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=malanje
    wabag
    Processing Record 173 wabag http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wabag
    torbay
    Processing Record 174 torbay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=torbay
    klaksvik
    Processing Record 175 klaksvik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=klaksvik
    guerrero+negro
    Processing Record 176 guerrero negro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=guerrero+negro
    puerto+ayora
    Processing Record 177 puerto ayora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+ayora
    half+moon+bay
    Processing Record 178 half moon bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=half+moon+bay
    merrill
    Processing Record 179 merrill http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=merrill
    yalta
    Processing Record 180 yalta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yalta
    shimoda
    Processing Record 181 shimoda http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shimoda
    ittiri
    Processing Record 182 ittiri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ittiri
    lagoa
    Processing Record 183 lagoa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lagoa
    bestobe
    Processing Record 184 bestobe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bestobe
    harunabad
    kommunar
    Processing Record 185 kommunar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kommunar
    the+hammocks
    Processing Record 186 the hammocks http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=the+hammocks
    cidreira
    Processing Record 187 cidreira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cidreira
    warqla
    borogontsy
    Processing Record 188 borogontsy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=borogontsy
    babolna
    Processing Record 189 babolna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=babolna
    kavieng
    Processing Record 190 kavieng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kavieng
    barentsburg
    saskylakh
    Processing Record 191 saskylakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saskylakh
    dodge+city
    Processing Record 192 dodge city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dodge+city
    hamilton
    Processing Record 193 hamilton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hamilton
    ketchikan
    Processing Record 194 ketchikan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ketchikan
    pointe-noire
    Processing Record 195 pointe-noire http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pointe-noire
    tiksi
    Processing Record 196 tiksi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tiksi
    santa+cruz
    Processing Record 197 santa cruz http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+cruz
    cayenne
    Processing Record 198 cayenne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cayenne
    galle
    Processing Record 199 galle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=galle
    carora
    Processing Record 200 carora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=carora
    salinas
    Processing Record 201 salinas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=salinas
    filingue
    Processing Record 202 filingue http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=filingue
    chuy
    Processing Record 203 chuy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chuy
    sisimiut
    Processing Record 204 sisimiut http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sisimiut
    hienghene
    Processing Record 205 hienghene http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hienghene
    khorramshahr
    Processing Record 206 khorramshahr http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khorramshahr
    raton
    Processing Record 207 raton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=raton
    mahendragarh
    Processing Record 208 mahendragarh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mahendragarh
    axim
    Processing Record 209 axim http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=axim
    haines+junction
    Processing Record 210 haines junction http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=haines+junction
    bolobo
    Processing Record 211 bolobo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bolobo
    yerbogachen
    Processing Record 212 yerbogachen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yerbogachen
    laguna
    Processing Record 213 laguna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=laguna
    hilo
    Processing Record 214 hilo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hilo
    meadow+lake
    Processing Record 215 meadow lake http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=meadow+lake
    burnie
    Processing Record 216 burnie http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=burnie
    saldanha
    Processing Record 217 saldanha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saldanha
    diffa
    Processing Record 218 diffa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=diffa
    urucui
    Processing Record 219 urucui http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=urucui
    okhotsk
    Processing Record 220 okhotsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=okhotsk
    hofn
    Processing Record 221 hofn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hofn
    balakhninskiy
    Processing Record 222 balakhninskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=balakhninskiy
    namikupa
    Processing Record 223 namikupa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=namikupa
    acapulco
    Processing Record 224 acapulco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=acapulco
    teya
    Processing Record 225 teya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=teya
    leshukonskoye
    Processing Record 226 leshukonskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=leshukonskoye
    kalemie
    Processing Record 227 kalemie http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kalemie
    labuan
    Processing Record 228 labuan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=labuan
    pacific+grove
    Processing Record 229 pacific grove http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pacific+grove
    rawson
    Processing Record 230 rawson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rawson
    gilgit
    Processing Record 231 gilgit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gilgit
    cuauhtemoc
    Processing Record 232 cuauhtemoc http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cuauhtemoc
    santa+cruz+de+la+palma
    Processing Record 233 santa cruz de la palma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+cruz+de+la+palma
    zavodskoy
    Processing Record 234 zavodskoy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zavodskoy
    panzhihua
    Processing Record 235 panzhihua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=panzhihua
    kashan
    Processing Record 236 kashan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kashan
    rusape
    Processing Record 237 rusape http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rusape
    evensk
    Processing Record 238 evensk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=evensk
    loubomo
    geraldton
    Processing Record 239 geraldton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=geraldton
    dosso
    Processing Record 240 dosso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dosso
    puerto+escondido
    Processing Record 241 puerto escondido http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+escondido
    oussouye
    Processing Record 242 oussouye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oussouye
    flinders
    Processing Record 243 flinders http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=flinders
    zamostea
    Processing Record 244 zamostea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zamostea
    barabai
    Processing Record 245 barabai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barabai
    arona
    Processing Record 246 arona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arona
    nurobod
    Processing Record 247 nurobod http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nurobod
    dinsor
    thinadhoo
    Processing Record 248 thinadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thinadhoo
    ojinaga
    Processing Record 249 ojinaga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ojinaga
    saint-augustin
    Processing Record 250 saint-augustin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-augustin
    iqaluit
    Processing Record 251 iqaluit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=iqaluit
    belfast
    Processing Record 252 belfast http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=belfast
    kavaratti
    Processing Record 253 kavaratti http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kavaratti
    zemio
    Processing Record 254 zemio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zemio
    karratha
    Processing Record 255 karratha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=karratha
    ayacucho
    Processing Record 256 ayacucho http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ayacucho
    korla
    ginda
    Processing Record 257 ginda http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ginda
    aguimes
    Processing Record 258 aguimes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aguimes
    pangody
    Processing Record 259 pangody http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pangody
    hanzhong
    Processing Record 260 hanzhong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hanzhong
    palo+alto
    Processing Record 261 palo alto http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palo+alto
    nacala
    Processing Record 262 nacala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nacala
    goderich
    Processing Record 263 goderich http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=goderich
    methoni
    Processing Record 264 methoni http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=methoni
    longlac
    kuche
    samusu
    chegdomyn
    Processing Record 265 chegdomyn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chegdomyn
    bukachacha
    Processing Record 266 bukachacha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bukachacha
    havre-saint-pierre
    Processing Record 267 havre-saint-pierre http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=havre-saint-pierre
    kutum
    Processing Record 268 kutum http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kutum
    kedrovoye
    Processing Record 269 kedrovoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kedrovoye
    atlantic+city
    popondetta
    Processing Record 270 popondetta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=popondetta
    mtimbira
    Processing Record 271 mtimbira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mtimbira
    manado
    Processing Record 272 manado http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=manado
    wajid
    Processing Record 273 wajid http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wajid
    tailai
    Processing Record 274 tailai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tailai
    severo-kurilsk
    Processing Record 275 severo-kurilsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=severo-kurilsk
    biak
    Processing Record 276 biak http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=biak
    challans
    Processing Record 277 challans http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=challans
    wenzhou
    Processing Record 278 wenzhou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wenzhou
    kalmunai
    Processing Record 279 kalmunai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kalmunai
    khrebtovaya
    Processing Record 280 khrebtovaya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khrebtovaya
    colac
    Processing Record 281 colac http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=colac
    oistins
    Processing Record 282 oistins http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oistins
    la+ronge
    Processing Record 283 la ronge http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+ronge
    hambantota
    Processing Record 284 hambantota http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hambantota
    port+moresby
    Processing Record 285 port moresby http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+moresby
    kabanjahe
    Processing Record 286 kabanjahe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kabanjahe
    mitu
    Processing Record 287 mitu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mitu
    longido
    Processing Record 288 longido http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=longido
    kapuskasing
    Processing Record 289 kapuskasing http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kapuskasing
    etoka
    Processing Record 290 etoka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=etoka
    cherskiy
    Processing Record 291 cherskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cherskiy
    formoso+do+araguaia
    madimba
    Processing Record 292 madimba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=madimba
    ban+dung
    Processing Record 293 ban dung http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ban+dung
    colgong
    Processing Record 294 colgong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=colgong
    kholodnyy
    Processing Record 295 kholodnyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kholodnyy
    umzimvubu
    seoul
    Processing Record 296 seoul http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=seoul
    mizan+teferi
    Processing Record 297 mizan teferi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mizan+teferi
    ola
    Processing Record 298 ola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ola
    nome
    Processing Record 299 nome http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nome
    healdsburg
    Processing Record 300 healdsburg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=healdsburg
    havelock
    Processing Record 301 havelock http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=havelock
    belaya+gora
    Processing Record 302 belaya gora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=belaya+gora
    khilok
    Processing Record 303 khilok http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khilok
    toftir
    sindand
    lolua
    acarau
    campobasso
    Processing Record 304 campobasso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=campobasso
    miri
    Processing Record 305 miri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miri
    pipar
    porto+novo
    Processing Record 306 porto novo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=porto+novo
    along
    Processing Record 307 along http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=along
    virginia+beach
    Processing Record 308 virginia beach http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=virginia+beach
    pestyaki
    Processing Record 309 pestyaki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pestyaki
    nylstroom
    vila
    Processing Record 310 vila http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila
    harper
    Processing Record 311 harper http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=harper
    aksu
    Processing Record 312 aksu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aksu
    flin+flon
    Processing Record 313 flin flon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=flin+flon
    amderma
    porto+santo
    fuzhou
    Processing Record 314 fuzhou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fuzhou
    churapcha
    Processing Record 315 churapcha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=churapcha
    ridgecrest
    Processing Record 316 ridgecrest http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ridgecrest
    deshna
    thessalon
    Processing Record 317 thessalon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thessalon
    catuday
    Processing Record 318 catuday http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=catuday
    shwebo
    Processing Record 319 shwebo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shwebo
    komsomolskiy
    Processing Record 320 komsomolskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=komsomolskiy
    coquimbo
    Processing Record 321 coquimbo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coquimbo
    dharmadam
    Processing Record 322 dharmadam http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dharmadam
    san+carlos+de+bariloche
    Processing Record 323 san carlos de bariloche http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+carlos+de+bariloche
    port+blair
    Processing Record 324 port blair http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+blair
    anqing
    Processing Record 325 anqing http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=anqing
    malatya
    aripuana
    Processing Record 326 aripuana http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aripuana
    limenaria
    Processing Record 327 limenaria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=limenaria
    jinchengjiang
    santa+fe
    Processing Record 328 santa fe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+fe
    vardo
    Processing Record 329 vardo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vardo
    tual
    Processing Record 330 tual http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tual
    oranjemund
    Processing Record 331 oranjemund http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oranjemund
    puerto+madryn
    Processing Record 332 puerto madryn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+madryn
    pecos
    Processing Record 333 pecos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pecos
    faanui
    Processing Record 334 faanui http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=faanui
    rundu
    Processing Record 335 rundu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rundu
    sao+joao+da+barra
    Processing Record 336 sao joao da barra http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+joao+da+barra
    comarapa
    Processing Record 337 comarapa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=comarapa
    talangnan
    Processing Record 338 talangnan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=talangnan
    westport
    Processing Record 339 westport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=westport
    churu
    Processing Record 340 churu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=churu
    vaitupu
    grand+gaube
    Processing Record 341 grand gaube http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grand+gaube
    el+carmen+de+bolivar
    Processing Record 342 el carmen de bolivar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=el+carmen+de+bolivar
    alice+springs
    Processing Record 343 alice springs http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alice+springs
    tazovskiy
    Processing Record 344 tazovskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tazovskiy
    rocha
    Processing Record 345 rocha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rocha
    pauini
    Processing Record 346 pauini http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pauini
    muroto
    Processing Record 347 muroto http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=muroto
    lindenhurst
    Processing Record 348 lindenhurst http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lindenhurst
    kathmandu
    Processing Record 349 kathmandu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kathmandu
    goundam
    Processing Record 350 goundam http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=goundam
    belyy+yar
    Processing Record 351 belyy yar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=belyy+yar
    berezovyy
    Processing Record 352 berezovyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=berezovyy
    tura
    Processing Record 353 tura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tura
    aklavik
    Processing Record 354 aklavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aklavik
    fairbanks
    Processing Record 355 fairbanks http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fairbanks
    lipari
    Processing Record 356 lipari http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lipari
    mareeba
    Processing Record 357 mareeba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mareeba
    colinas
    Processing Record 358 colinas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=colinas
    bathurst
    Processing Record 359 bathurst http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bathurst
    griffith
    Processing Record 360 griffith http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=griffith
    umm+kaddadah
    Processing Record 361 umm kaddadah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=umm+kaddadah
    trelew
    Processing Record 362 trelew http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=trelew
    lompoc
    Processing Record 363 lompoc http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lompoc
    abong+mbang
    Processing Record 364 abong mbang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=abong+mbang
    gilbues
    Processing Record 365 gilbues http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gilbues
    te+anau
    Processing Record 366 te anau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=te+anau
    ewo
    Processing Record 367 ewo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ewo
    jawhar
    Processing Record 368 jawhar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jawhar
    isangel
    Processing Record 369 isangel http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=isangel
    tabas
    Processing Record 370 tabas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tabas
    batagay
    Processing Record 371 batagay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=batagay
    koumac
    Processing Record 372 koumac http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=koumac
    morgan+city
    Processing Record 373 morgan city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=morgan+city
    umea
    Processing Record 374 umea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=umea
    narsaq
    Processing Record 375 narsaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=narsaq
    katsuura
    Processing Record 376 katsuura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katsuura
    shilovo
    Processing Record 377 shilovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shilovo
    nangong
    Processing Record 378 nangong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nangong
    charters+towers
    Processing Record 379 charters towers http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=charters+towers
    nabire
    Processing Record 380 nabire http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nabire
    khalkhal
    Processing Record 381 khalkhal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khalkhal
    souillac
    Processing Record 382 souillac http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=souillac
    tecpan
    Processing Record 383 tecpan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tecpan
    kieta
    Processing Record 384 kieta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kieta
    huilong
    Processing Record 385 huilong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=huilong
    tecoanapa
    Processing Record 386 tecoanapa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tecoanapa
    sandwick
    Processing Record 387 sandwick http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sandwick
    san+vicente
    Processing Record 388 san vicente http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+vicente
    georgetown
    Processing Record 389 georgetown http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=georgetown
    pavilosta
    Processing Record 390 pavilosta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pavilosta
    caravelas
    Processing Record 391 caravelas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=caravelas
    karkaralinsk
    teeli
    Processing Record 392 teeli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=teeli
    athabasca
    Processing Record 393 athabasca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=athabasca
    muncar
    Processing Record 394 muncar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=muncar
    bathsheba
    Processing Record 395 bathsheba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bathsheba
    tacoronte
    Processing Record 396 tacoronte http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tacoronte
    racale
    Processing Record 397 racale http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=racale
    rodbyhavn
    Processing Record 398 rodbyhavn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rodbyhavn
    baiyin
    Processing Record 399 baiyin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baiyin
    la+macarena
    Processing Record 400 la macarena http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+macarena
    iracoubo
    Processing Record 401 iracoubo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=iracoubo
    ovre+ardal
    Processing Record 402 ovre ardal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ovre+ardal
    makakilo+city
    Processing Record 403 makakilo city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=makakilo+city
    lazurne
    Processing Record 404 lazurne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lazurne
    zyryanka
    Processing Record 405 zyryanka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zyryanka
    cedar+city
    Processing Record 406 cedar city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cedar+city
    vredendal
    Processing Record 407 vredendal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vredendal
    palmer
    Processing Record 408 palmer http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palmer
    freeport
    Processing Record 409 freeport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=freeport
    vestmannaeyjar
    Processing Record 410 vestmannaeyjar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vestmannaeyjar
    svetlogorsk
    Processing Record 411 svetlogorsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=svetlogorsk
    eyl
    Processing Record 412 eyl http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=eyl
    puerto+del+rosario
    Processing Record 413 puerto del rosario http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+del+rosario
    sidi+bu+zayd
    mbaiki
    Processing Record 414 mbaiki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mbaiki
    karaul
    zhuanghe
    Processing Record 415 zhuanghe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zhuanghe
    syracuse
    Processing Record 416 syracuse http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=syracuse
    niquelandia
    Processing Record 417 niquelandia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=niquelandia
    dharchula
    Processing Record 418 dharchula http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dharchula
    yeppoon
    Processing Record 419 yeppoon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yeppoon
    bairiki
    kautokeino
    Processing Record 420 kautokeino http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kautokeino
    boyolangu
    Processing Record 421 boyolangu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=boyolangu
    tuy+hoa
    Processing Record 422 tuy hoa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tuy+hoa
    simao
    Processing Record 423 simao http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=simao
    uyskoye
    Processing Record 424 uyskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=uyskoye
    atar
    Processing Record 425 atar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atar
    khani
    Processing Record 426 khani http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khani
    nouadhibou
    Processing Record 427 nouadhibou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nouadhibou
    polyarnyy
    Processing Record 428 polyarnyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=polyarnyy
    bubaque
    Processing Record 429 bubaque http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bubaque
    bur+gabo
    olden
    Processing Record 430 olden http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=olden
    tianpeng
    Processing Record 431 tianpeng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tianpeng
    erzin
    Processing Record 432 erzin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=erzin
    tabatinga
    Processing Record 433 tabatinga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tabatinga
    campbell+river
    Processing Record 434 campbell river http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=campbell+river
    selishche
    kuruksay
    curillo
    Processing Record 435 curillo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=curillo
    nesbyen
    Processing Record 436 nesbyen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nesbyen
    ayia+galini
    Processing Record 437 ayia galini http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ayia+galini
    chara
    Processing Record 438 chara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chara
    tagusao
    Processing Record 439 tagusao http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tagusao
    santa+maria
    Processing Record 440 santa maria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+maria
    eureka
    Processing Record 441 eureka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=eureka
    russellville
    Processing Record 442 russellville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=russellville
    sioux+lookout
    Processing Record 443 sioux lookout http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sioux+lookout
    chumikan
    Processing Record 444 chumikan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chumikan
    cheyur
    college
    Processing Record 445 college http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=college
    peniche
    Processing Record 446 peniche http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=peniche
    bud
    Processing Record 447 bud http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bud
    debre+tabor
    Processing Record 448 debre tabor http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=debre+tabor
    providencia
    Processing Record 449 providencia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=providencia
    atambua
    Processing Record 450 atambua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atambua
    nolinsk
    Processing Record 451 nolinsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nolinsk
    sibolga
    Processing Record 452 sibolga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sibolga
    tiznit
    Processing Record 453 tiznit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tiznit
    fortuna
    Processing Record 454 fortuna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fortuna
    falmouth
    Processing Record 455 falmouth http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=falmouth
    san+quintin
    Processing Record 456 san quintin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+quintin
    margate
    Processing Record 457 margate http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=margate
    karla
    Processing Record 458 karla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=karla
    puerto+el+triunfo
    Processing Record 459 puerto el triunfo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+el+triunfo
    dibulla
    Processing Record 460 dibulla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dibulla
    calama
    Processing Record 461 calama http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=calama
    pisco
    Processing Record 462 pisco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pisco
    hillsboro
    Processing Record 463 hillsboro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hillsboro
    labuhan
    Processing Record 464 labuhan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=labuhan
    inzer
    Processing Record 465 inzer http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=inzer
    mecca
    Processing Record 466 mecca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mecca
    balkhash
    Processing Record 467 balkhash http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=balkhash
    dongsheng
    Processing Record 468 dongsheng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dongsheng
    birkeland
    Processing Record 469 birkeland http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=birkeland
    vao
    Processing Record 470 vao http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vao
    dingle
    Processing Record 471 dingle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dingle
    comodoro+rivadavia
    Processing Record 472 comodoro rivadavia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=comodoro+rivadavia
    broome
    Processing Record 473 broome http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=broome
    sumbe
    Processing Record 474 sumbe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sumbe
    kanker
    Processing Record 475 kanker http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kanker
    srednekolymsk
    Processing Record 476 srednekolymsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=srednekolymsk
    oroville
    Processing Record 477 oroville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oroville
    baherden
    Processing Record 478 baherden http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baherden
    wattegama
    Processing Record 479 wattegama http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wattegama
    bodden+town
    Processing Record 480 bodden town http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bodden+town
    ransang
    bolungarvik
    bucerias
    Processing Record 481 bucerias http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bucerias
    murud
    lingyuan
    Processing Record 482 lingyuan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lingyuan
    weyburn
    Processing Record 483 weyburn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=weyburn
    kankon
    Processing Record 484 kankon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kankon
    kota+belud
    Processing Record 485 kota belud http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kota+belud
    pali
    Processing Record 486 pali http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pali
    tautira
    Processing Record 487 tautira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tautira
    riberalta
    Processing Record 488 riberalta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=riberalta
    dunedin
    Processing Record 489 dunedin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dunedin
    samarai
    Processing Record 490 samarai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=samarai
    shirokiy
    Processing Record 491 shirokiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shirokiy
    ulladulla
    Processing Record 492 ulladulla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ulladulla
    moyobamba
    Processing Record 493 moyobamba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=moyobamba
    yulara
    Processing Record 494 yulara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yulara
    batagay-alyta
    Processing Record 495 batagay-alyta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=batagay-alyta
    shupiyan
    Processing Record 496 shupiyan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shupiyan
    talnakh
    Processing Record 497 talnakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=talnakh
    emerald
    Processing Record 498 emerald http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=emerald
    akureyri
    Processing Record 499 akureyri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=akureyri
    deniliquin
    Processing Record 500 deniliquin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=deniliquin
    kovdor
    Processing Record 501 kovdor http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kovdor
    wageningen
    Processing Record 502 wageningen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wageningen
    ratnagiri
    Processing Record 503 ratnagiri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ratnagiri
    miranda+de+ebro
    Processing Record 504 miranda de ebro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miranda+de+ebro
    mayskiy
    Processing Record 505 mayskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mayskiy
    ukmerge
    Processing Record 506 ukmerge http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ukmerge
    kibray
    Processing Record 507 kibray http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kibray
    tabiauea
    pimenta+bueno
    Processing Record 508 pimenta bueno http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pimenta+bueno
    nemuro
    Processing Record 509 nemuro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nemuro
    savannah+bight
    Processing Record 510 savannah bight http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=savannah+bight
    mims
    Processing Record 511 mims http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mims
    ngukurr
    qaqortoq
    Processing Record 512 qaqortoq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=qaqortoq
    sterling
    Processing Record 513 sterling http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sterling
    naze
    Processing Record 514 naze http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=naze
    takoradi
    Processing Record 515 takoradi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=takoradi
    darnah
    Processing Record 516 darnah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=darnah
    gambo
    Processing Record 517 gambo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gambo
    narovchat
    Processing Record 518 narovchat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=narovchat
    khudumelapye
    Processing Record 519 khudumelapye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khudumelapye
    marsa+matruh
    Processing Record 520 marsa matruh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marsa+matruh
    tres+arroyos
    Processing Record 521 tres arroyos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tres+arroyos
    belomorsk
    Processing Record 522 belomorsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=belomorsk
    san+ramon
    Processing Record 523 san ramon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+ramon
    rassvet
    Processing Record 524 rassvet http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rassvet
    visby
    Processing Record 525 visby http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=visby
    mirnyy
    Processing Record 526 mirnyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mirnyy
    port+shepstone
    Processing Record 527 port shepstone http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+shepstone
    zaysan
    Processing Record 528 zaysan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zaysan
    kara-tyube
    Processing Record 529 kara-tyube http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kara-tyube
    russell
    Processing Record 530 russell http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=russell
    meshcherino
    Processing Record 531 meshcherino http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=meshcherino
    galesong
    Processing Record 532 galesong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=galesong
    verkhoyansk
    Processing Record 533 verkhoyansk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=verkhoyansk
    platonovka
    el+mahalla+el+kubra
    puerto+baquerizo+moreno
    Processing Record 534 puerto baquerizo moreno http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+baquerizo+moreno
    birao
    Processing Record 535 birao http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=birao
    deputatskiy
    Processing Record 536 deputatskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=deputatskiy
    tambo
    Processing Record 537 tambo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tambo
    abrau-dyurso
    Processing Record 538 abrau-dyurso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=abrau-dyurso
    imbituba
    Processing Record 539 imbituba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=imbituba
    nanma
    Processing Record 540 nanma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nanma
    yinchuan
    Processing Record 541 yinchuan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yinchuan
    dwarka
    Processing Record 542 dwarka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dwarka
    alice
    Processing Record 543 alice http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alice
    kuusamo
    Processing Record 544 kuusamo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kuusamo
    doba
    Processing Record 545 doba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=doba
    gizo
    Processing Record 546 gizo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gizo
    terrace+bay
    Processing Record 547 terrace bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=terrace+bay
    dudinka
    Processing Record 548 dudinka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dudinka
    kharitonovo
    Processing Record 549 kharitonovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kharitonovo
    sciacca
    Processing Record 550 sciacca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sciacca
    beringovskiy
    Processing Record 551 beringovskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=beringovskiy
    husavik
    Processing Record 552 husavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=husavik
    ellisras
    Processing Record 553 ellisras http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ellisras
    luang+prabang
    Processing Record 554 luang prabang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=luang+prabang
    ondjiva
    Processing Record 555 ondjiva http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ondjiva
    ayan
    Processing Record 556 ayan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ayan
    krasnovishersk
    Processing Record 557 krasnovishersk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=krasnovishersk
    catia+la+mar
    Processing Record 558 catia la mar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=catia+la+mar
    kiruna
    Processing Record 559 kiruna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kiruna
    bulgan
    Processing Record 560 bulgan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bulgan
    road+town
    Processing Record 561 road town http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=road+town
    genhe
    Processing Record 562 genhe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=genhe
    shumskiy
    Processing Record 563 shumskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shumskiy
    moiyabana
    dhanera
    Processing Record 564 dhanera http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dhanera
    cotonou
    Processing Record 565 cotonou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cotonou
    grand-lahou
    Processing Record 566 grand-lahou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grand-lahou
    viedma
    Processing Record 567 viedma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=viedma
    bacuit
    suntar
    Processing Record 568 suntar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=suntar
    lavrentiya
    Processing Record 569 lavrentiya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lavrentiya
    katangli
    Processing Record 570 katangli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katangli
    kudahuvadhoo
    Processing Record 571 kudahuvadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kudahuvadhoo
    jasper
    Processing Record 572 jasper http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jasper
    pueblo
    Processing Record 573 pueblo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pueblo
    espanola
    Processing Record 574 espanola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=espanola
    pangai
    Processing Record 575 pangai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pangai
    rijeka
    Processing Record 576 rijeka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rijeka
    baykit
    Processing Record 577 baykit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baykit
    dolbeau
    csurgo
    Processing Record 578 csurgo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=csurgo
    sabzevar
    Processing Record 579 sabzevar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sabzevar
    sao+miguel+do+araguaia
    Processing Record 580 sao miguel do araguaia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+miguel+do+araguaia
    azare
    Processing Record 581 azare http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=azare
    mandera
    Processing Record 582 mandera http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mandera
    matagami
    Processing Record 583 matagami http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=matagami
    banjarmasin
    Processing Record 584 banjarmasin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=banjarmasin
    harare
    Processing Record 585 harare http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=harare
    floro
    Processing Record 586 floro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=floro
    port-cartier
    Processing Record 587 port-cartier http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port-cartier
    ciudad+bolivar
    Processing Record 588 ciudad bolivar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ciudad+bolivar
    taburi
    malakal
    berlevag
    Processing Record 589 berlevag http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=berlevag
    nohar
    Processing Record 590 nohar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nohar
    san+cristobal
    Processing Record 591 san cristobal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+cristobal
    kamenskoye
    arlit
    Processing Record 592 arlit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arlit
    cody
    Processing Record 593 cody http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cody
    mongui
    Processing Record 594 mongui http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mongui
    basco
    Processing Record 595 basco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=basco
    camacupa
    Processing Record 596 camacupa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=camacupa
    aflu
    la+orilla
    Processing Record 597 la orilla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+orilla
    phan+thiet
    Processing Record 598 phan thiet http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=phan+thiet
    gravdal
    Processing Record 599 gravdal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gravdal
    hovd
    Processing Record 600 hovd http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hovd
    paradwip
    bandarbeyla
    Processing Record 601 bandarbeyla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bandarbeyla
    ibra
    Processing Record 602 ibra http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ibra
    nagato
    Processing Record 603 nagato http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nagato
    emporia
    Processing Record 604 emporia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=emporia
    xining
    Processing Record 605 xining http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=xining
    florianopolis
    Processing Record 606 florianopolis http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=florianopolis
    hongjiang
    Processing Record 607 hongjiang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hongjiang
    lola
    Processing Record 608 lola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lola
    morbegno
    Processing Record 609 morbegno http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=morbegno
    sola
    Processing Record 610 sola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sola
    codrington
    Processing Record 611 codrington http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=codrington
    acacoyagua
    Processing Record 612 acacoyagua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=acacoyagua
    maumere
    Processing Record 613 maumere http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maumere
    buckeye
    Processing Record 614 buckeye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=buckeye
    olafsvik
    macomb
    Processing Record 615 macomb http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=macomb
    panaba
    Processing Record 616 panaba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=panaba
    anloga
    Processing Record 617 anloga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=anloga
    hualmay
    Processing Record 618 hualmay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hualmay
    port+hawkesbury
    Processing Record 619 port hawkesbury http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+hawkesbury
    bo+rai
    Processing Record 620 bo rai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bo+rai
    sambava
    Processing Record 621 sambava http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sambava
    san+policarpo
    Processing Record 622 san policarpo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+policarpo
    lazaro+cardenas
    Processing Record 623 lazaro cardenas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lazaro+cardenas
    stokmarknes
    Processing Record 624 stokmarknes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=stokmarknes
    miami
    Processing Record 625 miami http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miami
    jalu
    Processing Record 626 jalu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jalu
    port+hardy
    Processing Record 627 port hardy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+hardy
    tambura
    padang
    Processing Record 628 padang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=padang
    lemesos
    bar+harbor
    Processing Record 629 bar harbor http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bar+harbor
    dvinskoy
    Processing Record 630 dvinskoy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dvinskoy
    jati
    Processing Record 631 jati http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jati
    choma
    Processing Record 632 choma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=choma
    kalabo
    Processing Record 633 kalabo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kalabo
    makurdi
    Processing Record 634 makurdi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=makurdi
    parras
    dali
    Processing Record 635 dali http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dali
    pahrump
    Processing Record 636 pahrump http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pahrump
    barra+patuca
    Processing Record 637 barra patuca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barra+patuca
    nefteyugansk
    Processing Record 638 nefteyugansk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nefteyugansk
    macas
    Processing Record 639 macas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=macas
    mian+channun
    Processing Record 640 mian channun http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mian+channun
    tupik
    Processing Record 641 tupik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tupik
    barahona
    Processing Record 642 barahona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barahona
    praia+da+vitoria
    Processing Record 643 praia da vitoria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=praia+da+vitoria
    kloulklubed
    Processing Record 644 kloulklubed http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kloulklubed
    amahai
    Processing Record 645 amahai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=amahai
    whitehorse
    Processing Record 646 whitehorse http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=whitehorse
    fort+nelson
    Processing Record 647 fort nelson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fort+nelson
    mmabatho
    Processing Record 648 mmabatho http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mmabatho
    kayerkan
    Processing Record 649 kayerkan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kayerkan
    gamba
    Processing Record 650 gamba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gamba
    north+bend
    Processing Record 651 north bend http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=north+bend
    dhidhdhoo
    Processing Record 652 dhidhdhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dhidhdhoo
    rafai
    Processing Record 653 rafai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rafai
    tungkang
    meulaboh
    Processing Record 654 meulaboh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=meulaboh
    vila+do+maio
    Processing Record 655 vila do maio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila+do+maio
    korba
    Processing Record 656 korba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=korba
    mount+isa
    Processing Record 657 mount isa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mount+isa
    clacton-on-sea
    Processing Record 658 clacton-on-sea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=clacton-on-sea
    raudeberg
    Processing Record 659 raudeberg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=raudeberg
    tortoli
    Processing Record 660 tortoli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tortoli
    cascais
    Processing Record 661 cascais http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cascais
    nishihara
    Processing Record 662 nishihara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nishihara
    sumbawa
    tshela
    Processing Record 663 tshela http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tshela
    vuktyl
    Processing Record 664 vuktyl http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vuktyl
    gat
    Processing Record 665 gat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gat
    naenwa
    garowe
    Processing Record 666 garowe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=garowe
    danielskuil
    Processing Record 667 danielskuil http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=danielskuil
    stekolnyy
    atasu
    Processing Record 668 atasu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atasu
    bilma
    Processing Record 669 bilma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bilma
    plettenberg+bay
    Processing Record 670 plettenberg bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=plettenberg+bay
    praia
    Processing Record 671 praia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=praia
    dongying
    Processing Record 672 dongying http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dongying
    umm+jarr
    ippy
    Processing Record 673 ippy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ippy
    cabo+rojo
    Processing Record 674 cabo rojo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cabo+rojo
    maningrida
    Processing Record 675 maningrida http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maningrida
    brownwood
    Processing Record 676 brownwood http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=brownwood
    lima
    Processing Record 677 lima http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lima
    bage
    Processing Record 678 bage http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bage
    saint-joseph
    Processing Record 679 saint-joseph http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-joseph
    


```python
weather_dict = {
    "City": shortened_city_list,
    "Latitude": latitude,
    "Longitude": longitude,
    "Temperature": temperature,
    "Humidity": humidity,
    "Cloudiness": cloudiness,
    "Wind Speed": wind_speed
}
weather_data = pd.DataFrame(weather_dict)
weather_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Temperature</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>arraial do cabo</td>
      <td>24</td>
      <td>97</td>
      <td>-22.97</td>
      <td>-42.02</td>
      <td>71.82</td>
      <td>8.63</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hermanus</td>
      <td>32</td>
      <td>100</td>
      <td>-34.42</td>
      <td>19.24</td>
      <td>49.05</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>2</th>
      <td>suruc</td>
      <td>0</td>
      <td>29</td>
      <td>36.98</td>
      <td>38.42</td>
      <td>60.80</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>sarkand</td>
      <td>12</td>
      <td>62</td>
      <td>45.41</td>
      <td>79.91</td>
      <td>48.87</td>
      <td>4.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>chita</td>
      <td>40</td>
      <td>38</td>
      <td>52.03</td>
      <td>113.50</td>
      <td>39.20</td>
      <td>6.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
weather_data.count()
```




    City           679
    Cloudiness     679
    Humidity       679
    Latitude       679
    Longitude      679
    Temperature    679
    Wind Speed     679
    dtype: int64




```python
current_datetime = datetime.datetime.now().strftime("%m/%d/%Y")
current_datetime
```




    '04/18/2018'



# Latitude vs. Temperature Plot


```python
plt.scatter(weather_data["Latitude"], weather_data["Temperature"], edgecolor="black", linewidths=1, marker="o", alpha=0.8)

plt.title("Latitude vs Temperature (F) (" + current_datetime + ")")
plt.ylabel("Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-100, 100])
plt.ylim([-50, 120])

# Save the figure
plt.savefig("Latitude_Temperature.png")

# Show plot
plt.show()
```


![png](output_10_0.png)


# Latitude vs. Humidity Plot


```python
plt.scatter(weather_data["Latitude"], weather_data["Humidity"], edgecolor="black", linewidths=1, marker="o", alpha=0.8)

plt.title("Latitude vs. Humidity (%) (" + current_datetime + ")")
plt.ylabel("Humidity")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-100, 100])
plt.ylim([-5, 105])

# Save the figure
plt.savefig("Latitude_Humidity.png")

# Show plot
plt.show()
```


![png](output_12_0.png)


# Latitude vs. Cloudiness Plot


```python
plt.scatter(weather_data["Latitude"], weather_data["Cloudiness"], edgecolor="black", linewidths=1, marker="o", alpha=0.8)

plt.title("Latitude vs. Cloudiness (%) (" + current_datetime + ")")
plt.ylabel("Cloudiness")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-100, 100])
plt.ylim([-5, 105])

# Save the figure
plt.savefig("Latitude_Cloudiness.png")

# Show plot
plt.show()
```


![png](output_14_0.png)


# Latitude vs. Wind Speed Plot


```python
plt.scatter(weather_data["Latitude"], weather_data["Wind Speed"], edgecolor="black", linewidths=1, marker="o", alpha=0.8)

plt.title("Latitude vs. Wind Speed (mph) (" + current_datetime + ")")
plt.ylabel("Wind Speed")
plt.xlabel("Latitude")
plt.grid(True)
plt.xlim([-100, 100])
plt.ylim([-5, 50])

# Save the figure
plt.savefig("Latitude_Wind_Speed.png")

# Show plot
plt.show()
```


![png](output_16_0.png)



```python
weather_data.to_csv("weatherData.csv", index=False, header=True)
```
