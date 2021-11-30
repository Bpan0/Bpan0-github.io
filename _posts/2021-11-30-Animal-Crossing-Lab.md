---
layout: post
title: Animal Crossing Lab
subtitle: By Bulyn Panjamapirom
cover-img: /assets/img/Animal_Crossing_New_Horizons_Isabelle.jpeg
thumbnail-img: /assets/img/A49SHvJd5XCM7qBAqfRDYn-1200-80.jpeg
share-img: /assets/img/1280x720.jpeg
tags: [AnimalCrossing]
---
## Animal Crossing Lab
Collaborators: Darson Chen, Tuhin Ghosh, Elias Romero

![AnimalCrossing](https://assets.nintendo.com/image/upload/f_auto,q_auto/v1634304356/Nintendo%20Direct/2021/10-15-2021/aw7f2jh5/posters/ACNH-happy-home-paradise.jpg)

In this Lab, I converted an API into a CSV file and then took information from that to answer what different variations there are and the different colors. 

The first thing I did was converting the API into a CSV file. 

```python
class Sock:
    def __init__ (self,name,variation,diy,buy,sell,color1,color2,size,miles_price,source,source_notes,seasonal_availability,mannequin_piece,version,style,label_themes,villager_equippable,catalog,filename,internalid,uniqueentryid ):
        self.name = name
        self.variation = variation
        self.diy = diy
        self.buy = buy
        self.sell = sell
        self.color1 = color1
        self.color2 = color2
        self.size = size
        self.miles_price = miles_price
        self.source = source
        self.source_notes = source_notes
        self.seasonal_availability = seasonal_availability
        self.mannequin_piece = mannequin_piece
        self.version = version
        self.style = style
        self.label_themes = label_themes
        self.villager_equippable = villager_equippable
        self.catalog = catalog
        self.filename = filename
        self.internalid = internalid
        self.uniqueentryid = uniqueentryid

    def __str__ (self):
        return f"{self.name},{self.variation},{self.diy},{self.buy},{self.sell},{self.color1},{self.color2},{self.size},{self.miles_price},{self.source},{self.source_notes},{self.seasonal_availability},{self.mannequin_piece},{self.version},{self.style},{self.label_themes},{self.villager_equippable},{self.catalog},{self.filename},{self.internalid},{self.uniqueentryid}"

def csvtosock(csvline):
    parts = csvline.split(",")
    if len(parts) <= 1:
        return None
    name = parts[0]
    variation = parts[1]
    diy = parts[2]
    buy = parts[3]
    sell = parts[4]
    color1 = parts[5]
    color2 = parts[6]
    size = parts[7]
    miles_price = parts[8]
    source = parts[9]
    source_notes = parts[10]
    seasonal_availability = parts[11]
    mannequin_piece = parts[12]
    version = parts[13]
    style = parts[14]
    label_themes = parts[15]
    villager_equippable = parts[16]
    catalog = parts[17]
    filename = parts[18]
    internalid = parts[19]
    uniqueentryid = parts[20]
    return Sock(name,variation,diy,buy,sell,color1,color2,size,miles_price,source,source_notes,seasonal_availability,mannequin_piece,version,style,label_themes,villager_equippable,catalog,filename,internalid,uniqueentryid)
```
I made a Sock class in which I defined each list in dictionaries. I then took those those dictionaries from API's and then converted them into a CSV file. 

```python
import requests
from Socks import *

socks = []
url = "https://hm-cs.herokuapp.com/socks/?key=ArtOfDataKEY123&idx=" 
nextIndex = 1
while True: 
    response = requests.get(url + str(nextIndex)) 
    data = response.text
    s = csvtosock(data)
    if s == None:
        break
    socks.append(s) 
    nextIndex = nextIndex + 1

with open("./AnimalCrossingSheet.csv", "w") as f:
    f.write ("Name,Variation,DIY,Buy,Sell,Color 1,Color 2,Size,Miles Price,Source,Source Notes,Seasonal Availability,Mannequin Piece,Version,Style,Label Themes,Villager Equippable,Catalog,Filename,Internal ID,Unique Entry ID\n")
    for s in socks:
        f.write(str(s) + "\n")
```
