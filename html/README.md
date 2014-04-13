# HTML code standard

Work in progress


## Style

1. Indentation

    4 spaces

1. Comments

    Place comments on a new line above the container block element. Use single line short sentence as comment and place comments only for module and main block elements.

    ```
    <!-- Start header content area -->
    <div class="header">
      <a href="/" class="hsbc-logo">
        <img alt="HSBC" src="/images/hsbc-logo.png">
      </a>
    </div>
    <!-- End header content area -->
    ```

1. Close tags are more preferred

    `<br />` instead of `<br>`, for better visual consistency.


## Enforce HTML standard

1. Doctype declaration, always use

    ```
    <!DOCTYPE html>
    ```

    Unless the page is IE-only, or only works under quirks mode.

1. Tag and attribute names should be lowercase, prefix custom non-visible data with `data-*` attributes

    ```
    <button type="button" class="print-button" data-index="1">Print</button>
    ```


## Meta tags

1. General Meta tags

    ```
    <!-- always put charset as the first line in head -->
    <meta charset="utf-8" />
    <!-- tell IE to work on latest rendering mode -->
    <meta http-equiv="x-ua-compatible" content="IE=edge" />
    ```

1. Search engines

    ```
    <title></title>
    <meta name="robots" content="" />
    <meta name="description" content="" />
    <meta name="google-site-verification" content="" />
    ```

1. Optional tags for additional information

    ```
    <meta name="author" content="">
    <meta name="copyright" content="">
    ```

1. De facto tags for mobile devices

    ```
    <!-- general -->
    <meta name="viewport" content="width=device-width">

    <!-- for iOS devices or Android -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="format-detection" content="telephone=no">
    ```

    Optional tags for legacy devices:

    ```
    <!-- Windows Mobile -->
    <meta http-equiv="cleartype" content="on" />
    <meta name="MobileOptimized" content="480">

    <!-- Blackberry -->
    <meta name="HandheldFriendly" content="true" />
    ```

Notes:

1. `<meta>` tags always goes inside the `<head>` element.

1. Meta data is always passed as name value pairs.

1. The content attribute MUST be defined if `name` or `http-equiv` attribute is defined. If none of these are defined, the content attribute CANNOT be defined.


## Elements

### Block-level elements

By default, block-level elements begin on new lines.

Generally, block-level elements may contain inline elements and other block-level elements. Inherent in this structural distinction is the idea that block elements create "larger" structures than inline elements.

**Warning**: Never place a block-level element inside an inline element.

    <address>, <blockquote>, <dd>, <div>, <dl>, <fieldset>, <form>, <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <hr>, <noscript>, <ol>, <p>, <pre>, <table>, <tfoot>, <ul>

New block-level elements introduced in HTML5:

    <article>, <aside>, <audio>, <canvas>, <figcaption>, <figure>, <footer>, <header>, <hgroup>, <output>, <section>, <video>


### Inline elements

By default, inline elements do not begin with new line.

Generally, inline elements may contain only data and other inline elements.

    <b>, <big>, <i>, <small>, <tt>, <abbr>, <acronym>, <cite>, <code>, <dfn>, <em>, <kbd>, <strong>, <samp>, <var>, <a>, <bdo>, <br>, <img>, <map>, <object>, <q>, <script>, <span>, <sub>, <sup>, <button>, <input>, <label>, <select>, <textarea>

### Deprecated elements

You should **NOT** use these elements since they are no longer part of the family.

    <applet>, <acronym>, <bgsound>, <dir>, <frame>, <frameset>, <noframes>, <isindex>, <listing>, <nextid>, <noembed>, <plaintext>, <rb>, <strike>, <xmp>, <basefont>, <big>, <blink>, <center>, <font>, <marquee>, <multicol>, <nobr>, <spacer>, <tt>


## Proper way to use elements

### Sections

There are two semantically equivalent syntax for headings exists, the later one is introduced with the new section element.

1. Pure heading elements

    ```
    <h1>Let's call it a draw(ing surface)</h1>
    <h2>Diving in</h2>
    <h2>Simple shapes</h2>
    <h2>Canvas coordinates</h2>
    <h3>Canvas coordinates diagram</h3>
    <h2>Paths</h2>
    ```

2. Heading elements with the section element

    ```
    <h1>Let's call it a draw(ing surface)</h1>
    <section>
        <h1>Diving in</h1>
    </section>
    <section>
        <h1>Simple shapes</h1>
    </section>
    <section>
        <h1>Canvas coordinates</h1>
        <section>
            <h1>Canvas coordinates diagram</h1>
        </section>
    </section>
    <section>
        <h1>Paths</h1>
    </section>
    ```

**Which one to use?**

The answer depends on your site scale and the architecture of the site,

if there is no dynamic contents, and the site is developing as a whole,
the first suits you, and provides the maximum compatibility;

if the site is created dynamically, combined by components, usually the outer context of the inserted components are unknown, then it's best to use `<section>`, the content editors can use `<h1>` elements throughout, without having to worry about whether a particular section is at the top level, the second level, the third level, and so on.

The side affect of the second approach is some old softwares may interpret the heading numbers incorrectly, which is a minor drawback.


### Grouping content

#### The p element
#### The ol element
#### The ul element


### Text-level semantics

#### The br element

br elements must be used only for line breaks that are actually part of the content, as in poems or addresses.

The following example is correct usage of the br element:

    <p>P. Sherman<br />
    42 Wallaby Way<br />
    Sydney</p>

br elements must NOT be used for separating thematic groups in a paragraph.

The following examples are non-conforming, as they abuse the br element:

    <p><a ...>34 comments.</a><br />
    <a ...>Add a comment.</a></p>
    <p><label>Name: <input name="name"></label><br />
    <label>Address: <input name="address"></label></p>

Here are alternatives to the above, which are correct:

    <p><a ...>34 comments.</a></p>
    <p><a ...>Add a comment.</a></p>
    <p><label>Name: <input name="name"></label></p>
    <p><label>Address: <input name="address"></label></p>


#### The span element
#### The em element
#### The strong element
#### The small element
#### The i element
#### The b element


### Embedded content

#### The img element
#### The iframe element
#### The object element


### Forms

#### The label element


### Tabular data

#### The table element
#### The caption element


## References

1. [HTML Standard](http://www.whatwg.org/specs/web-apps/current-work/multipage/)
1. [MetaExtensions](http://wiki.whatwg.org/wiki/MetaExtensions)
1. [Meta tags that Google understands](https://support.google.com/webmasters/answer/79812?hl=en)
1. [META XHTML Element](http://msdn.microsoft.com/en-us/library/bb159711.aspx)
1. [Specifying legacy document modes](http://msdn.microsoft.com/en-us/library/jj676915(v=vs.85).aspx)
1. [Layout Meta Tag](http://msdn.microsoft.com/en-us/library/bb431690.aspx)
1. [HTML element: <meta>](http://docs.blackberry.com/en/developers/deliverables/6176/HTML_ref_meta_564143_11.jsp)
1. [Supported Meta Tags](https://developer.apple.com/library/safari/documentation/appleapplications/reference/SafariHTMLRef/Articles/MetaTags.html)
1. [Using the viewport meta tag to control layout on mobile browsers](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)
1. [Block-level elements](https://developer.mozilla.org/en-US/docs/HTML/Block-level_elements)
1. [Inline elements](https://developer.mozilla.org/en-US/docs/HTML/Inline_elements)
1. [Non-conforming features](http://www.whatwg.org/specs/web-apps/current-work/multipage/obsolete.html#non-conforming-features)
1. [Sections](http://www.whatwg.org/specs/web-apps/current-work/multipage/sections.html#sections)
1. [Grouping content](http://www.whatwg.org/specs/web-apps/current-work/multipage/grouping-content.html#grouping-content)
1. [Text-level semantics](http://www.whatwg.org/specs/web-apps/current-work/multipage/text-level-semantics.html#text-level-semantics)
1. [Embedded content](http://www.whatwg.org/specs/web-apps/current-work/multipage/edits.html#embedded-content)
1. [Tabular data](http://www.whatwg.org/specs/web-apps/current-work/multipage/tabular-data.html#tabular-data)
1. [Forms](http://www.whatwg.org/specs/web-apps/current-work/multipage/forms.html#forms)
