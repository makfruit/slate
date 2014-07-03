---
title: JavaScript API

toc_footers:
 - <a href='http://www.ecwid.com'>Register your application in Ecwid</a>
---

# JavaScript API

```js
Ecwid.OnPageLoad.add(function(page) {
        alert("My page load handler: " + page.type);
});
```

This API is intended for better integrating Ecwid with the surrounding web site. All most useful stuff is located in the **window.Ecwid** top-level object, e.g. **window.Ecwid.formatCurrency**. The API is based on two concepts: objects and extension points. Objects are simple containers for methods, while extension points are containers for the user-supplied callbacks (or extensions). Extensions are added to the extension points using the add() method.

This sample adds a function that is called every time a new page is loading in the product browser. Callbacks may be objects with multiple functions instead of just one function as shown in the example above, which may return useful values. The form of the extensions, their parameters and the need of a return value depends on the extension point as described below.
 
Note that the **add()** method call follows the script.js script of the standard Ecwid integration HTML code. It is important to include script.js before any use of the API methods. Moreover, because of the staged loading of Ecwid, only few of API functions are available during the page load. Most of the Ecwid Javascript API is available after Ecwid is loaded completely. This moment when you can use Javascript API can be caught by the **Ecwid.OnAPILoaded** extension point, as shown below:
 
## API Extensions
 
### Ecwid.OnAPILoaded
This extension point contains callback functions that get called exactly once when the Ecwid Javascript API loads and become available under the window.Ecwid top-level object. Functions supplied to this extension point as extensions do not accept any parameters and do not require to return any value.
 
### Ecwid.OnPageLoad/Ecwid.OnPageLoaded
> Ecwid.OnPageLoad event handler

```js
Ecwid.OnPageLoad.add(function(page) {
        alert("My page load handler: " + page.type);
});
```
These extension points contain callbacks that get called on each page change inside the product browser. The difference between **OnPageLoad** and **OnPageLoaded** is that the former is called when the page is changed (e.g. a link is clicked), while the later is called later when the corresponding page is loaded inside the product browser.
The callback functions accept one parameter of type **Page** specifying which page is to be loaded (or has already been loaded).
 
### Ecwid.OnSetProfile
This extension point contains callback functions that receive the changes in the current customer profile. If no customer is logged in, these functions receive **null**. Whenever a customer logs in/out, the callback functions are called with either the corresponding parameter of type **Customer** or **null**. Example:

```html
<script src="//app.ecwid.com/script.js?[STORE-ID]" type="text/javascript" charset="UTF-8"></script>
<script>
function dump(arr,level) {
var dumped_text = "";
if (!level) level = 0;
// The padding given at the beginning of the line.
var level_padding = "";
for (var j=0;j<level+1;j++) level_padding += " ";
if (typeof(arr) == 'object') { // Array/Hashes/Objects
for (var item in arr) {
var value = arr[item];
if (typeof(value) == 'object') { // If it is an array,
dumped_text += level_padding + "'" + item + "' ...\n";
dumped_text += dump(value,level+1);
} else {
dumped_text += level_padding + "'" + item + "' => \"" + value + "\"\n";
}
}
} else { // Stings/Chars/Numbers etc.
dumped_text = "===>"+arr+"<===("+typeof(arr)+")";
}
return dumped_text;
}
Ecwid.OnSetProfile.add(function(profile) {
if (profile == null) document.getElementById('CUSTOMER').innerHTML = 'not logged in';
else document.getElementById('CUSTOMER').innerHTML = dump(profile);
});
</script>
<div><pre id='CUSTOMER'/></div>
<script>
xProductBrowser();
</script>
```

### Ecwid.OnCartChanged
This extension point contains callback functions that get called each time when a shopping cart is changed — either by the customer or due to system events.
 
The callbacks are added as follows:

```js
Ecwid.OnCartChanged.add(function(cart){
     // your code here
})
```

The callback function receives in an argument the Cart object, that holds the new shopping cart state after the change is applied.
 
The callbacks added to Ecwid.*OnCartChanged* will be called when the shopping cart is initialized and on every occasion when either of the properties of the passed *Cart* object is changed. These occasions include:

* Cart initialization 
* Adding a product to cart
* Removing a product from cart
* Changing the product’s options
* Clearing the cart
* Applying a discount coupon
* Selecting and changing the selection of the payment method
* Selecting and changing the selection of the shipping method
* Syncing the cart contents, if there are a few browser tabs with the store are opened
* Clearing the cart upon user’s logout — in this occasion the callback receives null as an argument.
 
The passed *Cart* object represents only the basic properties of the shopping cart. It contains the data coming from the customer’s actions (like products, coupons, payment and shipping methods) and might not contain the calculated aggregates (like order totals, shipping costs, the discounted amounts or taxes). For the calculated aggregates, it is rather recommended to use the *Ecwid.Cart.calculateTotal()* method.
 
### Ecwid.OnProductOptionsChanged

Example:

```js
<script>
Ecwid.OnProductOptionsChanged.add(function(productid) {
   window.alert("Options changed, product id:"+productid);    
}
</script>
```
 
## API Objects
This section describes all possible objects involved in the Javascript API.
 
### Ecwid
The top-level object window.Ecwid itself provides some useful functions, besides references to other objects like Ecwid.OnPageLoad:
 
### Ecwid.getStaticBaseUrl()
Returns the base URL for static Ecwid files, like images and CSS, with the ’/’ at the end.
 
### Ecwid.getOwnerId()
Returns the store ID.
 
### Ecwid.formatCurrency(double number)
Converts the given currency value to a human-readable string according to the store settings.
 
### Ecwid.Cart
*Ecwid.Cart* is a namespace for cart-related functions of JavaScript API.
 
### Ecwid.Cart.addProduct
This function allows to add a product to shopping cart, modifying the cart on behalf of customer thus. Example:

```js
Ecwid.Cart.addProduct(product)
```

There are 2 possible ways to call this function.
 
**Adding by product ID**
`addProduct()` can accept 2 arguments:

```js
Ecwid.Cart.addProduct(productID, callback)
```

* **productID**: *Integer* — the Ecwid’s internal product ID to be added to cart (can be retrieved from Product API or seen in the URL of the product page)
* **callback**: *Function* — the callback function to be called once the operation is complete (either succeeded or failed). See below for details.
 
The most simple call to `Ecwid.Cart.addProduct` only requires to pass the numeric product ID. Example:

```js
var productId = 10;
Ecwid.Cart.addProduct(productId);
```

This code adds 1 item of the given product ID to cart.
 
If this product contains combinations and the base product is out of stock, the first combination that is in stock will be added to cart instead. If the product is out of stock (and there are no combinations in stock for this product), nothing is added to cart.
 
**Adding with extended options**
If it is necessary to specify options or quantity to be added to cart, the product parameter needs to be passed as an object.

```js
product = {
    id: 10,
    quantity: 3,
    options: {
        someTextOption: "optionVal",
        someDateOption: new Date().getTime().toString()
    },
    callback: function(success, product, cart) {
        // ...    
    }
}
```

```js
Ecwid.Cart.addProduct(product);
```

Since this method allows to specify the exact options to be added to cart, only the base product or combination matching those options will be added to cart. So, if the base product or matching combination is out of stock, the `addProduct` call will not add anything to cart, even if there are other combinations in stock.
NOTE: currently, the 'options' property supports only text and date types. We will add the other option types in the future versions. 
 
**Callback**
Adding to cart is done asynchronously, so if it is important to know the result of adding, the callback function can be passed as the second agrument of the function:

```js
Ecwid.Cart.addProduct(productID, function(success, product, cart){
        console.log(success); // true or false
        console.log(product.name);
    })
```
    
```js
Ecwid.Cart.addProduct({
        id: 10, 
        quantity: 3, 
        callback: function(success, product, cart){
            console.log(success); // true or false
            console.log(product.name);
        }
    })
```
    
Callback receives 3 arguments:

* **success**: *Boolean* (true/false) — indicates the overall status of addintion (succeeded or failed)
* **product**: *Object* (Product) — conatins the object representation of the product added to cart, or `null` if adding to cart failed (wrong product ID or product is out of stock).
* **cart**: *Object* (Cart) — contains the object representation of the shopping cart after addition (same as in Ecwid.OnCartChanged event)
 
### Ecwid.Cart.clear()
Clears the cart contents.
 
### Ecwid.Cart.get()
Retrieves the cart contents asynchronously and passes it as an argument of type Cart to the callback.

```js
Ecwid.Cart.get(function(cart) {
     alert(cart.productsQuantity + " products in cart now");
});
```

### Ecwid.Cart.calculateTotal()
Calculates the cart aggregates asynchronously and passes the result as an argument of type Order to the callback. Example:

```js
Ecwid.Cart.calculateTotal(function(order) {
    if (!order)
        alert('An error occurred!')
    else    
        alert('Order total: ' + order.total);    
});
```

Cart calculation involves a request to server, so this method should be called only occasionally. Calling it frequently, e.g. from loops or by timer, is not acceptable.
 
Since the calculation needs a server connection, it might fail due to network conditions. In this case, null is passed into the callback instead of Order object.
 
### Customer
The object describing the customer’s profile.
Fields:
 
**Name** | **Type** | **Description**
--------- | -----------| -----------
id | integer | The unique id of the customer
email | string | Customer’s email
billingPerson | **[Person](#person)** | Customer’s name along with his/her billing address, as entered in the last order. Empty if asking for billing address is disabled in the store
shippingAddresses | **[ShippingAddress](#shippingaddress)** | A list of addresses in the customer’s address book
registered | integer timestamp | The UNIX timestamp when the customer registered
 
 
### Person
Describes the person name, company and address.
Fields:
 
**Name** | **Type** | **Description**
--------- | -----------| -----------
name | string | The first and the last name of the person, separated by a space.
companyName | string, optional | The person’s company name, if applicable
street | string, optional | The street address of the person, if applicable. If there are two address lines, they are separated by a newline character ‘\n’
city | string, optional | The person’s city, if applicable
countryCode | string, optional | The person’s country code, as listed in ISO 3166-2
postalCode |string, optional | The person’s postal code or ZIP code, if applicable
stateOrProvinceCode | string, optional | The person’s region/state/province code by ISO 3166-2. Please note that not all countries regional codes are listed in the Ecwid database so far.
countryName | string, optional | Country name, if applicable
phone | string, optional | Phone number, if applicable
 
 
### Page
Describes the page displaying inside the product browser.
Fields:
 
**Name** | **Type** | **Description**
--------- | -----------| -----------
type | one of the following: `ACCOUNT_SETTINGS`, `ADDRESS_BOOK`, `ORDERS`, `CATEGORY`,`CART`, `CHECKOUT_ADDRESS_BOOK`, `CHECKOUT_PAYMENT_DETAILS`, `CHECKOUT_PLACE_ORDER`, `CHECKOUT_SHIPPING_ADDRESS`, `ORDER_CONFIRMATION`, `ORDER_FAILURE`, `CHECKOUT_RESULT`, `DOWNLOAD_ERROR`, `PRODUCT`, `SEARCH` | The type of the page. Some pages may have parameters like for example product id of the viewing product. Those parameters are described below.
keywords | string, optional | for type==`ORDERS`: the keywords that are used to find orders in the customer account page. For type==`SEARCH`: the keywords that are used to find products on the product search page.
from | integer timestamp, optional | for type==`ORDERS`: The timestamp of the start of the orders date range.
to | integer timestamp, optional | for type==`ORDERS`: The timestamp of the end of the orders date range.
offset | | for type==`ORDERS`: the position of the current order list page (starting from `0`). For type==`CATEGORY` and `SEARCH`: the position of the current product list page (starting from `0`).
categoryId | integer | for type==`CATEGORY`: the id of the showing product category or `0` if this is the starting page of the catalog and no categories are selected yet. For type==`PRODUCT`: the category internal id the current product has been navigated from. Zero `0` is the root category, `−1` meaning that the category is unknown (e.g. a product opened from a search result).
mainCategoryId |	integer	| for type==`PRODUCT` in the OnPageLoaded event: the internal id of category that is considered the default category of this product (in case if the product is assigned to a few different categories). If a product is assigned to a single category, mainCategoryId will be equeal to categoryId; if a product is not assigned to any category, its mainCategoryId is `0` (zero). For type==`PRODUCT` in the OnPageLoad event: always `0` (zero);
sort | string, one of: `normal`, `addedTimeDesc`, `priceAsc`, `priceDesc`, `nameAsc`, `nameDesc` | for type==`CATEGORY` and `SEARCH`: the order of the product list, as selected by the user in the ‘sort by’ drop-down. ‘Desc’ suffix stands for the descending order, ‘Asc’ suffix stands for the ascending order.
orderId | integer | for type==`CHECKOUT_RESULT`: the internal id of the order (not to be confused with the store order number)
ticket | integer | for type==`CHECKOUT_RESULT`: the security random code that allows to retrieve information about the order
errorType | one of the following: `expired`, `invalid`, `limit` | for type==`DOWNLOAD_ERROR`: the type of the error while downloading an e-good file.
key | integer, optional | for type==`DOWNLOAD_ERROR`: the downloading file internal id
productId | integer | for type==`PRODUCT`: the internal id of the displaying product (not to be confused with SKU).
 
 
### ShippingAddress
The customer’s address as stored in the address book.
Fields:
 
**Name** | **Type** | **Description**
--------- | -----------| -----------
id | integer | The unique address id Ecwid database
person | **Person** |The object describing the address along with the person’s name and phone number.
 
### Cart
Cart object is a snapshot of essential shopping cart properties, passed via various callbacks. Cart object does not provide direct memory access to the actual cart that Ecwid uses — i.e. changing this exact object will not alter the actual cart Ecwid uses for placing the order.

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
items |	Array of \<CartItem\> |	Enlists all items currently present in customer’s cart
productsQuantity |	Integer |	Total number of product varieties in cart
tax | Number | Total tax.
couponDiscount | Number | Discount is  zero 0 unless any coupon is applied.
couponName |	String |	The name of the coupon (if any) applied to the cart. If no coupon was applied, will contain undefined. Does not contain the actual code of coupon, just the name.
volumeDiscount | Number | Discount based on the total of the items.
discount | Number | Sum of all discounts.
weight |	Number |	Total weight of the items in cart
paymentMethod |	String |	The name of the selected payment method (if any)
shippingMethod |	String |	The name of the selected shipping method (if any)
 
### CartItem
CartItem represents a single item (product variety) in cart.

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
quantity |	Integer |	Quantity of the given product variety in cart
product |	\<Product\> |	The map of product properties (combination properties, if the combination is added to cart)
options |	Object | with option names and values	Map of the product options (option name as a key and option value as a value). For listboxes and radio buttons value will be the string value of the selected option. For checkboxes — names of the selected options, comma separated. For date options — string representing the selected date according to the shop’s format (Ecwid control panel > System settings > General > Formats and Units). For textboxes и textareas — the text given by the customer. For file upload options — string in the form of „4 files”

### Order

**Name** | **Type** | **Description**
--------- | -----------| -----------
total | Number | Total amount of order.
tax | Number | Total tax.
couponDiscount | Number | Discount is  zero 0 unless any coupon is applied.
couponName |	String |	The name of the coupon (if any) applied to the cart. If no coupon was applied, will contain undefined. Does not contain the actual code of coupon, just the name.
volumeDiscount | Number | Discount based on the total of the items.
discount | Number | Sum of all discounts.
shipping | Number | Cost of shipping.
Cart | Cart |  объект корзины Cart

### Product

**Name** | **Type** | **Description**
--------- | -----------| -----------
id | Number | 
sku | string | SKU of the item.
price | Number | Price of the item.
name | string | Name of the item.
weight | Number | Weight of the item.
shortDescription | string | Description of the item.
url | string |  // url до продукта в кастомерке

## Example of using Ecwid Javascript API
Redirect Ecwid Paypal Orders to Custom “Thank You” Page: http://stevestruemph.com/2012/11/redirect-ecwid-paypal-orders-to-custom-thank-you-page/

# Single Sign-On API

Single sign-on (SSO) is a user authentication process that permits a user to enter one login and password in order to access multiple applications. For example if your site already has the ability to create accounts and you are using Ecwid your customers may find it rather inconvenient that they have to log in to your site and store separately.
 
This API allows your customers to sign into your site and fully use your store without having to sign into Ecwid. I.e. if a customer is logged in to your site, he/she is logged in to your store automatically, even if he/she didn’t have an account in your store before. This API is helpful for sites with an existing user base, who wants to make checkout process more transparent and easy for their customers.
  
## API Details
 
Providing user information to Ecwid
 
To make use of Single Sign-on (SSO) in your website it is neccessary to pass the signed user information to the Ecwid JavaScript API. This can be done by declaring the **ecwid_sso_profile** variable in your page and assigning it a value, containing three parts separated by spaces:
Base64-encoded JSON string containing user profile fields. The format of the profile field object is given below;
HMAC SHA1 signature of the Base64-encoded profile plus timestamp. Use your SSO secret key as a signature key. The secret key can be obtained in **Control Panel → System Settings → API**.
Current timestamp, i.e. the number of seconds during UNIX epoch. The system clock on your server must be in sync with the real time, otherwise signatures generated by your server will fail to validate in Ecwid. Ecwid allows this timestamp to be up to 10 minutes late. The timestamp ensures that the message cannot be intercepted and misused later.
 
Every message should have different signature. If a message has a signature that has already been seen recently, Ecwid denies the sign-on request.
To specify that no user is logged in, pass an empty string to the **ecwid_sso_profile**. The **ecwid_sso_profile** variable can be declared anywhere in your web page, either before the script.js or after. The **ecwid_sso_profile** is read once when Ecwid loads.
 
Assuming your secret key is `TEST`, the following PHP example creates a signed profile string:
 
```php
<?php
$sso_secret = "TEST";
$message = base64_encode("{appId:'123',userId:'234',profile:{email:'test@example.com'}}");
$timestamp = time();
$hmac = hash_hmac('sha1', "$message $timestamp", $sso_secret);
echo "\<script\> var ecwid_sso_profile = '$message $hmac $timestamp' \</script\>";
?>
```
 
### Profile field object
The fields of the profile object are:

Name |	Type |	Description 
--------- | -----------| -----------
appId | string |	Any arbitrary string identifying the 3rd-party authentication system. Never change your appId! see note below. 
userId  |string | Any string identifying the user in the 3rd-party authentication system. The combination of appId and userId identifies the customer profile in Ecwid 
profile	| [Customer](#customer) | Contains information about the user. The ‘id’ field of this object is ignored. This field is optional. If omitted, an anonymous Ecwid customer profile is created.
If a customer with the given combination of appId and userId already exists in Ecwid database, its profile gets merged with the specified fields of the profile object, except for the customer’s address book (the field shippingAddresses), which is only imported once when profile is created at the Ecwid side.
 
 
### Dynamically signing in or off
 
There is also a way to provide changes to the signed profile without reloading the web page, e.g. when implementing AJAX login/logout buttons. The **Ecwid.setSsoProfile(profile)** API call does exactly the same as **ecwid_sso_profile**, but can be used multiple times.
 
Note that **Ecwid.setSsoProfile(profile)**, **Ecwid.setSignInUrls()** and **Ecwid.setSignInProvider()** only work when Ecwid is in SSO mode, that is, when the global variable **ecwid_sso_profile** is also defined.
 
### Providing sign in / sign out functionality
 
Albeit optional, but highly recommended that you provide Ecwid a way to sign in your website. You can do that in two ways:
 
**Either set up the sign in / sign out page URLs:**

```js
window.Ecwid.OnAPILoaded.add(function() {
    window.Ecwid.setSignInUrls({
        signInUrl: 'http://my.site.com/signin',
        signOutUrl: 'http://my.site.com/signout' // signOutUrl is optional
    });
});
```

**...or  set up JavaScript actions to be invoked when signin in or out:**

```js
window.Ecwid.OnAPILoaded.add(function() {
  window.Ecwid.setSignInProvider({
    addSignInLinkToPB: function() { return true; },
    signIn: function () { alert('sign in');
      window.Ecwid.setSsoProfile('<?php echo "$message $hmac $timestamp"; ?>');
    },
    canSignOut: function() { return true; },
    signOut: function () { alert('sign out') }
  });
});
```
 
Note the wrapping *window.Ecwid.OnAPILoaded* call. As usual, JS API methods are available after *window.Ecwid.OnAPILoaded* callbacks are signalled. This is explained in JavaScript API
 
### window.Ecwid.setSignInUrls method
 
Sets up URLS of sign in / sign out pages of the website. The only argument is an object with the following fields:
 
**Name** | **Type** |	**Description** 
--------- | -----------| -----------
signInUrl |	url, string |	URL to which a customer will be redirected when Ecwid needs authorization, like when viewing orders.
signOutUrl |	url, string |	Optional. If specified, Ecwid shows the 'sign out' link pointing at this URL
 
### window.Ecwid.setSignInProvider method
 
Sets up Javascript functions to be called when Ecwid requires authorization or to be called when clicking the 'sign out' link. The only argument is an object with the following fields (all fields are mandatory):
 
**Name** | **Type** |	**Description** 
--------- | -----------| -----------
addSignInLinkToPB |	function returning boolean |	Return true if you need the 'sign in' link inside your Product browser
signIn |	function |	This function is called when Ecwid is trying to authorize the customer, when either 'sign in' link is clicked or a secured page is opened inside Product Browser (e.g. 'My account' page). This function does not accept any arguments nor should return any result.
canSignOut |	function returning boolean |	Return true if you need the 'sign out' link inside your Product browser
signOut |	function |	This function is called when canSignOut returns true and a customer clicks the 'sign out' link.
 
 
### Notes
1. Ecwid does not allow two customers with the same email address in one store. If a customer with the same email already exists and has different SSO appId/userId, or does not have them at all, then Ecwid will fail to create a customer account and will behave as if no user is logged in. For example, If you have a customer “customer@example.com” from Facebook, you cannot have another “customer@example.com” signing in using SSO. Ecwid will simply ignore “customer@example.com” in the **ecwid_sso_profile** variable.
2. If the Ecwid store has no [paid subscription](http://www.ecwid.com/compare-plans.html), Ecwid stops processing SSO messages for that store and will behave as if no user is logged in.
3. **Never change your appId!** Changing **appId** of an existing authentication system will result in inability of registered customers to sign on your website, because new customers will have different appId/userId combination and conflict with existing database records with the same email.
 
 
## Examples
The following example shows how to pass the user profile information to Ecwid and how to “log out” the user using JavaScript API. When called with the ?logoff=1 parameter, this script behaves as no user is logged in.
 
```html
<html><body>
<script>
<?php
if (!$_REQUEST['logoff']) {
        $profile = array(
                'appId' => "My cool app",
                'userId' => "234",
                'profile' => array(
                        'email' => "test@example.com",
                        'billingPerson' => array(
                                'name' => "Tester",
                                'companyName' => "Company Name",
                                'street' => "Street",
                                'city' => "City",
                                'countryCode' => "US",
                                'postalCode' => "10001",
                                'stateOrProvinceCode' => "NY"
                        )
                )
        );
        $message = json_encode($profile);
        $message = base64_encode($message);
        $timestamp = time();
        $hmac = hash_hmac('sha1', "$message $timestamp", "A1Lu7ANIhKD6");
        echo "var ecwid_sso_profile='$message $hmac $timestamp'";
} else {
        echo "var ecwid_sso_profile=''";
}
?>
</script>
<script src="http://app.ecwid.com/script.js?1003"></script>
<script>
xProductBrowser();
function logout() {
        window.Ecwid.OnAPILoaded.add(function() {
                window.Ecwid.setSsoProfile('');
        });
}
</script>
<a href="javascript: logout()">Log out</a>
</body></html>
```