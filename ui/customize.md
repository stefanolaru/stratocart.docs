# Customizing UI

The UI is built using a JSON template which we convert to HTML. The JSON template is an array of objects representing the hierarchy of DOM elements (div, span, input) with their attributes, children, event handlers.

```json
{
        "tag": "div",
        "class": "step-header",
        "children": [
            {
                "tag": "h1",
                "text": "Checkout"
            },
            {
                "tag": "button",
                "html": "&times;",
                "class": ["button", "close-button"],
                "on": {
                    "click": "{{fn:closeCheckout}}"
                },
                "attrs": {
                    "data-x": "y",
                    "type": "button"
                }
            }
        ]
    },
```

Will output this HTML.

```html
<div class="step-header">
    <h1>Checkout</h1>
    <button data-x="y" type="button" class="button close-button">
        &times;
    </button>
</div>
```

## JSON template reference

| Property     | Type                | Description                                  |
| ------------ | ------------------- | -------------------------------------------- |
| **tag**      | String              | The DOM element                              |
| **class**    | String/Array/Object | The "class" attribute                        |
| **style**    | String/Array/Object | The "style" attribute                        |
| **text**     | String              | The text to be rendered inside (innerText)   |
| **html**     | String              | The HTML to be rendered (innerHTML)          |
| **children** | Array               | Children nodes (overrides text & html props) |
| **values**   | Array               | Options for the select fields                |
| **attrs**    | Object              | HTML attributes                              |
| **on**       | Object              | Event handlers                               |
| **model**    | String/Array        | The form input model                         |
| **if**       | Array               | Conditional logic                            |

## Event Handlers

**on** property is used to listen to DOM events and run some JavaScript when they're triggered. Multiple event listeners can be attached in name value pairs.

See [Functions & Variables](#functions-variables)

```json
{
    "tag": "button",
    "text": "Place Order",
    "on": {
        "click": "{{fn:submitCheckout}}"
    },
    "class": "button primary w-full",
    "attrs": {
        "type": "submit"
    }
}
```

## Data binding

The **model** is a two-way binding system, updates the template whenever the model changes and updates data model whenever the template changes. It uses the data fields from the [Cart](#cart) object and can be attached to any form input.

All template items with **model** property have the [on.input event handler](#event-handlers) attached by default, specifying an input handler will unbind the model from the input.

```json
{
    "tag": "input",
    "model": "shipping_address.city",
    "class": "input mb-4",
    "attrs": {
        "type": "text",
        "name": "shipping_city"
    }
}
```

## Input Validation

**model** validation rules are suported to validate user input and display errors. Pass the model as an Array<br /> **[<span style="color:#C00">model_name</span>, <span style="color:#C00">validation_rules</span>]**

The below example will make the customer.name a mandatory field and require the input value to be at least 2 chars.

```json
{
    "tag": "input",
    "model": [
        "customer.name",
        [
            {
                "rule": "required",
                "message": "Please enter your name"
            },
            {
                "rule": ["minLength", 2],
                "message": "Minimum length is 2 chars"
            }
        ]
    ],
    "class": "input mb-4",
    "attrs": {
        "type": "text",
        "name": "name",
        "placeholder": "Your name"
    }
}
```

Built-in validation rules

| Name          | Description                                                                               |
| ------------- | ----------------------------------------------------------------------------------------- |
| **required**  | Requires non-empty data. Checks for empty arrays and strings containing only whitespaces. |
| **minLength** | Requires the input to have a minimum specified length, inclusive                          |
| **maxLength** | Requires the input to have a maximum specified length, inclusive                          |
| **email**     | Accepts valid email addresses.                                                            |

## Conditional logic

The conditional logic allows to update DOM element properties dynamically, react to model data changes. The **if** property is an Array<br /> **[<span style="color:#C00">conditions</span>, <span style="color:#C00">properties_if_true</span>, <span style="color:#C00">properties_if_false</span>]**

The conditions will be declared as object of name/value pairs<br />

{**<span style="color:#C00">operator</span>**: **<span style="color:#C00">parameters</span>**}

The example below will switch the shipping address state field from a select dropdown to a text input based on shipping country input.

```json
{
    "model": "shipping_address.state",
    "if": [
        {
            "equals": ["{{shipping_address.country_code}}", "US"]
        },
        {
            "tag": "select",
            "values": "{{us_states}}"
        },
        {
            "tag": "input",
            "attrs": {
                "type": "text",
                "placeholder": "Region/County"
            }
        }
    ],
    "attrs": {
        "name": "state"
    }
}
```

## Vars & Functions

Built in variables and functions can be accessed/triggered using {{handlebars}} notation, functions will be prefixed with 'fn:'<br >

{{**<span style="color:#C00">variable_name</span>**}} or
{{**<span style="color:#C00">fn:functionName</span>**}}

Variables will access the cart data model.

Built in functions

| Name               | Description                                 |
| ------------------ | ------------------------------------------- |
| **closeCheckout**  | Close the checkout (back to shopping cart). |
| **submitCheckout** | Submit checkout form                        |
