# Customizing UI

The UI is built from a JSON schema, HTML code is outputed as below.

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

## JSON schema reference

| Property | Type                | Description                                                        |
| -------- | ------------------- | ------------------------------------------------------------------ |
| tag      | String              | The tag to be rendered (defaults to div)                           |
| children | Array               | Children nodes                                                     |
| class    | String/Array/Object | The "class" attribute                                              |
| style    | String/Array/Object | The "style" attribute                                              |
| text     | String              | The text to be rendered inside (innerText)                         |
| html     | String              | The HTML to be rendered (innerHTML)                                |
| attrs    | Object              | HTML attributes                                                    |
| model    | String              | The model to link with the form input (only for form input fields) |
| validate | Array               | The model validation rules                                         |
| on       | Object              | Event handlers                                                     |
| if       | Array               | Conditional logic                                                  |
