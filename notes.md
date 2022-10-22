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
Linear gradients
- [colorzilla](https://www.colorzilla.com/gradient-editor/)

# Patterns / often used

## Overriding browser defaults

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

## Setting linear gradient overlay on hero element

Increases readability of stuff we have over our hero element.

## Setting fonts for whole body and overriding for specific elements

Self explanatory.

## 1px solid red border for debugging

Self explanatory.

## Centering

### Without grid/flexbox

For block level elements `margin-left: auto`, `margin-right: auto`
For inline elements, select parent and `text-align: center`

## section-center

When setting up a section on our site, it can be a good idea to set up an outer `section` div and then an inner `section-center` div. Then we can make our section span the whole width of the screen, and the section-center can have a more limited width. See this example:

```
<body>
  <div class="section">
    <div class="section-title">
      <h1>section title</h1>
      <div class="title-underline"></div>
    </div>
    <div class="section-center">
      <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Qui culpa, aliquam ex sint labore suscipit et possimus, obcaecati deleniti eum fugiat dolores dolor eaque consectetur recusandae! Aliquid repellat totam optio, corporis quod nesciunt suscipit odit repellendus natus veritatis, debitis adipisci voluptatum ratione doloribus ea sint modi commodi impedit fugiat pariatur?</p>
    </div>
  </div>
</body>
</html>

.section {
  padding: 3rem;
  background: #fff;
}

.section-center {
  width: 90vw;
  max-width: 1170px;
  margin-left: auto;
  margin-right: auto;
}
```

This way we can limit the width of our content, so it doesn't span the whole width. While simultaneously having the section span the whole width. With the section-center, we can achieve a look like this:

<img src="./notes_assets/section-center.png">

Without section center, we can get either this, if we apply the styles (width and max-width) of section-center to section directly:

<img src="./notes_assets/no-section-center-1.png">

Or like this, if we don't include section-center or its styles at all and just have section:

<img src="./notes_assets/no-section-center-2.png">

## border-radius to get circular elements

If we want to create a circular button, or other element, a good way to do it is to give it `border-radius` of value equal to its `height` and `width`. 

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

### Display property

All elements have a default value for the display property. There are two main values:
- `block` these elements always start a new line and span the full width of the screen
- `inline` these elements do not start a new line and span only content. The browser does not respect their height, width, top and bottom margins.
- `inline-block` these elements also do not start a new line, but the browser does respect their width, height and top and bottom margins.

However, we can override this default behaviour by setting the property to the value we want.

#### horizontal centering

- For inline elements, in order to center them, we need to target their parent element and set `text-align: center`. For a block element, this will just center the text within the element, but it won't center the element within its parent.

<img src="./notes_assets/text_align_center.png" height="400px">

- For block elements, we first need to give them a width and then given them a margin-left and margin-right of auto. If we only give them margin-left of auto, it will align the element to the right and vice versa. Setting both will center the element.

#### width, height, margin-top and margin-bottom

- For block elements, the browser respect the width, height, margin-top and margin-bottom properties. However, for inline elements, setting a value for these properties will not actually affect anything. 
- We can fix this by setting `display: inline-block` for these elements.

#### box-sizing

We often add `box-sizing: border-box;` to our universal styles. The default value for `box-sizing` is `content-box`. The `box-sizing` property changes how padding affects the width and height of our element. If we have the default `content-box` setting, and we add padding of 20px to a div which has a height of 200px and a width of 200px, the actual size of the div will be 240px by 240px. If we seet `box-sizing: border-box` however, the div will remain 200px by 200px.

```
<body>
  <div class="box-1">I'm with border-box</div>
  <div class="box-2">I'm normal</div>
  <div class="box-3">I'm without border-box</div>
</body>
```

```
.box-1, .box-2, .box-3 {
  width: 200px;
  height: 200px;
  color: white;
  font-size: 2rem;
}

.box-1 {
  background: red;
  padding: 20px;
  box-sizing: border-box;
}

.box-2 {
  background: blue;
}

.box-3 {
  background: green;
  padding: 20px;
}
```

<img src ="./notes_assets/border-box.png" height=400px>

#### hiding elements

We can hide elements in a couple of different ways.

- Setting `display: none` removes the element from the DOM. Its space is collapsed/taken up by the other elements.
- Setting `opacity: 0` will make the element transparent, but leave it in the DOM and it will still take up space.
- Setting `visibility: hidden` will hide the element, but leave it in the DOM and it will still take up space.

### (Background) images

To set an image as background, we use the following syntax `background: url(<path to image>)`

By default, our image will repeat itself in both x and y directons. We can control this behaviour using the `background-repeat` property. This can take the values of `repeat`, `no-repeat`, `repeat-x`, `repeat-y`, `space` and `round`. `space` will put some space around the background image, and `round` will repeat the image as soon as another image fits.

<img src="./notes_assets/background_repeat.png" height="400px">

An example of `background-repeat` values of `space` and `round`. In the second image (`round`), because there is not yet enough space to fit a second image horizontally, the image gets stretched.

Typically, we will be using `no-repeat`. However, what do we do with the empty space left if we use `no-repeat`? For this, we use the `background-size` property. This has two main interesting values: `cover` and `contain`.

<img src="./notes_assets/background_size.png" height="400px">

`cover` will cover the whole element, even if it distorts the image. `contain` will not distort the image and therefore will not always cover the whole element.

The next property is `background-position`. We can give it either descriptive values, like `center`, `left`, `right`, `bottom` and `top`. Alternatively, we can give it numeric values, like `0 0` or `20% 50%`. These values determine the position of the image from the left and from the top.

The next property is `background-attachment`. This affects scrolling behaviour. If we set a `background-attachment` of `fixed`, then when scrolling the image will stay in place, while the text/content move up or down.

#### linear gradients (as background image overlays)

Linear gradients allow us to set up a transition from one color to another. Best shown with an example:

```
div {
  width: 150px;
  height: 150px;
  margin:5px;
}

.one {
  background: linear-gradient(red, green);
}

.two {
  background: linear-gradient(to right, red, yellow);
}

.three {
  background: linear-gradient(135deg, red, white, blue);
}

.four {
  background: linear-gradient(blue 50%, yellow);
}
```

<img src="./notes_assets/linear_gradients.png" height="400px">

The first argument of the `linear-gradient` property can optionally specify a direction, which can either have a descriptive value like `to left` or a numeric value in degrees, like `135deg`. This is then followed by any number of colors, which will be used for the transitions. We can also specify a percentage for the color, which will affect what proportion of the image it takes up.

**Use as overlay**

If we are including a hero element with a massive background image, and we put some text in front of it, it can often be hard to read. For example if we have a relatively light image and some white text. We can use a linear gradient to solve this:

```
background: linear-gradient(rgba(0,0,0, 0.4), rgba(0,0,0, 0.4)), url(".//big_image.jpg");
```

<img src="./notes_assets/hero_with_gradient.png" height="400px">

Compared this to the version with no gradient:

<img src="./notes_assets/hero_no_gradient.png" height="400px">

When we use a linear gradient as an overlay, we have to specify the color using an rgba value. Otherwise, the image would not be visible if the color in the gradient would not have some transparency.


### float

Using the float property, we can take elements out of the regular document flow and place them on the left or right side of their container, allowing text and inline elements to wrap around the floated element. Without using float:

```
<div class="banner">
    <img src="../17_background_imgs/small_image.jpg" alt="">
    <span>Hello there</span>
    <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Expedita assumenda autem cumque sequi. Exercitationem ut veniam neque sunt velit, illo, quam, dolore autem ipsa non asperiores qui similique quasi voluptates laborum ab fuga sit blanditiis quaerat optio unde animi tempora eaque. Vero voluptatem quo veritatis dignissimos saepe magnam omnis ut.</p>
</div>

.banner {
  border: 5px solid red;
}
```

<img src="./notes_assets/no-float.png">


The paragraph starts a new line, all the way below the image, as we would expect, since it is a block level element. The span on the other hand doesn't, as its inline. If, however, we add `float: left` to the image, we get the following:

<img src="./notes_assets/float.png">

The paragraph starts wrapping around the image.

We can also prevent the paragraph from wrapping around the image, by giving it a `clear: left`.

#### setting up multi column layout using float

Before flexbox and grid, this was apparently the way to create mutli column layouts.

```
<body>
  <div class="one">
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, dicta.</p>
  </div>
  <div class="two">
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, dicta.</p>
  </div>
  <div class="three">
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, dicta.</p>
  </div>
</body>

div {
  height: 200px;
  width: 33.33%;
  float: left;
}
```

### position

The default value for position is `static`, this doesn't really do anything. 

#### relative

We can use `position: relative` in combination with setting one of the properties `top`, `bottom`, `left` and `right` to a numeric value (in pixels for example), to change the position of an element "relative" to where it would normally be. Best shown on an example. Suppose we have a page like this:

<img src="./notes_assets/position_relative_before.png">

If we targer the blue paragraph, and give it `position: relative` and `top: 200px`, the paragraph will shift relative to where it would normally be, like so:

<img src="./notes_assets/position_relative_after.png">

#### absolute

By using `position: absolute`, the element will be positioned relative to its closest ancestor which has `position: relative`. Suppose we start with a page like this, where the pink elemnt is just a span inside the green paragraph:

<img src="./notes_assets/position_absolute_before.png">

If we give the pink span the following properties:

```
span {
  position: absolute;
  top: 0;
  left: 0;
}
```

The page will look like this: 

<img src="./notes_assets/position_absolute_after.png">

The span's ancestors are the green `<p>`, the yellow `<div>` and then the `<body>`. Neither the `<p>`, nor the `<div>` have `position: relative`, but the `<body>` does, so the span is placed in the top left corner of the body. If, however, we set `position: relative` on the `<div>`, the span would move to the top left corner of the `<div>` instead:

<img src="./notes_assets/position_absolute_second_after.png">

Also note that unlike with `position: relative` before, in this case, the space that the `<span>` used to take up is instead taken up by the text following the `<span>` in the paragraph. 

#### fixed and sticky

We can use `position: fixed` to make an element stay in place when scrolling. This is usually used for a nav bar, to make it stay in place, even as we scroll down the page.

By setting `position: sticky`, the element starts behaving as if it had `position: fixed` once we scroll to it. So we could have a nav bar with `margin-top: 100px`, so it would not start at the top of the page. And as we would start scrolling, we would scroll past the first 100px and after that the nav bar would stay on top of the document. 

### Media queries

