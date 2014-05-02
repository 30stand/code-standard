# Accessibility

Work in progress

Todo:

1.  xxx
1.  yyy
1.  zzz

### HTML markup
Doctype

Add a doctype for all the HTML pages: `<!DOCTYPE HTML>`

Lang and dir attribute

1. Define the language of the page using the lang attribute, eg `<html lang="en">`
2. The language of page content that is in a different language should be identified using the lang attribute, eg  `<blockquote lang="es">`, or `<span lang="fr">`
3. Do not use the Content-Language value for an http-equiv attribute on a meta element, eg do not use `<meta http-equiv="Content-Language" content="en" />`
4. When mixing languages with different directionality in HTML, use the dir attribute on an inline element and/or use a Unicode right-to-left mark (RLM)/left-to-right mark (LRM) to mix text direction inline

Page title and meta description

Provide descriptive page title and meta description via `<title>` and `<meta name="description", content="...">`

List

1. Use `<ol>` or `<ul>` for lists or groups of links
2. Do not use `<ul>` and `<li>` when there is only one item in the list

Emphasis

Use `<strong>` instead of `<bold>`, `<em>` tag instead of `<i>` for emphasis

Blockquote

Use `<blockquote>` instead of `<p class="quote">` for quotes


Validation

Load each page into a validator, eg http://validator.w3.org/ or the Firefox addon Html Validator 0.9.5.1, no HTML/XHTML errors are found

### Mega drop-down menu

This section is copied from http://adobe-accessibility.github.io/Accessible-Mega-Menu/

HTML

The HTML structure for the mega menu is a nav element, or any other container element, containing a list. Each list item contains a link which is followed by a div or any other container element which will serve as the pop up panel. The panel can contain any html content; in the following example, each panel contains three lists of links. You can explicitly define groups within the panel, between which a user can navigate quickly using the left and right arrow keys; in the following example, the CSS class .sub-nav-group identifies a navigable group.

```
    <nav>
        <ul class="nav-menu">
            <li class="nav-item">
                <a href="?movie">Movies</a>
                <div class="sub-nav">
                    <ul class="sub-nav-group">
                        <li><a href="?movie&genre=0">Action &amp; Adventure</a></li>
                        <li><a href="?movie&genre=2">Children &amp; Family</a></li>
                        <li>&#8230;</li>
                    </ul>
                    <ul class="sub-nav-group">
                        <li><a href="?movie&genre=7">Dramas</a></li>
                        <li><a href="?movie&genre=9">Foreign</a></li>
                        <li>&#8230;</li>
                    </ul>
                    <ul class="sub-nav-group">
                        <li><a href="?movie&genre=14">Musicals</a></li>
                        <li><a href="?movie&genre=15">Romance</a></li>
                        <li>&#8230;</li>
                    </ul>
                </div>
            </li>
            <li class="nav-item">
                <a href="?tv">TV Shows</a>
                <div class="sub-nav">
                    <ul class="sub-nav-group">
                        <li><a href="?tv&genre=20">Classic TV</a></li>
                        <li><a href="?tv&genre=21">Crime TV</a></li>
                        <li>&#8230;</li>
                    </ul>
                    <ul class="sub-nav-group">
                        <li><a href="?tv&genre=27">Reality TV</a></li>
                        <li><a href="?tv&genre=30">TV Action</a></li>
                        <li>&#8230;</li>
                    </ul>
                    <ul class="sub-nav-group">
                        <li><a href="?tv&genre=33">TV Dramas</a></li>
                        <li><a href="?tv&genre=34">TV Horror</a></li>
                        <li>&#8230;</li>
                    </ul>
                </div>
            </li>
        </ul>
    </nav>
```
By default, accessibleMegaMenu uses the the following CSS classes to define the top-level navigation items, panels, groups within the panels, and the hover, focus, and open states. It also defines a prefix for unique id strings, which are required to indicate the relationship of a top-level navigation item to the panel it controls.

```
 defaults = {
        /* unique ID's are required to indicate aria-owns, aria-controls and aria-labelledby */
        uuidPrefix: "accessible-megamenu",

        /* default css class used to define the megamenu styling */
        menuClass: "accessible-megamenu",

        /* default css class for a top-level navigation item in the megamenu */
        topNavItemClass: "accessible-megamenu-top-nav-item",

        /* default css class for a megamenu panel */
        panelClass: "accessible-megamenu-panel",

        /* default css class for a group of items within a megamenu panel */
        panelGroupClass: "accessible-megamenu-panel-group",

        /* default css class for the hover state */
        hoverClass: "hover",

        /* default css class for the focus state */
        focusClass: "focus",

        /* default css class for the open state */
        openClass: "open"
    }
```

You can optionally override the defaults to use the CSS classes you may have already defined for your mega menu.

JavaScript

Be sure to include jQuery and the jquery-accessibleMegaMenu.js plugin script.

```
<script src="js/vendor/jquery-1.10.1.min.js"></script>
    <script src="js/jquery-accessibleMegaMenu.js"></script>
```
The following initializes the first nav element in the document as an accessibleMegaMenu, with optional CSS class overrides.

```
$("nav:first").accessibleMegaMenu({
        /* prefix for generated unique id attributes, which are required 
           to indicate aria-owns, aria-controls and aria-labelledby */
        uuidPrefix: "accessible-megamenu",

        /* css class used to define the megamenu styling */
        menuClass: "nav-menu",

        /* css class for a top-level navigation item in the megamenu */
        topNavItemClass: "nav-item",

        /* css class for a megamenu panel */
        panelClass: "sub-nav",

        /* css class for a group of items within a megamenu panel */
        panelGroupClass: "sub-nav-group",

        /* css class for the hover state */
        hoverClass: "hover",

        /* css class for the focus state */
        focusClass: "focus",

        /* css class for the open state */
        openClass: "open"
    });
```

CSS
AccessibleMegaMenu handles the showing and hiding of panels by adding or removing a CSS class. No inline styles are added to hide elements or create animation between states.

Following is some rudimentary CSS for our example which enables the showing/hiding of and the layout of lists panels in the mega menu.

```
    /* mega menu list */
    .nav-menu {
        display: block;
        position: relative;
        list-style: none;
        margin: 0;
        padding: 0;
        z-index: 15;
    }

    /* a top level navigation item in the mega menu */
    .nav-item {
        list-style: none;
        display: inline-block;
        padding: 0;
        margin: 0;
    }

    /* first descendant link within a top level navigation item */
    .nav-item > a {
        position: relative;
        display: inline-block;
        padding: 0.5em 1em;
        margin: 0 0 -1px 0;
        border: 1px solid transparent;
    }

    /* focus/open states of first descendant link within a top level 
       navigation item */
    .nav-item > a:focus,
    .nav-item > a.open {
        border: 1px solid #dedede;
    }

    /* open state of first descendant link within a top level 
       navigation item */
    .nav-item > a.open {
        background-color: #fff;
        border-bottom: none;
        z-index: 1;
    }

    /* sub-navigation panel */
    .sub-nav {
        position: absolute;
        display: none;
        top: 2.6em;
        margin-top: -1px;
        padding: 0.5em 1em;
        border: 1px solid #dedede;
        background-color: #fff;
    }

    /* sub-navigation panel open state */
    .sub-nav.open {
        display: block;
    }

    /* list of items within sub-navigation panel */
    .sub-nav ul {
        display: inline-block;
        vertical-align: top;
        margin: 0 1em 0 0;
        padding: 0;
    }

    /* list item within sub-navigation panel */
    .sub-nav li {
        display: block;
        list-style-type: none;
        margin: 0;
        padding: 0;
    }
```

### Form control
1. For all input elements of type text, file or password, for all textareas and for all select elements in the Web page, a label element is attached before the input, textarea, or select element. The for attribute of the label element matches the id of the input, textarea, or select element.
	
	Sample code:
	```
	<label for="firstname">First name:</label> 
	<input type="text" name="firstname" id="firstname" />
	```

1. For all input elements of type checkbox or radio in the Web page, the label is positioned after the input element. The for attribute of the label element matches the id of the input element.
	
	Sample code:
	```
	<input type="checkbox" id="markuplang" name="computerskills" checked="checked">
	<label for="markuplang">HTML</label>
	```

1. Group the logically related input or select element within fieldset elements and each fieldset should has a legend element that describes the group. Sample code:

	```
	<form action="http://example.com/adduser" method="post">
	   <fieldset>
	     <legend>Residential Address</legend>
	     <label for="raddress">Address: </label>
	     <input type="text" id="raddress" name="raddress" />
	     <label for="rzip">Postal/Zip Code: </label>
	     <input type="text" id="rzip" name="rzip" />
	     ...more residential address information...
	   </fieldset>
	   <fieldset>
	     <legend>Postal Address</legend>
	     <label for="paddress">Address: </label>
	     <input type="text" id="paddress" name="paddress" />
	     <label for="pzip">Postal/Zip Code: </label>
	     <input type="text" id="pzip" name="pzip" />
	     ...more postal address information...
	   </fieldset>
	</form>
	```
1. When selection lists have groups of related options, use `<optgourp> to group `<option>` elements inside a `<select>`

Example code

```
	<form action="http://example.com/prog/someprog" method="post">
    <label for="food">What is your favorite food?</label>
    <select id="food" name="food">
      <optgroup label="Fruits">
        <option value="1">Apples</option>
        <option value="3">Bananas</option>
        <option value="4">Peaches</option>
        <option value="5">...</option>
      </optgroup>
      <optgroup label="Vegetables">
        <option value="2">Carrots</option>
        <option value="6">Cucumbers</option>
       <option value="7">...</option>
     </optgroup>
     <optgroup label="Baked Goods">
       <option value="8">Apple Pie</option>
       <option value="9">Chocolate Cake</option>
       <option value="10">...</option>
     </optgroup>
   </select>
</form>     
```

5. Indicate required form controls using label or legend

6. Provide client-side validation and alert/suggestion/feedback:
	1. To identify required fields that were not completed
	2. When user provides information that is not in the list of allowed values or when user input falls outside the required format or values
	3. If an input error is detected
	4. When data is submitted successfully
	

### Headings
1. Provide heading elements at the beginning of each section of content
2. Each page should only have one h1
3. Headings are designed to convey logical hierarchy. Don’t skip heading levels
4. Provide descriptive headings. Avoid duplicating heading
5. Do not use h tags to achieve visual results only
6. Do not use text formatting, such as font size or bold to give the visual appearance of headings

### Image
1. Always include alt attribute in `<img>`.
2. For decorative images, implement it via CSS, or implement it using `<img>` with alt="".
3. For non-decorative images, eg charts, diagram, alt text should be descriptive.
4. Do not embed text in image unless it is a logo.

### Table

1. Use `<th>` and scope attribute for header cells, eg '<th scope="row">' for row header and <th scope="col"> for column header. If the table header is empty, use `<td></td>`
2. Use `<caption>` to mark up the title/heading of data table, and `<summary>` for table summary, where appropriate. If both are used, the `<caption>` should not duplicate information in the `<summary>`.
3. Use id and headers attributes to associate data cells with multiple header cells. 

Example code:
```
	<table>
   <tr>
     <th rowspan="2" id="h">Homework</th>
     <th colspan="3" id="e">Exams</th>
     <th colspan="3" id="p">Projects</th>
   </tr>
   <tr>
     <th id="e1" headers="e">1</th>
     <th id="e2" headers="e">2</th>
     <th id="ef" headers="e">Final</th>
     <th id="p1" headers="p">1</th>
     <th id="p2" headers="p">2</th>
     <th id="pf" headers="p">Final</th>
   </tr>
   <tr>
    <td headers="h">15%</td>
    <td headers="e e1">15%</td>
    <td headers="e e2">15%</td>
    <td headers="e ef">20%</td>
    <td headers="p p1">10%</td>
    <td headers="p p2">10%</td>
    <td headers="p pf">15%</td>
   </tr>
  </table>
```
4. Avoid layout table. If layout table is used, do not include `<th>`, `<caption>` and `<summary>`.
