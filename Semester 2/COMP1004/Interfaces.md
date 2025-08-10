## CSS
- style/layout webpages to change colour, spacing, size, split into columns, animations

It is a rule-based language that requires the styles and elements that the rule applies to.

> 5em means 5x the standard size

It is common practice to avoid inline CSS whenever possible as it makes the code more difficult to read and understand. However, it can be good for dynamic changing with JavaScript.

Classes are denoted with the `.` selector

`span` can be used to apply something to a specific part of text, grouped together, inline (without line break). 

`li.special` - element type and the class. “Target any element of type `li` that has a class `special`”.

There can be multiple selectors 

`li em` - applies to only `em` if it’s within `li` (a descendent of).

> A comma between two selectors means for both


body h1 + p .special
> Within the special class, a paragraph within a h1 element in the body.

### Rules
CSS @rules (at-rules) can be used to provide instructions for what CSS should perform or how it should behave. Some are simple with just a keyword and value.

- The @import rule is used at the top of a stylesheet and can import other styles from other stylesheets.
- The @media rule is used to create media queries, using conditional logic to apply styles

### Shorthand Rules
`padding: 10px 15px 15px 5px` is equivalent to top, right, bottom and left (clockwise) instead of specifying padding-top/right

## Box Model
All elements in CSS are boxes - with borders, size, etc., but it is not always visible.

A block box will start a new line, an inline will not. If a box has an outer display type of block, it will break onto a new line, with given `width` and `height`. The padding, margin and border will cause other elements to be pushed away. If width is not specified, it will try and take up as much width as possible.