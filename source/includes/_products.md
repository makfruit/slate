# Products


<!--
---------------------------------------------------------------------------------------------------------
    Get product details
---------------------------------------------------------------------------------------------------------
-->

## Get a product

### Request

> Request example

```http
GET /api/v3/4870020/products/123123?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}`

Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
<aside class="notice">
Parameters in bold are mandatory
</aside>

### Response

> Response example (JSON)

```json
{
    "id": 37208339,
    "sku": "00007",
    "thumbnailUrl": "http://app.ecwid.com/default-store/00007-230-sq.jpg",
    "quantity": 67,
    "inStock": true,
    "name": "Radish",
    "price": 1.15,
    "listPrice": 1.15,
    "wholesalePrices": [
        {
            "quantity": 10,
            "price": 1.05
        }
    ],
    "compareToPrice": 1.34,
    "weight": 0.31,
    "url": "http://app.ecwid.com/store/4870020#!/~/product/id=37208339",
    "created": "2009-07-23 17:22:37 +0400",
    "lastUpdateTime": "2014-07-30 10:32:37 +0400",
    "productClassId": 0,
    "enabled": true,
    "options": [
        {
            "type": "RADIO",
            "name": "Size",
            "choices": [
                {
                    "text": "Small",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                },
                {
                    "text": "Large",
                    "priceModifier": 0.5,
                    "priceModifierType": "ABSOLUTE"
                }
            ],
            "defaultChoice": 0,
            "required": false
        },
        {
            "type": "SELECT",
            "name": "Color",
            "choices": [
                {
                    "text": "Red",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                },
                {
                    "text": "White",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                }
            ],
            "defaultChoice": 0,
            "required": false
        }
    ],
    "warningLimit": 0,
    "fixedShippingRateOnly": false,
    "fixedShippingRate": 0,
    "defaultCombinationId": 7084076,
    "imageUrl": "http://app.ecwid.com/default-store/00007-sq.jpg",
    "smallThumbnailUrl": "http://app.ecwid.com/default-store/00007-80-sq.jpg",
    "description": "<h5>Radish</h5>\n<p>The radish (Raphanus sativus) is an edible root vegetable of the Brassicaceae family that was domesticated in Europe in pre-Roman times. They are grown and consumed throughout the world. Radishes have numerous varieties, varying in size, color and duration of required cultivation time. There are some radishes that are grown for their seeds; oilseed radishes are grown, as the name implies, for oil production.</p>\n<p> </p>\n<div style=\"padding: 24px 24px 24px 21px; display: block; background-color: #ececec;\">From <a style=\"color: #1e7ec8; text-decoration: underline;\" title=\"Wikipedia\" href=\"http://en.wikipedia.org\">Wikipedia</a>, the free encyclopedia</div>",
    "galleryImages": [
        {
            "alt": "Radish with friends",
            "url": "http://images-cdn.ecwid.com/images/4870020/237132118.jpg",
            "thumbnail": "http://images-cdn.ecwid.com/images/4870020/237132119.jpg",
            "width": 220,
            "height": 293
        }
    ],
    "categoryIds": [
        9691095
    ],
    "defaultCategoryId": 9691095,
    "attributes": [
        {
            "id": 5029057,
            "name": "Brand",
            "value": "SuperVegetables"
        }
    ],
    "files": [],
    "relatedProducts": {
        "productIds": [
            37208340,
            37208340
        ],
        "relatedCategory": {
            "enabled": true,
            "categoryId": 9691095,
            "productCount": 1
        }
    },
    "combinations": [
        {
            "id": 7084071,
            "combinationNumber": 6,
            "options": [
                {
                    "name": "Color",
                    "value": "White"
                },
                {
                    "name": "Size",
                    "value": "Large"
                }
            ],
            "sku": "000076",
            "quantity": 1,
            "unlimited": false,
            "weight": 0.41,
            "warningLimit": 1
        },
        {
            "id": 7084072,
            "combinationNumber": 5,
            "options": [
                {
                    "name": "Color",
                    "value": "Red"
                },
                {
                    "name": "Size",
                    "value": "Large"
                }
            ],
            "sku": "000075",
            "quantity": 0,
            "unlimited": false,
            "weight": 0.41,
            "warningLimit": 0
        },
        {
            "id": 7084075,
            "combinationNumber": 2,
            "options": [
                {
                    "name": "Size",
                    "value": "Small"
                },
                {
                    "name": "Color",
                    "value": "White"
                }
            ],
            "sku": "000072",
            "quantity": 67,
            "unlimited": true,
            "warningLimit": 0
        },
        {
            "id": 7084076,
            "combinationNumber": 1,
            "options": [
                {
                    "name": "Size",
                    "value": "Small"
                },
                {
                    "name": "Color",
                    "value": "Red"
                }
            ],
            "sku": "000071",
            "quantity": 61,
            "unlimited": false,
            "warningLimit": 0
        }
    ]
}
```


A JSON object of type 'Product' with the following fields:

#### Product
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Unique integer product identifier
sku | string |  Product SKU. Items with options can have several SKUs specified in the product combinations.
quantity |  number | Amount of product items in stock. *This field is omitted for the products with unlimited stock*
inStock | boolean | `true` if the product or any of its combinations is in stock (quantity is more than zero) or has unlimited quantity. `false` otherwise.
name |  string |  Product title
price | number |  Base product price
listPrice | number |  Product price displayed in the product list. May differ from the *price* value when the product has combinations and the default combination's price is different from the base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
weight |  number | Product weight in the units defined in store settings. *Omitted for intangible products*
url | string |  URL of the product's details page in the store
created | string | Date and time of the product creation. Example: `2014-07-30 10:32:37 +0400`
lastUpdateTime |  string | Product last update date/time
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` if product is enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | A list of the product options. Empty (`[]`) if no options are specified for the product. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
defaultCombinationId |  number |  Identifier of the default product combination, which is defined by the default values of product options.
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 500x500. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 80x80. *The original uploaded product image is available in the `originalImageUrl` field.*
originalImageUrl |  string  | URL of the original not resized product image
description | string  | Product description *in HTML*
galleryImages | Array\<*GalleryImage*\> |  List of the product gallery images
categoryIds | Array\<number\> | List of the categories, which the product belongs to
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<*AttributeValue*\> | Product attributes and their values
files | Array\<*ProductFile*\> | Downloadable files (E-goods) attached to the product
relatedProducts | [RelatedProducts*  | Related or "You may also like" products of the product
combinations | Array\<*Combination*\> | List of the product combinations

#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
quantity |  number |  Number of product items on this wholesale tier
price | number |  Product price on the tier

#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
name |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *This field is omitted for the product option with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection. Only presents if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`

#### GalleryImage
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
alt | string |  Image description, displayed in the image tag's *alt* attribute
url | string |  Image URL
thumbnail | string  | Image thumbnail URL resized to fit 46x42px box
width | number |  Image width
height |  number |  Image height

#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Unique attribute ID. See [Product Classes](#product-classes) for the information on attribute IDs
name |  string |  Attribute displayed name
value | string  | Attribute value

#### ProductFile
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Internal ID of the file 
name |  string |  File name
description | string |  File description defined by the store administrator
size |  number |  File size, bytes (64-bit integer)

#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
productIds | Array\<number\>  | IDs of the related products
relatedCategory | *RelatedCategory*  | Describes the "N random related products from a category" option

#### RelatedCategory
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
categoryId |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related

#### Combination
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Combination ID
combinationNumber | number |  Combination # number, which is displayed in the combinations table in Control panel
options | Array\<*OptionValue*\> | Set of options that identifies this combination. An array of name-value pairs
sku | string  | Combination SKU. `null` means the combinations inherits the base product's SKU
smallThumbnailUrl | string  | URL of the combination thumbnail resized to fit 80x80 px box. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
thumbnailUrl |  string  | URL of the combination thumbnail displayed on the product list pages if the combination is default one. Thumbnails size is defined in the store settings and the same as the product thumbnail size. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the combination image resized to fit 500x500. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
originalImageUrl |  string  | URL of the original not resized combination image. `null` means the combinations inherits the base product's image.
quantity |  number  | Amount of the combination items in stock. `null` means the combinations inherits the base product's quantity.
unlimited | boolean | `true` if the combination is unlimited (that is, never runs out)
price | number  | Combination price. `null` means the combinations inherits the base product's price.
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of the combination's wholesale price tiers (quantity limit and price). `null` means the combinations inherits the base product's tiered price settings. 
weight |  number  |  Combination weight in the units defined in store settings. `null` means the combinations inherits the base product's weight.
warningLimit | number | The minimum 'warning' amount of the product items in stock for this combination, if set. When the combination in stock amount reaches this level, the store administrator gets an email notification. `null` means the combinations inherits the base product's settings.


#### OptionValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
name |  string |  Option name
value | string |  Option value

#### ProductOptionChoice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
text |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

### Errors

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Meaning
------------|--------
404 | Product is not found
500 | Cannot get the product because of an error on the server

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Create product
---------------------------------------------------------------------------------------------------------
-->

## Add a product

### Request

> Request body

```http
POST /api/v3/4870020/products?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
  "sku": "000012199",
  "quantity": 10,
  "inStock": true,
  "name": "New Product",
  "price": 20.99,
  "compareToPrice": 24.99,
  "categoryIds": [
    9691094
  ],
  "weight": 10,
  "enabled": true,
  "description": "A <b>new</b> product description",
  "productClassId": 0,
  "created":"2014-01-01",
  "fixedShippingRateOnly": false,
  "fixedShippingRate": 1.2
}
```


`POST https://app.ecwid.com/api/v3/{storeId}/products?token={token}`


Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**token** |  string |  oAuth token


### Request body

A JSON object of type 'Product' with the following fields:

#### Product
Field | Type |  Description
------| ---- | ------------
**sku** | string |  Product SKU
**name** |  string |  Product title
quantity |  number | Amount of product items in stock. Leave empty for the products with unlimited stock
price | number |  Base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
weight |  number | Product weight in the units defined in store settings. *Leave empty for intangible products*
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` to make product enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | List of the product options. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
description | string  | Product description *in HTML*
categoryIds | Array\<number\> | List of the categories, which the product belongs to
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<*AttributeValue*\> | Product attributes and their values
relatedProducts | [RelatedProducts*  | Related or "You may also like" products of the product


#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier


#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`


#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**id** |  number |  Unique attribute ID. See [Product Classes](#product-classes) for the information on attribute IDs
value | string  | Attribute value

#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**productIds** | Array\<number\>  | IDs of the related products
relatedCategory | *RelatedCategory*  | Describes the "N random related products from a category" option

#### RelatedCategory
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
**categoryId** |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related

#### OptionValue
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
**name** |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**text** |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

<aside class="notice">
Parameters in bold are mandatory
</aside>


### Response


> Response example

```json
{
    "id": 39766764,
    "message": "Successfully created",
    "success": true
}
```

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
id | number | ID of the created product
message | string | Status message 
success | boolean | `true` if the product has been created, `false` otherwise


### Errors

```http
HTTP/1.1 409 Conflict
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description.

#### HTTP codes

**HTTP Status** | **Response JSON** | **Description**
-------------- | -------------- | --------------
400 | Request parameters are malformed
409 | The product with such SKU already exists
402 | The functionality/method is not available on the merchant plan
402 | The merchant plan product limit is reached
404 | Some of the linked entities in the request doesn't exist. For example, the product class is not found

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Edit product
---------------------------------------------------------------------------------------------------------
-->

## Update a product

> Request example

```http
PUT /api/v3/4870020/products/39766764?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

{
  "compareToPrice": 24.99,
  "categoryIds": [
    9691094
  ]
}
```

`PUT https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}`


Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token


### Request body

A JSON object of type 'Product' with the following fields:

#### Product
Field | Type |  Description
------| ---- | ------------
sku | string |  Product SKU
name |  string |  Product title
quantity |  number | Amount of product items in stock. Leave empty for the products with unlimited stock
price | number |  Base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
weight |  number | Product weight in the units defined in store settings. *Leave empty for intangible products*
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` to make product enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | List of the product options. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
description | string  | Product description *in HTML*
categoryIds | Array\<number\> | List of the categories, which the product belongs to
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<*AttributeValue*\> | Product attributes and their values
relatedProducts | [RelatedProducts*  | Related or "You may also like" products of the product

<aside class="notice">
All fields are optional
</aside>


#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier


#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`


#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**id** |  number |  Unique attribute ID. See [Product Classes](#product-classes) for the information on attribute IDs
value | string  | Attribute value

#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**productIds** | Array\<number\>  | IDs of the related products
relatedCategory | *RelatedCategory* | Describes the "N random related products from a category" option


#### RelatedCategory
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
**categoryId** |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related


#### OptionValue
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
**name** |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**text** |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.


### Response

> Response example (JSON)

```json
{
  "message": "Product was successfully updated",
  "updateCount": 1,
  "success": true
}
```

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus

Field | Type |  Description
-------------- | -------------- | --------------
message | string | Status message 
updateCount | number | The number of updated products (`1` or `0` depending on whether the update was successful)
success | boolean | `true` if the product has been updated, `false` otherwise

### Errors

```http
HTTP/1.1 400 Bad Request
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Description
-------------- | --------------
400 | Request parameters are malformed
409 | The product with such SKU already exists
402 | The functionality/method is not available on the merchant plan
402 | The merchant plan product limit is reached
404 | Some of the linked entities in the request doesn't exist. For example, the product class is not found

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Delete product
---------------------------------------------------------------------------------------------------------
-->

## Delete a product

> Request example

```http
DELETE /api/v3/4870020/products/39847403?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

### Response

> Response example

```json
{
    "message":"",
    "deleteCount":1,
    "success":true
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

Field | Type |  Description
----- | ---- | --------------
message | string | Status message 
deleteCount | number | The number of deleted products (`1` or `0` depending on whether the request was successful)
success | boolean | `true` if the product has been deleted, `false` otherwise



<!--
---------------------------------------------------------------------------------------------------------
    Upload product image
---------------------------------------------------------------------------------------------------------
-->

## Upload product image

Upload product image: if the product already has an image attached, the uploaded image will replace the existing one.

> Request example

```http
POST /api/v3/4870020/products/1234657/image?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

binary data
```

`POST https://app.ecwid.com/api/v3/{storeId}/products/{productId}/image?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

### Response

> Response example

```json
{
    "id": 240198557
}
```

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** | **Type** |  **Description**
--------- | ---------| -----------
id |    number | Internal image ID

### Errors

> Error response example 

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8

{
    "errorMessage": "Internal server error"
}
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | **Description**
--------- | -----------| -----------
500 | Uploading of the image file failed or there was an internal server error while processing a file
404 | Product is not found
413 | The image file is too large
400 | Request parameters are malformed
402 | The functionality/method is not available on the merchant plan

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Delete product image
---------------------------------------------------------------------------------------------------------
-->

## Delete product image

> Request example

```http
DELETE /api/v3/4870020/products/1234657/image?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/image?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

### Response

> Response example

```json
{
    "deleteCount": 1,
    "success": true
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted images (`1` or `0` depending on whether the request was successful)
success | boolean | `true` if the image has been deleted, `false` otherwise

### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | **Description**
--------- | -----------| -----------
500 | Deleting of the image file failed or there was an internal server error
404 | Product is not found

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message




<!--
---------------------------------------------------------------------------------------------------------
    Upload product file
---------------------------------------------------------------------------------------------------------
-->

## Upload product file

> Request example

```http
POST /api/v3/4870020/products/1234567/files?token=123456789abcd&fileName=photo+large.psd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

binary data
```

Uploading a product file (e-goods)


`POST https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files?token={token}&fileName={fileName}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
fileName | string | Name of the file that customers will see


### Response

> Response example

```json
{
    "id": 6738222
}
```

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
Field | Type |  Description
--------- | ---------| -----------
id | number | Internal file ID

### Errors

> Error response example 

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8

{
    "errorMessage": "Internal server error"
}
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | **Description**
--------- | -----------| -----------
500 | Uploading of the file failed or there was an internal server error while processing a file
404 | Product is not found
413 | The file is too large
400 | Request parameters are malformed
402 | The functionality/method is not available on the merchant plan

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message



<!--
---------------------------------------------------------------------------------------------------------
    Delete product egoods file
---------------------------------------------------------------------------------------------------------
-->

## Delete product file

> Request example

```http
DELETE /api/v3/4870020/products/1234657/files/193639?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

*Delete product's file (e-goods) by the file ID*

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files/{fileId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**fileId** | number | Internal file ID
**token** |  string |  oAuth token

### Response

> Response example

```json
{
    "deleteCount": 1,
    "success": true
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted files (`1` or `0` depending on whether the request was successful)
success | boolean | `true` if the file has been deleted, `false` otherwise

### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | **Description**
--------- | -----------| -----------
500 | Deleting of the file failed or there was an internal server error
404 | Product is not found

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message



<!--
---------------------------------------------------------------------------------------------------------
    Delete all product egoods files
---------------------------------------------------------------------------------------------------------
-->

## Delete all product files

> Request example

```http
DELETE /api/v3/4870020/products/39847403/files?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

*Remove all downloadable files attached to the product (e-goods)*

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

### Response

> Response example

```json
{
    "deleteCount": 3,
    "success": true
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted files
success | boolean | `true` if the deletion was successful, `false` otherwise

### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | **Description**
--------- | -----------| -----------
500 | Deleting of the files failed or there was an internal server error
404 | Product is not found

#### Error response body (optional)

**Field** | **Type** |  **Description**
--------- | ---------| -----------
errorMessage | string | Error message