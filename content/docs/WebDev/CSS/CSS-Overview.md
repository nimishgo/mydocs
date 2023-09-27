---
title: "CSS Intro"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# CSS Refresher



Every CSS starts with a selector for eg. `h1` here

followed by `{}` which has css declaration as

`property : values`



```css
h1 /*css type(h1) selector*/ {
    /* css declaration box*/
    color : red;
}
```



### Universal selector `*` 

```css
* { 
    
}
```

similarly : 

class selector `.[className] ` selects class

id selector `#idName ` selects id



### attribute selector :  

for eg we have a element with element attribute

`data-name = "name"`

in css we will do 

```css
[data-name='name'] {
    color : blue;
}
```

copy the attribute and place it in square brackets.



## Specificity

* !important rules over every selector
* inline css 
* id `1 0 0 ` // number of id’s
* class `0 1 0` // number of classes
* elements `0 0 1` // number of elements

**CSS** is acronym for cascading style sheet when style conflicts it will look at specificity if its same then it will look for the last source or bottom of the cascade.



## CSS with inheritance

for list if we color `ul` it will affect all li’s color font font family can be inherited accept width height margin & padding.



* `:inherit` : color/property value passed by parent element.
* `:initial`  : sets properties to browser default style

## CSS Devtools

![Layout of the inspect option](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1550792075/transcript-images/debug-css-with-the-chrome-devtools-inspect-option.jpg)



![Adding styles to our a tag](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1550792076/transcript-images/debug-css-with-the-chrome-devtools-a-tag.jpg)



![Manually adding padding](https://res.cloudinary.com/dg3gyk0gu/image/upload/v1550792077/transcript-images/debug-css-with-the-chrome-devtools-padding.jpg)



## Box Model

* margin
  * border
    * padding
      * content

`box-sizing : border-box` : makes the height and width to include padding and border.

Default is `content-box` content has the given height and width.

This styles only applies when display is block. When set to Inline height and width is ignored.



```css
h1 {
    font-size : 30px; /*200% 32 px is font size of default is 16px*/
    padding: 2em; /* 60 px*/
    
}
```



* px : are absolute units
* em : relative to the given font size;
* rem : relative to the default root font size
* 100% : same as default if 200% 2x that of default.

### Colors

	* color : #ff0000     (r , g , b) where they are in hex from 0 to f
	* rgb : (255, 0 , 0) same r , g and b where each value is from 0 to 255

 * hsl : (0, 100% , 50%)   
   * First value hue is color its from 0  to 360.   
   * 2nd value is saturation from gray to complete colors
   * 3rd value is lightness dark to light



### Background

`background` is a short code, we can specify image , color , position , size (cover) , repeat no repeat . 

background attachment.

```css
.class {
    background : radial-gradient(crimson, blue) fixed; /* with fixed it will remain at center*/
}
```



## Hide and show html element using css

Opacity is helpful in transition and animation.

```css
h1 {
    opacity : 0; /* dissapears but occupies the space*/
}

/* lets add a class to add transition */
h1.transition {
    transition : 1s; /* when we toggle it it appears and dissapears in 1sec*/
    opacity : 1;
    visibility : hidden; /* difference no inbetween option transition doesnt work*/
    display : none /*completely hides it and take up no space*/
}
```



## Psuedo-classes

A CSS pseudo-class is a keyword added to a selector that specifies a specific state of the selected element. As the name suggests, and as we saw, when this selector enters a state, all of the styles within this block will apply to the selector. `:hover` : `nth-child `, `:first-child `, `:focus` 



## Position 

`Relative` : Element original position will be in flow of document. 

Relative positioning allows you to position an element relative to its normal position on the page. When an element is set to `position: relative;`, you can then use properties like `top`, `right`, `bottom`, and `left` to offset it from its default position.

The `.relative-element` also has relative positioning, which means that the `top` and `left` properties will move it 20 pixels down and 30 pixels to the right from its normal position inside the container.

`Absolute ` :  we can move but it will not break flow of page. It will be in flow of parent element.

`fixed` : always relative to document and scrolling doesn’t effect it.



## Media Queries

```css
@media (max-width : 750px) {
    /* if the style goes below 750 */
}

@media (min-width : 750px) {
    /* if the style goes above 750 */
}
```



## CSS Variables

We can declare them in root it has higher specificity than html tag.

```css
:root {
    --main : red;
    --base : blue;
}

.title {
    color : var(--main);
}
```



We can change this variables using js 

```js
const h1 = document.querySelector('.title');
console.log(getComputedStyle(h1).getPropertyValye('--main'));
// we have an onClick property which will change the variable size
function enlarge() {
    document.documentElement.style.setProperty('--size','50px');
}
```



















