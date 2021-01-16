# API Reference

Welcome to the Stratocart API. You can use this to access Stratocart API endpoints, which can get information about your shop & orders.

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.stratocart.com"
  --header 'X-APIKEY: yourapikey' \
  --header 'Content-Type: application/json' \
```

> Make sure to replace `yourapikey` with your API key.

Stratocart uses API keys to allow access to the API. To obtain an API key please go to https://www.stratocart.com

We expect for the API key to be included for all the private API requests in a header that looks like the following:

`X-APIKEY: yourapikey`

<aside class="notice">
You must replace <code>yourapikey</code> with your API key.
</aside>

We expect for the SHOPID to be included for all the public API requests in a header that looks like the following:

`X-SHOPID: yourshopid`

<aside class="notice">
You must replace <code>yourshopid</code> with your shop ID.
</aside>

## Cart

We expect for the shop_id to be included for all **/cart** API requests in a header that looks like the following:

`X-SHOPID: yourshopid`

_The X-APIKEY header will be ignored._

<aside class="notice">
The <strong>/cart</strong> methods are publicly accessible.
</aside>

### Get Cart

> Sample request for retrieving the cart data:

```shell
curl -x GET "https://api.stratocart.com/cart/a35a29b5-4a0d-4681-b070-ee19db86ed46" \
  -h 'X-SHOPID: 0a6c50ce-9006-4bda-bea4-2a6832f86684' \
```

`GET /cart or GET /cart/:cart_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |

If **cart_id** wasn't provided a new cart will be created, the cart_id will be available in the response.

If **cart_id** was provided but no cart exists, a new cart will be created with a new cart_id.

This method will return the updated [Cart](#cart) object on success or [Error](#error) on failure.

### Update Cart

> Sample request for emptying the cart items:

```shell
curl -x PATCH "https://api.stratocart.com/cart/a35a29b5-4a0d-4681-b070-ee19db86ed46" \
  -h 'X-SHOPID: 0a6c50ce-9006-4bda-bea4-2a6832f86684' \
  -h 'Content-Type: application/json' \
  -d '{"items": []}'
```

`PATCH /cart/:cart_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |

Pass the [Cart](#cart) object properties to be updated as body.

This method will return the updated [Cart](#cart) object on success or [Error](#error) on failure.

### Delete Cart

> Sample request for deleting the cart with all it's data:

```shell
curl -x DELETE "https://api.stratocart.com/cart/a35a29b5-4a0d-4681-b070-ee19db86ed46" \
  -h 'X-SHOPID: 0a6c50ce-9006-4bda-bea4-2a6832f86684' \
```

`DELETE /cart/:cart_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |

This method will **true** on success or [Error](#error) on failure.

## Cart Items

We expect for the shop_id to be included for all **/cartitems** API requests in a header that looks like the following:

`X-SHOPID: yourshopid`

_The X-APIKEY header will be ignored._

<aside class="notice">
The <strong>/cartitems</strong> methods are publicly accessible.
</aside>

### Add Item

> Sample request for adding an item to cart:

```shell
curl -x POST "https://api.stratocart.com/cartitems/a35a29b5-4a0d-4681-b070-ee19db86ed46" \
  -h 'X-SHOPID: 0a6c50ce-9006-4bda-bea4-2a6832f86684' \
  -h 'Content-Type: application/json' \
  -d '{"id": "HEADPHONES", "name": "Wireless Headphones", "price": 89, "quantity": 1, "description": "Something here to be updated", "images": ["https://www.stratocart.com/assets/images/product-1.jpg"]}'
```

> Sample cart item object:

```json
{
    "id": "HEADPHONES",
    "name": "Wireless Headphones",
    "price": 89,
    "quantity": 1,
    "description": "Something here to be updated",
    "images": ["https://www.stratocart.com/assets/images/product-1.jpg"]
}
```

Use this method to add new items to cart.

`POST /cartitems/:cart_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |

Pass the [CartItem](#cartitem) object as body.

This method will return the updated [Cart](#cart) object on success or [Error](#error) on failure.

### Update Item

`PUT /cartitems/:cart_id/:item_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |
| item_id   | The cart item ID   |

Pass the [CartItem](#cartitem) object as body.

This method will return the updated [Cart](#cart) object on success or [Error](#error) on failure.

### Remove Item

`DELETE /cartitems/:cart_id/:item_id`

| URL Param | Description        |
| --------- | ------------------ |
| cart_id   | The cart unique ID |
| item_id   | The cart item ID   |

This method will return the updated [Cart](#cart) object on success or [Error](#error) on failure.

## Orders

In progress.

## Shop

### Get Shop (public data)

```shell
curl -x GET "https://api.stratocart.com/shop" \
  -h 'X-SHOPID: 0a6c50ce-9006-4bda-bea4-2a6832f86684' \
```

`GET https://api.stratocart.com/shop`

We expect for the shop_id to be included in the API requests in a header that looks like the following:

`X-SHOPID: yourshopid`

This method will return the [Shop](#shop) object on success or [Error](#error) on failure.
