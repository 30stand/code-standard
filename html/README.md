# HTML code standard
Work in progress

## Overview
The HTML guideline decrees our approach to front-end development, HTML and HTML5 tags usage at Digital publishing delivery team in HSBC Global publishing services.

## General HTML standard:
1. Tag and attribute names should be lowercase, prefix your customized properties with "data-"
    
    ```
    <button type="button" class="print-button" data-index="1">Print</button>
    ```

1. Use HTML tags instead of XHTML / XML

    for example, `<br>` instead of `<br />`, there is no necessity to close tags since it's only a XML standard.

1. Doctype declaration, always use
    
    ```
    <!DOCTYPE html>
    ```

## VIEWPORT Meta tag usage

General Meta tags:

    <meta charset="utf-8" >
    <meta http-equiv="x-ua-compatible" content="IE=edge">
    <meta http-equiv="cleartype" content="on">

For robots: Tell robots to how index the content, and/or follow links

	<meta name="title" content="">
	<meta name="description" content="">
	<meta name="google" content="">
	<meta name="robots" content="">
	<meta name="google-site-verification" content="">

For company:

	<meta name="author" content="HSBC">
	<meta name="copyright" content="Copyright 2014. All Rights Reserved.">

For the responsive website or to support Mobile browser: 

	<meta name="HandheldFriendly" content="True">
	<meta name="MobileOptimized" content="320">
	<meta name="viewport" content="width=device-width">
	<meta name="apple-mobile-web-app-capable" content="yes">
	<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
	<meta name="format-detection" content="telephone=no">
  

Note: `<meta>` tags always goes inside the `<head>` element.  
Note: Metadata is always passed as name/value pairs.  
Note: The content attribute MUST be defined if the name or the http-equiv attribute is defined. If none of these are defined, the content attribute CANNOT be defined.


## Block and inline element placing

### Block elements

Block level elements normally start (and end) with a new line when displayed in a browser.

	<h1>One</h1>, <P>Paragraph</p>, <ul>unordered list</ul>, 
	<table>Table</table>, <header>Header</header>,
	<nav>Navigation</nav>

`<div>` is also block element that used as container.

#### Sample code block:

	<div class="container">
	  <header class="header"></header>
	  <section class="body-copy"></section>
	  <footer class="footer"></footer>
	</div>


### Inline elements

Inline elements are normally displayed without starting a new line. 

	<b>, <td>, <a>, <img>, <em>, <i>, <cite>, <mark>, <code>

`<span>` tags also inline tags that used as text container 

#### Sample code block:

	<section class="body-copy"> 
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit,
        <a class="internal-link" href="#">sed do eiusmod</a>,
        sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
	</section>


## Proper indentation

For the indentation use 4 spaces

## Code commenting

Place comments on a new line above the container block element. Use single line short sentence as comment and place comments only for module and main block elements.

    <!-- Start header content area -->
    <header class="header">
      <a href="#" class="hsbc-logo" title="HSBC">
        <img alt="HSBC" src="../images /HSBC-logo.png">
      </a>
      <nav class="utility-nav"><nav>
      <nav class="main-nav"></nav>
    </header>
    <!-- End header content area -->


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

### Image
1. Always include alt attribute in '<img>'.
2. For decorative images, implement it via CSS, or implement it using '<img>' with alt="".
3. For non-decorative images, eg charts, diagram, alt text should be descriptive.

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



