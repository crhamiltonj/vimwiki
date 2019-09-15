# Forms and Input

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