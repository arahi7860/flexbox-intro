# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) SOFTWARE ENGINEERING IMMERSIVE

# Flexbox

### Learning Objectives

-   Define the flexible box module (flexbox!)
-   Give an example of a problem solved by flexbox
-   Contrast flex containers and flex items
-   Describe the difference between the main axis and the cross axis
-   Use flexbox to solve common design problems without using hacks

# Intro to flexbox!

### What is flexbox?

Flexbox is short for "The CSS3 Flexible Box Module". From [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes), here's a definiton:

> Flexbox ... is a layout mode providing for the arrangement of elements on a page such that the elements behave predictably when the page layout must accommodate different screen sizes and different display devices. ... The defining aspect of the flex layout is the ability to alter its items' width and/or height to best fit in the available space on any display device.

### Flex context vs block context

-   Up to this point we've been working with the block context -- `display: block;`. This means that in order to position things, we needed to float them, use clearfix, etc.
-   Flexbox introduces a new context: `display: flex;`.
-   Elements with `display: flex;` have, largely, an external block context -- they exist in the document flow like any other kind of element.
-   Internally, they create a new type of context that has its own properties.

## Flex containers and flex items

### A flex _container_ is an element that creates a flex context.

#### Follow along in the ✨ code-along ✨ folder in this repo

From the [W3 Specification](https://www.w3.org/TR/css-flexbox-1/#flex-containers):

> A flex container establishes a new flex formatting context for its contents. This is the same as establishing a block formatting context, except that flex layout is used instead of block layout. For example, floats do not intrude into the flex container ... Flex containers form a containing block for their contents exactly like block containers do.

The flex context works a little differently from the ordinary block context that is the default of the document flow. A number of properties are different or do not apply.

-   `float` and `clear` don't have any effect on flex items
-   `vertical-align` has no effect on a flex item
-   Some pseudoelements, like `::first-line` and `::first-letter`, don't apply to flex containers.

### A flex _item_ is an element that exists within a flex context.

## Flex Properties and Axes

There's a long list of CSS properties that are specific to either flex containers or flex items. We'll go through a few of them, and then you'll get practice with the rest during lab.

### Main Axis, Cross Axis

A lot of the power in flexbox comes from the ability to switch which axis is which with just one property.

![Flex containers and flex items](./assets/flex-cont-item.jpg)

### 📚 Flex Container Properties

([Taken largely from CSSTricks complete guide to flexbox.](https://css-tricks.com/snippets/css/a-guide-to-flexbox/))

<dl>
  <dt><code>display</code></dt>
  <dd>In order to create a flex context, you must declare it using <code>display: flex;</code>. (Note: You may also occasionally see <code>display: inline-flex;</code> but I have not had to use this. If you want to know what it does, I encourage you to mess around.)</dd>
  
  <dt><code>flex-direction</code></dt>
  <dd><code>flex-direction</code> establishes which axis is the main axis and which is the cross axis. The possible values are <code>row</code>, <code>row-reverse</code>, <code>column</code>, and <code>column-reverse</code>. The behavior of other properties are dependent on <code>flex-direction</code>.</dd>
  
  <dt><code>flex-wrap</code></dt>
  <dd>By default, flex items all try to fit into one line with the default <code>nowrap</code>. <code>flex-wrap</code> changes this behavior, allowing items to wrap to new lines. The other possible values are <code>wrap</code> and <code>wrap-reverse</code>.</dd>
  
  <dt><code>flex-flow</code></dt>
  <dd>A shorthand property for <code>flex-direction</code> and <code>flex-wrap</code>. The default value is <code>row nowrap</code>. There's a bunch of different possible values -- essentially, pick one <code>flex-direction</code> value and one <code>flex-wrap</code> value and combine them.</dd>
  
  <dt><code>justify-content</code></dt>
  <dd>Defines the alignment and spacing along the main axis, and helps distribute extra, leftover free space. The possible values are <code>flex-start</code>, <code>flex-end</code>, <code>center</code>, <code>space-between</code>, and <code>space-around</code>. <a href='https://css-tricks.com/snippets/css/a-guide-to-flexbox/#article-header-id-6' target='_blank'>See CSS Tricks article for reference</a>.</dd>
  
  <dt><code>align-items</code></dt>
  <dd><code>align-items</code> describes how flex items are placed relative to the flex container. The possible values are <code>flex-start</code>, <code>flex-end</code>, <code>center</code>, <code>stretch</code> (the default), and <code>baseline</code>.</dd>
  
  <dt><code>align-content</code></dt>
  <dd>This aligns a flex container's lines when there's extra space on the cross axis. The available values are <code>flex-start</code>, <code>flex-end</code>, <code>center</code>, <code>stretch</code> (the default), <code>space-between</code>, and <code>space-around</code>. <b>NOTE!</b> This property has no effect unless there's more than one line of flex items.  </dd>
</dl>

### 📚 Flex Item Properties

([Taken largely from CSSTricks complete guide to flexbox.](https://css-tricks.com/snippets/css/a-guide-to-flexbox/))

<dl>
  <dt><code>order</code></dt>
  <dd>The order in which you want flex items to appear along the main axis. The default is 0. Negative numbers are allowed.</dd>
  
  <dt><code>flex-grow</code></dt>
  <dd>Defines the proportion of the space in the container that the flex item will take up. For ex, if all flex items in a flex container have a <code>flex-grow</code> property of 1, they will all take up equal width. If one of the children has <code>flex-grow: 2;</code>, it will be twice as wide as the others.</dd>
  
  <dt><code>flex-shrink</code></dt>
  <dd>Defines the ability for a flex item to shrink if necessary.</dd>
  
  <dt><code>flex-basis</code></dt>
  <dd>Defines the default size of an element. You can use any CSS unit of measurement -- percent, pixels, em, etc.</dd>
  
  <dt><code>flex</code></dt>
  <dd>This is a shorthand property that combines <code>flex-grow</code>, <code>flex-shrink</code>, and <code>flex-basis</code>. It's recommended to use <code>flex</code> instead of setting the other properties individually. You have to include <code>flex-grow</code>, but the other two parameters are optional. Usually you'll include <code>flex-grow</code> and <code>flex-basis</code>, like this: <code>flex: 1 300px;</code>.</dd>
  
  <dt><code>align-self</code></dt>
  <dd>This allows the default alignment (as set by <code>align-items</code>) to be overridden for individual items.</dd>
</dl>

## 🚀 Practice: [Flexbox Froggy](http://flexboxfroggy.com)! 🐸

For this lab, you'll be getting more acquainted with the flex properties, and applying them to flex items and flex containers. Hit the link above and start helping the frogs find their lilypads! (Feel free to work in pairs or groups!!)

# Why use flexbox?

As you may have noticed, **_flexbox is literally magic_**. Problems that take hours of messing with floats, positions, and so on, are solved in minutes. And responsiveness is a dream -- just change the `flex-direction` between mobile and desktop and you're all set.

There are a number of classic web design problems that once took odd CSS hacks and patches to fix, but are now a breeze with flexbox. Let's walk through one of them together.

### 🏆 [The Holy Grail](https://codepen.io/brunopgalvao/pen/EMPBoX)

You've seen the Holy Grail layout about a billion times. It looks like this:

![holy grail](./assets/holy-grail.png)

To put this image into words, the Holy Grail layout:

1. Has a fluid center (i.e. the center column changes width as the browser window changes width) and fixed-width sidebars, all of which are the same height;
2. Allows the center column to appear first in the HTML;
3. Allows any column to have the most content;
4. Has fixed-height header and footer that span the width of the page;
5. Has a footer that reaches at least the bottom of the browser window no matter the height of the content without using absolute or fixed positioning;
6. Requires only one extra element; and
7. Uses as little CSS as possible.

(This is based on the description of the Holy Grail problem from [A List Apart](https://alistapart.com/article/holygrail).)

We're going to be working from this HTML:

```html
<body>
    <header>Header</header>
    <main>
        <article>Content</article>
        <aside class="left">Left sidebar</aside>
        <aside class="right">Right sidebar</aside>
    </main>
    <footer>Footer</footer>
</body>
```

<details>
<summary>Let's walk through it together step by step.</summary>

```css
body {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

header,
footer {
    flex: 0 150px;
}

main {
    flex: 1;
    display: flex;
}

article {
    order: 2;
    flex: 3;
}

aside {
    flex: 0 300px;
}

.left {
    order: 1;
}

.right {
    order: 3;
}

@media screen and (max-width: 1025px) {
    main {
        flex-direction: column;
    }

    article {
        order: 0;
    }

    aside {
        flex: 0;
    }
}
```

</details>

