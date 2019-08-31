# HTML

<img src="https://www.w3.org/html/logo/downloads/HTML5_Logo_128.png">

## HTML Basics

- DOCTYPE -- tells the browser what type of document it is
  Must be the very first tag in the document
- html -- Surrounds the entire HTML document
- head -- Contains information about the page. Language, keywords, title etc
- body -- Contains the actual displayable content of the page
- <!-- Comment --> -- Comment block. Will not be displayed or interpreted by the browser

### Meta Tags

- charset="UTF-8" -- describes the character encoding of the page
- name="viewport" -- Sets the dimensions of the browser window for responsive design
- http-eqiv="X-UA-Compatible" -- Sets the browser compatibility\*
- description -- used and displayed by search engines
- keywords -- describes the pages content using key phrases
- robots -- Instructions to web crawlers to index or not

## Typography

- hx -- Headings numbered 1 -6(largest to smallest)
- p -- paragraph denotes a block of text seprated from other elements by new lines
- strong -- bolds text
- em -- italicizes text
- br -- line break
- hr -- horizontal rule creates a visible line in the document

## Links and Images

- a -- anchor element creates a link to another document or another part of the same document
  - Links in the same document are notated with an `#<anchortag>` in the href
  - Links to other docuemnts in the same site have the page as the href
  - External sites have the full url in the href
  - How the link opens can be specified with the target attribute
    - target="\_blank" -- opens a new browser tab or window
- img -- Images
  - src -- the location of the image file (local or remote)
  - alt -- A text description of the image for assistive technologies

## Lists and Tables

- Lists
  - ul -- Unordered Lists
  - ol -- Ordered List
  - li -- List Item
    Lists can be nested
- Tables
  - table -- top level table element encloses entire table
  - thead -- Denotes a table heading
  - tbody -- Denotes main body of table
  - tfooter -- Denotes the footer of the table
  - tr -- Denotes a table row for
  - th -- denotes a column heading
  - td -- Denotes a data element

## Forms and Input

- form -- Surround all the form elements and specifies what to do when form is submitted
  - action -- What should be done with the submitted form
  - method -- The HHTP method to send the form to the server [GET, POST, PUT, etc]
  - input -- Denotes a entry field can be one of the following types:
    - text -- Alpha numeric Characters. Default value can be set in value attribute. Also supports a placeholder for instructive text.
    - email -- Like text but must match the format of a valid email address [x@y.z]
    - number -- must be a numeric value has increment and decrement arrows on right edge of field
    - date -- Has styling to increment and decrement 1 day and a date picker
    - radio -- Displays a radio button. Other radio inputs with the same name will be mutually exclusive. Can have the option of checked to denote a default
    - checkbox -- Displays a checkbox. Multiple options with the same name are not exclusive.
  - textarea -- Allows long form text
  - select -- Displays a drop down list to select an item
    - option -- Specified one option in a select list for will return the attribute in value. add selected attribute to denote default selection
  - label -- attaches a label to an input field in a form
    - for -- the id of the input field the label is attached
  - submit -- Can be done two ways:
    1. `<input type="submit" value="Submit">`
    2. `<button type="submit">Submit</button>`
  - reset -- Reset the fields back to the form load values
    - `<button value='reset'>Reset</button>`

## Block and Inline Elements

- Block level elements take up the width of a page
- Inline only take up the space that the content needs the next element will be right next to it.

## Divs / Spans and IDs / Classes

- div -- Block level element to organize/style other elements
- span -- inline element to organize/style other elements
- id -- IDs are a name given to an element. Only one element on the page can have that id
- class -- Classes are also a name givin to an element. But a single class can apply to more than one element in the page.

## Entities and Symbols

- Used to insert special characters that are not available on a standard keyboard or need to be translatable to different charsets
  - `&copy;` -- &copy;
  - `&nbsp;` -- Non breaking space
  - `&gt;` -- Greater than
  - `&lt;` -- Less Than

## Semantic HTML

- header -- Header content such as logo and searchbox
- nav -- Navigation entries such as a main or feature menu
- main -- The main content of the page
- section -- seprates different sections
- article -- any type of repeatable content
- aside -- content not directly related to the main section
- footer -- Content such as copyright, ptivacy and TOS, contact info etc.
