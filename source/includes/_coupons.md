# Coupons


<!--
---------------------------------------------------------------------------------------------------------
    Search coupons
---------------------------------------------------------------------------------------------------------
-->

## Search coupons

### Request

> Request examples

```http
GET /api/v3/4870020/discount_coupons?discount_type=ABS%2CPERCENT&availability=ACTIVE%2CEXPIRED&token=123abcd HTTP/1.1
Host: app.ecwid.com
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/discount_coupons?code={code}&discount_type={discount_type}&availability={availability}&token={token}`

Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**token** |  string | oAuth token
code | string | Coupon code
discount_type | string | Comma separated list of discount types. Supported values: `ABS`, `PERCENT`, `SHIPPING`
availability |  string | Comma separated list of coupon states. Supported values: `ACTIVE`, `PAUSED`, `EXPIRED`, `USEDUP`

<aside class="notice">
If no filters are set in the URL, API will return all discount coupons
</aside>

<aside class="notice">
Parameters in bold are mandatory
</aside>

### Response

> Response example (JSON)

```json
{
    "total": 3,
    "count": 3,
    "limit": 10,
    "offset": 0,
    "items": [
-{
name: "Coupon # 2"
code: "J3N4JM3SIPCJ"
discountType: "SHIPPING"
status: "ACTIVE"
discount: 0
launchDate: "2014-06-06 00:00:00 +0400"
expirationDate: "2014-09-27 23:59:59 +0400"
totalLimit: 50.4
usesLimit: "UNLIMITED"
repeatCustomerOnly: false
creationDate: "2014-06-06 18:57:19 +0400"
orderCount: 0
}
-{
name: "Coupon # 1"
code: "MOXQ3YCWXRXA"
discountType: "ABS"
status: "ACTIVE"
discount: 1
launchDate: "2014-06-06 08:00:00 +0400"
usesLimit: "UNLIMITED"
repeatCustomerOnly: false
creationDate: "2014-06-06 18:57:19 +0400"
orderCount: 0
-catalogLimit: {
-products: [
37208342
37208338
]
categories: [ ]
}
}
-{
name: "Coupon # 3"
code: "O3Q4AP5FKXJ1"
discountType: "PERCENT"
status: "PAUSED"
discount: 5
launchDate: "2014-06-06 08:00:00 +0400"
usesLimit: "UNLIMITED"
repeatCustomerOnly: false
creationDate: "2014-06-06 18:57:19 +0400"
orderCount: 0
}
]
}
```

A JSON object of type 'DiscountCouponSearchResults' with the following fields:

#### DiscountCouponSearchResults
Field | Type | Description
----- | ---- | -----------
total | number | The total number of found items (might be more than the number of returned items)
count | number | The number of returned items
offset | number | Offset from the beginning of the returned items list (for paging)
limit | number | Maximum number of returned items. Maximum allowed value: `100`. Default value: `10`
items | Array\<*CouponSearchEntry*\> | The items list

#### CouponSearchEntry
Field | Type  | Description
----- | ----- | -----------
name |  string | Coupon title
code |  string | Unique coupon code
discountType | string | Discount type: `ABS`, `PERCENT` or `SHIPPING`
status | string | Discount coupon state: `ACTIVE`, `PAUSED`, `EXPIRED` or `USEDUP`
discount | number | Discount amount
launchDate | string | The date of coupon launch
expirationDate | string | Coupon expliration date, e.g. `2014-06-06 08:00:00 +0400`
totalLimit | number *nullable* | The minimum order subtotal the coupon applies to
usesLimit | string | Coupon usage number limitations: `UNLIMITED`, `ONCEPERCUSTOMER`, `SINGLE`
repeatCustomerOnly | boolean | Coupon usage limitation flag identifying whether the coupon works for all customers or only repeat customers
creationDate |  string | Coupon creation date
orderCount | number | Coupon usage number
catalogLimit |  \<*DiscountCouponCatalogLimit*\> | The products and categories the coupon can be applied to

#### DiscountCouponCatalogLimit
Field | Type | Description
----- | ---- | -----------
products | Array\<number\> | The list of product IDs the coupon can be applied to
categories | Array\<number\> | The list of category IDs the coupon can be applied to

### Errors

> Error response example

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Meaning
------------|--------
400 | Request parameters are malformed
500 | Cannot retrieve the coupons info because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message



<!--
---------------------------------------------------------------------------------------------------------
    Get coupon details
---------------------------------------------------------------------------------------------------------
-->

## Get coupon

### Request

> Request example

```http
GET /api/v3/4870020/discount_coupons/123123?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/discount_coupons/{couponId}?token={token}`

Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**couponId** | number | Coupon ID
**token** |  string |  oAuth token

### Response

> Response example (JSON)

```json
{
    "id": 15319410,
    "email": "johnsmith@example.com",
    "registered": "2014-09-01 23:25:27 +0400",
    "billingPerson": {
        "name": "John Smith",
        "companyName": "Unreal Company",
        "street": "W 3d st",
        "city": "New York",
        "countryCode": "US",
        "postalCode": "10001",
        "stateOrProvinceCode": "NY",
        "phone": "+1234567890"
    },
    "shippingAddresses": [
        {
            "id": 8315122,
            "name": "John Smith",
            "companyName": "",
            "street": "W 3d st",
            "city": "New York",
            "countryCode": "US",
            "postalCode": "10001",
            "stateOrProvinceCode": "NY",
            "phone": "123567890"
        },
        {
            "id": 8315123,
            "name": "Jane Smith",
            "companyName": "",
            "street": "1733 W Madison St",
            "city": "Chicago",
            "countryCode": "US",
            "postalCode": "60612",
            "stateOrProvinceCode": "IL",
            "phone": ""
        }
    ]
}
```


A JSON object of type 'Coupon' with the following fields:

#### Coupon
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique internal coupon ID
email | string |  Coupon email
registered | string | Registration date, e.g `2014-06-06 18:57:19 +0400`
billingPerson | <Person> | Coupon's billing name/address
shippingAddresses | Array<ShippingAddress> | Coupon address book items

#### Person
Field | Type  | Description
-------------- | -------------- | --------------
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

#### ShippingAddress
Field | Type  | Description
------| ----- | -----------
id | number | Internal address ID
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

### Errors

> Error response example

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Meaning
------------|--------
404 | Coupon is not found
500 | Cannot retrieve the coupon info because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Create coupon
---------------------------------------------------------------------------------------------------------
-->

## Create coupon

### Request

> Request body

```http
POST /api/v3/4870020/discount_coupons?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
    "email": "example@example.com",
    "password": "ecwidiscool",
    "billingPerson": {
        "name": "John Smith",
        "companyName": "Imaginary Company",
        "street": "Hedgehog Street, 1",
        "city": "Bucket",
        "countryCode": "US",
        "postalCode": "90002",
        "stateOrProvinceCode": "CA",
        "phone": "11111111111"
    },
    "shippingAddresses": [
        {
            "name": "John Smith",
            "companyName": "Imaginary Company",
            "street": "W 3d st",
            "city": "New York",
            "countryCode": "US",
            "postalCode": "10001",
            "stateOrProvinceCode": "NY",
            "phone": "11111111111"
        }
      ]
}
```


`POST https://app.ecwid.com/api/v3/{storeId}/discount_coupons?token={token}`


Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**token** |  string |  oAuth token


### Request body

A JSON object of type 'Coupon' with the following fields:

#### Coupon
Field | Type  | Description
-------------- | -------------- | --------------
**email** | string |  Coupon email
**password** | string |  Coupon email
billingPerson | <Person> | Coupon's billing name/address
shippingAddresses | Array<ShippingAddress> | Coupon address book items

#### Person
Field | Type  | Description
-------------- | -------------- | --------------
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

#### ShippingAddress
Field | Type  | Description
------| ----- | -----------
id | number | Internal address ID
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

<aside class="notice">
Parameters in bold are mandatory
</aside>


### Response


> Response example

```json
{
    "id": 15319442,
    "success": true
}
```

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
Field | Type |  Description
-------------- | -------------- | --------------
id | number | ID of the created coupon
success | boolean | `true` if the coupon has been created, `false` otherwise


### Errors

> Error response example

```http
HTTP/1.1 409 Conflict
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description.

#### HTTP codes

**HTTP Status** | **Response JSON** | Description
-------------- | -------------- | --------------
400 | Request parameters are malformed
409 | The coupon with the given email already exists
500 | The creation request failed because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message


<!--
---------------------------------------------------------------------------------------------------------
    Edit coupon
---------------------------------------------------------------------------------------------------------
-->

## Update coupon

### Request

> Request body

```http
PUT /api/v3/4870020/discount_coupons?10293737&token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
    "email": "new-email@example.com",
    "password":"newpassword",
    "billingPerson": {
        "name": "New Name",
        "companyName": "Ecwid",
        "street": "Updated street",
        "city": "Bucket",
        "countryCode": "US",
        "postalCode": "90002",
        "stateOrProvinceCode": "CA",
        "phone": "11111111111"
    },
    "shippingAddresses": [
        {
            "name": "Eugene K",
            "companyName": "Hedgehog and Bucket",
            "street": "Hedgehog Street, 3",
            "city": "Bucket",
            "countryCode": "US",
            "postalCode": "90002",
            "stateOrProvinceCode": "CA",
            "phone": "11111111111"
        }
      ]
}
```


`PUT https://app.ecwid.com/api/v3/{storeId}/discount_coupons/{couponId}?token={token}`


Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**token** |  string | oAuth token
**couponId** | number | Internal coupon ID


### Request body

A JSON object of type 'Coupon' with the following fields:

#### Coupon
Field | Type  | Description
-------------- | -------------- | --------------
email | string |  Coupon email
password | string |  Coupon email
billingPerson | <Person> | Coupon's billing name/address
shippingAddresses | Array<ShippingAddress> | Coupon address book items

#### Person
Field | Type  | Description
-------------- | -------------- | --------------
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

#### ShippingAddress
Field | Type  | Description
------| ----- | -----------
id | number | Internal address ID
name | string | Coupon full name
companyName | string | Coupon company name
street | string | Street
city | string | City
countryCode | string | Country (2-digits code)
postalCode | string | Postal code (zip code)
stateOrProvinceCode | string | State/province code
phone | string | Phone number

<aside class="notice">
All fields are optional
</aside>


### Response


> Response example

```json
{
    "updateCount": 1,
    "success": true
}
```

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
Field | Type |  Description
-------------- | -------------- | --------------
updateCount | number | The number of update coupons (`0` or `1` depending on whether the request was successful)
success | boolean | `true` if the coupon has been updated, `false` otherwise


### Errors

> Error response example

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description.

#### HTTP codes

**HTTP Status** | **Response JSON** | Description
-------------- | -------------- | --------------
400 | Request parameters are malformed
404 | The coupon with given ID is not found
409 | The coupon with the given email already exists
500 | The update request failed because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message











<!--
---------------------------------------------------------------------------------------------------------
    Delete coupon
---------------------------------------------------------------------------------------------------------
-->

## Delete coupon

> Request example

```http
DELETE /api/v3/4870020/discount_coupons/39847403?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/discount_coupons/{couponId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**couponId** | number | Coupon ID
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
----- | ---- | ------------
deleteCount | number | The number of deleted coupons (`1` or `0` depending on whether the request was successful)
success | boolean | `true` if the coupon has been deleted, `false` otherwise


### Errors

> Error response example

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description.

#### HTTP codes

**HTTP Status** | **Response JSON** | Description
-------------- | -------------- | --------------
400 | Request parameters are malformed
404 | The coupon with given ID is not found
500 | The update request failed because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message