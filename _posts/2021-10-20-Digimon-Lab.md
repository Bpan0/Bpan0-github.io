---
layout: post
title: Lab 1: Digimon
subtitle: By Bulyn Panjamapirom
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [digimon]
---

Digimon Lab

Collaborators: Tuhin Ghosh, Darson Chen, Justin Gurvitch, Elias Romero, Mr. Lee.

In this lab, we answered a series of questions related lists of dictionaries in a csv file. 

The first problem I solved was finding the top 3 digimon with the most HP. In order to do this, I sorted the HP of all digimon from descending order. Then, I assigned the digimon name to the top 3 most HP inorder to solve the problem. 

```python
SortedDigimon = sorted (DigimonHP,reverse = True) #sorts the digimon HP in terms of descending order
Digimon1 = SortedDigimon[0]
Digimon2 = SortedDigimon[1] 
Digimon3 = SortedDigimon[2] 
Digimon1_name = DigimonHP[Digimon1]
Digimon2_name = DigimonHP[Digimon2] 
Digimon3_name = DigimonHP[Digimon3] 
```

Finding the average speed was pretty easy for me. All we had to do was take the total speed of all the digimon and divide it by the number of digimon present and we would get the average speed. 

```python
for Digimon in data: 
    DigimonSum += int(Digimon["Spd"]) 
    DigimonCounter += 1 
AverageSpeed = DigimonSum/DigimonCounter 
```
The first thing I thought of when finding a function that can count the number of Digimon with a specific attribute was to create a count_digimon function. Like the previeous problem, I also found this pretty easy. The code that we did from a previeous assignment allowed me to make a starting counter and add a counter to the attribute. 

```python
def count_digimon(header, attribute): 
    Digimoncounter = 0 
    for Digimon in data: 
        if Digimon[header] == attribute: 
            Digimoncounter = Digimoncounter + 1 
```

The final question asks to make a team of 3 digimon with to 15 memory and over 300 attack in total. I got to the answer of Flamdramon, Wormmon, and Tsumemon. Out of the three questions, I thought this one was the most complicated for me. I started by preparing a list for the group then sorting it by comparing the digimon against eachother. I compared it so that it whould have at least 15 memory and greater than 300 attack. 

```

winner = [] 
for Digimon1 in data: 
    for Digimon2 in data:
        for Digimon3 in data: 
            if Digimon1 != Digimon2 and Digimon2 != Digimon3 and Digimon1 != Digimon3: 
                if int(Digimon1["Memory"]) + int(Digimon2["Memory"]) + int(Digimon3["Memory"]) <= 15: 
                    if int(Digimon1["Atk"]) + int(Digimon2["Atk"]) + int(Digimon3["Atk"]) >= 300: #and attack adds up to more than 300
                        winner = [Digimon1, Digimon2, Digimon3] #the winning group
                        
```

