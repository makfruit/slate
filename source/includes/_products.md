# Products

## Get a product

### Request

> Request example

```shell
curl "https://app.ecwid.com/api/v3/4870020/products/37208339?token=1234567890abcde"
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
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
weight |  number | Product weight in the units defined in store settings. *Omitted for intangible products*
url | string |  URL of the product's details page in the store
created | string | Date and time of the product creation. Format TODO
lastUpdateTime |  string | Product last update date/time. Can be null for products that were created before this. TODO: check for just created products
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` if product is enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product. TODO: check if it's empty or omitted
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
defaultCombinationId |  number |  Identifier of the default product combination, which is defined by the default values of product options.
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 500x500. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 80x80. *The original uploaded product image is available in the `originalImageUrl` field.*
originalImageUrl |  string  | URL of the original not resized product image
description | string  | Product description *in HTML*
galleryImages | Array\<[GalleryImage](http://google.com)\> |  List of the product gallery images
categoryIds | Array\<number\> | List of the categories, which the product belongs to
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<[AttributeValue](http://google.com)\> | Product attributes and their values
files | Array\<[ProductFile](http://google.com)\> | Downloadable files (E-goods) attached to the product
relatedProducts | [RelatedProducts](http://google.com)  | Related or "You may also like" products of the product
combinations | Array\<[Combination](http://google.com)\> | List of the product combinations

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
choices | Array\<[ProductOptionChoice](http://google.com)\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *This field is omitted for the product option with no selection (e.g. text, datepicker or upload file options)*
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
relatedCategory | [RelatedCategory](http://google.com)  | Describes the "N random related products from a category" option

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
options | Array\<[OptionValue](http://google.com)\> | Set of options that identifies this combination. An array of name-value pairs
sku | string  | Combination SKU. `null` means the combinations inherits the base product's SKU
smallThumbnailUrl | string  | URL of the combination thumbnail resized to fit 80x80 px box. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
thumbnailUrl |  string  | URL of the combination thumbnail displayed on the product list pages if the combination is default one. Thumbnails size is defined in the store settings and the same as the product thumbnail size. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the combination image resized to fit 500x500. `null` means the combinations inherits the base product's image. *The original uploaded combination image is available in the `originalImageUrl` field.*
originalImageUrl |  string  | URL of the original not resized combination image. `null` means the combinations inherits the base product's image.
quantity |  number  | Amount of the combination items in stock. `null` means the combinations inherits the base product's quantity.
unlimited | boolean | `true` if the combination is unlimited (that is, never runs out)
price | number  | Combination price. `null` means the combinations inherits the base product's price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  Sorted array of the combination's wholesale price tiers (quantity limit and price). `null` means the combinations inherits the base product's tiered price settings. 
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
**HTTP Status** | **Response JSON** | **Description**
-------------- | -------------- | --------------
404 | [NotFoundError](#notfounderror) TODO: link | Product is not found
500 | [InternalError](#internalerror) TODO: link | Cannot get the product due to an error on the server. 


## Add a product

Add a product

### URL

`POST /storeId/products?token=string`

### URL Parameters

**Name** |  **Type** |  **Description**
-------------- | -------------- | --------------
storeId* |  number |  ID of the Ecwid store.
token* |  string |  Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Product' with the following fields:

#### Product
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
sku* |  string |  Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
quantity |  number |  
inStock* |  boolean | `true` if any of the product combinations or the product itself has positive quantity or is unlimited.
name* | string |  Product name as a plain text.
price* |  number |  Basic product price.
listPrice* |  number |  The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs. Default is empty.
compareToPrice |  number  | 'Compare To' price shown strike-out in the customer frontend.
weight | number |  Product weight in the units defined in store settings. *Omit for intangible products*
created* |  string |  Product creation date/time.
lastUpdateTime |  string  | Product last update date/time. Can be null for products that were created before this.
productClassId* | number |  Id of a product class this product belongs to (like 'Books'). Zero `0` value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled* |  boolean | `true` if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product. Default is empty.
warningLimit |  number |  The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly* |  boolean  |  `true` if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate* |  number |  For fixedShippingRateOnly=`true`, this value is used instead of the shipping. For `fixedShippingRateOnly=false`, this value adds to the shipping cost.
description | string  | Product description in HTML.
categoryIds | Array\<number\> | A list of categories which this product belongs to. Default is empty.
defaultCategoryId | number   |  Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> | If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor. Default is empty.
relatedProducts | RelatedProducts | The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *Fields in bold are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier
\* *Fields in bold are mandatory.*

#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<[ProductOptionChoice](http://google.com)\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`
\* *Fields in bold are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*


#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**id** |  number |  Unique attribute ID. See [Product Classes](#product-classes) for the information on attribute IDs
value | string  | Attribute value
\* *Fields in bold are mandatory.*

#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
productIds | Array\<number\>  | IDs of the related products
relatedCategory | [RelatedCategory](http://google.com)  | Describes the "N random related products from a category" option

#### Combination
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
combinationNumber* |  number |  A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<OptionValue\> |  Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku | string  | If present, combination SKU, unique code. If null, product sku is assumed.
quantity |  number   |  Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited | boolean | `true`, if the combination is unlimited (that is, never runs out).
price | number  | Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |  number  |
tangible |  boolean  |  `true` if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |  number |  The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |  number |  Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields in bold are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
enabled | boolean | Флаг включенности выбора связанных товаров из категории
categoryId |  number |  Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |  number |  Number of random products from a given category (or from all store, if categoryId==0), which should be shown as a related products of a given product.
\* *Fields in bold are mandatory.*

#### OptionValue
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
name |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text
\* *Fields in bold are mandatory.*

#### ProductOptionChoice
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
text* | string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* | number | Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`
priceModifierType* | string | Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT`. Default is `ABSOLUTE`.
\* *Fields in bold are mandatory.*

### Response

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
message | string | Детальное сообщение о том, как прошло создание сущности
success | boolean | Успешно ли прошло создание

### Errors

**HTTP Status** | **Response JSON** | **Description**
-------------- | -------------- | --------------
400 | [IllegalParameterError](#illegalparametererror) | Некоторые парамеры в запросе заданы неверно
409 | [NonUniqueError](#nonuniquerror) |  Продукт с таким sku уже существует
402 | [PaidFeatureError](#paidfeatureerror) | Запрошена функциональность не доступная для данного плана
402 | [LimitError](#limiterror) | Уперлись в лимит на количество товаров для данного плана
404 | [NotFoundError](#notfounderror) | Сущность, на которую есть ссылка в продукте, не существует(например на продуктовый класс)


## Update a product

Update a product

### URL

`PUT /[storeId]/products/[productId]?token=string`

### URL Parameters

**Name** |  **Type** | **Description**
-------------- | -------------- | --------------
storeId* |  number |  ID of the Ecwid store.
productId* |  number |  Идентификатор изменяемого продукта
token* |  string |  Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Product' with the following fields:

#### Product
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
sku | string |  Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
quantity |  number  | 
inStock | boolean | `true` if any of the product combinations or the product itself has positive quantity or is unlimited.
name |  string |  Product name as a plain text.
price | number |  Basic product price.
listPrice | number |  The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)/> |  The sorted array of (quantity limit, price) pairs.
compareToPrice |  number  | 'Compare To' price shown strike-out in the customer frontend.
weight |  number |  
created | string |  Product creation date/time.
lastUpdateTime |  string  | Product last update date/time. Can be null for products that were created before this.
productClassId |  number |  Id of a product class this product belongs to (like 'Books'). Zero '0' value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled | boolean | `true` if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product.
warningLimit |  number  | The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly | boolean | `true` if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate | number |  For fixedShippingRateOnly=`true`, this value is used instead of the shipping. For fixedShippingRateOnly=false, this value adds to the shipping cost.
description | string |  Product description in HTML.
categoryIds | Array\<number\> | A list of categories which this product belongs to.
defaultCategoryId | number  | Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> | If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor.
relatedProducts | [RelatedProducts](http://google.com)  | The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.**

#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier
\* *Fields in bold are mandatory.*

#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<[ProductOptionChoice](http://google.com)\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`
\* *Fields in bold are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
**id** |  number |  Unique attribute ID. See [Product Classes](#product-classes) for the information on attribute IDs
value | string  | Attribute value
\* *Fields in bold are mandatory.*


#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
productIds | Array\<number\>  | IDs of the related products
relatedCategory | [RelatedCategory](http://google.com)  | Describes the "N random related products from a category" option
\* *All fields are optional. Missing fields do not affect existing values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Combination
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
combinationNumber* |  number |  A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> | Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku | string  | If present, combination SKU, unique code. If null, product sku is assumed.
quantity |  number  | Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited* |  boolean |
price | number  | Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)> | The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |  number  |
tangible |  boolean  | TODO:copy. + Null if the weight should be inherited from the product.
warningLimit |  number  | The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |  number  | Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields in bold are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
enabled | boolean | Флаг включенности выбора связанных товаров из категории
categoryId |  number |  Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |  number |  Number of random products from a given category (or from all store, if `categoryId==0`), which should be shown as a related products of a given product.
\* *All fields are optional. Missing fields do not affect existing field values*

#### OptionValue
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
name* | string |  Option name, as in Product.options[i].name
value* |  string |  Option value one of Product.options[i].choices[j].text
\* *Fields in bold are mandatory.*

#### ProductOptionChoice
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
text* | string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* |  number |  Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`.
priceModifierType* |  string |  Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT` Default is `ABSOLUTE`.
\* *Fields in bold are mandatory.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
message  | string | Детальное сообщение о том, как прошел апдейт
updateCount | number | Количество обновленных сущностей
success | boolean | Успешно ли прошел апдейт

### Errors

**HTTP Status** | **Response JSON** | **Description**
-------------- | -------------- | --------------
400 | [IllegalParameterError](#illegalparametererror) | Некоторые парамеры в запросе заданы неверно
409 | [NonUniqueError](#nonuniqueerror) | Продукт с таким sku уже существует
402 | [PaidFeatureError](#paidfeatureerror) | Запрошена функциональность не доступная для данного плана
402 | [LimitError](#limiterror) | Уперлись в лимит на количество товаров для данного плана
404 | [NotFoundError](#notfounderror) | Сущность, на которую есть ссылка в продукте, не существует (например на продуктовый класс)


## Delete a product

Delete a product

### URL

`DELETE /[storeId]/products/[productId]?token=string`

### URL Parameters

**Name** |  **Type** | **Description**
-------------- | -------------- | --------------
storeId*  | number |  ID of the Ecwid store.
productId* |  number |  Идентификатор удаляемого продукта
token* |  string |  Oauth токен для доступа к данной функциональности
* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
message | string | Детальное сообщение о том как прошло удаление
deleteCount | number | Количество удаленных сущностей
success | boolean | Успешно ли прошло удаление