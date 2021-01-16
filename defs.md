# Object Definitions

Common object definitions

## Cart

```json
{
    "cart_id": "0a6c50ce-9006-4bda-bea4-2a6832f86684",
    "items": [
        // Array of CartItem
    ],
    "created": 1610181890,
    "updated": 1610181900,
    "expires": 1611391500, // updated + 14 days
    "items_amount": 0,
    "customer": {
        // customer info
    },
    "shipping_amount": 0,
    "shipping_address": {
        // shipping address
    },
    "shipping_method": null,
    "billing_method": null,
    "billing_address": {
        // billing address
    },
    "tax_amount": 0,
    "total_amount": 0
}
```

| Property         | Type   | Description                             |
| ---------------- | ------ | --------------------------------------- |
| _cart_id_        | String | The cart unique identifier              |
| items            | Array  | Items in the cart [CartItem](#cartitem) |
| _created_        | Int    | The UNIX timestamp the cart was created |
| _updated_        | Int    | The UNIX timestamp the cart was updated |
| _expires_        | Int    | The UNIX timestamp the cart will expire |
| items_amount     | Int    | The total amount of the cart items      |
| customer         | Object | Customer [Customer](#customer)          |
| shipping_amount  | Int    | The items shipping amount               |
| shipping_address | Object | Shipping address [Address](#address)    |
| shipping_method  | String | The shipping method ID                  |
| billing_address  | Object | Billing address [Address](#address)     |
| billing_method   | String | The shipping method ID                  |
| tax_amount       | Int    | The items tax amount                    |
| _total_amount_   | Int    | The total amount of the cart            |

<aside class="notice">
The <em>emphasized</em> properties are read only. <br />The fields marked with <strong>*</strong> are required
</aside>

## CartItem

```json
{
    "id": "SPARKRC900TEAM",
    "name": "Scott Spark RC900 Team Bike",
    "description": "The SCOTT Spark RC is perhaps the most successful full-suspension XC race bike of its time.",
    "price": 359998,
    "quantity": 1,
    "images": ["https://placehold.it/1600x1200"],
    "options": [
        {
            "name": "Color",
            "value": "Orange"
        },
        {
            "name": "Size",
            "value": "M"
        }
        // ...
    ],
    "addons": [
        {
            "name": "Syncros Bottle Cage (Left)",
            "price": 999
        }
        // ...
    ],
    "metadata": {}
}
```

The cart item object reference. The cart item object is flexible, you can extend it using the **meta** property.

| Property    | Type     | Description                              |
| ----------- | -------- | ---------------------------------------- |
| id          | String\* | The item unique ID                       |
| name        | String\* | Item name                                |
| description | String   | Item description                         |
| price       | Int\*    | Item price in cents (price/100)          |
| quantity    | Int\*    | Item quantity                            |
| images      | Array    | Image URLs (must be publicly accessible) |
| options     | Array    | [CartItemOption](#cartitemoption)        |
| addons      | Array    | [CartItemAddon](#cartitemaddon)          |
| metadata    | Object   | Custom meta object                       |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>

## CartItemOption

```json
{
    "name": "Size",
    "value": "Medium"
}
```

Use for CartItem that have options (like colors and sizes).

| Property | Type     | Description  |
| -------- | -------- | ------------ |
| name     | String\* | Option name  |
| value    | String\* | Option value |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>

## CartItemAddon

```json
{
    "name": "Size",
    "price": 200
}
```

Use for CartItem that have addons (like extra bacon).

| Property | Type     | Description                      |
| -------- | -------- | -------------------------------- |
| name     | String\* | Option name                      |
| price    | Int\*    | Addon price in cents (price/100) |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>

## Checkout

```json
{
    "cart_id": "0a6c50ce-9006-4bda-bea4-2a6832f86684",
    "customer": {},
    "shipping_address": {},
    "billing_address": {}
}
```

| Property | Type     | Description                          |
| -------- | -------- | ------------------------------------ |
| shop_id  | String\* | The shop unique identifier           |
| cart_id  | String\* | The cart item unique identifier      |
| customer | Object   | Customer [Customer](#customer)       |
| billing  | Object   | Billing address [Address](#address)  |
| shipping | Object   | Shipping address [Address](#address) |

## Customer

The customer object reference.

## Address

```json
// example of the address object
{
    "company": "",
    "name": "Marissa Doe",
    "line1": "132 Harvest Way",
    "line2": "",
    "city": "Crandall",
    "state": "TX",
    "postal_code": "75114",
    "country": "US"
}
```

| Field       | Type   | Description                                 |
| ----------- | ------ | ------------------------------------------- |
| company     | String | Company name                                |
| name        | String | Recipient name                              |
| line1       | String | Address line 1                              |
| line2       | String | Address line 2                              |
| city        | String | The address city                            |
| state       | String | The address state/county/provice            |
| postal_code | String | The address post/zip code                   |
| country     | String | The address country (ISO 3166 Alpha-2 code) |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>

## Error

```json
{
    "error": "The hepful but dreaded error message"
}
```

The API uses the following error codes:

| Code | Meaning                                                                                   |
| ---- | ----------------------------------------------------------------------------------------- |
| 400  | Bad Request -- Your request is invalid.                                                   |
| 401  | Unauthorized -- Your API key is wrong.                                                    |
| 403  | Forbidden -- You're not allowed to access that listing.                                   |
| 404  | Not Found -- The specified listing could not be found.                                    |
| 405  | Method Not Allowed -- You tried to access listing with an invalid method.                 |
| 500  | Internal Server Error -- We had a problem with our server. Try again later.               |
| 503  | Service Unavailable -- We're temporarily offline for maintenance. Please try again later. |
