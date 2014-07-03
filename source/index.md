---
title: Ecwid REST API

language_tabs:
  - shell

toc_footers:
 - <a href='http://www.ecwid.com'>Register your application with Ecwid</a>
 - <a href='http://help.ecwid.com'>Ecwid Help</a>
---

# ---Using Ecwid REST API---

TODO

* What can it be used for
* Rest
* oAuth


# Authentication
Ecwid supports oAuth2 protocol to provide external applications with access to store data via APIs. Ecwid user grants or denies access to certain data in its store for the particular application - the application gets its own secure access token upon authorization and uses that token as a key to make API calls to Ecwid on behalf of the user.

The authorization flow includes the following steps.

##1. App sends the user to Ecwid authorization dialog
> Request example

```
GET https://my.ecwid.com/api/oauth/authorize?client_id=abcd0123&redirect_uri=https%3A%2F%2Fwww%2Eexample%2Ecom%2Fmyapp&response_type=code
```

###Request
`GET https://my.ecwid.com/api/oauth/authorize`

Parameter | Required | Description
--------- | -------- | -----------
client_id | required | application ID
redirect_uri | required | URI in your app where users will be sent after authorization. It must match the domain/URL of the registered refirect_uri specified in the app settings. I.e. if the registered redirect_uri is `http://www.example.com`, the redirect_uri in request might be `http://www.example.com/oauth/callback.php` , but not `http://www.example2.com/`
response_type | required | `code` (must always be `code`)
scope | optional | Scope of access that your app requests from the user, separated by space. See details [below](#scopes)


###Scopes
*Scopes are permissions that identifies the scope of access your app requests from the user*

* read_store_profile (requested in all cases even if not specified)
* update_store_profile
* read_catalog
* update_catalog
* create_catalog
* read_orders
* update_orders
* create_orders


##2. Ecwid redirects the user back to the app
> Successfull authorization

```url
https://www.example.com/myapp?code=1234567890
```

> The user denied to provide access

```
https://www.example.com/myapp?error=access_denied
```

*Upon authorization, Ecwid will redirect the user to the app `redirect_uri` specified in request.*

###Request
`GET *redirect_uri*`

Parameter | Description
--------- | -----------
code | If the user successfully authorizes the application, the query contains the code parameter. That is a temporary key that the app will exchange to its own access token on the next step
error | If the user does not allow authorization to the application, query parameters indicate the user canceled authorization in error field

##3. The app requests the access_token from Ecwid. 

*The access_token will be used by the app as API key in all API calls.*

###Request
> Request

```shell
curl "https://my.ecwid.com/api/oauth/token" \
-d client_id=abcd0123 \
-d client_secret=01234567890abcdefg \
-d code=987654321hgfdsa \
-d grant_type=authorization_code
```

`POST https://my.ecwid.com/api/oauth/token`

Parameter | Required | Description
--------- | -------- | -----------
client_id | required | Application ID
client_secret | required | Application secret key
code | required | The temporary code received on the step #2
grant_type | required | Must be `authorization_code`

###Response
> Response

```json
{
 "access_token":"12345",
 "token_type":"bearer",
 "scope":"read_store_profile update_catalog",
 "store_id":"1003"
}
```

Ecwid responds with a JSON-formatted data containing the access token and additional information. 

Field | Description
----- | -----------
token_type | `bearer` (it's always "bearer")
scope | List of permissions (API access levels) given to the app, separated by space
store_id | Ecwid store ID (a unique Ecwid account identificator)


<aside class="notice">
For security reasons, a temporary code can be exchanged to an access token only once. In case of second attempt, the previously provided access token is automatically disabled.
</aside>


# ---REST API Reference---


# Products

## Get a product

### Request

`GET https://app.ecwid.com/api/v3/**storeId**/products/**productId**?token=string`


Name | Type    | Description
---- | ------- | --------------
storeId* |  number |  ID of the Ecwid store.
productId | number |  Идентификатор запрашиваемого продукта.
token* |  string |  Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'Product' with the following fields:

#### Product
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  A unique integer product ID.
sku | string |  Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
thumbnailUrl |  string *nullable* | An URL of the product thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
quantity |  number *nullable* | Amount of the product in stock as an integer value. Absent for unlimited products.
inStock | boolean | True if any of the product combinations or the product itself has positive quantity or is unlimited.
name |  string |  Product name as a plain text.
price | number |  Basic product price.
listPrice | number |  The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs.
compareToPrice |  number *nullable* | 'Compare To' price shown strike-out in the customer frontend.
weight |  number |  Product weight, in the store units. Absent for intangible products.
url | string |  URL of the product's description web page.
created | string |  Product creation date/time.
lastUpdateTime |  string *nullable* | Product last update date/time. Can be null for products that were created before this.
productClassId |  number |  Id of a product class this product belongs to (like 'Books'). Zero '0' value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled | boolean | 'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product.
warningLimit |  number *nullable* | The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly | boolean | True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate | number |  For `fixedShippingRateOnly=true`, this value is used instead of the shipping. For `fixedShippingRateOnly=false`, this value adds to the shipping cost.
defaultCombinationId |  number |  Id of a combination corresponding to the default product option values. E.g. if the default t-shirt color is 'white', and there is a separate combination for the white t-shirts, that combination is returned.
imageUrl |  string *nullable* | An URL of a product image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
smallThumbnailUrl | string *nullable* | An URL of the product thumbnail fitted in the 80x80 box.
originalImageUrl |  string *nullable* | An URL of an original product image that was uploaded for this product.
description | string *nullable* | Product description in HTML.
galleryImages | Array\<[GalleryImage](http://google.com)\> |  A list of gallery images.
categoryIds | Array\<number\> | A list of categories which this product belongs to.
defaultCategoryId | number *nullable* | Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> | If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor.
files | Array\<[ProductFile](http://google.com)\> | E-goods attached to the product. This field is only available for authorized requests.
relatedProducts | [RelatedProducts](http://google.com) *nullable* | The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
combinations | Array\<[Combination](http://google.com)\> |  This can only be used when product retrieval. This field is absent on saving a product.
* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### WholesalePrice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
quantity |  number |  Number of items for which the special price is eligible.
price | number |  Special price for the product when ordered more the 'quantity' items.

#### ProductOption
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
name |  string |  Option name, like 'Color', as a plain text.
choices | Array\<[ProductOptionChoice](http://google.com)\> | All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty
defaultChoice | number *nullable* | The number, starting from `0`, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | "true" if this option is required, "false" otherwise. Default is false
* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
alt | string |  The image description, displayed in 'alt' image attribute, as a plain text.
url | string |  The image url.
thumbnail | string *nullable* | An URL of the image thumbnail fit into the 46x42 box.
width | number |  Width of the image.
height |  number |  Height of the image.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
name |  string |  The attribute's printable name
value | string *nullable* | The attribute value. Set to null in product update request to remove the attribute.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  Unique integer file ID.
name |  string |  A plain-text file name.
description | string |  A plain-text file description.
size |  number |  File size, in bytes, as a 64-bit integer.

#### RelatedProducts
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
productIds | Array\<number\> *nullable* | IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory | [RelatedCategory](http://google.com) *nullable* | Specifies the random number of related products from a given category.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Combination
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
id |  number |  A unique integer combination ID.
combinationNumber | number |  A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> | Set of options which identifies this combination. An array of {name:, value:} objects.
sku | string *nullable* | If present, combination SKU, unique code. If null, product sku is assumed.
smallThumbnailUrl | string *nullable* | An URL of the product combination thumbnail fitted in the 80x80 box. If null, product thumbnail is assumed.
thumbnailUrl |  string *nullable* | An URL of the product combination thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. If null, product thumbnail is assumed.
imageUrl |  string *nullable* | An URL of a combination image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. If null, product image is assumed.
originalImageUrl |  string *nullable* | An URL of a non-resized combination image that was uploaded for this combination. If null, product image is assumed.
quantity |  number *nullable* | Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited | boolean | "true", if the combination is unlimited (that is, never runs out).
price | number *nullable* | Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place.
weight |  number *nullable* | Product weight, in the store units. If null, the weight is inherited from the product.
tangible |  boolean *nullable* |  True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |  number *nullable* | The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
enabled | boolean | Флаг включенности выбора связанных товаров из категории
categoryId |  number |  Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |  number |  Number of random products from a given category (or from all store, if `categoryId==0`), which should be shown as a related products of a given product.

#### OptionValue
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
name |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
**Field** | **Type**  | **Description**
-------------- | -------------- | --------------
text |  string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier | number |  Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`
priceModifierType | string |  Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT`. Default is `ABSOLUTE`.

### Errors

**HTTP Status** | **Response JSON** | **Description**
-------------- | -------------- | --------------
404 | [NotFoundError](#notfounderror) | Возвращается в случае, когда продукт не найден по заданному идентификатору.
500 | [InternalError](#internalerror) | Невозможно получить продукт произошла внутренняя ошибка сервера.


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
quantity |  number |  Amount of the product in stock as an integer value. Absent for unlimited products.
inStock* |  boolean | True if any of the product combinations or the product itself has positive quantity or is unlimited.
name* | string |  Product name as a plain text.
price* |  number |  Basic product price.
listPrice* |  number |  The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs. Default is empty.
compareToPrice |  number *nullable* | 'Compare To' price shown strike-out in the customer frontend.
weight* | number |  Product weight, in the store units. Absent for intangible products.
created* |  string |  Product creation date/time.
lastUpdateTime |  string *nullable* | Product last update date/time. Can be null for products that were created before this.
productClassId* | number |  Id of a product class this product belongs to (like 'Books'). Zero `0` value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled* |  boolean | 'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product. Default is empty.
warningLimit |  number |  The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly* |  boolean *nullable* |  True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate* |  number |  For fixedShippingRateOnly=true, this value is used instead of the shipping. For `fixedShippingRateOnly=false`, this value adds to the shipping cost.
description | string *nullable* | Product description in HTML.
categoryIds | Array\<number\> | A list of categories which this product belongs to. Default is empty.
defaultCategoryId | number  *nullable* |  Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> | If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor. Default is empty.
relatedProducts | RelatedProducts | The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### WholesalePrice
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
quantity* | number |  Number of items for which the special price is eligible.
price* |  number |  Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

#### ProductOption
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`. Default is `SELECT`.
name* | string |  Option name, like 'Color', as a plain text.
choices | Array\<[ProductOptionChoice](http://google.com)> |  All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty.
defaultChoice | number *nullable* | The number, starting from 0, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required* | boolean | "true" if this option is required, "false" otherwise. Default is false
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
alt | string *nullable* | The image description, displayed in 'alt' image attribute, as a plain text.
url* |  string |  The image url.
thumbnail | string *nullable* | An URL of the image thumbnail fit into the 46x42 box.
width* |  number |  Width of the image.
height* | number |  Height of the image.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
id |  number |  Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
value | string *nullable* | The attribute value. Set to null in product update request to remove the attribute.
Fields marked with  are mandatory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
id* | number |  Unique integer file ID.
name* | string |  A plain-text file name.
description* |  string |  A plain-text file description.
size* | number |  File size, in bytes, as a 64-bit integer.
\* *Fields marked with * are mandatory.*

#### RelatedProducts
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
productIds | Array\<number\> *nullable* | IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory | [RelatedCategory](http://google.com) *nullable* | Specifies the random number of related products from a given category.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Combination
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
combinationNumber* |  number |  A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<OptionValue\> |  Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku | string *nullable* | If present, combination SKU, unique code. If null, product sku is assumed.
quantity |  number *nullable*  |  Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited | boolean | "true", if the combination is unlimited (that is, never runs out).
price | number *nullable* | Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |  The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |  number *nullable* | Product weight, in the store units. If null, the weight is inherited from the product.
tangible |  boolean *nullable* |  True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |  number |  The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |  number |  Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
enabled | boolean | Флаг включенности выбора связанных товаров из категории
categoryId |  number |  Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |  number |  Number of random products from a given category (or from all store, if categoryId==0), which should be shown as a related products of a given product.
\* *Fields marked with * are mandatory.*

#### OptionValue
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
name |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text
\* *Fields marked with * are mandatory.*

#### ProductOptionChoice
**Field** | **Type** |  **Description**
-------------- | -------------- | --------------
text* | string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* | number | Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`
priceModifierType* | string | Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT`. Default is `ABSOLUTE`.
\* *Fields marked with * are mandatory.*

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
quantity |  number *nullable* | Amount of the product in stock as an integer value. Absent for unlimited products.
inStock | boolean | True if any of the product combinations or the product itself has positive quantity or is unlimited.
name |  string |  Product name as a plain text.
price | number |  Basic product price.
listPrice | number |  The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)/> |  The sorted array of (quantity limit, price) pairs.
compareToPrice |  number *nullable* | 'Compare To' price shown strike-out in the customer frontend.
weight |  number |  Product weight, in the store units. Absent for intangible products.
created | string |  Product creation date/time.
lastUpdateTime |  string *nullable* | Product last update date/time. Can be null for products that were created before this.
productClassId |  number |  Id of a product class this product belongs to (like 'Books'). Zero '0' value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled | boolean | 'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> | A list of the product options. Empty if no options are specified for the product.
warningLimit |  number *nullable* | The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly | boolean | True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate | number |  For fixedShippingRateOnly=true, this value is used instead of the shipping. For fixedShippingRateOnly=false, this value adds to the shipping cost.
description | string |  Product description in HTML.
categoryIds | Array\<number\> | A list of categories which this product belongs to.
defaultCategoryId | number *nullable* | Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> | If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor.
relatedProducts | [RelatedProducts](http://google.com) *nullable* | The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.**

#### WholesalePrice
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
quantity* | number |  Number of items for which the special price is eligible.
price* |  number |  Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

#### ProductOption
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`. Default is `SELECT`.
name* | string |  Option name, like 'Color', as a plain text.
choices | Array\<[ProductOptionChoice](http://google.com)\> | All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty.
defaultChoice | number *nullable* | The number, starting from `0`, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required* | boolean | "true" if this option is required, "false" otherwise. Default is false
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
alt | string *nullable* | The image description, displayed in 'alt' image attribute, as a plain text.
url* |  string |  The image url.
thumbnail | string *nullable* | An URL of the image thumbnail fit into the 46x42 box.
width* |  number |  Width of the image.
height* | number |  Height of the image.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
id* | number |  Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
value | string *nullable*  |  The attribute value. Set to null in product update request to remove the attribute.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
id* | number |  Unique integer file ID.
name* | string |  A plain-text file name.
description* |  string |  A plain-text file description.
size* | number |  File size, in bytes, as a 64-bit integer.
\* *Fields marked with * are mandatory.*

#### RelatedProducts
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
productIds  | Array\<number\> *nullable* |  IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory | [RelatedCategory](http://google.com) *nullable* | Specifies the random number of related products from a given category.
\* *All fields are optional. Missing fields do not affect existing field values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Combination
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
combinationNumber* |  number |  A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> | Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku | string *nullable* | If present, combination SKU, unique code. If null, product sku is assumed.
quantity |  number *nullable* | Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited* |  boolean | "true", if the combination is unlimited (that is, never runs out).
price | number *nullable* | Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)> | The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |  number *nullable* | Product weight, in the store units. If null, the weight is inherited from the product.
tangible |  boolean *nullable* |  True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |  number *nullable* | The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |  number *nullable* | Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields marked with * are mandatory.*

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
\* *Fields marked with * are mandatory.*

#### ProductOptionChoice
**Field** | **Type** | **Description**
-------------- | -------------- | --------------
text* | string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* |  number |  Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`.
priceModifierType* |  string |  Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT` Default is `ABSOLUTE`.
\* *Fields marked with * are mandatory.*

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