#typography #design #css

# [Fittext: A jquery plugin for inflating web type](http://fittextjs.com/)

In a fluid layout, browser width and typographic measure are linked: the wider the viewport, the more characters per line. Keeping in mind that a range of [45-75 characters per line is generally accepted as safe for comfortable reading](http://www.webtypography.net/Rhythm_and_Proportion/Horizontal_Motion/2.1.2/), there are a few things that can be done to avoid extra long lines of text in fluid layouts.

1. check paragraphs to see if the layout is blowing out the characters per line at any given width. When it does, increase the font-size until things are back in that safe 45-75 range. A simple, effective trick I’ve used is dropping some _lorem_ text into the layout with two asterisks. The first marks the 45th character, and the second marks the 75th.
2. As you widen the browser window, if at any point the two asterisks appear on the same line of text, it’s time to increase the font size. These adjustments are easy (usually 1 CSS property) if you use percentage, [em, and rem](http://blog.typekit.com/2011/11/09/type-study-sizing-the-legible-letter/) (not pixel) units in your CSS.


```css
html { 
	font-size: 16px; 
} 

@media screen and (min-width: 320px) { 
	html { 
		font-size: calc(16px + 6 * ((100vw - 320px) / 680));
	} 
} 

@media screen and (min-width: 1000px) { 
	html { 
		font-size: 22px; 
	} 
}
```
https://css-tricks.com/snippets/css/fluid-typography/

The reason that math is a little complicated is that we’re trying to avoid type ever getting smaller than our minimum or bigger than our maximum, which is very easy to do with viewport units.

For example, if we want the our font size in a range where `14px` is the minimum size at the smallest viewport width of `300px` and where `26px` is the maximum size at the largest viewport width of `1600px`, then our equation looks like this:

```css
body {
  font-size: calc(14px + (26 - 14) * ((100vw - 300px) / (1600 - 300)));
}
```

<iframe src="https://www.madebymike.com.au/writing/fluid-type-calc-examples/" height="500" style="width: 100%"></iframe>