---
layout: slidedeck
title: Custom Web Fonts and Icon Fonts Slides
---

{% highlight html %}
name: inverse
layout: true
class: center, middle, inverse

---

# Using Custom Web Fonts

.title-logo[![Red logo](../../public/img/red-logo-white.svg)]

---
layout: false

# Agenda

1. Custom fonts on the web
2. Using `@font-face`
3. Using Google Fonts
4. Web font services
5. Choosing and pairing fonts
6. What is an icon font (and how to use one)

---

template: inverse

# Intro to Web Fonts

---
class: center, middle

### A bit of history...

We used to be limited to using **web-safe fonts** on our websites, in other words, fonts that you could be reasonably sure would already be installed on a user's computer system.

---

.left-column[
  ## Web-Safe Fonts
]

.right-column[
As a result, we had very few choices:

  - <span style="font-family: Arial">Arial</span>
  - <span style="font-family: Times">Times New Roman</span>
  - <span style="font-family: Courier">Courier New / Courier</span>
  - <span style="font-family: Comic Sans, Comic Sans MS">Comic Sans</span>
  - <span style="font-family: Verdana">Verdana</span>
]

---
class: center, middle

.large[
   Thanks to CSS3, <br />those days are over!
]

---
template: inverse

# @font-face

---

# Using @font-face

The `@font-face` property in CSS allows us to embed custom fonts directly in our website.

That means we don't have to depend on a user having that font already installed on their computer.

```css
@font-face {
    font-family: 'robotoregular';
    src: url('Roboto-Regular-webfont.eot');
}
```

---

# Using @font-face

Once you've included an `@font-face` declaration at the top of your stylesheet, you can use it throughout your CSS:

```css
body {
   font-family: 'robotoregular', Arial, sans-serif;
}
```

---

# There's a Catch

Unfortunately, different browsers support different font formats, so when we use `@font-face` we need to make sure we include multiple versions of the same font:

- **EOT** - IE only.
- **WOFF** - Compressed, emerging standard.
- **TTF** - Works in most browsers except IE and iPhone.
- **SVG** - iPhone/iPad.

---

# Font Formats

A full example:

```css
@font-face {
    font-family: 'robotoregular';
    src: url('Roboto-webfont.eot');
    src: url('Roboto-webfont.eot?#iefix') format('embedded-opentype'),
         url('Roboto-webfont.woff') format('woff'),
         url('Roboto-webfont.ttf') format('truetype'),
         url('Roboto-webfont.svg#robotoregular') format('svg');
    font-weight: normal;
    font-style: normal;
}
```

Order matters! You'll want to include the `src` files for your fonts in this order: `eot`, `woff`, `ttf/otf`, and then `svg`.

---

# Font Squirrel

The website [Font Squirrel](http://www.fontsquirrel.com/) is a great resource for finding and creating `@font-face` font packages:

.inline-images[
   ![Font Squirrel Webfont Generator](../../public/img/slide-assets/font-squirrel-generator.jpg)
]

---
class: center, middle

## Thar be copyright dragons!

Before you embed a font on your website using `@font-face` you need to be sure that its license enables you to do so.

---

# Exercise 1

Go to **[Font Squirrel](http://www.fontsquirrel.com/)** and generate the Webfont Kits for the custom typefaces that we'll be using for Project 1: **Karla** (Regular and Bold) and **Pacifico** (Regular only).

You'll need to download both of the weights and their italic versions too for the Karla typeface. Add the contents of your generated web font packages to your project's CSS (but only the required files).

You’ll also want to read up on how to **[avoid faux italics and bolding](http://www.metaltoad.com/blog/how-use-font-face-avoid-faux-italic-and-bold-browser-styles)** with your `@font-face` typefaces, and adjust your CSS accordingly.

---

template: inverse

# Google Web Fonts

---

# Using Google Fonts

One popular alternative to directly embedding fonts in your website with `@font-face` is to use [Google Fonts](https://www.google.com/fonts).

To use Google Fonts, simple select the font you want to use, and embed the link in the head of your website:

```html
<link href='http://fonts.googleapis.com/css?family=Roboto' rel='stylesheet' type='text/css'>
```

You can then use it throughout your CSS:

```css
body {
   font-family: 'Roboto', sans-serif;
}
```

---

# Fonts vs. Performance

When using custom fonts (whether through `@font-face` or Google Fonts), be sure to think about performance:

.inline-images[
   ![Google Fonts weight](../../public/img/slide-assets/google-fonts-weight.png)
]

---
template: inverse

# Web Font Services

---

# Third-Party Services

For fonts with licensing restrictions, you may have to use a third-party web font services if you want to use the font on your website.

Some of these services include:

- [Typekit](https://typekit.com/)
- [Hoefler & Co.](http://www.typography.com/cloud/welcome/)
- [Webtype](http://www.webtype.com/)

---
template: inverse

# Choosing and Pairing Fonts

---
class: center, middle

.large[
   With great power...
]

---
class: center, middle

### Contrast

When pairing typefaces, make sure they are discernibly different from one another.

---
class: center, middle

### Serif + Sans-serif

When pairing serif with sans-serif, look for typefaces based on the same geometric principles.

---
class: center, middle

### Dial Down the Fancy

If you're using display or script typefaces, stick to just one.

---
class: center, middle

### Leverage CSS

Take advantage of the many CSS properties that can help adjust text display.

---
class: center, middle

### Consider the Message

When choosing a typeface, consider its personality and if it complements the message being communicated.

---
template: inverse

# What's an Icon Font?

---
class: center, middle

### Icon fonts are just fonts.

But instead of containing letters and numbers, they contain symbols (aka **glyphs**).

---

# Why Are They Awesome?

- You can target CSS at them, just like a normal font
- They're SVGs, so they scale without pixelating (so they're very responsive)
- They're supported even as far back as IE6!
- All of the icons supported by the font load with one HTTP request

---
class: center, middle

.large[
   The old way...
]

---
class: center, middle

.inline-images[
   ![Image sprite example](../../public/img/slide-assets/image-sprite-example.png)
]

---
template: inverse

# Using an Icon Font

---

# Pick a Font

There are a few ready-made icon fonts out there that you can use on your website for free:

- [Font Awesome](http://fortawesome.github.io/Font-Awesome/)
- [IcoMoon](https://icomoon.io/)

We're going to take a look at Font Awesome...

---
class: center, middle

.inline-images[
   ![Font Awesome logo](../../public/img/slide-assets/font-awesome-logo.jpg)
]

---

# Using Font Awesome

To use Font Awesome, you can either externally link to it on Content Delivery Network (CDN), or you can download and include the entire package directly on your website.

You would include this code in the `<head>` tag of your website:

```html
<!-- Option 1: CDN -->
<script src="https://use.fontawesome.com/4fbf87bab3.js"></script>

<!-- Option 2: Font Awesome -->
<link rel="stylesheet" href="path/to/font-awesome/css/font-awesome.min.css">
```

---

# Using Font Awesome

Now for the fun part&mdash;you actually get to start using the icons.

Let's say we want to include a [bicycle icon](http://fortawesome.github.io/Font-Awesome/icon/bicycle/) on our website.

All we would need to do is include an `<i>` tag with some special classes applied:

```html
<i class="fa fa-bicycle"></i>
```

And the result will look like this:

<i class="fa fa-bicycle"></i>

---

# Using Font Awesome

We can adjust the size of the icons with extra classes:

```html
<i class="fa fa-bicycle fa-lg"></i> fa-lg
<i class="fa fa-bicycle fa-2x"></i> fa-2x
<i class="fa fa-bicycle fa-3x"></i> fa-3x
<i class="fa fa-bicycle fa-4x"></i> fa-4x
```

<i class="fa fa-bicycle fa-lg"></i> fa-lg<br />
<i class="fa fa-bicycle fa-2x"></i> fa-2x<br />
<i class="fa fa-bicycle fa-3x"></i> fa-3x<br />
<i class="fa fa-bicycle fa-4x"></i> fa-4x

---

# Using Font Awesome

And animate the icons:

```html
<i class="fa fa-circle-o-notch fa-spin fa-3x"></i>
<i class="fa fa-spinner fa-pulse fa-3x"></i>
<i class="fa fa-bicycle fa-spin fa-3x"></i>
```

.inline-images[
   <br /><i class="fa fa-circle-o-notch fa-spin fa-3x"></i>&nbsp;&nbsp;&nbsp;
   <i class="fa fa-spinner fa-pulse fa-3x"></i>&nbsp;&nbsp;&nbsp;
   <i class="fa fa-bicycle fa-spin fa-3x"></i>
]
<br />

You can find all of Font Awesome's [icons referenced here](http://fortawesome.github.io/Font-Awesome/icons/) and [usage examples here](http://fortawesome.github.io/Font-Awesome/examples/).

---

# Using Font Awesome

Every Font Awesome icon also has a [Unicode value](http://fortawesome.github.io/Font-Awesome/cheatsheet/). Using those values, we can use Font Awesome directly in our CSS too:

```html
<button class="menu-toggle"><span>Menu</span></button>
```

```css
.menu-toggle span {
   display: none;
}

.menu-toggle:after {
   content: "\f0c9";
   display: block;
}
```

---

# Exercise 2

Add Font Awesome to your Project 1 (using the CDN option).

Once you have successfully added it to your project, try adding the social media icons to your site's `footer`. 

Now that you have the icons added, how will you get the social network names to appear and disappear at the various breakpoints?

---

# What We've Learned

- How to use `@font-face`
- How to use Google Fonts
- What licensed font services are available
- What an icon font is
- The advantages of using an icon font
- How to use Font Awesome

---

template: inverse

# Questions?

{% endhighlight %}
