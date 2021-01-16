# Hosted UI

Hosted UI is a small Javascript library that will help seamlessly integrate the shopping cart and checkout flow into a website.

Getting started is as easy:

1. Visit https://stratocart.com to get a shop ID.
2. Install stratocart.js via script tag.

```html
<script src="https://js.stratocart.com/latest.js"></script>
<script>
    window.Stratocart && window.Stratocart.init("shop/id");
</script>
```

Now, let's use this code to open/close the shopping cart element.

```javascript
// opens the cart
Stratocart.open();

// closes the cart
Stratocart.close();
```

Whoa! That's simple!
