# Customizing UI

The UI is built from a JSON schema, HTML code will be outputed as referenced below.

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

Will output this.

```html
<div class="step-header">
    <h1>Checkout</h1>
    <button data-x="y" type="button" class="button close-button">
        &times;
    </button>
</div>
```
