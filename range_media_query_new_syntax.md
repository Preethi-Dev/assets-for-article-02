# Range Media Queries' New Syntax

In Media Queries Level 4 Specification, A new syntax was introduced in the media queries having range media features which utilizing common Mathematical comparison operators that make more sense syntactically as well as solve a niche problem. Before proceeding further, Let's need to familiarize with the concepts like Media Query, User Agent, Media Type, Media Features, Media Conditions, Media Query Modifier, and specifically Discrete and Range Media features. After strongly familiarizing with concepts will get clear concerning precisely where the changes are made.

Media Queries enable displaying the document disparately in the user agent or device based on device type (_technically known as media type_) or specific characteristics (_technically known as media features_) of the user agent or device that the document is being displayed in.

> A user Agent is a computer program or software, characterized on behalf of the user. For instance, Web Browser - Every request made by a browser to the server must include User Agent HTTP Header known as UA String or User Agent String for self-identification. This UA String describes the request made from which browser, version number, and its host operating system.

## Syntax of media query

According to Media Queries Level 4 Specification, The syntax of a media query consists of,

- Media Type (optional)
- Zero or more Media Features
- Media Query Modifier (optional)

### Media Type

Media Type is a wide classification of user agent devices. In earlier days, A document uses disparate stylesheets based on the user agent's device type (means media type). But, It's not going well as wished.

Media Types have proven insufficient as a way of discriminating between devices with different styling needs. Most of the media types were depreciated like tty, tv, projection, handheld, braille, embossed, aural, and speech.

Still, we can use

- All
- Print
- Screen

  _Recommended to use **media features** that determine certain aspects of the device required to query in media queries._

## Media Feature

According to W3C Specification, The concept of media queries originates from HTML4. That specification only defined media types but media query had a forward-compatible syntax that accommodated the addition of future concepts like media features. Media feature test the specific characteristic or feature of the User Agent or device that the document is being displayed in.

Media feature mimics the CSS property alike,

![Media feature]()

CSS Properties consist of the property name, colon, and then value. Likewise, the Media feature consists of the feature name, colon, and then value.

![Example of Media Feature]()

### Differences between Media Feature and CSS Property

CSS Property describes how the document will look like. Media features will determine the prerequisite of user agent or device or environment for document being displayed.

Media features must be wrapped with parentheses and combined with logical operators('and', 'or') like `(color) and (min-width: 600px)` rather than separated by semicolon.

A media feature can omit the colon and value. some media features may represent with its name only which often evaluated in boolean context. For example: `(color)` media feature.

> Boolean Context: If feature would be true for any value other than the value '0' or the keyword 'none', The media feature evaluates to true. Otherwise, it evaluates to false.

CSS Properties can carry complex values. Though, Media features accept single values either a keyword or a number.

### Media Feature Types

In the specification, Every media feature defines its “type” as either “range” or “discrete” in its definition table.

**Discrete media features** accept the values as keywords or boolean numbers(0 and 1).

Let's catch an instance for keyword values: Media feature `pointer` have three different values: `none`, `coarse`, and `fine`.

- If `pointer` value set to `none` ensure whether the user interacts with the website by keyboard.

- If `pointer` value set to `coarse` ensure primary input mechanism isn't very accurate.

- If `pointer` will set to `fine` ensure whether the user interacts with the website by mouse or stylus.

![keyword instance]()

For the boolean instance, Media feature `monochrome` evaluate whether the user agent or output device displays shades of grey. If a device is a monochrome display, will return true otherwise return false.

![boolean instance]()

An essential side note: There is no intrinsic order for discrete type and none of the values getting compared like 'less-than' or 'greater than'.

**Range media feature** takes value from a range. Range media features being true, When it matches the feature is greater than/less than/equal to the given value.

For instance, Required to style an element based on the viewport width. Styles getting disparate If width greater than 790px. We can write a range media features for this condition in two ways,

- A Standard Ancienter way of Range Media Feature.
- A brand new syntax for range media features.

### A Standard Ancienter way of Range Media Feature:

Use the `min-` and `max-` prefixes on the feature name. We could write a range media feature for above instance as,

```
(min-width: 790px)
```

The feature name `width` prefixed with `min-`, then colon with feature value. This `(min-width: 790px)` will true and apply disparate styles if screen's viewport size is greater than or equal to 790px. Otherwise, It evaluates to false and retain the default styles.

![min-width instance illustration]()

- Use `min-` for greater than or equal to comparison.
- Use `max-` for lesser than or equal to comparison.

This will be works same for other range media features like `height`, `aspect-ratio`.

We can combine one or more media features using boolean algebra(and, or, not). Chaining media features together using boolean algebra(and, or, not) will often known as **media condition**.

![media condition]()

let's take an small profound use case:

```
(min-width: 400px) and (max-width: 1000px)
```

The above query will return true if the device matches the screen's viewport width is greater than / equal to 400px and lesser than / equal to 1000px.

- If We placed the `and` between media features, Query will return true if all the media features should be true.

- If we placed the `or` between the media features, Query will return true if anyone of the feature should be true.

`not` have some special charcterstics from others. This single keyword which alter the meaning of the media query. Prefixing the media query with `not` will negate the result of media query. Let's see a minimal usecase:

```
not ((color) or (hover))
```

will return true if the device was monochrome(not a color device) or didn't have hover capabilities. If we remove the prefix `not`, The meaning of the media query will change completely. According to the spec, A media query may optionally be prefixed by a single keyword that alters the meaning of the media query will be known as **media query modifier**.

**Discrete** type media features do not accept `min-` or `max-` prefixes. Adding such a prefix to a discrete type media feature simply results in an unknown feature name. For example, (`min-grid: 1`) is invalid, because the media feature `grid` is a discrete type which evaluated in boolean context and will return 1 if the output device is a grid or bitmap. Otherwise, return 0. The media feature `grid` doesn’t accept the prefixes. (Even though the grid media feature appears to be numeric, as it accepts the values 0 and 1.)

In boolean context, The media features are evaluated to `0` or `1` rather than greater than / lesser than. So, There is no need of range prefixes. In simple terms, Attempting to evaluate a min/max prefixed media feature in a boolean context is invalid and a syntax error.

### A brand new syntax for range media features

Already, We familiarized with media queries, media types, media features, and their types and some crucial terms. This is the right context to uncover the new syntax and you will encounter exactly where the syntax is getting improved.

It would be new to media queries level 4 specification, Writing range media features using ordinary mathematical comparison operators:

- `<` (less than)
- `>` (greater than)
- `<=` (less than or equal to)
- `>=` (greater than or equal to)

```
(width >= 790px)
```

or

```
(790px <= width)
```

Above two new syntax will be equal to `(min-width: 790px)`. The base form of range media features new syntax is **feature name, a comparison operator and then value**.

![Range media feature new syntax]()

let's see a small profound use case for range media features, Define disparate styles if the device matches the screen's viewport width is greater than / equal to 400px and lesser than / equal to 1000px.

In standard range syntax:

```
(min-width: 400px) and (max-width: 1000px)
```

In new improved range syntax: Removed the prefixes from the feature name and utilized the Mathematical comparison operators solitary.

```
(width >= 400px) and (width <= 1000px)
```

We can rewrite the chained media features without using boolean algebra in new range media feature syntax,

```
(400px <= width <= 1000px)
```

Now, You can see how the syntax is getting refactored as simply as possible. Occasionally, Some developers like me in the early stages get confused with `min-` and `max-` like which one is greater than or lesser than? will resolve by the common Mathematical comparison operators that make more sense than the prefixed (`min-`, `max-`) feature name.

Let's implement the range media feature's new syntax in below modern layout:

![Modern Layout Usecase](./assets/modern-layout.png)

I followed the Mobile-First approach. I just defined the base or default styles that are common to all breakpoints. Afterward, Start to revamp styles for mobile and tablet breakpoints. In both breakpoints, `header` and `footer` go with flexbox and `main` declared as grid container with a 4-column grid. In `main`, There is some tiny difference between mobile and tablet. You can encounter the difference via the below illustrations:

![mobile and tablet layout]()

Just skip the styles defined in mobile view. Let's move onto Tablet view, The hidden nav list getting displayed as well as `title` in `main` getting increased in `font-size`. Observe the below GIF to see the transformation.

![Tablet layout tranformation gif]()

Above changes getting queried when the output device's viewport width is greater than or equal to 768px. This usecase seems range type. let's implement the usecase in range media feature's new syntax:

```
@media screen and (width >= 768px) {
   header {
    justify-content: space-between;
  }

  header ul {
    display: flex;
    justify-content: space-between;
    gap: 3rem;
  }

  main .title p {
    font-size: 5.75rem;
  }
}
```

![explaination of media query]()

In laptop and desktop breakpoints, `main` getting adapted to a popular 12-column grid as well as a button displayed and positioned on the image and `title` overlaping on `image`. These changes queried when the device viewport width is greater than or equal to 1000px.

![laptop and sektop layout tranformation gif]()

I'm sure, You derived the media query in mind like below:

```
@media screen and (width >= 1000px) {
  .grid {
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: auto 250px;
  }

  main .title p {
    font-size: 7.75rem;
  }

  main .title {
    grid-row: 1;
  }

  main .images {
    grid-row: 1 / span 2;
    align-self: end;

    position: relative;
  }

  main .images .button {
    display: block;

    position: absolute;
    bottom: 5rem;
    right: -1rem;
  }
}
```

You can always see the `>=` operator because of Mobile-First approach. It will vary for the context we using. Explore the below codepen for how things getting disparate for every breakpoint:

[CodePen Demo](https://codepen.io/preethi-dev/pen/rNvQPeg)

### New Syntax resolved the nuanced querying issue

Beyond the syntactic difference between standard and improved syntax, They are functioning slightly different. As per standard range feature syntax, Using prefixes(`max-`, `min-`) on a feature name is equivalent to using mathematical comparsion operators:

- Using a `max-` prefix on a feature name is equivalent to using the `<=` operator. For example, `(max-width: 320px)` is equivalent to `(width <= 320px)`.
- Using a `min-` prefix on a feature name is equivalent to using the `>=` operator. For example, `(min-width: 320px)` is equivalent to `(width >= 320px)`.

_There is no `>` or `<` operators are equivalents to feature name with prefixes._

Let's take a familier usecase from W3C Spec, Define different styles based on a breakpoint in the viewport width using prefixed range features. Assuming a breakpoint at 320px.

```
@media (max-width: 320px){ /* styles for viewports <= 320px */ }
@media (min-width: 320px){ /* styles for viewports >= 320px */ }
```

Both media queries evaluate to true at the viewport width is 320px. Based on specificity, The finally defined media query won the match. To avoid that implicit changes. Ensure that both media queries don’t evaluate to true simultaneously. Let's rewrite the media query as

```
@media (max-width: 320px){ /* styles for viewports <= 320px */ }
@media (min-width: 321px){ /* styles for viewports >= 321px */ }
```

While this ensures that the two sets of styles don’t apply simultaneously when the viewport width is 320px. Though, Any viewport widths that fall between 320px and 321px will result in none of the styles being applied. One approach to resolve this issue is to increase the second comparsion scale value (numbers after the decimal point) to 320.01px:

```
@media (max-width: 320px) { /* styles for viewports <= 320px */ }
@media (min-width: 320.01px) { /* styles for viewports >= 320.01px */ }
```

However, in these situations, range feature improved new syntax (which are not limited to `>=` and `<=` comparisons) offer a more appropriate solution:

```
@media (width <= 320px) { /* styles for viewports <= 320px */ }
@media (width > 320px) { /* styles for viewports > 320px */ }
```

We can define seperate styles for viewport width upto 320px and then from 320px(it may be 320.01px or 320.5px or anything after 320px), we can define disparate styles.

### Browser Compatability

The new syntax will support in firefox, chrome and edge from firfox 63, chrome 104, edge 104. More browsers starts to support the range media feature new syntax. Check for more support in [caniuse.com](https://caniuse.com/css-media-range-syntax).
According to the spec, This improved syntax is new to Level 4 of Mediaqueries, and thus is not as widely supported at the moment as the `min-`/`max-` prefixes.

### Wrapping Up

- Media queries constructed with zero or more media feature, optional media condition and optional media types. According to spec, Most of the media types were depreciated. Recommended to use media features than media types.

- Prefixed(`min-`, `max-`) range media feature is equivalent to mathematical operators like `min-` is equivalent to `>=`, `max-` is equivalent to `<=` and there is no `>`, `<` operators.

- New improved syntax was introduced in media query's range media feature. This improved Syntax utilizing the common mathematical comparison operators: `>`, `<`, `>=`, `<=` supports more usecases compared to prefixed(`min-`, `max-`) range media feature. This is not supported as widely as the `min-`/`max-` prefixes.

- Improved Syntax will fix the nuaunce issues raise in some usecases like both media queries evaluates to true at certain aspect of user agent or output device.
