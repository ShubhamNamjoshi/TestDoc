# Disease Resistant Plant Breeding- Approach used 

We have used HTML,CSS  to draw the plants on screen.&nbsp;  
To draw the plants dynamiccally and to show the animation when user clicks on the plant, we have used Typescript.


To draw one tree, we have used different div tags with class name for these functionalities
 
1. tree-container: To hold all the divs used for a tree.
1. stem: To hold these divs used to draw left,right,top leaves and plant stem
    1. left-leaf-container: to hold 6 divs that draws left side leaves
    1. right-leaf-container: to hold 6 divs that draws right side leaves
    1. top: to set position of one leaf at top.
    1. leaf: to draw single leaf.
1. soil: to hold 3 divs that draws half circles to display plant soil.
1. tag-container: div to display plant type below the plant.

## These css are applied to above classes

```css
.tree-container {
    position: relative;
    box-sizing: border-box;
    cursor: pointer;
    border: none;
    display: flex;
    flex-direction: column;
    overflow: hidden; 
}
```

```css
.stem {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: flex-end; 
    background-color: transparent;  
}
```

### This class is added to div dynamically to start the animation.
```css
.stem-out {
 animation: blink 1s infinite ease-in-out alternate;  
}
```
```css
@keyframes blink {
    0% {
        transform: scale(1);
    }
    100% {
        transform: scale(1.2);
    }
}
```
### To draw a single leaf.
```css
.leaf {
    
    background: green;
    border-radius: 100% 0%;
    z-index: -1;
}
```
```css
.left-leaf-container .leaf {
    transform: translate(20%, var(--p)) rotate(-180deg);
}
```
```css
.right-leaf-container .leaf {
    
    transform: translate(-20%, -100%);
}
```
```css

.left-leaf-container {
    transform: rotateX(-180deg);
}
```
### To draw soil of plant
```css
.soil {
    position: relative;
    width: 100%;
    background: transparent;
}

```
```css
.half-circle1 {
    position: absolute;
    background: #743e0c;
    width: 30%;
    height: 40%;
    top: 60%;
    border-top-left-radius: 100%;
    border-top-right-radius: 100%;
}
```
```css
.half-circle2 {
    position: absolute;
    background: #743e0c;
    width: 60%;
    height: 75%;
    top: 25%;
    left: 20%;
    border-top-left-radius: 100%;
    border-top-right-radius: 100%;
}
```
```css
.half-circle3 {
    position: absolute;
    width: 45%;
    background: #743e0c;
    height: 60%;
    top: 40%;
    left: 55%;
    border-top-left-radius: 100%;
    border-top-right-radius: 100%;
}
```
