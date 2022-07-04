# Disease Resistant Plant Breeding- Technical Documentation

# Documentation Contents


|-[Home](#home)  
    &emsp;&emsp;|- [Introduction](#introduction)  
|-[Get Started](#get-started)  
    &emsp;&emsp;|-[How to play the game](#how-to-play-the-game)  
    &emsp;&emsp;|-[Game Rules](#game-rules)  
|-[Technical Specifications](#technical-specification)  
    &emsp;&emsp;|-[Compilation commands](#compilation-command)  
|-[Develop](#develop)  
    &emsp;&emsp;|- [Directory structure of Game](#1-directory-structure-of-game)  
    &emsp;&emsp;|- [File name and its application](#2-file-name-and-its-application)  
    &emsp;&emsp;|- [Typescript Classes used](#3-typescript-classes-used)  
    &emsp;&emsp;|- [Initialising the game](#4initialising-the-game)  
    &emsp;&emsp;|- [Using Mouse events](#5using-mouse-events)  
    &emsp;&emsp;|- [Calculating scores](#6calculating-scores)  
    &emsp;&emsp;|- [Generating next level trees](#7-generating-next-level-trees)  
    &emsp;&emsp;|- [Using generic testing tool](#8using-generic-testing-tool)  
    |-[Performance of application](#performance-of-application)  
    &emsp;&emsp;|-[Heap storage used](#1heap-storage-used)  
    &emsp;&emsp;|-[Google Lighthouse analysis](#2google-lighthouse-analysis)  
    &emsp;&emsp;|-[CPU analysis while using simulation](#3cpu-analysis-while-using-simulation)  
    &emsp;&emsp;|-[Time taken by activities](#4time-taken-by-activites)



# Home

## Introduction

Plant breeding applies genetic principles to produce plants that are more useful to humans. This is 
accomplished by selecting plants found to be economically or aesthetically desirable, first by 
controlling the mating of selected individuals, and then by selecting certain individuals 
among the progeny. Such processes, repeated over many generations, can change the 
genetic makeup and value of a plant population far beyond the natural limits of previously 
existing populations.


> The goal is to effectively do the cross-breeding between the 
plants that will give rise to a complete disease resistant crop.
 
One way of increasing yield is to develop varieties resistant to diseases and insects. In 
many cases the development of resistant varieties has been the only practical method 
of pest control.

**In our game, farmers have two kinds of plant varieties, one that fights diseases better. 
The other varieties cannot fight. Scientists have found out that the genetic make-up of 
plant determines the ability of plants to fight diseases. If rice plants have at least one
copy of a gene called Disease Fighter (denoted as “D”) then those plants are the 
strongest – they fight diseases well. The non-disease fighter gene is denoted as “d”. 
Plants with both copies of “d”, the dd plants, cannot fight diseases well and are prone 
to dying more due to infections.** &nbsp;   
But outwardly, the DD, Dd and dd plants look all the 
same.

---

# Get Started
# How to play the game
We have 30 Healthy plants of which the 10 DD gene plants, 15 Dd gene plants, and 5 
dd gene plants. From these, we want to select plant parents to create as many 
surviving plants continuously across generations.

These are the survival chances of different plants

- DD : 100% 
- Dd : 50%
- dd : 0%

You have to select two plants for cross breeding, the goal is to score 100%.

After selecting two plants, you will see your score and if its below 100% then you will get your next generation crop, which is generated from cross breeding of your two selected plants from previous generation. 

For example, If you select Dd and Dd plants, next generation will have DD,Dd,Dd,dd plants,that is 25% DD,50% Dd and 25% dd plants.

# Game Rules
* you have to select two plants randomly for cross breeding per generation. 
* You can see the plant type only after selecting the plant.
* If you score below 50% you lose the game at any generation and you have to restart.
* You have 3 generations to win the game.
* If you fail to win the game in 3 generations you lose, you can play again or you can use genetic testing tool.
* Using genetic testing tool you can see the plants type before selecting.
---
# Technical Specification
# Compilation command
* Download node.js from here
https://nodejs.org/en/download/

* Install typescript using npn with this command

```
npm install typescript@latest -g 
```
We need to compile our typescript files into js files.
Open command prompt in game folder and run this command
It will compile the ts files in watch mode.
```
tsc -w
```
# Develop
# Frontend

## HTML divs
* Game instructions and generation level are displayed using this div 
```
<div class="instruction-main-container"> 
 ```
* trees are displayed using 
```
    <div class="game-container">
 ```
* Score is displayed in 
```
    <div class="score-container">
```
* score div also contains sub divs for
    1. Tool hint
    1. emojis
    1. score description
    1. score
    1. buttons

* We have 3 buttons 
    1. Next Generation
    1. Play Again
    1. Testing Tool


# Backend 
Backed for this application is built using typescript.

**This section is divided into the following parts**
1. Directory structure of Game
1. File name and its application
1. Classes used
1. Initialising the game
1. Using Mouse events
1. Calculating scores
1. Generating next level trees
1. Using generic testing tool

## 1. Directory structure of Game
```
|-Plant Game
    |-simulation
        |-css
        |-TS
        |-jS
    |-storyboard
```
## 2. File name and its application
1. index.html :- This html file is HomePage for game app.

1. style.css :- This css file contains all the necessary styles and animations used to design game.

1. Tree.ts :- This file contains Point and Tree classes used in game.

1. GameApp.ts :- This file is entrypoint of the game, it contains main functions like mouseevents,and functions used to start the game.

1. GameUtills.ts :- This file contains all the necessary utility functions required for the game.

## 3. Typescript classes used

    1. Point class

This class contains two parameters x,y to store x and y cordinates of document.

it has constructor and getter setter methods.


    2. Tree class
It contains parameters for tree points,tree height,width,type and boolean variable isLocked to check if tree is clicked or not and also two div elements to hold the tree and its type.

```typescript
    pt: Point;
    width: number;
    height: number;
    type: string;
    isLocked: boolean;
    obj: Element;
    tag: HTMLDivElement;
```

it contains following methods
* constructor: to initialise the parameters
* changePoints: to chamge the tree point to given point
* write type: to make the tree type div visible and to set its colour according to the type.
* isinside: to check if given point is inside the tree
* selectTree:when selected this method is called and set the islocked variable true, adds stem-out class to its div which starts the animation using css and to make the tree type visible.
* deselectTree: to change all settings back to default for the perticular tree.
* updateTree: Updates tree point,height,width.

## 4.Initialising the game

Main function is called to start the game 

```typescript
function main()
```
## functions in main

|No.    | Function      |  
|-------|:--------------|
|1      | [setHightWidth](#function-sethightwidth) |
|2      | [drawTrees](#function-drawtrees)     |
|3      | [generateTreeList](#function-generatetreelist) |
|4      | [setTreeType](#function-settreetype) |
|5      | [shuffleTree](#function-shuffletree) |
|6      | [randomNumber](#function-randomnumbermin-max) |

### function setHightWidth()
 
* to set the height,width of div containing trees 

### function drawTrees()

* to display the trees in div

    * firstly it sets the row and coloumn with respect to screen width, for big screens its 3 rows and 10 coloumns,for mobile devices its 5 rows and 6 coloumns, so total 30 trees we have to display. 

    * then loop runs for each row and second loop for coloumn adding each div for tree,leaf,tree type,3 half circles for soil dynamically in the document body.



### function generateTreeList()

*  it provids unique id for each div used to display tree type, and creates Tree class objects and store them in the list array.

### function setTreeType() 

* It is used to initialising the tree types.

### function shuffleTree()

* it shuffles the tree types using random number

### function randomNumber(min, max)

* It generates random number between min and max values.

## 5.Using mouse events

1. Mouse click:

if testing tool button is clicked and tools switch is checked and it must be mobile device

selected tree will display its type using tree classes writetype method and for other trees deselectTree method will be called.


if its not mobile device, it will check for each tree in the list if click is inside any tree it will get selected, if choisecount is 2 that means user has selected two trees for cross breeding that we have to generate the result.

if generation count is 4 then we have to stop the game user has reached maximum genration, if user have lost the game, display respective buttons.


2. Mouse move

if it is not mobile device and testing tool button is clicked then on mouse move testing tool should appear.

for each tree if mouse is inside any tree its type will be visible.


## 6.Calculating scores

To calculate the score firstly we need to generate the combination with 2 selected trees.

generateCombinations() method is used for it.

firstly all possible combinations from 2 selected trees are stored in the combinationTrees array.

Then resultString containing type and occurence percentage is calculated for each distinct element in combinationTrees array.
and distinct elemnt is pushed in the new array , distinctTypes.

before pushing in distincttypes array, we check if element is already present in the array or not, if occurence is 0 then it is not present in the array.

getOccurences() method returns the occurence of given type in available combinations list.

showResult() method calculates the score according to tree type and percentage,
if type is DD whole percentage is added to score 
if type is Dd half of its percentage is added and if type is dd no percentage is added.

showResultDescription() function displays the message according to the percentage using its divs innerHTML attribute and making it visible.

According to result we have to set the button visibe, btnNextgen,btnPlayAgain.

## 7.  Generating next level trees

when clicing on Next Generation button these functions are getting called.


Here deselectTrees() deselects both 2 selected trees to their default form.

extractValue function sets the percentage and type from string array containing both , to a map objact.


generateNextGenerationTrees() function sets the percentage of each type to their respective variables

setTypeAndValueOfTrees() function calculates how many objacts of perticular trr type will be created according to their percentage.
generateArrayWithRandomNumber()  function generates the calculates tree numbers according to their types.

## 8.Using generic testing tool
After user can not win in 3 generations, When clicking on generic testing tool button we have to reset all variables to start the game with generation 1 with tool.


resetValues() functions resets all the required variables.

# Performance of application

## 1.Heap storage used

Using "flame Chart Visualizer For Javascript profiles" extension in visual studio code IDE it was recorded that application is using 42 MB of heap storage.  

## 2.Google Lighthouse analysis

![Lighthouse result](/documentation/images/Lighthouse%20report.png)

## 3.CPU analysis while using simulation
![CPU Analysis](/documentation/images/cpu%20analysis%20while%20using%20simulation.png)

## 4.Time taken by activites

![Time Taken](/documentation/images/Time%20taken%20by%20activites.png)