---
layout: post
title: Lab 1: Digimon
subtitle: By Bulyn Panjamapirom
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [digimon]
---

Collaborators: Tuhin Ghosh, Darson Chen, Justin Gurvitch, Elias Romero, Mr. Lee.

What we did in this lab is answering a series of questions related lists of dictionaries in a csv file. 

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

Finding the average speed was pretty easy. All we had to do was take the total speed of all the digimon and divide it by the number of digimon present.

```python
for Digimon in data: 
    DigimonSum += int(Digimon["Spd"]) 
    DigimonCounter += 1 
AverageSpeed = DigimonSum/DigimonCounter 
```



1. What is the average speed (Spd) of all Digimon?
The average Speed of all Digimon is 120.4. 

2. Write a function that can count the number of Digimon with a specific attribute. For example, count_digimon("Type", "Vaccine") would return 70.


3. The Digimon on your team are restricted by the total amount of Memory that they need. If your team only has 15 Memory, name a team of up to 3 Digimon that has at least 300 attack (Atk) in total.
Flamdramon, Wormmon, Tsumemon
