# CSS

<img src="https://upload.wikimedia.org/wikipedia/commons/d/d5/CSS3_logo_and_wordmark.svg" width="128px">
## CSS Selector Format

```css
a {
  background-color: yellow;
}
```

- selector: The tag class or ID that you are trying to style (a)
- property: the property that you want to change (background-color)
- value: the value you want to change the property to (yellow)

## Implementing CSS

1. Inline CSS -- Use the style attribute to style a single tag in an HTML document
2. Internal CSS -- Style tag inside the head section -- only applies to the current HTML document
3. External CSS -- A seperate file that can be included into multiple documents to give a common style to all documents `<link rel="stylesheet" href="css/style.css">`

## Selectors

- tag -- the html tag that you want to target. Applies to all tags of that type in the document unless overridden by a class, id or cascading. Target by using the tag without the <>.
- id -- An attribute that can be added to a tag. There can multiple ids in a document, but only one tag with that specific name. Use the '#' to target
- class -- An attribute that can be added to one or more tags. The same class can apply to different types of tags and it will modify the same properties for each tag. Use the '.' to target.
- Target multiple selectors by seperating them with a comma
- Target nested selectors by sperating the elements with a space from parent to child

## Fonts

1. font-family: specify a list of fonts for the browser to try to use, browser will try from left to right until it finds one that it can use.
2. font-size: specifies the size of the font. The default is 16px.
3. line-height: specifies the height of each line. specified in em units
4. font-weight: the lightness or heavyness of the font on the screen

CSS Units

- pixels: (px) 1/96th inch
- em: 1em is the font size for the parent element; The number is a multplier of that value
- rem: 1rem is the font size of the root element; The number is a multiplier of that value
- vw: 1% of the viewport width
- vh: 1% of the viewport height

## Color Types

1. named: a named color such as red, white, coral aliceblue
2. rgb: rgb(0,0,0) comma separted list of red green blue values
3. rgba: same as rgb with alpha (transparency)
4. hex: 6 hex characters that represent red green blue value. specify shades of grey by using 3 hex characters

## Backgrounds and Borders

1. background-color: changes the background color of an element
2. border: changes the style of the border. can be specified seperately or on one line

   ```css
   box {
     border: 3px red solid;

     /* is the same as */
     border-width: 3px;
     border-color: red;
     border-style: solid;
   }
   ```

3. color: whanges the color of the font
4. border-radius: rounds the corners of a border
5. background-image: `background-image: url(filename)`
6. background-repeat: repeats the image within the element. options are repeat-x, repeat-y and no-repeat
7. background-position: moves the background image within the div. positive values move down and right. negative values move up and left. you can also specify center to center the image within the div on the x or y (or both) axis
8. background-size: sets the size of the image in the element. cover sizes the image to the size of the element
9. background-attachement: setting the value to fixed makes the background image fixed to its position in the browser window

## Box Model, Margin & Padding

1. margin: the space that is outside of the border. can be set to 0
2. padding: the space that is inside the border. can be set to 0
3. box-sizing: set to border-box to include padding in the calculation of the element size

### Specifying padding or margin per side

- padding-top, padding-right, padding-bottom, padding-left
- padding shorthand: padding: top bottom right left
- even shorter: padding: tb rl
- margin-top, margin-right, margin-bottom, margin-left
- margin shorthand: margin: top bottom right left
- even shorter: margin: tb rl

## Float and alignment

### Centering

1. create a container div
2. create the elements you want to center inside the div
3. set a max-width for the container less than the display width
4. set the margin to auto

```css
.container {
  width: 960px;
  margin: auto;
}
```

- text-align: values include left, right, right center and justify

### Floats (Should not use in new websites)

1. set the width of on element to a percentage of the max-width
2. set float to left
3. set the width of the other element to the remaining percentage of the max width
4. set float to right
5. create a clear class that will clear both floats
6. COntinue with the rest of the elements

## Link and Button styling

Links and buttons can be styled identically and made to look identical. You may want to do this if you want a button that isn't attached to a form or have a button that is attached to a form but consistent with the rest of the site

- cursor: pointer -- will make the link or the button change to a pointer when you haver over it
- adding border-radious will halp both links and buttons look more modern
- adding a :hover pseudo tag will give indication to the user that the element can be click on

## Nav menu styling

### side-menu

- Use an unordered list
- remove the bullets -- `list-style: none`

### Nav Menu

- set list-style: none
- set margin and padding to 0
- set the list items to float left
- set overflow to auto
- give padding to each li

## Inline, Block and Inline-Block

- inline: use when a block element needs to act line an inline element (li items on a nav menu)
- block: use when an inline element needs to act like a block (center an image on a screen)
- inline-block: use when a block element needs to be shown inline but still needs to set width

## Positioning

- static -- not affected by tblr properties/values
- relative -- tblr values cause element to be moved from its normal position
- absolute -- positioned releative to its parent element that is positioned relative
- fixed -- positioned relative to the viewport
- sticky -- positioned based on scroll position

[Back to Index](index.md)
