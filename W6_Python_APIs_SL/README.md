
# Analysis
Observed Trend 1 - The latitude vs. temperature plot shows that the highest temperatures are closest to the equator.<br>
Observed Trend 2 - The latitude vs. humidity plot shows that humidity increases near the equator.<br>
Observed Trend 3 - The data does not suggest a strong relationship between latitude and cloudiness or wind speed.<br>


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




    777



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

    yining
    Processing Record 1 yining http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yining
    hobart
    Processing Record 2 hobart http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hobart
    santa+rosa
    Processing Record 3 santa rosa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+rosa
    puerto+ayora
    Processing Record 4 puerto ayora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+ayora
    geraldton
    Processing Record 5 geraldton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=geraldton
    khatanga
    Processing Record 6 khatanga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=khatanga
    avarua
    Processing Record 7 avarua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=avarua
    malanje
    Processing Record 8 malanje http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=malanje
    mataura
    Processing Record 9 mataura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mataura
    saint-philippe
    Processing Record 10 saint-philippe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-philippe
    busselton
    Processing Record 11 busselton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=busselton
    letterkenny
    Processing Record 12 letterkenny http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=letterkenny
    fortuna
    Processing Record 13 fortuna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fortuna
    namibe
    Processing Record 14 namibe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=namibe
    ereymentau
    Processing Record 15 ereymentau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ereymentau
    faanui
    Processing Record 16 faanui http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=faanui
    jabiru
    kavieng
    Processing Record 17 kavieng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kavieng
    maldonado
    Processing Record 18 maldonado http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maldonado
    nurota
    Processing Record 19 nurota http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nurota
    inirida
    Processing Record 20 inirida http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=inirida
    cape+town
    Processing Record 21 cape town http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cape+town
    bengkulu
    eureka
    Processing Record 22 eureka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=eureka
    atuona
    Processing Record 23 atuona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atuona
    esperance
    Processing Record 24 esperance http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=esperance
    ushuaia
    Processing Record 25 ushuaia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ushuaia
    batagay-alyta
    Processing Record 26 batagay-alyta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=batagay-alyta
    waitati
    Processing Record 27 waitati http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=waitati
    nome
    Processing Record 28 nome http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nome
    sibolga
    Processing Record 29 sibolga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sibolga
    malatya
    chokurdakh
    Processing Record 30 chokurdakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chokurdakh
    palembang
    Processing Record 31 palembang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palembang
    castro
    Processing Record 32 castro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=castro
    dikson
    Processing Record 33 dikson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dikson
    ovalle
    Processing Record 34 ovalle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ovalle
    jamestown
    Processing Record 35 jamestown http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jamestown
    havoysund
    Processing Record 36 havoysund http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=havoysund
    rikitea
    Processing Record 37 rikitea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rikitea
    san+quintin
    Processing Record 38 san quintin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+quintin
    viransehir
    Processing Record 39 viransehir http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=viransehir
    barrow
    Processing Record 40 barrow http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barrow
    qaanaaq
    Processing Record 41 qaanaaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=qaanaaq
    butembo
    Processing Record 42 butembo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=butembo
    chuy
    Processing Record 43 chuy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chuy
    boyolangu
    Processing Record 44 boyolangu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=boyolangu
    east+london
    Processing Record 45 east london http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=east+london
    cabo+san+lucas
    Processing Record 46 cabo san lucas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cabo+san+lucas
    punta+arenas
    Processing Record 47 punta arenas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=punta+arenas
    hilo
    Processing Record 48 hilo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hilo
    isangel
    Processing Record 49 isangel http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=isangel
    aizkraukle
    Processing Record 50 aizkraukle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aizkraukle
    souillac
    Processing Record 51 souillac http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=souillac
    lazurne
    Processing Record 52 lazurne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lazurne
    yellowknife
    Processing Record 53 yellowknife http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yellowknife
    bluff
    Processing Record 54 bluff http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bluff
    polovinnoye
    Processing Record 55 polovinnoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=polovinnoye
    san+jeronimo
    Processing Record 56 san jeronimo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+jeronimo
    lasa
    Processing Record 57 lasa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lasa
    hasaki
    Processing Record 58 hasaki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hasaki
    saint-augustin
    Processing Record 59 saint-augustin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-augustin
    kahului
    Processing Record 60 kahului http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kahului
    lata
    Processing Record 61 lata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lata
    mys+shmidta
    thompson
    Processing Record 62 thompson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thompson
    okoneshnikovo
    Processing Record 63 okoneshnikovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=okoneshnikovo
    port+elizabeth
    Processing Record 64 port elizabeth http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+elizabeth
    impfondo
    Processing Record 65 impfondo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=impfondo
    quesnel
    Processing Record 66 quesnel http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=quesnel
    yarmouth
    Processing Record 67 yarmouth http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yarmouth
    san+cristobal
    Processing Record 68 san cristobal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+cristobal
    valparaiso
    Processing Record 69 valparaiso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=valparaiso
    lagoa
    Processing Record 70 lagoa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lagoa
    paucartambo
    vaini
    Processing Record 71 vaini http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vaini
    baruun-urt
    Processing Record 72 baruun-urt http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baruun-urt
    barentsburg
    norman+wells
    Processing Record 73 norman wells http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=norman+wells
    wakkanai
    Processing Record 74 wakkanai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wakkanai
    dingle
    Processing Record 75 dingle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dingle
    grenaa
    Processing Record 76 grenaa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grenaa
    dorado
    Processing Record 77 dorado http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dorado
    male
    Processing Record 78 male http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=male
    oranjemund
    Processing Record 79 oranjemund http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oranjemund
    port+lincoln
    Processing Record 80 port lincoln http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+lincoln
    mandalgovi
    Processing Record 81 mandalgovi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mandalgovi
    saldanha
    Processing Record 82 saldanha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saldanha
    correntina
    Processing Record 83 correntina http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=correntina
    hithadhoo
    Processing Record 84 hithadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hithadhoo
    sentyabrskiy
    toliary
    zyryanovsk
    Processing Record 85 zyryanovsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zyryanovsk
    acarau
    kaitangata
    Processing Record 86 kaitangata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kaitangata
    ribeira+grande
    Processing Record 87 ribeira grande http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ribeira+grande
    bouca
    Processing Record 88 bouca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bouca
    saint+george
    Processing Record 89 saint george http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint+george
    tuktoyaktuk
    Processing Record 90 tuktoyaktuk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tuktoyaktuk
    victoria
    Processing Record 91 victoria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=victoria
    kochki
    Processing Record 92 kochki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kochki
    ahipara
    Processing Record 93 ahipara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ahipara
    tasiilaq
    Processing Record 94 tasiilaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tasiilaq
    lebu
    Processing Record 95 lebu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lebu
    palabuhanratu
    cherskiy
    Processing Record 96 cherskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cherskiy
    henties+bay
    Processing Record 97 henties bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=henties+bay
    pastavy
    Processing Record 98 pastavy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pastavy
    itaituba
    Processing Record 99 itaituba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=itaituba
    dera+din+panah
    ravar
    Processing Record 100 ravar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ravar
    sechura
    Processing Record 101 sechura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sechura
    bambous+virieux
    Processing Record 102 bambous virieux http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bambous+virieux
    cairns
    Processing Record 103 cairns http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cairns
    tiksi
    Processing Record 104 tiksi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tiksi
    ponta+do+sol
    Processing Record 105 ponta do sol http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ponta+do+sol
    afikpo
    Processing Record 106 afikpo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=afikpo
    kapaa
    Processing Record 107 kapaa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kapaa
    vieques
    Processing Record 108 vieques http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vieques
    sinop
    Processing Record 109 sinop http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sinop
    albany
    Processing Record 110 albany http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=albany
    longyearbyen
    Processing Record 111 longyearbyen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=longyearbyen
    mount+isa
    Processing Record 112 mount isa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mount+isa
    tumannyy
    carnarvon
    Processing Record 113 carnarvon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=carnarvon
    blagodatnoye
    Processing Record 114 blagodatnoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=blagodatnoye
    along
    Processing Record 115 along http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=along
    vardo
    Processing Record 116 vardo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vardo
    qaqortoq
    Processing Record 117 qaqortoq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=qaqortoq
    tura
    Processing Record 118 tura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tura
    osorno
    Processing Record 119 osorno http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=osorno
    waingapu
    Processing Record 120 waingapu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=waingapu
    pochutla
    Processing Record 121 pochutla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pochutla
    shahr-e+babak
    Processing Record 122 shahr-e babak http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shahr-e+babak
    sarakhs
    Processing Record 123 sarakhs http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sarakhs
    aklavik
    Processing Record 124 aklavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aklavik
    vao
    Processing Record 125 vao http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vao
    marsh+harbour
    Processing Record 126 marsh harbour http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marsh+harbour
    sioux+lookout
    Processing Record 127 sioux lookout http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sioux+lookout
    yumen
    Processing Record 128 yumen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yumen
    vostok
    Processing Record 129 vostok http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vostok
    chegdomyn
    Processing Record 130 chegdomyn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chegdomyn
    chapais
    Processing Record 131 chapais http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chapais
    caravelas
    Processing Record 132 caravelas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=caravelas
    carlyle
    Processing Record 133 carlyle http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=carlyle
    hirara
    Processing Record 134 hirara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hirara
    tautira
    Processing Record 135 tautira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tautira
    matara
    Processing Record 136 matara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=matara
    taolanaro
    la+ronge
    Processing Record 137 la ronge http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+ronge
    kodiak
    Processing Record 138 kodiak http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kodiak
    ishigaki
    Processing Record 139 ishigaki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ishigaki
    tay+ninh
    Processing Record 140 tay ninh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tay+ninh
    karauli
    Processing Record 141 karauli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=karauli
    hermanus
    Processing Record 142 hermanus http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hermanus
    lipin+bor
    Processing Record 143 lipin bor http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lipin+bor
    pizarro
    Processing Record 144 pizarro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pizarro
    sola
    Processing Record 145 sola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sola
    boa+vista
    Processing Record 146 boa vista http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=boa+vista
    leshukonskoye
    Processing Record 147 leshukonskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=leshukonskoye
    ashland
    Processing Record 148 ashland http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ashland
    petropavlovskaya
    Processing Record 149 petropavlovskaya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=petropavlovskaya
    talnakh
    Processing Record 150 talnakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=talnakh
    road+town
    Processing Record 151 road town http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=road+town
    huazolotitlan
    bouza
    Processing Record 152 bouza http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bouza
    houma
    Processing Record 153 houma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=houma
    bengbu
    Processing Record 154 bengbu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bengbu
    coihaique
    Processing Record 155 coihaique http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coihaique
    port+alfred
    Processing Record 156 port alfred http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+alfred
    taoudenni
    Processing Record 157 taoudenni http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=taoudenni
    sitka
    Processing Record 158 sitka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sitka
    alma
    Processing Record 159 alma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alma
    high+level
    Processing Record 160 high level http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=high+level
    westport
    Processing Record 161 westport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=westport
    bethel
    Processing Record 162 bethel http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bethel
    boditi
    Processing Record 163 boditi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=boditi
    mahebourg
    Processing Record 164 mahebourg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mahebourg
    shalakusha
    Processing Record 165 shalakusha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shalakusha
    antofagasta
    Processing Record 166 antofagasta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=antofagasta
    gejiu
    Processing Record 167 gejiu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gejiu
    mar+del+plata
    Processing Record 168 mar del plata http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mar+del+plata
    avera
    Processing Record 169 avera http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=avera
    tarakan
    Processing Record 170 tarakan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tarakan
    itarema
    Processing Record 171 itarema http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=itarema
    jutai
    Processing Record 172 jutai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jutai
    cefalu
    Processing Record 173 cefalu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cefalu
    krutaya+gorka
    Processing Record 174 krutaya gorka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=krutaya+gorka
    ashwaubenon
    Processing Record 175 ashwaubenon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ashwaubenon
    bunbury
    Processing Record 176 bunbury http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bunbury
    umzimvubu
    lorengau
    Processing Record 177 lorengau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lorengau
    cidreira
    Processing Record 178 cidreira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cidreira
    georgetown
    Processing Record 179 georgetown http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=georgetown
    kuching
    Processing Record 180 kuching http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kuching
    sheridan
    Processing Record 181 sheridan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sheridan
    telimele
    Processing Record 182 telimele http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=telimele
    karaul
    parfino
    Processing Record 183 parfino http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=parfino
    merauke
    Processing Record 184 merauke http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=merauke
    saint-denis
    Processing Record 185 saint-denis http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-denis
    saint-francois
    Processing Record 186 saint-francois http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-francois
    porto+velho
    Processing Record 187 porto velho http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=porto+velho
    naze
    Processing Record 188 naze http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=naze
    rio+gallegos
    Processing Record 189 rio gallegos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rio+gallegos
    saskylakh
    Processing Record 190 saskylakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saskylakh
    bredasdorp
    Processing Record 191 bredasdorp http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bredasdorp
    selma
    Processing Record 192 selma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=selma
    mirnyy
    Processing Record 193 mirnyy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mirnyy
    ca+mau
    Processing Record 194 ca mau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ca+mau
    omboue
    Processing Record 195 omboue http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=omboue
    gamba
    Processing Record 196 gamba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gamba
    nizhneyansk
    san+alberto
    Processing Record 197 san alberto http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+alberto
    at-bashi
    Processing Record 198 at-bashi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=at-bashi
    mount+gambier
    Processing Record 199 mount gambier http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mount+gambier
    tiznit
    Processing Record 200 tiznit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tiznit
    attawapiskat
    uva
    Processing Record 201 uva http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=uva
    raychikhinsk
    Processing Record 202 raychikhinsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=raychikhinsk
    barra
    Processing Record 203 barra http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barra
    slonim
    Processing Record 204 slonim http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=slonim
    kosh-agach
    Processing Record 205 kosh-agach http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kosh-agach
    ilulissat
    Processing Record 206 ilulissat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ilulissat
    arraial+do+cabo
    Processing Record 207 arraial do cabo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arraial+do+cabo
    los+llanos+de+aridane
    Processing Record 208 los llanos de aridane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=los+llanos+de+aridane
    arman
    Processing Record 209 arman http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arman
    olkhovatka
    Processing Record 210 olkhovatka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=olkhovatka
    nioki
    Processing Record 211 nioki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nioki
    vryburg
    Processing Record 212 vryburg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vryburg
    yulara
    Processing Record 213 yulara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yulara
    bonnyville
    Processing Record 214 bonnyville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bonnyville
    tsihombe
    illoqqortoormiut
    sandwick
    Processing Record 215 sandwick http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sandwick
    oksovskiy
    Processing Record 216 oksovskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oksovskiy
    agadez
    Processing Record 217 agadez http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=agadez
    severo-kurilsk
    Processing Record 218 severo-kurilsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=severo-kurilsk
    luderitz
    Processing Record 219 luderitz http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=luderitz
    seymchan
    Processing Record 220 seymchan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=seymchan
    butaritari
    Processing Record 221 butaritari http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=butaritari
    port+moresby
    Processing Record 222 port moresby http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+moresby
    cayenne
    Processing Record 223 cayenne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cayenne
    ramona
    Processing Record 224 ramona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ramona
    alofi
    Processing Record 225 alofi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alofi
    cap+malheureux
    Processing Record 226 cap malheureux http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cap+malheureux
    sumbawa
    vahan
    Processing Record 227 vahan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vahan
    pangnirtung
    Processing Record 228 pangnirtung http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pangnirtung
    vaitupu
    coahuayana
    Processing Record 229 coahuayana http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coahuayana
    samusu
    natal
    Processing Record 230 natal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=natal
    mocuba
    Processing Record 231 mocuba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mocuba
    pemba
    Processing Record 232 pemba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pemba
    ancud
    Processing Record 233 ancud http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ancud
    kitami
    Processing Record 234 kitami http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kitami
    upernavik
    Processing Record 235 upernavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=upernavik
    san+benito+abad
    Processing Record 236 san benito abad http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+benito+abad
    moses+lake
    Processing Record 237 moses lake http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=moses+lake
    ketchikan
    Processing Record 238 ketchikan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ketchikan
    kruisfontein
    Processing Record 239 kruisfontein http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kruisfontein
    saint-louis
    Processing Record 240 saint-louis http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-louis
    nantucket
    Processing Record 241 nantucket http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nantucket
    hunza
    caucaia
    Processing Record 242 caucaia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=caucaia
    iqaluit
    Processing Record 243 iqaluit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=iqaluit
    hambantota
    Processing Record 244 hambantota http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hambantota
    natalinsk
    rio+grande
    Processing Record 245 rio grande http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rio+grande
    yuzhou
    Processing Record 246 yuzhou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yuzhou
    airai
    Processing Record 247 airai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=airai
    miri
    Processing Record 248 miri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miri
    marystown
    Processing Record 249 marystown http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marystown
    nan
    Processing Record 250 nan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nan
    kirkwall
    Processing Record 251 kirkwall http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kirkwall
    harper
    Processing Record 252 harper http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=harper
    paris
    Processing Record 253 paris http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=paris
    salalah
    Processing Record 254 salalah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=salalah
    aldan
    Processing Record 255 aldan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aldan
    rawson
    Processing Record 256 rawson http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rawson
    new+norfolk
    Processing Record 257 new norfolk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=new+norfolk
    coquimbo
    Processing Record 258 coquimbo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coquimbo
    oranjestad
    Processing Record 259 oranjestad http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oranjestad
    kiunga
    Processing Record 260 kiunga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kiunga
    cabedelo
    Processing Record 261 cabedelo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cabedelo
    portland
    Processing Record 262 portland http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=portland
    harrisburg
    Processing Record 263 harrisburg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=harrisburg
    codrington
    Processing Record 264 codrington http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=codrington
    margate
    Processing Record 265 margate http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=margate
    husavik
    Processing Record 266 husavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=husavik
    adre
    Processing Record 267 adre http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=adre
    palmares+do+sul
    Processing Record 268 palmares do sul http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palmares+do+sul
    tonekabon
    Processing Record 269 tonekabon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tonekabon
    port+hedland
    Processing Record 270 port hedland http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+hedland
    jinka
    Processing Record 271 jinka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jinka
    tongren
    Processing Record 272 tongren http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tongren
    kavaratti
    Processing Record 273 kavaratti http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kavaratti
    ixtapa
    Processing Record 274 ixtapa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ixtapa
    marzuq
    Processing Record 275 marzuq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marzuq
    kyra
    oktyabrskiy
    Processing Record 276 oktyabrskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=oktyabrskiy
    rundu
    Processing Record 277 rundu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rundu
    praia+da+vitoria
    Processing Record 278 praia da vitoria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=praia+da+vitoria
    singaparna
    Processing Record 279 singaparna http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=singaparna
    egvekinot
    Processing Record 280 egvekinot http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=egvekinot
    zhytomyr
    Processing Record 281 zhytomyr http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zhytomyr
    itoman
    Processing Record 282 itoman http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=itoman
    lolua
    esmeraldas
    Processing Record 283 esmeraldas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=esmeraldas
    katsuura
    Processing Record 284 katsuura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katsuura
    lompoc
    Processing Record 285 lompoc http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lompoc
    torbay
    Processing Record 286 torbay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=torbay
    nikolskoye
    Processing Record 287 nikolskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nikolskoye
    beringovskiy
    Processing Record 288 beringovskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=beringovskiy
    bardiyah
    metkovic
    Processing Record 289 metkovic http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=metkovic
    padang
    Processing Record 290 padang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=padang
    grand-bourg
    Processing Record 291 grand-bourg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grand-bourg
    la+rioja
    Processing Record 292 la rioja http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+rioja
    hamilton
    Processing Record 293 hamilton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hamilton
    kuusamo
    Processing Record 294 kuusamo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kuusamo
    grand+river+south+east
    viedma
    Processing Record 295 viedma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=viedma
    duz
    huaicheng
    Processing Record 296 huaicheng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=huaicheng
    crab+hill
    puerto+madryn
    Processing Record 297 puerto madryn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+madryn
    kolobovo
    Processing Record 298 kolobovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kolobovo
    sagopshi
    Processing Record 299 sagopshi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sagopshi
    acapulco
    Processing Record 300 acapulco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=acapulco
    flinders
    Processing Record 301 flinders http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=flinders
    smidovich
    Processing Record 302 smidovich http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=smidovich
    belushya+guba
    belaya+gora
    Processing Record 303 belaya gora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=belaya+gora
    christchurch
    Processing Record 304 christchurch http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=christchurch
    thiers
    Processing Record 305 thiers http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thiers
    haines+junction
    Processing Record 306 haines junction http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=haines+junction
    shelburne
    Processing Record 307 shelburne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shelburne
    san+jose
    Processing Record 308 san jose http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+jose
    broome
    Processing Record 309 broome http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=broome
    miramar
    Processing Record 310 miramar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miramar
    praia
    Processing Record 311 praia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=praia
    ukiah
    Processing Record 312 ukiah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ukiah
    sibu
    Processing Record 313 sibu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sibu
    honningsvag
    Processing Record 314 honningsvag http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=honningsvag
    novobirilyussy
    Processing Record 315 novobirilyussy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=novobirilyussy
    saleaula
    mercedes
    Processing Record 316 mercedes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mercedes
    smirnykh
    Processing Record 317 smirnykh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=smirnykh
    amderma
    asau
    iracoubo
    Processing Record 318 iracoubo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=iracoubo
    kroya
    Processing Record 319 kroya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kroya
    narsaq
    Processing Record 320 narsaq http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=narsaq
    bonthe
    Processing Record 321 bonthe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bonthe
    kisangani
    Processing Record 322 kisangani http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kisangani
    kandrian
    Processing Record 323 kandrian http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kandrian
    zhaotong
    Processing Record 324 zhaotong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zhaotong
    placetas
    Processing Record 325 placetas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=placetas
    moree
    Processing Record 326 moree http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=moree
    banjar
    Processing Record 327 banjar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=banjar
    madang
    Processing Record 328 madang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=madang
    tuatapere
    Processing Record 329 tuatapere http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tuatapere
    mudgee
    Processing Record 330 mudgee http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mudgee
    marysville
    Processing Record 331 marysville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marysville
    terme
    Processing Record 332 terme http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=terme
    port+blair
    Processing Record 333 port blair http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+blair
    puerto+palomas
    Processing Record 334 puerto palomas http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+palomas
    west+bay
    Processing Record 335 west bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=west+bay
    kamenskoye
    sabla
    Processing Record 336 sabla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sabla
    sabha
    Processing Record 337 sabha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sabha
    rocha
    Processing Record 338 rocha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rocha
    mahibadhoo
    Processing Record 339 mahibadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mahibadhoo
    krasnoselkup
    elko
    Processing Record 340 elko http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=elko
    robertsport
    Processing Record 341 robertsport http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=robertsport
    nuuk
    Processing Record 342 nuuk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nuuk
    xiamen
    Processing Record 343 xiamen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=xiamen
    perpignan
    Processing Record 344 perpignan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=perpignan
    gewane
    Processing Record 345 gewane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gewane
    kigoma
    Processing Record 346 kigoma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kigoma
    vila+velha
    Processing Record 347 vila velha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila+velha
    doha
    Processing Record 348 doha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=doha
    tarm
    Processing Record 349 tarm http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tarm
    alugan
    Processing Record 350 alugan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alugan
    noshiro
    Processing Record 351 noshiro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=noshiro
    sunnyside
    Processing Record 352 sunnyside http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sunnyside
    grand+gaube
    Processing Record 353 grand gaube http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grand+gaube
    blacksburg
    Processing Record 354 blacksburg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=blacksburg
    saint+anthony
    Processing Record 355 saint anthony http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint+anthony
    duku
    Processing Record 356 duku http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=duku
    la+sarre
    Processing Record 357 la sarre http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+sarre
    uchiza
    Processing Record 358 uchiza http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=uchiza
    kuanshan
    kazalinsk
    touros
    Processing Record 359 touros http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=touros
    homer
    Processing Record 360 homer http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=homer
    verkh-usugli
    Processing Record 361 verkh-usugli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=verkh-usugli
    inhambane
    Processing Record 362 inhambane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=inhambane
    petropavlovsk-kamchatskiy
    Processing Record 363 petropavlovsk-kamchatskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=petropavlovsk-kamchatskiy
    nhulunbuy
    Processing Record 364 nhulunbuy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nhulunbuy
    urumqi
    berdigestyakh
    Processing Record 365 berdigestyakh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=berdigestyakh
    krasnoarmeysk
    Processing Record 366 krasnoarmeysk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=krasnoarmeysk
    montepuez
    Processing Record 367 montepuez http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=montepuez
    marathon
    Processing Record 368 marathon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marathon
    magalia
    Processing Record 369 magalia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=magalia
    menongue
    Processing Record 370 menongue http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=menongue
    tomohon
    Processing Record 371 tomohon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tomohon
    dembi+dolo
    Processing Record 372 dembi dolo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dembi+dolo
    half+moon+bay
    Processing Record 373 half moon bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=half+moon+bay
    sao+filipe
    Processing Record 374 sao filipe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+filipe
    moose+factory
    Processing Record 375 moose factory http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=moose+factory
    vung+tau
    Processing Record 376 vung tau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vung+tau
    gat
    Processing Record 377 gat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gat
    hovd
    Processing Record 378 hovd http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hovd
    orta+nova
    Processing Record 379 orta nova http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=orta+nova
    lavrentiya
    Processing Record 380 lavrentiya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lavrentiya
    klyuchi
    Processing Record 381 klyuchi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=klyuchi
    dubai
    Processing Record 382 dubai http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dubai
    kamenka
    Processing Record 383 kamenka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kamenka
    san+patricio
    Processing Record 384 san patricio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+patricio
    shenjiamen
    Processing Record 385 shenjiamen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shenjiamen
    buala
    Processing Record 386 buala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=buala
    mizpe+ramon
    bedford
    Processing Record 387 bedford http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bedford
    palafrugell
    Processing Record 388 palafrugell http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=palafrugell
    urengoy
    Processing Record 389 urengoy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=urengoy
    neryungri
    Processing Record 390 neryungri http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=neryungri
    cervo
    Processing Record 391 cervo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cervo
    maceio
    Processing Record 392 maceio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maceio
    blythe
    Processing Record 393 blythe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=blythe
    humboldt
    Processing Record 394 humboldt http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=humboldt
    shingu
    Processing Record 395 shingu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shingu
    faya
    Processing Record 396 faya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=faya
    necochea
    Processing Record 397 necochea http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=necochea
    yatou
    Processing Record 398 yatou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yatou
    springbok
    Processing Record 399 springbok http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=springbok
    sayaxche
    Processing Record 400 sayaxche http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sayaxche
    puerto+del+rosario
    Processing Record 401 puerto del rosario http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=puerto+del+rosario
    thinadhoo
    Processing Record 402 thinadhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thinadhoo
    uray
    Processing Record 403 uray http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=uray
    kibala
    Processing Record 404 kibala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kibala
    canavieiras
    Processing Record 405 canavieiras http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=canavieiras
    sao+joao+da+barra
    Processing Record 406 sao joao da barra http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+joao+da+barra
    mendahara
    la+peca
    Processing Record 407 la peca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+peca
    skalistyy
    rungata
    fairbanks
    Processing Record 408 fairbanks http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fairbanks
    ayame
    Processing Record 409 ayame http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ayame
    norrkoping
    Processing Record 410 norrkoping http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=norrkoping
    la+asuncion
    Processing Record 411 la asuncion http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=la+asuncion
    dicabisagan
    Processing Record 412 dicabisagan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dicabisagan
    mallama
    china
    Processing Record 413 china http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=china
    broken+hill
    Processing Record 414 broken hill http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=broken+hill
    boulder+city
    Processing Record 415 boulder city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=boulder+city
    korla
    monrovia
    Processing Record 416 monrovia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=monrovia
    santander
    Processing Record 417 santander http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santander
    siniscola
    Processing Record 418 siniscola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=siniscola
    mentok
    srednekolymsk
    Processing Record 419 srednekolymsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=srednekolymsk
    navabad
    vilhena
    Processing Record 420 vilhena http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vilhena
    gamboma
    Processing Record 421 gamboma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=gamboma
    polunochnoye
    Processing Record 422 polunochnoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=polunochnoye
    nara
    Processing Record 423 nara http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nara
    kamalpur
    Processing Record 424 kamalpur http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kamalpur
    inderborskiy
    nabire
    Processing Record 425 nabire http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nabire
    badou
    Processing Record 426 badou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=badou
    dhidhdhoo
    Processing Record 427 dhidhdhoo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dhidhdhoo
    pisco
    Processing Record 428 pisco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pisco
    uruzgan
    Processing Record 429 uruzgan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=uruzgan
    kampil
    Processing Record 430 kampil http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kampil
    kayerkan
    Processing Record 431 kayerkan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kayerkan
    martapura
    Processing Record 432 martapura http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=martapura
    ulladulla
    Processing Record 433 ulladulla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ulladulla
    lima
    Processing Record 434 lima http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lima
    banamba
    Processing Record 435 banamba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=banamba
    nuevo+casas+grandes
    Processing Record 436 nuevo casas grandes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nuevo+casas+grandes
    lasem
    Processing Record 437 lasem http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lasem
    kapit
    Processing Record 438 kapit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kapit
    silver+city
    Processing Record 439 silver city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=silver+city
    kachug
    Processing Record 440 kachug http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kachug
    mitsamiouli
    Processing Record 441 mitsamiouli http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mitsamiouli
    pevek
    Processing Record 442 pevek http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pevek
    vila+franca+do+campo
    Processing Record 443 vila franca do campo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila+franca+do+campo
    ijaki
    soyo
    Processing Record 444 soyo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=soyo
    bosaso
    Processing Record 445 bosaso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bosaso
    mackenzie
    Processing Record 446 mackenzie http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mackenzie
    huilong
    Processing Record 447 huilong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=huilong
    alice+springs
    Processing Record 448 alice springs http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alice+springs
    zhezkazgan
    Processing Record 449 zhezkazgan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zhezkazgan
    teofilo+otoni
    Processing Record 450 teofilo otoni http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=teofilo+otoni
    porbandar
    Processing Record 451 porbandar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=porbandar
    san+policarpo
    Processing Record 452 san policarpo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+policarpo
    miram+shah
    Processing Record 453 miram shah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=miram+shah
    saint-leu
    Processing Record 454 saint-leu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=saint-leu
    biloela
    Processing Record 455 biloela http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=biloela
    buraydah
    Processing Record 456 buraydah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=buraydah
    taunggyi
    Processing Record 457 taunggyi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=taunggyi
    paamiut
    Processing Record 458 paamiut http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=paamiut
    hibbing
    Processing Record 459 hibbing http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hibbing
    sovetskiy
    Processing Record 460 sovetskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sovetskiy
    hun
    Processing Record 461 hun http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hun
    tenkasi
    Processing Record 462 tenkasi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tenkasi
    cocobeach
    Processing Record 463 cocobeach http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cocobeach
    marrakesh
    Processing Record 464 marrakesh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marrakesh
    sorong
    Processing Record 465 sorong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sorong
    rio+verde+de+mato+grosso
    Processing Record 466 rio verde de mato grosso http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rio+verde+de+mato+grosso
    mons
    Processing Record 467 mons http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mons
    panalingaan
    Processing Record 468 panalingaan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=panalingaan
    bulawayo
    Processing Record 469 bulawayo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bulawayo
    roebourne
    Processing Record 470 roebourne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=roebourne
    tefe
    Processing Record 471 tefe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tefe
    wanning
    Processing Record 472 wanning http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wanning
    turukhansk
    Processing Record 473 turukhansk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=turukhansk
    chaumont
    Processing Record 474 chaumont http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chaumont
    skibbereen
    Processing Record 475 skibbereen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=skibbereen
    panjwin
    kaeo
    Processing Record 476 kaeo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kaeo
    killybegs
    Processing Record 477 killybegs http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=killybegs
    litovko
    Processing Record 478 litovko http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=litovko
    les+cayes
    Processing Record 479 les cayes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=les+cayes
    bud
    Processing Record 480 bud http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bud
    copala
    Processing Record 481 copala http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=copala
    byron+bay
    Processing Record 482 byron bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=byron+bay
    katihar
    Processing Record 483 katihar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katihar
    turbat
    Processing Record 484 turbat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=turbat
    karabuk
    Processing Record 485 karabuk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=karabuk
    okhotsk
    Processing Record 486 okhotsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=okhotsk
    pocone
    Processing Record 487 pocone http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pocone
    bolungarvik
    paracuru
    Processing Record 488 paracuru http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=paracuru
    adrar
    Processing Record 489 adrar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=adrar
    ostrovnoy
    Processing Record 490 ostrovnoy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ostrovnoy
    ankang
    Processing Record 491 ankang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ankang
    preobrazheniye
    Processing Record 492 preobrazheniye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=preobrazheniye
    colorado
    Processing Record 493 colorado http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=colorado
    bridlington
    Processing Record 494 bridlington http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bridlington
    kudat
    Processing Record 495 kudat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kudat
    sharjah
    Processing Record 496 sharjah http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sharjah
    jasper
    Processing Record 497 jasper http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jasper
    melville
    Processing Record 498 melville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=melville
    san+carlos+de+bariloche
    Processing Record 499 san carlos de bariloche http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+carlos+de+bariloche
    clyde+river
    Processing Record 500 clyde river http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=clyde+river
    juneau
    Processing Record 501 juneau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=juneau
    alexandria
    Processing Record 502 alexandria http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alexandria
    bandarbeyla
    Processing Record 503 bandarbeyla http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bandarbeyla
    diapaga
    Processing Record 504 diapaga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=diapaga
    mesyagutovo
    Processing Record 505 mesyagutovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mesyagutovo
    provideniya
    Processing Record 506 provideniya http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=provideniya
    severnyy
    ranong
    Processing Record 507 ranong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ranong
    san+ramon+de+la+nueva+oran
    Processing Record 508 san ramon de la nueva oran http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+ramon+de+la+nueva+oran
    tual
    Processing Record 509 tual http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tual
    brae
    Processing Record 510 brae http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=brae
    takoradi
    Processing Record 511 takoradi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=takoradi
    safwah
    parainen
    merritt
    Processing Record 512 merritt http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=merritt
    manggar
    Processing Record 513 manggar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=manggar
    dianopolis
    tazovskiy
    Processing Record 514 tazovskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tazovskiy
    axim
    Processing Record 515 axim http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=axim
    tarazona
    Processing Record 516 tarazona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tarazona
    general+teran
    Processing Record 517 general teran http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=general+teran
    nguiu
    hay+river
    Processing Record 518 hay river http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hay+river
    quatre+cocos
    Processing Record 519 quatre cocos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=quatre+cocos
    yemtsa
    Processing Record 520 yemtsa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yemtsa
    cururupu
    Processing Record 521 cururupu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cururupu
    katherine
    Processing Record 522 katherine http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katherine
    souris
    Processing Record 523 souris http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=souris
    andili
    Processing Record 524 andili http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=andili
    alpena
    Processing Record 525 alpena http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=alpena
    whitehorse
    Processing Record 526 whitehorse http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=whitehorse
    veinticinco+de+mayo
    Processing Record 527 veinticinco de mayo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=veinticinco+de+mayo
    berlevag
    Processing Record 528 berlevag http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=berlevag
    tecpan
    Processing Record 529 tecpan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tecpan
    galdar
    Processing Record 530 galdar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=galdar
    sao+miguel+do+araguaia
    Processing Record 531 sao miguel do araguaia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+miguel+do+araguaia
    shimoda
    Processing Record 532 shimoda http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shimoda
    viligili
    tikhvin
    Processing Record 533 tikhvin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tikhvin
    garango
    Processing Record 534 garango http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=garango
    sur
    Processing Record 535 sur http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sur
    biak
    Processing Record 536 biak http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=biak
    port+hardy
    Processing Record 537 port hardy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port+hardy
    san+luis
    Processing Record 538 san luis http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=san+luis
    kununurra
    Processing Record 539 kununurra http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kununurra
    beyneu
    Processing Record 540 beyneu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=beyneu
    paidha
    Processing Record 541 paidha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=paidha
    pailon
    Processing Record 542 pailon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pailon
    marigot
    Processing Record 543 marigot http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marigot
    porto+belo
    Processing Record 544 porto belo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=porto+belo
    maragogi
    Processing Record 545 maragogi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maragogi
    tabou
    Processing Record 546 tabou http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tabou
    atar
    Processing Record 547 atar http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=atar
    guiuan
    Processing Record 548 guiuan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=guiuan
    sao+paulo+de+olivenca
    Processing Record 549 sao paulo de olivenca http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sao+paulo+de+olivenca
    dukat
    Processing Record 550 dukat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dukat
    bosobolo
    Processing Record 551 bosobolo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bosobolo
    ust-kamchatsk
    macau
    Processing Record 552 macau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=macau
    guayaramerin
    Processing Record 553 guayaramerin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=guayaramerin
    piacabucu
    Processing Record 554 piacabucu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=piacabucu
    kahramanmaras
    Processing Record 555 kahramanmaras http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kahramanmaras
    karratha
    Processing Record 556 karratha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=karratha
    klaksvik
    Processing Record 557 klaksvik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=klaksvik
    pangoa
    Processing Record 558 pangoa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pangoa
    mehamn
    Processing Record 559 mehamn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mehamn
    baykit
    Processing Record 560 baykit http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=baykit
    kaihua
    Processing Record 561 kaihua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kaihua
    jidong
    Processing Record 562 jidong http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jidong
    chifeng
    Processing Record 563 chifeng http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chifeng
    villanueva
    Processing Record 564 villanueva http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=villanueva
    sinkat
    marcona
    desaguadero
    Processing Record 565 desaguadero http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=desaguadero
    vila
    Processing Record 566 vila http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vila
    verkhovazhye
    Processing Record 567 verkhovazhye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=verkhovazhye
    inta
    Processing Record 568 inta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=inta
    aginskoye
    Processing Record 569 aginskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aginskoye
    majene
    Processing Record 570 majene http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=majene
    zlobin
    Processing Record 571 zlobin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zlobin
    torrington
    Processing Record 572 torrington http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=torrington
    istok
    Processing Record 573 istok http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=istok
    umm+lajj
    Processing Record 574 umm lajj http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=umm+lajj
    charters+towers
    Processing Record 575 charters towers http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=charters+towers
    numbrecht
    Processing Record 576 numbrecht http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=numbrecht
    kahta
    Processing Record 577 kahta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kahta
    tilichiki
    Processing Record 578 tilichiki http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tilichiki
    jiexiu
    Processing Record 579 jiexiu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=jiexiu
    whitianga
    Processing Record 580 whitianga http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=whitianga
    kanigoro
    Processing Record 581 kanigoro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kanigoro
    katobu
    Processing Record 582 katobu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=katobu
    pereslavl-zalesskiy
    Processing Record 583 pereslavl-zalesskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pereslavl-zalesskiy
    chase
    Processing Record 584 chase http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chase
    zyryanka
    Processing Record 585 zyryanka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zyryanka
    verkhneye+dubrovo
    Processing Record 586 verkhneye dubrovo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=verkhneye+dubrovo
    champerico
    Processing Record 587 champerico http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=champerico
    amod
    Processing Record 588 amod http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=amod
    te+anau
    Processing Record 589 te anau http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=te+anau
    komsomolskiy
    Processing Record 590 komsomolskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=komsomolskiy
    tezu
    Processing Record 591 tezu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tezu
    falealupo
    kidal
    Processing Record 592 kidal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kidal
    dunedin
    Processing Record 593 dunedin http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dunedin
    arona
    Processing Record 594 arona http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arona
    banda+aceh
    Processing Record 595 banda aceh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=banda+aceh
    balkanabat
    Processing Record 596 balkanabat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=balkanabat
    port-gentil
    Processing Record 597 port-gentil http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=port-gentil
    hakui
    Processing Record 598 hakui http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hakui
    kongolo
    Processing Record 599 kongolo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kongolo
    guiberoua
    Processing Record 600 guiberoua http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=guiberoua
    chernolesskoye
    Processing Record 601 chernolesskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chernolesskoye
    camocim
    Processing Record 602 camocim http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=camocim
    ulagan
    Processing Record 603 ulagan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ulagan
    altamira
    Processing Record 604 altamira http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=altamira
    mayumba
    Processing Record 605 mayumba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mayumba
    bathsheba
    Processing Record 606 bathsheba http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bathsheba
    taltal
    Processing Record 607 taltal http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=taltal
    kieta
    Processing Record 608 kieta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kieta
    kano
    Processing Record 609 kano http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kano
    meadow+lake
    Processing Record 610 meadow lake http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=meadow+lake
    grindavik
    Processing Record 611 grindavik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=grindavik
    hsinchu
    Processing Record 612 hsinchu http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hsinchu
    makakilo+city
    Processing Record 613 makakilo city http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=makakilo+city
    norden
    Processing Record 614 norden http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=norden
    clonakilty
    Processing Record 615 clonakilty http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=clonakilty
    coracora
    Processing Record 616 coracora http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=coracora
    samalaeulu
    kyshtovka
    Processing Record 617 kyshtovka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kyshtovka
    greymouth
    Processing Record 618 greymouth http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=greymouth
    maryville
    Processing Record 619 maryville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=maryville
    bojnurd
    Processing Record 620 bojnurd http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bojnurd
    shiyan
    Processing Record 621 shiyan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=shiyan
    aljezur
    Processing Record 622 aljezur http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=aljezur
    nanga+eboko
    Processing Record 623 nanga eboko http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nanga+eboko
    general+pico
    Processing Record 624 general pico http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=general+pico
    hofn
    Processing Record 625 hofn http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hofn
    charleston
    Processing Record 626 charleston http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=charleston
    cruzeiro+do+sul
    Processing Record 627 cruzeiro do sul http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=cruzeiro+do+sul
    kampong+chhnang
    Processing Record 628 kampong chhnang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kampong+chhnang
    lethem
    Processing Record 629 lethem http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lethem
    hargeysa
    Processing Record 630 hargeysa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hargeysa
    emerald
    Processing Record 631 emerald http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=emerald
    lilongwe
    Processing Record 632 lilongwe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lilongwe
    deputatskiy
    Processing Record 633 deputatskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=deputatskiy
    new+bern
    Processing Record 634 new bern http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=new+bern
    pital
    Processing Record 635 pital http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pital
    north+bend
    Processing Record 636 north bend http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=north+bend
    lusambo
    Processing Record 637 lusambo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lusambo
    zacualpan
    Processing Record 638 zacualpan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zacualpan
    voznesenskoye
    Processing Record 639 voznesenskoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=voznesenskoye
    ofunato
    Processing Record 640 ofunato http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ofunato
    namie
    Processing Record 641 namie http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=namie
    maridi
    markova
    Processing Record 642 markova http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=markova
    manta
    Processing Record 643 manta http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=manta
    paka
    Processing Record 644 paka http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=paka
    araouane
    Processing Record 645 araouane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=araouane
    lanigan
    Processing Record 646 lanigan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lanigan
    nadym
    Processing Record 647 nadym http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nadym
    malakal
    wichita+falls
    Processing Record 648 wichita falls http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=wichita+falls
    mooresville
    Processing Record 649 mooresville http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mooresville
    volkhov
    Processing Record 650 volkhov http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=volkhov
    tarko-sale
    Processing Record 651 tarko-sale http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=tarko-sale
    guerrero+negro
    Processing Record 652 guerrero negro http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=guerrero+negro
    comodoro+rivadavia
    Processing Record 653 comodoro rivadavia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=comodoro+rivadavia
    bulgan
    Processing Record 654 bulgan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bulgan
    quelimane
    Processing Record 655 quelimane http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=quelimane
    ocos
    Processing Record 656 ocos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ocos
    rolim+de+moura
    irpa+irpa
    Processing Record 657 irpa irpa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=irpa+irpa
    nanortalik
    Processing Record 658 nanortalik http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nanortalik
    sainte-suzanne
    Processing Record 659 sainte-suzanne http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sainte-suzanne
    chanika
    Processing Record 660 chanika http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=chanika
    zemio
    Processing Record 661 zemio http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=zemio
    leningradskiy
    Processing Record 662 leningradskiy http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=leningradskiy
    dois+vizinhos
    Processing Record 663 dois vizinhos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dois+vizinhos
    mlonggo
    Processing Record 664 mlonggo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mlonggo
    kurilsk
    Processing Record 665 kurilsk http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kurilsk
    ginda
    Processing Record 666 ginda http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ginda
    okha
    Processing Record 667 okha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=okha
    vincennes
    Processing Record 668 vincennes http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vincennes
    vagamo
    Processing Record 669 vagamo http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=vagamo
    hanumangarh
    Processing Record 670 hanumangarh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hanumangarh
    fuengirola
    Processing Record 671 fuengirola http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fuengirola
    fernie
    Processing Record 672 fernie http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fernie
    beloha
    Processing Record 673 beloha http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=beloha
    hami
    Processing Record 674 hami http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hami
    elat
    Processing Record 675 elat http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=elat
    arbazh
    Processing Record 676 arbazh http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=arbazh
    sharan
    Processing Record 677 sharan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=sharan
    roald
    Processing Record 678 roald http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=roald
    lagos
    Processing Record 679 lagos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=lagos
    avrille
    Processing Record 680 avrille http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=avrille
    thunder+bay
    Processing Record 681 thunder bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=thunder+bay
    pacific+grove
    Processing Record 682 pacific grove http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=pacific+grove
    nizwa
    Processing Record 683 nizwa http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nizwa
    utiroa
    mozarlandia
    Processing Record 684 mozarlandia http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mozarlandia
    leiyang
    Processing Record 685 leiyang http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=leiyang
    richards+bay
    Processing Record 686 richards bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=richards+bay
    kutum
    Processing Record 687 kutum http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kutum
    santa+cruz
    Processing Record 688 santa cruz http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=santa+cruz
    marquette
    Processing Record 689 marquette http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=marquette
    yerbogachen
    Processing Record 690 yerbogachen http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=yerbogachen
    koungou
    peruibe
    Processing Record 691 peruibe http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=peruibe
    kharan
    Processing Record 692 kharan http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kharan
    chagda
    rovnoye
    Processing Record 693 rovnoye http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=rovnoye
    bad+lauterberg
    Processing Record 694 bad lauterberg http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=bad+lauterberg
    barao+de+melgaco
    Processing Record 695 barao de melgaco http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=barao+de+melgaco
    razole
    Processing Record 696 razole http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=razole
    nakonde
    Processing Record 697 nakonde http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=nakonde
    consett
    Processing Record 698 consett http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=consett
    hervey+bay
    Processing Record 699 hervey bay http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=hervey+bay
    dodoma
    Processing Record 700 dodoma http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=dodoma
    flin+flon
    Processing Record 701 flin flon http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=flin+flon
    ondjiva
    Processing Record 702 ondjiva http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=ondjiva
    kiama
    Processing Record 703 kiama http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=kiama
    castanos
    Processing Record 704 castanos http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=castanos
    fairview
    Processing Record 705 fairview http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=fairview
    stromness
    Processing Record 706 stromness http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=stromness
    southampton
    Processing Record 707 southampton http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=southampton
    mavrovi+anovi
    Processing Record 708 mavrovi anovi http://api.openweathermap.org/data/2.5/weather?appid=5bf423bd383fb0cb5155fc161cbe794f&units=imperial&q=mavrovi+anovi
    


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
      <td>yining</td>
      <td>0</td>
      <td>51</td>
      <td>29.04</td>
      <td>114.56</td>
      <td>74.92</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>1</th>
      <td>hobart</td>
      <td>75</td>
      <td>54</td>
      <td>-42.88</td>
      <td>147.33</td>
      <td>57.20</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>santa rosa</td>
      <td>12</td>
      <td>92</td>
      <td>-36.62</td>
      <td>-64.29</td>
      <td>62.55</td>
      <td>5.95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>puerto ayora</td>
      <td>0</td>
      <td>98</td>
      <td>-0.74</td>
      <td>-90.35</td>
      <td>75.64</td>
      <td>6.62</td>
    </tr>
    <tr>
      <th>4</th>
      <td>geraldton</td>
      <td>5</td>
      <td>44</td>
      <td>49.72</td>
      <td>-86.95</td>
      <td>37.40</td>
      <td>6.93</td>
    </tr>
  </tbody>
</table>
</div>




```python
weather_data.count()
```




    City           708
    Cloudiness     708
    Humidity       708
    Latitude       708
    Longitude      708
    Temperature    708
    Wind Speed     708
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
