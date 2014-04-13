# CSS code standard

Work in progress

## General Guidelines

1. Include a commented link at the top of the style sheets back to the coding standards document.

1. Use expanded styles for development and compressed styles for production

    **Development phase**

        ```css
        .success {
            background-color: #dff0d8;
            border-color: #d6e9c6;
            color: #468847;
        }

        .error {
            background-color: #ecc7c7;
            border-color: #db0011;
            color: #468847;
        }
        ```

    **Production phase** (compressed)

        ```css
        .success{background-color:#dff0d8;border-color:#d6e9c6;color:#468847;}.error{background-color:#ecc7c7;border-color:#db0011;color:#468847;}
        ```

    When minifing a CSS, include a commented link at the top to view the unminified CSS


## Naming convention

Use lowercase and dashes for Class, ID names, also CSS properties and values, follow the naming principles of [BEM](http://bem.info/method/definitions/).

    ```css
    <!-- block -->
    <ul class="menu">
        <!-- block-element -->
        <li class="menu-item">…</li>
        <!-- block-element-modifier -->
        <li class="menu-item-alternative">…</li>
    </ul>
    ```
Try to describe the element clearly without abbreviations by "What it is" not "How it looks like", leave the definition of styles out of names.

    ```css
    .menu-item-alternative {...} /*recommended*/

    .blue-bold-heading {...} /*not recommended*/
    ```

Avoid using IDs for styling. IDs are great for anchor links and JS hooks, but avoid using them as styling hooks.

    ```css
    /*not recommended*/
    #title {
        background-image: url("path/to/image.jpg");
        text-decoration: underline;
    }
    ```

Avoid qualifying class names with type selectors. you may want to apply it in a different element

    ```css
    .nav {...}/*recommended*/
    .important {...} /*recommended*/

    ul.nav {...} /*not recommended*/
    span.important {...} /*not recommended*/
    ```

Prefix status classes with is-` for more meaningful naming

    ```css
    .is-hidden {...}/*recommended*/
    .is-collapsed {...} /*recommended*/

    .hidden {...} /*not recommended*/
    .collapsed {...} /*not recommended*/
    ```

## Style

1. Indentation

    4 spaces

1. Multiple lines

    Separate selectors and declarations by new lines for multi-lined properties.

    ```css
    .menu-item,
    .menu-item-alternative {
        background-color: #dff0d8;
        border-color: #d6e9c6;
        color: #468847;
    }
    ```

1. Curly brackets

    1. Add a single space before the opening bracket `{` in rule sets.

    1. Place opening bracket of declaration block in the same line with the declaration and place the closing bracket of declaration block on a new line

    ```css
    /*recommended*/
    .success {
        background-color: #dff0d8;
        border-color: #d6e9c6;
        color: #468847;
    }

    .success {
        background-color: #dff0d8;
        border-color: #d6e9c6;
        color: #468847;
        }

    /*not recommended*/
    .success
    {
      background-color: #dff0d8;
      border-color: #d6e9c6;
      color: #468847;
    }

    /*not recommended*/
    .success {
      background-color: #dff0d8;
      border-color: #d6e9c6;
      color: #468847; }
    ```

1. Space

    Add one blank line between rule sets

    ```css
    /*recommended*/
    .success {
        background-color: #dff0d8;
        border-color: #d6e9c6;
        color: #468847;
    }

    .error {
        background-color: #ecc7c7;
        border-color: #db0011;
        color: #468847;
    }

    /*not recommended*/
    .success {
        background-color: #dff0d8;
        border-color: #d6e9c6;
        color: #468847;
    }
    .error {
        background-color: #ecc7c7;
        border-color: #db0011;
        color: #468847;
    }
    ```

    Add a space between properties and values after the colon `:`

    ```css
    /*recommended*/
    .success {
        color: #468847;
    }

    /*not recommended*/
    .success {
        color:#468847;
    }
    ```

1. Semicolons

    Include a semicolon after every declaration, including the last declaration

    ```css
    /*recommended*/
    .selector {
        color: #468847;
        background: #db0011;
    }

    /*not recommended*/
    .selector {
        color: #468847;
        background: #db0011
    }
    ```

1. Double quotes

    ```css
    input[type="checkbox"] {...} /*recommended*/

    input[type=checkbox] {...} /*not recommended*/
    ```

## Comments

1. Place comments on a new line above their subject.

    ```css
    /* Resetting the HTML elements for a cross-browser compatibility */
    article,
    aside,
    details,
    figcaption,
    figure,
    footer,
    header,
    hgroup,
    nav,
    section {
        display: block;
    }

    audio,
    canvas,
    video {
        display: inline-block;
        *display: inline;
        *zoom: 1;
    }

    audio:not([controls]) {
        display: none;
    }
    ```

2. Comment any illogical "for others developers", unnecessary or css hacks properties/declarations describing why you did that, and include a link for an article or detailed fix steps if any.

    ```css
    .entry-featured {
        *display: inline; /* IE7 and lower fix */
        *zoom: 1; /* IE7 and lower fix */
    }

    /* IE7 and lower to force the element to hasLayout
     * http://stackoverflow.com/a/1794381
     */
    .gain-haslayout {
        *zoom: 1;
        *position: relative;
    }
    ```

3. Keep line length to a sensible maximum, e.g., 80 columns.

    **recommended**
    ```css
    /*
     * The first sentence of the long description starts here and continues on
     * this line for a while finally concluding here at the end of this paragraph.
     */
    ```

    **not recommended**
    ```css
    /*
     The first sentence of the long description starts here and continues on this line for a while finally concluding here at the end of this paragraph.
    */
    ```

1. Create a comment for each main section, base, layout, modules, and state

    ```css
    /* -----------------------------------------------------------
     Section comment block
    ----------------------------------------------------------- */
    ```


1. Create comments for sub-sections and add 3 lines before when they follow styles

    **recommended**

    ```css
    .icon_red_douple_uparrow {
        background-position: 0 -98px;
        height: 11px;
        width: 9px;
    }

    .icon_red_downarrow {
        background-position: 0 -556px;
        height: 7px;
        width: 9px;
    }

    .icon_red_leftarrow {
        background-position: 0 -279px;
        height: 10px;
        width: 7px;
    }



    /* ------- Sub-section comment block ------- */
    ```

    **not recommended**

    ```css
    .icon-uparrow {
        background-position: 0 -98px;
        height: 11px;
        width: 9px;
    }

    .icon-downarrow {
        background-position: 0 -556px;
        height: 7px;
        width: 9px;
    }

    .icon-leftarrow {
        background-position: 0 -279px;
        height: 10px;
        width: 7px;
    }
    /* ------- Sub-section comment block ------- */
    ```


## Units, numbers

1. No units for `line-height`

    If there is a unit for `line-height`, it will multiply the number with parent element font-size instead of current element.

    ```css
    p {
        font-size: 12px;
        line-height: 1.5; /* correct */
        line-height: 1.5em; /* wrong */
        line-height: 150%; /* wrong */
    }
    ```

1. Numbers should be divisible by 2, otherwise there will be pixel offset under different browsers.

1. If the number is 0, no units should be provided, it's not necessary.

1. Keep leading `0`s in values.

    For better readability.

    ```css
    /*recommended*/
    .selector {
        font-size: 0.6rem;
    }

    /*not recommended*/
    .selector {
        font-size: .6rem;
    }
    ```


## Best practices

### Do not restate certain properties

    ```css
    li {
        float: left;
        display: block; /* unneccessary */
    }

    button {
        position: absolute;
        display: block; /* unneccessary */
    }
    ```

### Clear floats

Create a class called `clearfix` with the following styles and attached it to any parent that has a floated children

    ```css
    /*
     * Read more about this approach
     * http://nicolasgallagher.com/micro-clearfix-hack/
     *
     * For modern browsers
     * 1. The space content is one way to avoid an Opera bug when the
     *    contenteditable attribute is included anywhere else in the document.
     *    Otherwise it causes space to appear at the top and bottom of elements
     *    that are clearfixed.
     * 2. The use of `table` rather than `block` is only necessary if using
     *    `:before` to contain the top-margins of child elements.
     */
    .clearfix:before,
    .clearfix:after {
        content: " "; /* 1 */
        display: table; /* 2 */
    }

    .clearfix:after {
        clear: both;
    }

    /**
     * For IE 6/7 only
     * Include this rule to trigger hasLayout and contain floats.
     */
    .clearfix {
        *zoom: 1;
    }
    ```

    **HTML Usage**
    ```html
    <div class="module-name clearfix">
        <div class="module-name-child-floated-left">...</div>
        <div class="module-name-child-floated-right">...</div>
    </div>
    ```

### Center elements

Centering elements by giving it `auto` horizontal margins

    ```css
    .centered-element {
        margin-left: auto;
        margin-right: auto;
    }

    /*or*/
    /* 0 is just for demonstration,
     * it indicates top and bottom margin
     */
    .centered-element {
        margin: 0 auto;
    }
    ```

### !important

Do not use `!important` declarations unless you really have to do so

### Normalize

Normalize your main anchor declaration by setting all anchor statuses "normal, hover, active and focus"

    ```css
    a {...}
    a:hover {...}
    a:active {...}
    a:focus {...}
    ```
