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

The first thing I did was creating a sock class and initializing variables for the csv file based on what the api gives us. 

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
```
Then I made a string method as shown above and defined a csv to sock which converts a single line of sock into a sock object and then I split single line of csv into individual cells as well as making associative dictionary lines where names are keys to columns as shown below. 
```python
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

def dicttosock(csvdict): 
    name = csvdict["Name"]
    variation = csvdict["Variation"]
    diy = csvdict["DIY"]
    buy = csvdict["Buy"]
    sell = csvdict["Sell"]
    color1 = csvdict["Color 1"]
    color2 = csvdict["Color 2"]
    size = csvdict["Size"]
    miles_price = csvdict["Miles Price"]
    source = csvdict["Source"]
    source_notes = csvdict["Source Notes"]
    seasonal_availability = csvdict["Seasonal Availability"]
    mannequin_piece = csvdict["Mannequin Piece"]
    version = csvdict["Version"]
    style = csvdict["Style"]
    label_themes = csvdict["Label Themes"]
    villager_equippable = csvdict["Villager Equippable"]
    catalog = csvdict["Catalog"]
    filename = csvdict["Filename"]
    internalid = csvdict["Internal ID"]
    uniqueentryid = csvdict["Unique Entry ID"]
    return Sock(name,variation,diy,buy,sell,color1,color2,size,miles_price,source,source_notes,seasonal_availability,mannequin_piece,version,style,label_themes,villager_equippable,catalog,filename,internalid,uniqueentryid)
```

After this, I imported this file into another python file and created a list of socks found on the api. I took the api and found the limit of how far it goes (it went all the way to 351 lines). Then I wrote that information into the csv file using f.write. 
```python
import requests 
from Thesocks import *

socks = [] 
url = "https://hm-cs.herokuapp.com/socks/?key=ArtOfDataKEY123&idx=" 
nextIndex = 1
hasmore = True
while hasmore: 
    response = requests.get(url + str(nextIndex)) 
    data = response.text
    s = csvtosock(data)
    if s == None:
        hasmore = False
    else:
        socks.append(s) 
        nextIndex = nextIndex + 1

with open("./AnimalCrossingSheet.csv", "w") as f:
    f.write ("Name,Variation,DIY,Buy,Sell,Color 1,Color 2,Size,Miles Price,Source,Source Notes,Seasonal Availability,Mannequin Piece,Version,Style,Label Themes,Villager Equippable,Catalog,Filename,Internal ID,Unique Entry ID\n")
    for s in socks:
        f.write(str(s) + "\n") 
```

Then, I had to answer two questions. How many socks of each color there are and Which socks had the most variations. The first thing I did was create a list of sock objects in csv file. Then, by sock name, list of all variations and then by color, list of all sock names that have that color. I then got variables from the sock object and made an if statement. This said if a new sock name is found then prepare empty list for the variations and then append this variation to the socks list of variation. I then found the list of things with the most variations and saw how many variations those things have. Afterwards, I made a forloop where if this is more than we've seen, then clear the list. Otherwise if it finds one that ties with the prev sock, then append it to the list and then print. 

```python
import csv
from Thesocks import *
socks = [] 
with open("./AnimalCrossingSheet.csv", "r") as f:  
    data = list(csv.DictReader(f)) 
    for item in data:
        s = dicttosock(item)
        socks.append(s)
    
variations = dict() 
colors = dict() 
for s in socks: 
    name = s.name 
    variation = s.variation
    color_1 = s.color1
    color_2 = s.color2
    if not name in variations: 
        variations[name] = [] 
    variations[name].append(variations) 
    if not color_1 in colors:
        colors[color_1] = []
    colors[color_1].append(name)
    if color_1 != color_2:
        if not color_2 in colors:
            colors[color_2] = []
        colors[color_2].append(name)

mostvar = [] 
mostvarcount = 0 
for var in variations:
    vars = len(variations[var]) 
    if vars > mostvarcount: 
        mostvar = [] 
        mostvar.append(var) 
        mostvarcount = vars 
    elif vars == mostvarcount: 
        mostvar.append(var)
print(mostvar, mostvarcount)

for color in colors:
    print(color,len(colors[color]))
```

The answers that I got for the different variations are 
argyle crew socks 
color-blocked socks
frilly knee-high socks
holey tights
kiddie socks
mixed-tweed socks
no-show socks
semi-opaque socks
semi-opaque tights
sequin leggings
simple-accent socks
striped socks
striped tights
tube socks
ultra no-show socks
vivid leggings
vivid socks
vivid tights
                all have 8 variations to them
       
As for how many socks for each color there are, the answers that I found are: 

| Color |  number |
| :------ |:--- | 
|Pink | 41 |
|Red  |39 |
|Green | 50 |
|Light blue  |33 |
|Orange |27 |
|Purple| 37 |
|Blue |47 |
|Yellow| 33 |
|Beige |15 |
|White |85 |
|Black |59 |
|Brown |11 |
|Gray |31 |
|Colorful |14 |



