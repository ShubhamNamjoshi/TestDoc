# Disease Resistant Plant Breeding


# Introduction

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

# How to play the game
We have 30 Healthy plants of which the 10 DD gene plants, 15 Dd gene plants, and 5 
dd gene plants. From these, we want to select plant parents to create as many 
surviving plants continuously across generations.

You have to select two plants for cross breeding, the goal is to score 100%.

## Game Rules
* If you score below 50% you lose the game and you have to restart.
* You have 3 generations to win the game.
* If you fail to win the game in 3 generations you lose, you can play again or you can use genetic testing tool.
* Using genetic testing tool you can see the plants type before selecting.



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

1. Classes used
1. Initialising the game
1. Using Mouse events
1. Calculating scores
1. Generating next level trees
1. Using generic testing tool


## 1.Classes used

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

## 2.Initialising the game

Main function is called to start the game 

```typescript
function main() {
    isGameStarted = true;
    setHightWIdth();
    drawTrees();
    generateTreeList();
    
    setTreeType();
    shuffleTree(); 
}
```
## functions in main

*  setHightWIdth() : to set the height,width of div containing trees 
```typescript
function setHightWIdth() {

    if (window.screen.width > 992) 
    {
        game.style.width = "70vw"
        game.style.height = "70vh"
    } else {
        game.style.width = "95vw"
        game.style.height = "70vh"
    }
}
```

* drawTrees():to display ther trees in div

    * firstly it sets the row and coloumn with respect to screen width, for big screens its 3 rows and 10 coloumns,for mobile devices its 5 rows and 6 coloumns, so total 30 trees we have to display. 

    * then loop runs for each row and second loop for coloumn adding each div for tree,leaf,tree type,3 half circles for soil dynamically in the document body.


*  generateTreeList(): it provids unique id for each div used to display tree type, and creates Tree class objects and store them in the list array.

```typescript
function generateTreeList() {
    list = document.querySelectorAll(".tree-container");

    var row = 1;
    var cols = 1

    for (var i = 0; i < list.length; i++) {
        let htmlClass = "plant_" + row + "_" + cols;
        let obj = document.querySelector("#" + htmlClass + " #stem");
        let tag_container: HTMLDivElement = <HTMLDivElement>document.getElementById("tag" + row + "_" + cols);
        treeObj = new Tree(new Point(list[i].getBoundingClientRect().x,
            list[i].getBoundingClientRect().y),
            list[i].getBoundingClientRect().width,
            list[i].getBoundingClientRect().height,
            obj,
            tag_container
        )
        treeList.push(treeObj);
        if (cols % totalCols == 0) {
            row++;
            cols = 0;
        }

        cols++;
    }
}

```

* setTreeType(): It is used to just initialising the tree types.

```typescript
function setTreeType() {
    treeList[0].type = "DD";
    treeList[1].type = "DD";
    treeList[2].type = "Dd";
    treeList[3].type = "Dd";
    treeList[4].type = "dd";
    treeList[5].type = "Dd";
    treeList[6].type = "Dd";
    treeList[7].type = "DD";
    treeList[8].type = "dd";
    treeList[9].type = "DD";
    treeList[10].type = "Dd";
    treeList[11].type = "dd";
    treeList[12].type = "Dd";
    treeList[13].type = "DD";
    treeList[14].type = "Dd";
    treeList[15].type = "DD";
    treeList[16].type = "Dd";
    treeList[17].type = "DD";
    treeList[18].type = "dd";
    treeList[19].type = "Dd";
    treeList[20].type = "dd";
    treeList[21].type = "DD";
    treeList[22].type = "Dd";
    treeList[23].type = "Dd";
    treeList[24].type = "DD";
    treeList[25].type = "Dd";
    treeList[26].type = "Dd";
    treeList[27].type = "Dd";
    treeList[28].type = "DD";
    treeList[29].type = "Dd";
}
```
* shuffleTree(): it shuffles the tree types using random number

```typescript
function shuffleTree() {
    for (let i = 0; i < treeList.length; i++) {
        let random: number = randomNumber(i, treeList.length - 1);

        let tmp = treeList[i].type;
        treeList[i].type = treeList[random].type;
        treeList[random].type = tmp;
    }

}
function randomNumber(min, max) { // min and max included 
    return Math.floor(Math.random() * (max - min + 1) + min)
}
```
## 3.Using mouse events

1. Mouse click:
if testing button is clicked and tools switch is checked and it must be mobile device

selected tree will display its type using tree classes writetype method and for other trees deselectTree method will be called.

``` typescript
if(isTestingBtnClicked &&screen.width<992 && toolSwitch.checked){
        for (var i = 0; i < list.length; i++) {
            if (!isTwoTreeSelected&&!treeList[i].isLocked && clickX >= treeList[i].pt.x && clickX <= (treeList[i].pt.x + treeList[i].width) && clickY >= treeList[i].pt.y && clickY <= (treeList[i].pt.y + treeList[i].height)) {
                treeList[i].writeType();
            }
            else if (!treeList[i].isLocked) {
                treeList[i].deselectTree();
            }
        }    
    }
```
if its not mobile device, it will check for each tree in the list if click is inside any tree it will get selected, if choisecount is 2 that means user has selected two trees for cross breeding that we have to generate the result.

```typescript
 for (var i = 0; i < list.length; i++) {
            if (!isTwoTreeSelected&&!treeList[i].isLocked && clickX >= treeList[i].pt.x && clickX <= (treeList[i].pt.x + treeList[i].width) && clickY >= treeList[i].pt.y && clickY <= (treeList[i].pt.y + treeList[i].height)) {
    
                userTrees[choiseCount++] = treeList[i];
                treeList[i].selectTree();
    
                if (choiseCount == 2) {
    
                    testingToolDivHint.style.display="none";
                    switchDiv.style.display="none";
                    if (isTestingBtnClicked)
                        isTestingBtnClicked = false;
    
                    isTwoTreeSelected=true;
    
                    generateCombination();
                    showResult();
                    showResultDescription();
    
                    choiseCount = 0;
                    genCount++;
                    if (score >= 50)
                        btnNextGen.style.display = "block";
                    else {
                        btnPlayAgain.style.display = "block";
                    }
                    if (score == 100) {
                        btnNextGen.style.display = "none";
                        btnPlayAgain.style.display = "block";
                    }
                }
            }
        }
```

if generation count is 4 then we have to stop the game user has reached maz=ximum genration, if user have lost the game, display respective buttons.

```typescript
if (genCount == 4 && score <= 99 && !isTestingBtnClicked) {
            btnNextGen.style.display = "none"
            btnTestingTool.style.display = "block"
            btnPlayAgain.style.display = "block"
    
        }
```

2. Mouse move

if it is not mobile device  and testing button is clicked then on mouse move testing tool should appear.

for each tree if mouse is inside any tree its type will be visible.

```typescript
 for (var i = 0; i < list.length; i++) {
            if (!treeList[i].isLocked && clickX >= treeList[i].pt.x && clickX <= (treeList[i].pt.x + treeList[i].width) && clickY >= treeList[i].pt.y && clickY <= (treeList[i].pt.y + treeList[i].height)) {

                treeList[i].writeType();

            }
            else if (!treeList[i].isLocked) {
                treeList[i].deselectTree();
            }
        }
```

## 4.Calculating scores

To calculate the score firstly we need to generate the combination with 2 selected trees.

generateCombinations() method is used for it.

firstly all possible combinations from 2 selected trees are stored in the combinationTrees array.

```typescript
  for (let i = 0; i < 2; i++) {
        for (let j = 0; j < 2; j++) {
            let result: string = userTrees[0].type.charAt(i) + userTrees[1].type.charAt(j);
            if (result == "dD")
                result = "Dd";
            combintionTrees.push(result);
        }
    }
```
Then resultString containing type and occurence percentage is calculated for each distinct element in combinationTrees array.
and distinct elemnt is pushed in the new array , distinctTypes.

before pushing in distincttypes array, we check if element is already present in the array or not, if occurence is 0 then it is not present in the array.
```typescript
    for (let i = 0; i < combintionTrees.length; i++) {

        let occurence = getOccurences(combintionTrees[i], distinctTypes);
        if (occurence == 0) { //is distinct element


            occurence = getOccurences(combintionTrees[i], combintionTrees);
            resultStrings.push(occurence * 25 + "%" + combintionTrees[i]);
            distinctTypes.push(combintionTrees[i]);
        }
    }
```
getOccurences() method returns the occurence of given type in available combinations list.


showResult() method calculates the score according to tree type and percentage,
if type is DD whole percentage is added to score 
if type is Dd half of its percentage is added and if type is dd no percentage is added.

```typescript
function showResult() {


    ddPercent = [];


    for (let i = 0; i < resultStrings.length; i++) {
        let percent = Number(resultStrings[i].substring(0, resultStrings[i].indexOf("%")));
        let type = resultStrings[i].substring(resultStrings[i].indexOf("%") + 1)

        ddPercent.push(percent + "% " + type);
        if (type == "DD") {
            score += percent;
        }
        else if (type == "Dd") {
            score += 0.5 * percent;
        }

    }
}
```

showResultDescription() function displays the message according to the percentage using its divs innerHTML attribute and making it visible.

According to result we have to set the button visibe, btnNextgen,btnPlayAgain.

## 5.  Generating next level trees

when clicing on Next Generation button these functions are getting called.

```typescript
btnNextGen.onclick = function () {
    deSelectTrees();
    isTestingBtnClicked = false;
    extractValue(ddPercent);
    resetValues();
    btnNextGen.style.display = "none";
    genLevel.innerHTML = "Generation Level: " + genCount;
    updatePoints();
}
```

Here deselectTrees() deselects both 2 selected trees to their default form.

extractValue function sets the percentage and type from string array containing both , to a map objact.


```typescript
function extractValue(arr1: string[]) {
    map = new Map<string, string>();
    for (var i = 0; i < arr1.length; i++) {
        var arr = arr1[i].split("% ");
        map.set(arr[1], arr[0]);
        tmp = arr[1];

    }

    generateNextGenerationTrees(map);

}
```
generateNextGenerationTrees() function sets the percentage of each type to their respective variables

```typescript
function generateNextGenerationTrees(map: Map<string, string>) {

    var dd: number
    var DD: number
    var Dd: number
    if (map.get("dd"))
        dd = parseInt(map.get("dd"))
    if (map.get("DD"))
        DD = parseInt(map.get("DD"))
    if (map.get("Dd"))
        Dd = parseInt(map.get("Dd"))

    setTypeAndValueOfTrees(dd, Dd, DD);
}

```
setTypeAndValueOfTrees() function calculates how many objacts of perticular trr type will be created according to their percentage.

```typescript

function setTypeAndValueOfTrees(dd = 0, Dd = 0, DD = 0) {
    var dd: number = dd != 0 ? ((treeList.length) * dd) / 100 : 0
    var Dd: number = Dd != 0 ? ((treeList.length) * Dd) / 100 : 0
    var DD: number = DD != 0 ? ((treeList.length) * DD) / 100 : 0
    if (dd.toString().includes(".") && Dd.toString().includes(".")) {
        dd = dd + 0.5
        Dd = Dd - 0.5
    } else if (dd.toString().includes(".") && DD.toString().includes(".")) {
        dd = dd + 0.5
        DD = DD - 0.5

    } else if (Dd.toString().includes(".") && DD.toString().includes(".")) {
        Dd = Dd + 0.5
        DD = DD - 0.5

    }

    generateArrayWithRandomNumber(dd, Dd, DD);
}

```

generateArrayWithRandomNumber()  function generates the calculates tree numbers according to their types.

```typescript
function generateArrayWithRandomNumber(dd: number, Dd: number, DD: number) {

    let AllTypes: string[] = ["dd", "Dd", "DD"];
    let ddCounter = 0, DDCounter = 0, DdCounter = 0;
    for (let i = 0; i < treeList.length; i++) {

        let random = randomNumber(0, AllTypes.length - 1);
        if (AllTypes[random] == "dd" && ddCounter < dd) {
            treeList[i].type = AllTypes[random];
            ddCounter++
        }
        else if (AllTypes[random] == "Dd" && DdCounter < Dd) {
            treeList[i].type = AllTypes[random];
            DdCounter++
        }
        else if (AllTypes[random] == "DD" && DDCounter < DD) {
            treeList[i].type = AllTypes[random];
            DDCounter++
        } else {
            i--;

        }
    }
    shuffleTree();
}

```

## 6.Using generic testing tool
After user can not win in 3 generations, When clicking on generic testing tool button we have to reset all variables to start the game with generation 1 with tool.

```typescript
btnTestingTool.onclick = function () {
    deSelectTrees();
    isTestingBtnClicked = true;
    choiseCount = 0;
    genCount = 1;
    setTreeType();
    shuffleTree();
    resetValues();
    
    btnPlayAgain.style.display = "none";
    btnTestingTool.style.display = "none";
    scoreDiv.style.display = "none";
    scoreImgDiv.style.display = "none";
    calMain.style.display = "none";
    genLevel.innerHTML = "Generation Level: " + genCount;
    testingToolDivHint.style.display="block";

    if(screen.width>992){
        testingToolDivHint.innerHTML="Generic testing tool is on, hover over plant to use it.";
        switchDiv.style.display="none";
        
    }
    else{
        switchDiv.style.display="flex";
        testingToolDivHint.innerHTML="Generic testing tool is on, click on plant to check its type.Turn off tool for selecting plant for cross breeding.";
    }
}
```

resetValues() functions resets all the required variables.

```typescript
function resetValues() {
    if (score < 50 || score == 100 || isTestingBtnClicked) {
        game_instruction.innerHTML = "We have 30 Healthy plants of which the 10 DD gene plants, 15 Dd gene plants, and 5" +
            "dd gene plants. From these, we want to select plant parents to create as many " +
            "surviving plants continuously across generations.<br><br>" +
            "In the first step select two parent plants for cross-breeding:";
    }
    choiseCount = 0;

    score = 0;
    ddPercent = [];
    resultStrings = [];
    userTrees = [];
    combintionTrees = [];
    isTwoTreeSelected=false;
    toolSwitch.checked=true;

    calMain.style.display = "none";
    document.getElementById("emoji").innerHTML = "";
    scoreDiv.style.display = "none";

}
```