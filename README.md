.CSS Style Guide {
==================

*A mostly reasonable approach to CSS*
*Based on the excellent work done by Richard Powell [here](https://github.com/byrichardpowell/CSS-Style)*

## General

### Minimise the use of element selectors

Selectors that contain elements tightly coupled the CSS to specific markup. It is not a safe assumption that the semantics of the content will never change so authors should prefer classes which exist independent of markup and create more flexible CSS.

Source: [SMACSS on modules](http://smacss.com/book/type-module)

### Do not use location based selectors

A location based selector is a selector that changes a modules appearance based on its location (content area, side bar, header etc).  Where a module has different appearances it is better to use a module subclass.  If the appearance and/or content is very different it would be better to use a different module

Source: [OOCSS, slide 20](http://www.slideshare.net/stubbornella/object-oriented-css)

### Do not use ID's in CSS Selectors

It is never safe to assume there will only ever be one of something on a page so do not use ID's for CSS.  Id's are much better used as javascript hooks so use them for this instead.

Source: [SMACSS on layout](http://smacss.com/book/type-layout)

### Animate an interface using classes not inline styles

Inline styles added by javascript are harder to update and maintain, prefer to add classes using javascript.  CSS3 transitions can then handle any animations and if CSS3 transitions are not supported the state will still be updated.

Source: [SMACSS on state](http://smacss.com/book/type-state)

### Selectors should be 4 or less levels deep

Long complex selector chains spawn specificity wars and are slower for the browser to evaluate.  Its unlikely you _need_ to use a selector more than 4 levels deep.  If it is, consider adding additional classes to the markup to enable a shorter  selector length.

### Don't use a Preprocessor to produce bloated CSS

Utilise a preprocessors features such as mixins, variables, nested rules and functions to make code easier to maintain but always double check compiled stylesheets to avoid code bloat.  Preprocessors, when used inefficiently, can cause code bloat.

Source: [SMACSS on preprocessors (members only)](https://smacss.com/book/preprocessors)

### Minimise HTTP requests

HTTP Requests are expensive and slow the rendering of a page, so minimise them. Ideally a HTML page should contain just one CSS file with extra CSS being loaded as the page changes.

### Always Minimise CSS

Minifying code can save up to 60% on a files size.  Use a tool like [YUI Compressor](http://yui.github.io/yuicompressor/) or [Grunt CSS Min](https://github.com/gruntjs/grunt-contrib-cssmin) together with build tools such as [Grunt](gruntjs.com) or [Maven](maven.apache.org/) to manage this and it's easy-peasy.

Source: [Google Page Speed on Minifying CSS](https://developers.google.com/speed/docs/best-practices/payload#MinifyCSS)

### Always use a CSS Linter

Using a CSS Linter will make obvious whenever a rule is not matching the coding standard and best practices. It will make developers know something is wrong even before looking at it in the browser.
When using Sublime Text a great solution is to use [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter), there are other options for other IDEs and it can also be used online via http://csslint.net/

### Never Use Single line formatting

CSS Architecture is more difficult to do well than it is difficult to understand CSS Properties. Reading long lines of CSS code makes it difficult to understand the properties of the rule. This, together with the correct ordering of the CSS properties make it really easy to understand a rule as first sight.

Source: [SMACSS on formatting](https://smacss.com/book/formatting)

### Use dashes to separate words

CSS properties do not use underscores or camel case, they use dashes.  Do the same with classes

## Coding Style

### General coding guidelines

* Use soft-tabs with a two space indent.
* Put spaces after `:` in property declarations.
* Put spaces before `{` in rule declarations.
* Use hex color codes #000 unless using rgba.

Syntax example:

```css
.styleguide-format {
  border: 1px solid #0F0;
  color: #000;
  background: rgba(0,0,0,0.5);
}
```

### Multiple selectors should each be on a single line

```css
.my-class,
.our-class,
.your-class {
  border: 1px solid #0F0;
}
```

### Each property should be on a new line

```css
/* BAD */
.my-class { border: 1px solid #0F0; color: #F00; margin-top: 20px; }

/* GOOD */
.my-class {
  border: 1px solid #0F0;
  color: #F00;
  margin-top: 20px;
}
```
### Use hyphens to concatenate class names

E.g. `.demo-image` not `.demoImage` or `.demo_image`

### Use a semicolon after every declaration
```css
/* BAD */
.my-class {
  border: 1px solid #0F0;
  color: #F00
}

/* GOOD */
.my-class {
  border: 1px solid #0F0;
  color: #F00;
}
```

## Cross Browser

### Use browser prefixes correctly & Painlessly

When using prefixed properties ensure that Microsoft, Opera, Webkit and Mozilla prefixes are supported and that the non prefixed version is too.  Make this less painful by abstracting it away into a preprocessor mixin.

### Use Conditional classes for Internet Explorer

Aim to avoid separate styles for internet explorer, but where unavoidable do not use conditional stylesheets or CSS hacks to target specific versions of IE. Instead use conditional classes as explained by Paul Irish.

Source: [Conditional stylesheets vs CSS hacks…](http://paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/)

### Group IE Conditional styling with the code they alter

Aim to avoid separate styles for internet explorer, but where unavoidable place the "fixes" next to the style it effects.  Not doing so makes it easy to miss when updating to changing the original styles

### Normalise Don't Reset

A global reset is a convenient way of ensuring consistent styling cross browser but it is often overkill and it makes CSS harder to debug in developer tools.

Source: [Normalise.css](http://necolas.github.com/normalize.css/)

### Don't be over-zealous when normalising

When normalising it is important to not add styles to elements that then need to be overridden in future modules.  Tables and form elements are great examples of this.

Source: [SMACSS on drop the base](http://smacss.com/book/drop-the-base)

## Architecture

### Split CSS into Normalise, Layout, Module & Icon files

Splitting CSS into multiple files in a constant way makes it easier to find the CSS you are looking for.

### Keep CSS files under 500 lines of code

It sucks to have to search through 1000+ lines of code, so avoid it.  This rule may mean having to split the CSS module file into multiple files. When doing this make sure to only serve one file to the user.

### Order properties: box, border, background, text & other

Always order your properties grouping by categories. Box properties (Position, layout, display), box borders, background properties, text properties (font size, family, weight, etc), and so on.

Source: [SMACSS on formatting](https://smacss.com/book/formatting)

## Layout

### Separate Layout and Module rules

A Module defines the appearance and positing of its elements, nothing else.  If a module were to define a specific width then it would not be flexible enough to be included in multiple locations of different dimensions.

Source: [SMACSS on layout](http://smacss.com/book/type-layout)

## Modules

### A Module should have flexible dimensions

If a module needs to be contained do so using another class or a wrapper.  Modules need to be flexible, forcing their dimensions is not being flexible.

### Comment a module thoroughly

At the start of a module a comment should provide a picture of what content it contains, how that content looks and anything that is unusual about it.  Ideally it should also provide a link to an example of the module in a HTML file.

### Ensure modules are self contained and reusable

Friends don't let friends write modules that may bleed into other modules or can only be used in a limited number of places.    Time spent upfront avoiding these two problems will save that time 10 fold later in the project.

### Module names should be self explanatory but short

It should be possible to look at a modules class and instantly have an idea what that module represents.  Do not provide a detailed description in the class name, just an overview.  A detailed description belongs in a comment at the top of the module CSS.

### Module Specific Classes should be module name prefixed

Adding the modules name to the start of all its classes ensures that if a module sits inside another module, the parent's styles will not bleed into the child's styles.  It also makes scanning the HTML easier as it is immediately clear which classes belong to which modules.

### Use a nested selector to group module rules

Preprocessors provide an opportunity to make it crystal clear where a modules rules start and end.  Use that opportunity but be sure not to nest nested selectors inside other nested selectors.  This would produce large selector chains, which are a bad idea.

### Split Modules into default, state, & subclass groups

Consistently architecting modules in this way makes it easy to scan the module and get a good overview of it.  Being inconsistent is likely to lead to mistakes and oversights when the module is edited at a later date.

### Subclass a module to create different versions of it

A module subclass will make changes to a module that might be major in appearance but should be minor in terms of the amount of styles it is changing.  A module subclass should not be used if the module subclass would need to overuse many styles and make it unrecognisable from its module.  If a module is subclassed its wrapper will need the class for the module and for the subclass of that module.

Source: [SMACSS on modules](http://smacss.com/book/type-module)

### Module Subclass class names should be: module--subclass

The double dash makes it clear that this class represents a subclass and which module the subclass is affecting.  The wrapper for this module will need the module class and the subclass module.

### State classes should be prefixed with is

A state class ( e.g: .is-active, .is-empty ) is similar to a pseudo class in that it updates the appearance of an element.  Where it differs is that a state class will be added by javascript or the app when the page loads.  Adding is- to the start of the class clearly indicates that this module has been affected by a state class.

Source: [SMACSS on state](http://smacss.com/book/type-state)

### Only State classes may use !important

!important should be avoided as much as possible, as such state classes are the only acceptable use of important.  Even so !important should not be the go to solution as its akin to using a grenade when careful diplomacy would suffice.

Source: [SMACSS on state](http://smacss.com/book/type-state)

### Icons do not belong in modules

By styling icons independently of the module where it was first used you are making an icon that can be used in future modules without the need for duplication of code.

### Remove overly similar modules

If two modules are very similar with only barely noticeable changes to stuff like the shadow, padding and colours combine them into one.  The user will never know the difference and chances are this is a mistake introduced before the development stage.

Source: [OOCSS, slide 39](http://www.slideshare.net/stubbornella/object-oriented-css)

## Icons

### Split icon styles into ico, ico-size & ico-img classes

Specifying that something is an icon, its size and its image separately allows for maximum flexibility and minimal code repetition

Source: [SMACSS on Icons](http://smacss.com/book/icon-module)

### Optimise icon images into sprites late in the project

Sprite images are an important way to reduce HTTP requests but they can be cumbersome to manage when an interface is in its infancy.  Do not over optimise too early. Wait until the project is ready to deploy and make time for sprite sheet optimisation then.

### Sprited Icons should be added to empty elements

If you add a sprite image to the background of an element that has text what happens when that element receives more text and expands?  It will happen and you'll feel silly, so avoid the pain and add icons to empty elements even though that means more markup.

Adding icons to elements that have their text hidden out of bounds is also a good approach.

Source: [SMACSS on Icons](http://smacss.com/book/icon-module)

}
=
