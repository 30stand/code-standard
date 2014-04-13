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


## Block-level elements and inline elements

Never place a block-level element inside an inline element.


### Block-level elements

By default, block-level elements begin on new lines.

Generally, block-level elements may contain inline elements and other block-level elements. Inherent in this structural distinction is the idea that block elements create "larger" structures than inline elements.

    <address>, <blockquote>, <dd>, <div>, <dl>, <fieldset>, <form>, <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <hr>, <noscript>, <ol>, <p>, <pre>, <table>, <tfoot>, <ul>

New block-level elements introduced in HTML5:

    <article>, <aside>, <audio>, <canvas>, <figcaption>, <figure>, <footer>, <header>, <hgroup>, <output>, <section>, <video>


### Inline elements

By default, inline elements do not begin with new line.

Generally, inline elements may contain only data and other inline elements.

    <b>, <big>, <i>, <small>, <tt>, <abbr>, <acronym>, <cite>, <code>, <dfn>, <em>, <kbd>, <strong>, <samp>, <var>, <a>, <bdo>, <br>, <img>, <map>, <object>, <q>, <script>, <span>, <sub>, <sup>, <button>, <input>, <label>, <select>, <textarea>


## Use proper tags

### General elements


1. The `<br>`is used to insert a line break in a sentence. Examples might be to correctly lay out an address. Use paragraph elements to split up your content and use CSS margins to alter the spacing between them.
2. The `<div>` tag is perfectly acceptable to use to define the main page structure, but always try to use more suitable tags for your page elements. Paragraph tags, ordered/unordered lists and definition lists can be more semantic choices.
3. CSS should always be used for presentational styling, so use the font-size CSS property to control your text sizes.
4. The `<small>` HTML tag is reserved for defining small print or legal text.
5. these days the CSS border property is the correct solution in most situations; however the `<hr>` tags still has its use in specific situations when defining layouts containing copy such as book chapters or poetry stanzas.
5. The `<title>` should accurately but concisely describe the contents of the page. It’s important to include keywords that relate to the content as it is recognised by search engines, but it shouldn’t be abused.
6. `<img>` tag alt attributes should contain an accurate description of the image. If the image is being used as a link give an insight to where the link will go. If the image has no importance an empty alt attribute is acceptable.
7. Use the `<label>` tag to relate a field to its descriptive label. For extra usability points add the for attribute to allow the user to click the label to activate the relevant input field.
8. The correct use of the `<address>` tag is to define the author or owner of the document. Therefore it’s usually wrapped around their name along with their contact email address or telephone number.
9. A `<p>` signifies a paragraph. It should be used only to wrap a paragraph of text.
10. To use the `<span>`element, simply surround the text that you want to add styles to with the `<span>2014<span>`
11. Use `<strong>` element instead of `<b>`


### Table

1. Table heads use `<th>` rows and columns use `<scope>` attribute.
2. able have `<summary>` and/or `<caption>` elements where appropriate


### Structural elements

1. `<ul>, <ol>`List markup is used whenever items are in a visual list.
2. Quotations use `<blockquote>` and cite elements (and these are used for quotations only).
3. Emphasis is achieved using `<em>` or `<strong>`.
4. Abbreviations and acronyms use `<abbr>` the first time they are introduced on a page.
5. Blocks of repeated content (e.g. primary navigation lists) can be bypassed with a skip link.
6. `<iframes>` have descriptive title attributes describing the content being loaded with alternative content if appropriate.
7. Use `<i>` for Italicised text
8. Use `<fieldset>` and “legend" to ground fields together.
9. Use `<section>` to either group different articles into different purposes or subjects, or to define the different sections of a single article.
10. The `<aside>` element represents a section of a page that consists of content that is tangentially related to the content around the aside element, and which could be considered separate from that content. Such sections are often represented as sidebars in printed typography.


## References

1. [HTML Living Standard](http://www.whatwg.org/specs/web-apps/current-work/multipage/index.html#contents)
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
