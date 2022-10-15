# VS code
### extensions
- live server
- auto rename tag
- highlight matching tag
### shortcuts
- (CTRL + K V) opens markdown preview side by side 
- (CTRL + B) opens/closes sidebar
- (CTRL + L) selects whole current line
- (ALT + arrow up/down) moves line up/down
- (CTRL + D) select instances
- (CTRL + K W) closes all open tabs/windows

# Emmet
[docs](https://docs.emmet.io/)
- Exclamation mark (!) creates basic HTML structure
- element, followed by tab automatically creates both opening and closing tab, so for example type "h1", hit Tab and you get `<h1></h1>`
- `link:css` creates `<link>` to stylesheet
- `h1{hello world}*5` creates `<h1>hello world</h1>` 5 times
- `lorem20` generates lorem text with 20 words


<br>

# Useful resources
### Images
Copyright-free high-quality images
- [pexels](https://www.pexels.com/)
- [pixabay](https://pixabay.com/)
- [gratisography - funny images](https://gratisography.com/)
### Colors
Color palettes, schemes, gradients
- [coolors](https://coolors.co/)


# CSS

### External vs internal vs inline
- last rule principle - if we have multiple styles given to the same property of the same element, the one that was defined "most recently" will be applied. If there is an inline style, it will be the inline style. If there isn't an inline style, external vs internal actually depends on the exact placement of the `<link>` and `<styles>` tags in the document. Consider the examples below:
```
<head>
  <link rel="stylesheet" href="./styles.css">
  <style>
    h1 {
      color: green;
    }
    </style>
  <title>Document</title>
</head>
```
```
<head>
  <style>
    h1 {
      color: green;
    }
    </style>
    <link rel="stylesheet" href="./styles.css">
  <title>Document</title>
</head>
``` 
#### **order matters when linking stylesheets**

In the first example, the internal styling in the `<style>` tags is defined after the `<link>` to the external style sheet. Therefore, the internal style will apply. However, in the second example, the external style will be applied, because the `<link>` is defined after the internal styling.

This raises an important point to `<link>`ing of external stylesheets. Generally, if we are using external stylesheets from 3rd party sources (for example bootstrap), as well as our own external stylesheets, we want to link our own stylesheets last, as this will allow us to override any styles defined in the previous third party stylesheets.

### selectors
We can group selectors with a comma
```
h1, h2, h3 {

}

.class {

}

#id {

}

/* (any) descendant selector - only selects <p> which is inside .container */
.container p {

}

/* direct descendant selector */
.container > p {

}

/* combination of classes selector - will only be applied if both classes present */
.container.special-container {

}
```

### inheritance
- In CSS, children inherit styles from the parent, unless they have their own style. More immediate parents take priority over less immediate parents, so if a `<p>` element is in a `<div>` which is inside the `<body>`, and both the div and body have a style specified for a given property, the style from the div would prevail, because it's the more immediate parent.
- However, not all properties are inherited, for example `border` is not inherited.


### order matters when specifying different styles for the same element/property
<br>

```
p {
  color: blue
}

thousands of line of code

p {
  color: red
}
```
If we have a situation similar to the example above, where we define different values for the same style and property, the last defined rule will take precedent.

### Specificity
Broadly speaking, id is most specific, then class, then type (of element). For a more thorough description, see [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). For conflicting properties, the more specific selector prevails.


### Colors
#### properties
Two properties of interest: `color` and `background-color`. They are self-explanatory. One interesting thing is that there's also the `background` property, which can be used to set color, or a background image, or some kind of combination.
#### values
The simplest way of setting values for colors is just typing the **name** of the color. You can see all CSS named colors [here](https://www.w3schools.com/colors/colors_names.asp).

The next possibility is to specify **RGB** values. This is done using the following syntax:
```
#black {
  color: rgb(0, 0, 0)
}
#white {
  color: rgb(255, 255, 255)
}
# red {
  color: rgb(255, 0, 0)
}
```
Each of the three *primary colors of light* - red, green and blue - are added together in various ways (given a value of 0 - 255) to reproduce a broad array of colors.

<img src="./notes_assets/RGB_combination_on_wall.png" height="200px">

We also have the possibility of specifying **RGBA** values. Where RGB uses a 3-tuple of red, green and blue, RGBA adds another value, it is a 4-tuple, where the last value specifies the transparency/opacity of the color, ranging from 0 to 1. The typical use of RGBA is to use an overlay on a background image, to improve the legibility of the text on the image.

#### VS code color help
If we mouse over a color in our CSS, we get the color picker as shown below. We can choose a color anywhere on the palette, and VS code will set the value for us. Additionally, we can click on the color value at the top of the picker (#ff0000) in order to switch between hex/rgb/hsl values for the same color.

<img src="./notes_assets/vs_colors.png" height="250px">

### Units

Two main types of units in CSS - relative and absolute. 
#### %
One example of relative units are percentage units. Percentage units are relative and **depend on the size of the parent**.

```
some HTML

<div id="outer">
  <div id="inner"></div>
</div>

#outer {
  width: 300px;
}

#inner {
  width: 50%
}
```
The example above illustrates that when using percentage units, the actual, absolute size depends on the size of the parent. So in the example above, the inner div would have a width of 150px.

#### em
The em is a relaive unit also, it depends on the parent. The way it works is that the em value, such as `1 em`, `2 em` etc, is multiplied by a base value. The base value is given either by a parent element, or the user's browser settings if there is no parent element, or the parent element does not specify font size. 
```
<div>
  <h3>My heading</h3>
</div>

div {
  font-size: 10px;
}

h3 {
  font-size: 2em
}

```
In the example above, the h3 would have a font size of 20px. If the heading did not have a parent element, or if its parent element did not specify a font-size, then it would depend on the user's browser font size settings.
#### rem
These are similar to `em` units, but rather than being dependent on the parent, they are dependent on the root - which is the browser font setting (unless we override the font-size of the `<html>` root element).

#### vh and vw
These are viewport units - vh being viewport height and vw being viewport width. Their values range from 0 to 100, where 100 takes up the whole screen (whatever the screen size).

### Default browser styles and Chrome dev tools
Chrome dev tools are very useful in web dev. 

<img src="./notes_assets/dev_tools.png" height="250px">

Above, we see two features highlighted - in red, is an element selector - we can use it to select any element on the page by clicking, and Chrome will navigate to it in the Elements tab. In blue is the Toggle device toolbar, which allows us to simulate viewing the page on various devices/screen sizes.

<img src="./notes_assets/default_styles.png" height="250px">

And here we can see a demonstration of default browser styles. Even though the page we set up has just an `<h1>` element, and absolutely no styling in CSS, the `h1` still has some styles, as we can see in the dev tools. These are the default browser styles. These are the styles the browser falls back to if the developer doesn't specify any themselves.

<img src="./notes_assets/dev_tools_style_source.png" height="300px">

In the dev tools it also specifically shows us the sources of various styles. `user-agent-stylesheet` means default browser styles. For styles which are not browser defaults, we can even override the directly in the devtools, as is shown with font-size. This is useful for quick prototyping/checking.

### calc function

The calc function allows us to define sizes in terms of calculations. Best shown on an example:

```
<body>
  <ul class="navbar">
    <li>simple link</li>
  </ul>
  <div class="banner"></div>
</body>

* {
  margin: 0;
}

.navbar {
  background: blue;
  height: 100px;
  color: white;
  font-size: 3rem;
}

.banner {
  height: calc(100vh - 100px);
  background: red;
}
```

If we wanted to create a webpage with a navbar on top and then a hero element below, such that they take up the whole screen together vertically, without scrolling, `calc` is the ideal tool. We can set a given height for the navbar, and then for the hero element we can express its height in terms of `calc(100vh - {navbar-height}px)`

### Overflowing content, min-height

When we specify a height for an element, such as a `<div>`, we can run into problems with content overflow. If we continue with the example right above and add another div, specify some height and put some content inside, we will get something like the following:
```
<ul class="navbar">
  <li>simple link</li>
</ul>
<div class="banner"></div>
<div class="example">
  <p>hello world</p>
  <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Reiciendis natus iusto modi, tempora placeat voluptatibus? Repellendus maxime repudiandae illum quos. </p>
  <p>hello world</p>
</div>

* {
  margin: 0;
}

.navbar {
  background: blue;
  height: 100px;
  color: white;
  font-size: 3rem;
}

.banner {
  height: calc(100vh - 100px);
  background: red;
}

.example {
  background: green;
  width: 20rem;
  height: 25rem;
}
```

And the bottom of the page looks like this in the browser:

<img src="./notes_assets/little_bit_text.png" height="400px">

However, if we add more text into the green div, the following happens:

<img src="./notes_assets/a_lot_text.png" height="400px">

The text is overflowing out of our `<div>`, since we gave it a specific height of 25rem, but the text does not fit within that. 

#### overflow
We have a few options here. We could either deal with it using the `overflow` property. We could specify `overflow: hidden;`, which would cut off all the text flowing over the bottom of the div, though that's obviously not a good solution. Alternatively, we could specify `overflow: scroll`, which would keep the height of the div to 25rem, and add a scrollbar so that we can optionally view all the text. 

#### min-height
Alternatively, we could change the div to have `min-height: 25rem`, rather than `height: 25rem`. The div would then have a height of 25rem when its content (text) fits within the 25rem height, but its height would automatically increase to contain all of the text if it did not fit within the 25rem height.

### Typography

Two properties are key for typography - `font-size` and `font-family`. Additionally, we will look at how to use Google Fonts.

**Pattern**: setting a font-family for the whole body, and then overriding for specific elements/headings.

#### Font-stack and generic fonts
It could happen that a given browser does not support a given specific font that we have chosen. In that case, we can supply fallback options. Supplying multiple different fonts, ending with a generic font classification. This is called a font stack. VS code suggestions include some font stacks.

```
h1 {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

p {
  font-family: 'Courier New', Courier, monospace;
}
```

Notice that fonts whose names consist of multiple words are written in quotation marks.

#### Google Fonts

We can use fonts from external sources, such as Google Fonts. There are many fonts to choose from, and usually there are also many versions of the same font, with different thickness, cursive vs regular and so on.

<img src="./notes_assets/google_fonts.png" height="600px">

In the bar on the right side, we can see three fonts selected: Merriweather, Lato and Roboto Condesed. Google Fonts then provides two ways to link the fonts to your website, either via a `<link>` tag to include in your HTML, or via an `@import` statement to include in your CSS (provided under **Use on the web**). They also give you the exact CSS rules to specify the font families you have chose (provided under **CSS rules to specify families**). Note that they also include fallback fonts, should the Google Fonts not load.

**Keep in mind**: the more Google Fonts you'll use/include on your site, the slower it will load, since they all need to be requested from Google's servers. Additionally, using the `<link>` way of importing the fonts is [quicker](https://sia.codes/posts/making-google-fonts-faster/) than the CSS way.

#### System fonts

System fonts are fonts which are already included on the user's device. Note that this will make the site look different on different OS devices. To use system fonts, just start typing "system-ui" after the font-family, and VS code should auto complete.

```
body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
```

#### font-weight and font-style

The `font-weight` property determines the boldness of our font. We can either specify it using numeric values, ranging from 1 to 1000, though usually the values are specified to the nearest hundred (100, 200 etc). Alternatively it can be specified using keywords `normal` and `bold`, or keyword values relative to the parent `lighter` and `bolder`.

With `font-style` we can specify either `italic`, `oblique` or `normal`.

#### More properties

For `text-align`, we can set either `right`, `left` or `center`.

For `text-indent`, we can set a size in units (px, rem etc.), which will make the text start indented by a certain amount.

For `line-height` we can set a size in units, or we can just put a unitless number, which will make the line-height be a multiple of the font-size.

For `letter-spacing` we can set a size in units.

For `word-spacing` we can set a size in units.

For `text-decoration` we can set `dashed`, `dotted`, `underline`, `none` and others. 

For `text-transform` we can use `uppercase`, `capitalize` or `lowercase`.

### CSS box model

Every HTML element is in a box. Boxes have their content, padding, borders and a margin:

<img src="./notes_assets/css_box_model.png" height="400px">

#### shorthand

When we define `padding` or `margin` for our element, we can either separately specify properties for `padding-top`, `padding-bottom`, `padding-left` and `padding-right`. Or, we can use a shorthand, like this:
```
/* adds 2rem padding all around */
h1 {
  padding: 2rem;
}

/* adds 2 rem padding top and bottom and 4rem padding left and right
div {
  padding: 2rem 4rem;
}

/* adds 1rem top, 2rem right, 3rem bottom and 4rem left
h2 {
  padding: 1rem 2rem 3rem 4rem;
}
```

For borders, we have the following shortcuts:

```
/* width, style, color */
div {
  border: 1px solid red;
}
/* specific side of the border */
div {
  border-bottom: 1rem dashed green;
}
```

#### margin

By default, browser already has a margin. So we usually will want to add the following to all our projects:
```
* {
  margin: 0;
}
```

**Margin collapse**: margins collapse. This means that if we have two elements, one on top of the other, if we set margin-bottom for the top element and a margin-top for the bottom element, these margins do not add up together. Only the larger of the two margins is considered. 

**Negative margin**: We can also give a negative margin to elements, which will make one element cover another element.

#### outline

Our previous CSS box model image was actually missing the outline:

<img src="./notes_assets/css_outline.png">

The outline behaves basically the same as the border, but it has one additional property which we can use to make interesting designs - `outline-offset`.

```
#one {
  border: 0.2rem solid black;
}

#two {
  outline-width: 0.2rem;
  outline-color: black;
  outline-style: solid;
  outline-offset: 10px;
}
```
<img src="./notes_assets/outline_example.png">