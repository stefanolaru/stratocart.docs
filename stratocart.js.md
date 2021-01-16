# stratocart.js

```html
<script src="https://js.stratocart.com/latest.js"></script>
<script>
    window.Stratocart && window.Stratocart.init("shop/id");
</script>
```

stratocart.js is a small Javascript library that will help seamlessly integrate the shopping cart and checkout flow into a website.

Getting started is as easy:

1. Visit https://stratocart.com to get a shop ID.
2. Install stratocart.js via script tag.

```js
// opens the cart
Stratocart.open();

// closes the cart
Stratocart.close();
```

Now, let's use this code to open/close the shopping cart element.

Whoa! That's simple!

## Add an item

```js
Stratocart.addItem({
    id: "unique-product-id",
    name: "My nice Product",
    quantity: 1,
    price: 7999,
})
    .then((item) => {
        // successfully added to cart
        console.log(item.name + " was added to cart");
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Add an item to the shopping cart.

_Returns a Promise_

| Property | Type     | Description                     |
| -------- | -------- | ------------------------------- |
| id       | String\* | The item unique ID              |
| name     | String\* | Item name                       |
| price    | Int\*    | Item price in cents (price/100) |
| quantity | Int\*    | Item quantity                   |

See the complete list of [CartItem properties](#cartitem)

## Update an item

```js
Stratocart.updateItem("unique-product-id", {
    quantity: 3,
})
    .then((item) => {
        // successfully updated
        console.log(item.name + " was updated");
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Update properties of a single cart item by ID.

See the complete list of [CartItem properties](#cartitem)

_Returns a Promise_

## Remove an item

```js
Stratocart.removeItem("unique-product-id")
    .then((item) => {
        // successfully removed
        console.log(item.name + " was removed from the cart");
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Remove a single item from the cart by ID.

_Returns a Promise_

## Fetch Cart

```js
Stratocart.fetch()
    .then((cart) => {
        // successfully returned the updated cart object
        console.log(cart);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Refresh the cart object from the API.

_Returns a Promise with the full [Cart](#cart) object on success_

## Update Cart

```js
Stratocart.update({
    shipping_method: "express",
})
    .then((cart) => {
        // successfully returned the updated cart object
        console.log(cart);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Updates the [Cart](#cart) object properties.

_Returns a Promise with the full [Cart](#cart) object on success_

## Delete Cart

```js
Stratocart.delete()
    .then(() => {
        // successfully deleted the cart
        console.log(cart);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Deletes the cart session from the API.

_Returns a Promise_

## Get cart items

```js
Stratocart.getItems()
    .then((items) => {
        // successfully returned the array of items
        // loop through the array of items
        if (items.length) {
            items.forEach((item) => {
                console.log(item.name);
            });
        }
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Get the list of items from the cart.

_Returns a Promise with an array of [CartItem](#cartitem) on success_

## Empty the cart

```js
Stratocart.empty()
    .then(() => {
        // successfully emptied the cart
        console.log("The cart was emptied");
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Removes all items from the cart.

_Returns a Promise_

## Set Customer

```js
Stratocart.setCustomer({
    email: "john.doe@stratocart.com",
    name: "John Doe",
})
    .then((cart) => {
        // successfully updated customer info
        console.log("The customer was updated.");
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

Update the cart with customer information.

_Returns a Promise with the full [Cart](#cart) object on success_

## Set Shipping Info

```js
// set shipping amount
Stratocart.setShippingAmount(amount)
    .then((cart) => {
        // successfully updated shipping amount
        console.log(cart.shipping_amount);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });

// set shipping address
Stratocart.setShippingAddress(address)
    .then((cart) => {
        // successfully updated shipping address
        console.log(cart.shipping_address);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });

// set shipping method
Stratocart.setShippingMethod(method)
    .then((cart) => {
        // successfully updated shipping method
        console.log(cart.shipping_method);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

### setShippingAmount(amount)

Update the shipping amount. Helpful when you want to set the shipping costs from external source.

| Parameter | Type  | Description                         |
| --------- | ----- | ----------------------------------- |
| amount    | Int\* | Shipping price in cents (price/100) |

_Returns a Promise with the full [Cart](#cart) object on success_

### setShippingAddress(address)

Update the shipping address.

| Parameter | Type     | Description                          |
| --------- | -------- | ------------------------------------ |
| address   | Object\* | Shipping address [Address](#address) |

_Returns a Promise with the full [Cart](#cart) object on success_

### setShippingMethod(method)

Update the shipping method.

| Parameter | Type     | Description        |
| --------- | -------- | ------------------ |
| method_id | String\* | Shipping method ID |

_Returns a Promise with the full [Cart](#cart) object on success_

## Set Billing Info

```js
// set billing address
Stratocart.setBillingAddress(address)
    .then((cart) => {
        // successfully updated billing address
        console.log(cart.billing_address);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });

// set billing method
Stratocart.setBillingMethod(method)
    .then((cart) => {
        // successfully updated billing method
        console.log(cart.billing_method);
    })
    .catch((err) => {
        // oops something bad happened
        console.error(err);
    });
```

### setBillingAddress(address)

Update the billing address.

| Parameter | Type     | Description                         |
| --------- | -------- | ----------------------------------- |
| address   | Object\* | Billing address [Address](#address) |

_Returns a Promise with the full [Cart](#cart) object on success_

### setBillingMethod(method)

Update the billing method.

| Parameter | Type     | Description       |
| --------- | -------- | ----------------- |
| method_id | String\* | Billing method ID |

_Returns a Promise with the full [Cart](#cart) object on success_

## Events

These events will fire anytime an action happen in the shopping cart or checkout flow. Use listeners to customise the experience.

```js
Stratocart.on("ready", (data) => {
    // GumCart is loaded, do something here
});
```

```js
Stratocart.on("totals.change", (data) => {
    // GumCart totals change, console log the amounts
    console.log("Shipping: $" + data.shipping_price);
    console.log("Tax: $" + data.tax_amount);
    console.log("Total amount: $" + data.total_amount);
});
```

| Event name      | Data     | Description                |
| --------------- | -------- | -------------------------- |
| ready           | -        | The cart is loaded & ready |
| open            | -        | The shopping cart opened   |
| close           | -        | The shopping cart closed   |
| item.added      | item     | Item was added to cart     |
| item.updated    | item     | The cart item was updated  |
| item.removed    | item     | Item was removed from cart |
| customer.change | customer | Customer data was updated  |
| shipping.change | shipping | Shipping info was updated  |
| billing.change  | billing  | Billing info was updated   |
| order.create    | order    | The order was created      |
