---
title: API

language_tabs:
  - shell
  - python

toc_footers:
 - <a href='http://www.ecwid.com'>Register your application in Ecwid</a>
---


# Store profile

## Get profile

Returns store settings, including most of the settings configurable in the System Settings menu.

### URL

`GET http(s)://app.ecwid.com/api/v2/[STORE-ID]/profile?secure_auth_key=string`


### URL Parameters

**Name** |	**Type**	| **Description**
-------------- | -------------- | --------------
STORE-ID* |	number |	ID of the Ecwid store.
secure_auth_key |	string |	Product API secret key (can be found in the System Settings → API tab) or an OAuth authentication token. secure_auth_key allows access to the private profile fields. You should use HTTPS to pass this parameter. *Requires authentication*
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'Profile' with the following fields:

#### Profile
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
id	| number |	Store ID.
storeDescription |	string *nullable*	| The description of a store which is shown when users browses to the store front page.
mobileUrl	| string	| The URL of the mobile version of the store.
**System Settings → General → Store Profile** |
closed	| boolean	| 'true' if the store is closed for maintenance and 'false' if it is open.
enableIps | string *nullable*	| "Remain open for the IPs (comma-separated): setting. *Requires authentication*
storeName |	string *nullable*	| Store name.
storeUrl |	string |	Store url.
timezone | string	| Timezone as set in General → Store Profile.
googleAnalyticsId |	string *nullable* |	General → Store Profile → "Google Analytics ID" setting.
useGoogleRemarketing |	boolean |	"Remarketing with Google Analytics" setting.
companyName	| string *nullable*	| The store company name.
companyEmail |	string *nullable*	| The store company email. *Requires authentication*
officeLocation	| [Address](http://google.com) |	Company address and phone.
invoiceLogoUrl	| string |	Invoice Logo. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
**System Settings → General → Formats & Units** |
currency |	string |	Currency code, used in this store, as in ISO 4217 (`USD`, `CAD` etc.).
currencyPrefix |	string |	Prefix of the currency notation (e.g. $)
currencySuffix |	string |	Suffix of the currency notation
currencyPrecision | number	| Numbers of digits in the store price`s fractional part. Usually 2($2.99) or 0 (¥500).
currencyGroupSeparator |	string |	A thousands separator. Possible values: space, dot("."), comma (","), or empty value.
currencyDecimalSeparator |	string |	A symbol used in the store to mark the boundary between the integral and the fractional parts in prices. Possible values: dot or comma, For example "." for $59.99 or "," for "34,50руб".
currencyTruncateZeroFractional |	boolean |	If "true", remove trailing zeros after decimal point.
currencyRate |	number |	Currency rate, the cost of the current currency in U.S. dollars, as set in the System General → Formats & Units.
weightUnit |	string |	Weight unit used in store. One of `CARAT`, `GRAM`, `OUNCE`, `POUND`, `KILOGRAM`ю
weightPrecision |	number |	Numbers of digits in the store weight`s fractional part.
weightGroupSeparator |	string |	A thousands separator. Possible values: space, dot("."), comma (","), or empty value.
weightDecimalSeparator |	string |	A symbol used in the store to mark the boundary between the integral and the fractional parts in prices. Possible values: dot or comma, For example "." for $59.99 or "," for "34,50руб".
weightTruncateZeroFractional |	boolean |	If "true", remove trailing zeros after decimal point.
dateFormat |	string |	Date format, e.g. "dd-MM-yyyy". See [Date and time patterns](http://google.com) for the meaning of the special characters.
timeFormat |	string |	Time format, e.g. "HH:mm:ss". See [Date and time patterns](http://google.com) for the meaning of the special characters.
**System Settings → General → Languages** |
enabledLanguages |	 Array\<string\> |	Languages, enabled in General → Languages. The first language in list is the default one.
**System Settings → General → Cart** |
hideOutOfStockProducts |	boolean |	Hide out of stock products.
showBuyNow |	boolean |	Show "Buy now" buttons on products list pages.
defaultProductSortOrder |	string |	Default Products Sort Order. One of the following:
 | `normal` 	|
 | `addedTimeDesc` | Date added
 | `priceAsc`	| Price: low to high
 | `priceDesc` | Price: high to low
 | `nameAsc` |	Name: A to Z
 | `nameDesc` |	Name: Z to A
minSubtotal	| number *nullable* |	Minimum subtotal allowed before a customer can checkout. Absent if not limited.
maxSubtotal	| number *nullable*	| Maximum subtotal allowed before a customer can checkout. Absent if not limited.
skipPaymentMethodSelectionWhenZeroTotal |	boolean |	Skip payment method selection, if order total is zero.
orderStatusWhenZeroTotal |	string *nullable* |	Set order status to this value when `orderStatusWhenZeroTotal==true`. One of `ACCEPTED`, `QUEUED`.
forceRegistrationOnCheckout |	boolean |	General → Cart → "Require customers to create accounts on checkout" setting.
requirePhoneOnCheckout |	boolean |	General → Cart → "Require phone number on checkout" setting.
askOptionsOnAddition |	boolean |	True to ask the customer to select product options when adding products to the cart from a product list. False to use default option values.
openBagOnAddition |	boolean |	General → Cart → 'Open bag when "Add to bag" is clicked' setting.
askCompanyName |	boolean |	General → Cart → "Ask for the company name" setting.
affiliateCodeEnabled |	boolean |	Tracking code on "Thank you for your order" page is enabled.
affiliateCode |	string *nullable* |	When `affiliateCodeEnabled==true`, this is a tracking code on "Thank you for your order" page.
billingAddressDuringCheckoutEnabled |	boolean |	Ask for a billing address during checkout.
showCompareToOnProductList |	boolean |	Display “Compare to” price on product list.
compareToPriceName |	string |	"Compare to" price name.
compareToPriceSaveUnit |	string |	Value of the "Show “Save” in" setting. One of `PERCENT`, `CURRENCY`, `NOTSHOW`.
enableOrderNoted |	boolean |	True if order notes field is enabled.
orderNotedCaption |	string |	Order notes field caption.
requireTermsOnCheckout |	boolean |	True if the “Terms and Conditions” checkbox is enabled.
termsOnSeparateUrl |	boolean |	If `requireTermsOnCheckout==true`, this flag is true if you want to show an external URL as your terms.
externalTermsUrl |	string *nullable* |	If both `requireTermsOnCheckout` and `termsOnSeparateUrl` are true, this is the URL of your terms.
checkoutTerms |	string *nullable* |	If `requireTermsOnCheckout==true` and `termsOnSeparateUrl==false`, this is the terms text shown in a popup.
orderNumberSettings |	[OrderNumberSettings](http://google.com) |	Order number generation config, as in System Settings → General → Cart. *Requires authentication*
enableRelatedProductsOnCart |	boolean |	True if Related products are enabled on cart page.
**System Settings → General → E-goods** |
downloadConfig |	[DownloadConfig](http://google.com) |	E-goods download config, as in System Settings → General → E-goods. *Requires authentication*
System Settings → General → Migrations |
adaptiveDesignMigration |	boolean |	The 'Adaptive design for Product browser' flag.
newContinueButtonMigration |	boolean |	The 'New "Continue" buttons on the checkout pages' flag.
System Settings → Zones |
zones |	Array[\<Zone\>](http://google.com) |	Geographical zones settings. *Requires authentication*
**System Settings → Shipping** |
shippingSettings |	[ShippingSettings](http://google.com) |	Shipping settings.
carrierOnlineSettings |	[CarrierOnlineSettings](http://google.com) |	Configuration of online shipping rate services. *Requires authentication*
storeSameAsOffice |	boolean |	True, if the officeLocation is used as the 'from' address for shipping.
storeLocation |	[Address](http://google.com) *nullable* |	A separate address used to deliver items from. If `storeSameAsOffice == true`, the office address is used instead to calculate shipping cost.
**(System Settings → Taxes** |
showTaxes |	boolean |	Taxes → "Show included taxes on product details page" setting.
taxes |	 Array[\<Tax\>](http://google.com) |	Taxes configuration.
**System Settings → Payment** |
paymentMethods | Array[\<PaymentMethod\>](http://google.com)	| Payment → Payment Methods configuration. Note that payment processor configuration is stored separately in the `paymentModulesConfiguration` field. *Requires authentication*
paymentModulesConfiguration |	[PaymentModulesConfiguration](http://google.com) |	Configuration of payment modules, including Google Wallet and PayPal Express Checkout.
**System Settings → Design** |
themeSettings |	[ThemeSettings](http://google.com) |	Storefront CSS theme settings as in System Settings → Design → Design Settings. *Requires authentication*
productThumbnailSize	| number |	Width and height of the box product thumbnails should fit in. Default in 160 pixels.
categoryThumbnailSize |	number |	Width and height of the box category thumbnails should fit in. Default in 160 pixels.
**System Settings → Mail** |
fromEmail |	string *nullable* |	System Settings → Mail → Customer notifications → "From" email address. *Requires authentication*
useCompanyEmail |	boolean |	True, if "same as company" is checked.
fromAdminEmail |	string *nullable* |	System Settings → Mail → Admin notifications → Send notifications to email. *Requires authentication*
useCompanyAdminEmail |	boolean |	True, if "same as company" is checked. *Requires authentication*
mailNotifications | Array\<[MailNotification](http://google.com)\>	| Notification email templates. *Requires authentication*
**System Settings → Social Tools → Share buttons** |
fbLikeButtonConfig	| [FBLikeButtonConfig](http://google.com) |	Facebook Like Button settings.
tumblrButtonConfig |	[TumblrButtonConfig](http://google.com)	| Tumblr configuration.
twitterButtonConfig |	[TwitterButtonConfig](http://google.com)	| Twitter configuration.
pinterestButtonConfig |	[PinterestButtonConfig](http://google.com)	| Pinterest configuration.
googleButtonConfig |	[GoogleButtonConfig](http://google.com) |	Google Plus configuration.
vkButtonConfig |	[VKButtonConfig](http://google.com) |	VKontakte button configuration.
**System Settings → Social Tools → FB Comments** |
fbCommentConfig |	[FBCommentConfig](http://google.com) |	Facebook comments settings.
**System Settings → Social Tools → Share Purchase** |
sharePurchaseConfig	| [SharePurchaseConfig](http://google.com) |	Share Purchase settings.
**System Settings → Social Tools → Ask Friends** |
enableAskForAdvice |	boolean |	Ask a customer to advise product.
**Promotions → Discounts** |
discounts | Array\<[Discount](http://google.com)\> |	Discounts Based on Subtotal. *Requires authentication*
billMeLaterConfig |	[BillMeLaterConfig](http://google.com) *nullable* |	Settings on the Promotion → Bill Me Later tab. Null if the Bill Me Later banner is disabled.
Deprecated fields |
groupSeparator |	string |	Deprecated as of API v2. Use currencyGroupSeparator or weightGroupSeparator instead.
decimalSeparator |	string |	Deprecated as of API v2. Use currencyDecimalSeparator or weightDecimalSeparator instead.
numericPrecision |	number |	Deprecated as of API v2. Use currencyPrecision instead.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Address
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
street |	string *nullable* |	A newline-separated street address. Up to two lines allowed.
city	| string *nullable* |	City name.
countryCode	| string *nullable*	| A two-letter ISO code of the country.
postalCode	| string *nullable* |	Postal code or ZIP code.
stateOrProvinceCode	| string *nullable* |	State code (e.g. `NY`). See list of supported state codes.
phone |	string *nullable* |	
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OrderNumberSettings
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
nextNumber |	number	| Use this number as the next order number, if it is less then any existing order number.
numberLength |	number |	Pad order number to this length with zeroes `0`. `0` means no padding.
numberPrefix |	string	| Prefix every new order number with the given prefix.
numberSuffix |	string	| Add the given suffix to every generated order number.

#### DownloadConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
timeToLiveHours |	number |	Number of hours the download link is valid. Zero means unlimited.
maxDownloads	| number	| Maximum number of downloads by customer. Zero means unlimited.

#### Zone
**Field**	| **Type**	| **Description**
-------------- | -------------- | --------------
id |	string |	Unique zone ID.
name |	string |	Zone display name.
countryCodes	| Array\<string\> |	Country codes this zone contains.
stateOrProvinceCodes |	Array\<string\>	| State or province codes the zone contains.
postCodes | Array\<string\> |	Postcode (or zipcode) templates this zone contains.

#### ShippingSettings
**Field**	| **Type**	| **Description**
-------------- | -------------- | --------------
entries | Array\<[ShippingMethod](http://google.com)\>	

#### CarrierOnlineSettings
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
AP |	[AustraliaPostConfig](http://google.com) |	The **Australia Post** shipping module configuration.
BC |	[BrasilCorreiosConfig](http://google.com) |	The **Brasil Correios** shipping module configuration.
CP |	[CanadaPostConfig](http://google.com) |	The **Canada Post** shipping module configuration.
DHL |	[DHLConfig](http://google.com) |	The **DHL/Airborne** shipping module configuration.
EMS |	[EMSConfig](http://google.com) |	The **EMS Russian Post** shipping module configuration.
FEDEX |	[FedExConfig](http://google.com) |	The **FedEx** shipping module configuration.
MDS |	[MDSConfig](http://google.com) |	The **MDS Collivery** shipping module configuration.
UPS	| [UPSConfig](http://google.com) |	The **UPS** shipping module configuration.
USPS |	[USPSConfig](http://google.com) |	The **U.S.P.S.** shipping module configuration.

#### Tax
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id |	number |	Unique ID of the tax.
name |	string |	Display name of the tax.
enabled |	boolean |	True if the tax should apply.
includeInPrice |	boolean |	True is the tax should be included in the product price.
useShippingAddress |	boolean |	True to use shipping address for zone matching. False to use billing address. Note that e-goods are always taxed by the billing address.
taxShipping |	boolean |	True if the tax should apply to the shipping cost as well as the ordered items.
appliedByDefault |	boolean |	True if the tax should apply to all products. False enables per-product tax application. See property 'taxes' of the Product model.
rules | Array\<[TaxRule](http://google.com)\>	| Tax amount per geographical zone.
defaultTax |	number |	Tax value, in %, when none of the zones above match.

#### PaymentMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
name |	string |	Name of the payment method that is shown to customers, plain text.
instructions |	string |	An optional plain text note that is shown to the right from the payment method name.
enabled |	boolean |	True to show the method to customers.
paymentInstructionsTitle |	string *nullable* |	An optional plain text title of a separate block that is shown when the method is chosen.
paymentInstructions |	string *nullable* |	An optional HTML text shown in a separate block when the method is chosen.
processor |	string *nullable* |	The payment processor selected by the merchant in the payment method table. Null if not selected. One of the following:
 | `sagePayCC` |	Credit Card: SagePay
 | `payJunctionCC` |	Credit Card: PayJunction hosted checkout (QuickShop)
 | `suomenVerkkomaksutCC`	| Credit Card: Paytrail (Finnish Web Payments)
 | `beanStreamCC` |	Credit Card: BeanStream Hosted Payment Form 
 | `twoCheckoutCC` |	Credit Card: 2Checkout 
 | `authorizeNetCC` |	Credit Card: Authorize.Net SIM
 | `epath` |	Credit Card: e-Path
 | `sageEVD` |	Credit Card: Sage Exchange
 | `NMICC` |	Credit Card: Network Merchants
 | `HSBC` |	Credit Card: HSBC Secure ePayments
 | `HSBC_GLOBAL_IRIS` |	Credit Card: Realex Payments/Global Iris
 | `iPay` |	Credit Card: iPay88
 | `eSelectPlusCC` |	Credit Card: eSELECT Plus Hosted Paypage
 | `eWay` |	Credit Card: eWay Hosted Payment Page
 | `globalGatewayE4` |	Credit Card: First Data Global Gateway e4
 | `vcs` |	Credit Card: Virtual Card Services
 | `payFast` |	Credit Card: PayFast
 | `clickandbuy` |	ClickandBuy
 | `bancomer` |	Credit Card: BBVA Bancomer / eGlobal
 | `multiSafepay` |	MultiSafepay
 | `twoCheckoutECheck` |	ECheck: 2Checkout
 | `amex` |	Credit Card: American Express Payment Gateway
 | `authorizeNetECheck` |	ECheck: Authorize.Net SIM
 | `paypalStandard` |	PayPal Website Payments Standard
 | `paypalProHosted` |	PayPal Payments Pro Hosted
 | `paypalPayflowLink` |	Payflow Link
 | `paypalPayflowAdvanced` |	PayPal Payments Advanced
 | `paypalExpressCheckout` |	paypal
 | `iPayment` |	iPayment von 1 & 1
 | `pagSeguro` |	PagSeguro UOL
 | `robokassa`	Robokassa
 | `qiwi` |	QIWI Кошелек
 | `iDEALMollie` |	iDEAL / Mollie
 | `payOnline` |	PayOnline System
 | `offline` |	Offline Basic
 | `offlineCheck` |	Offline Check
 | `offlinePurchaseOrder` |	Purchase order
 | `demoAccept` |	Demo (accept all orders)
 | `demoDecline` |	Demo (decline all orders)
tag |	string *nullable* |	An optional tag which tags 'special' payment methods. One of 'robokassa', 'qiwi', 'paypal'
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PaymentModulesConfiguration
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
Authorize.Net	| [AuthorizeNetConfig](http://google.com)  *nullable* |	The **Credit Card: Authorize.Net SIM** payment module configuration.
NetworkMerchants |	[AuthorizeNetEmlConfig](http://google.com)  *nullable* |	The **Credit Card: Network Merchants** payment module configuration.
ESelectPlus |	[ESelectPlusConfig](http://google.com)  *nullable*|	The **Credit Card: eSELECT Plus Hosted Paypage** payment module configuration.
SagePay |	[SagePayConfig](http://google.com) *nullable* |	The **Credit Card: SagePay** payment module configuration.
SageExchangeVirtualDesktop  |	[SageEVDConfig](http://google.com) *nullable* |	The **Credit Card: Sage Exchange** payment module configuration.
BeanStream |	[BeanStreamConfig](http://google.com)  *nullable* |	The **Credit Card: BeanStream Hosted Payment Form** payment module configuration.
eWay |	[EWayConfig](http://google.com) *nullable* |	The **Credit Card: eWay Hosted Payment Page** payment module configuration.
GlobalIris	| [HSBCGlobalIrisConfig](http://google.com) *nullable* |	The **Credit Card: Realex Payments/Global Iris** payment module configuration.
PayJunction |	[PayJunctionConfig](http://google.com) *nullable* |	The **Credit Card: PayJunction hosted checkout (QuickShop)** payment module configuration.
SuomenVerkkomaksut |	[SuomenVerkkomaksutConfig](http://google.com) *nullable* |	The **Credit Card: Paytrail (Finnish Web Payments)** payment module configuration.
IDEALMollie |	[IDEALMollieConfig](http://google.com) *nullable* |	The **iDEAL / Mollie** payment module configuration.
PayOnline |	[PayOnlineConfig](http://google.com) *nullable* |	The **PayOnline System** payment module configuration.
Robokassa |	[RobokassaConfig](http://google.com) *nullable* |	The **Robokassa** payment module configuration.
iPayment |	[IPaymentConfig](http://google.com) *nullable* |	The **iPayment von 1 & 1** payment module configuration.
pagSeguro |	[PagSeguroConfig](http://google.com) *nullable* |	The **PagSeguro UOL** payment module configuration.
Qiwi |	[QiwiConfig](http://google.com) *nullable* |	The **QIWI Кошелек** payment module configuration.
PayPalStandard |	[PayPalStandardConfig](http://google.com) *nullable* |	The **PayPal Website Payments Standard** payment module configuration.
PayPalPayflowLink |	[PayPalPayflowLinkConfig](http://google.com) *nullable* |	The **Payflow Link** payment module configuration.
IPay |	[IPayConfig](http://google.com) *nullable* |	The **Credit Card: iPay88** payment module configuration.
VCS	| [VCSConfig](http://google.com) *nullable* |	The **Credit Card: Virtual Card Services** payment module configuration.
MultiSafepay |	[MultiSafepayConfig](http://google.com) *nullable* |	The **MultiSafepay** payment module configuration.
ClickAndBuy |	[ClickAndBuyConfig](http://google.com) *nullable* |	The **ClickandBuy** payment module configuration.
2Checkout.com |	[TwoCheckoutConfig](http://google.com) *nullable* |	The **Credit Card: 2Checkout** payment module configuration.
e-Path |	[EPathConfig](http://google.com) *nullable* |	The **Credit Card: e-Path** payment module configuration.
Bancomer |	[BancomerConfig](http://google.com) *nullable* |	The **Credit Card: BBVA Bancomer / eGlobal** payment module configuration.
Amex |	[AmexConfig](http://google.com) *nullable* |	The **Credit Card: American Express Payment Gateway** payment module configuration.
PayFast |	[PayFastConfig](http://google.com) *nullable* |	The **Credit Card: PayFast** payment module configuration.
PayPalPro	| [PayPalProConfig](http://google.com) *nullable* |	The **PayPal Payments Pro Hosted** payment module configuration.
GlobalGatewayE4 |	[GlobalGatewayE4Config](http://google.com) *nullable* |	The **Credit Card: First Data Global Gateway e4** payment module configuration.
google |	[GoogleConfig](http://google.com) *nullable* |	The **Google Checkout** payment module configuration.
paypal |	[PayPalConfig](http://google.com) *nullable* |	The **PayPal Checkout** payment module configuration.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ThemeSettings
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
customThemes | Array\<[CustomTheme](http://google.com)\> |	CSS themes developed by store owner.
activeThemeId |	string |	An identifier of an active theme, either custom or built-in. Build-id themes are "Standard.css", "Red.css", and "Beige.css"

#### MailNotification
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
type |	string |	Notification type. One of the following:
 | `ADMIN_ACTIVATION` |	Welcome to Ecwid!
 | `ADMIN_VALIDATION` |	!MailNotification.admin_validation!
 | `NEW_ORDER_ADMIN` |	New order
 | `ORDER_PAID_ADMIN` |	Order is paid
 | `ORDER_FAILED_ADMIN` |	Order payment failed
 | `STOCK_ADMIN` |	Stock notification
 | `PASSWORD` |	Password reminder
 | `REGISTRATION` |	Successful registration
 | `ORDER_COMPLETED` |	Order is completed
 | `ORDER_REJECTED` |	Order is rejected
 | `EGOODS` |	Egoods download
 | `SHIPPING` |	Order shipped
enabled |	boolean |
subjectTemplate |	string |	
bodyTemplate |	string | 

#### FBLikeButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show	| boolean |	Show Like button.
display |	string |	Like button position. One of `DETAILS`, `LIST_DETAILS`.
sendButton |	boolean |	Show Send button.
colorScheme |	string |	Color Scheme. One of `light`, `dark`
font |	string |	Font used for the button text (e.g. `Arial` or `Lucida`).

#### TumblrButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Tumblr button.
display |	string |	Button design type. One of `tumblr_1`, `tumblr_1T`, `tumblr_2`, `tumblr_2T`, `tumblr_4`, `tumblr_4T`

#### TwitterButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Twitter button.
displayCounter |	boolean |	True to show share counter.
viaAccount |	string *nullable* |	Twitter account
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PinterestButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Pinterest button.
displayCounter |	boolean |	True to show share counter.

#### GoogleButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Google Plus button.

#### VKButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show VKontakte button.

#### FBCommentConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show FB comments.
colorScheme |	string |	Color Scheme. One of `light`, `dark`.
posts |	number |	Number of posts
width |	number |	Width, px
appId |	string |	Your FB app id
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### SharePurchaseConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
sharePurchase |	boolean |	Ask a customer to share his purchase.
shareTwitterAccount |	string *nullable* |	Your store's Twitter account
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Discount
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
base |	string |	Specifies condition when this discount is valid. *One of the following:*
 | `ON_TOTAL` |	Order total should be at least the one specified in the `orderTotal` field
 | `ON_MEMBERSHIP` |	Customer should be a member of a group with ID membershipId
 | `ON_TOTAL_AND_MEMBERSHIP` |	Both order total and customer's membership conditions apply
orderTotal |	number |	Minimal order total required for this discount to be applicable.
membershipId |	number |	An ID of the customer group this discount is applicable to.
value |	number |	Discount value, in % or currency, depending on the `type` field.
type |	string |	The type of the 'value' field: % or currency. One of `ABS`, `PERCENT`.

#### BillMeLaterConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
publisherId |	string |	An internal ID retrieved from PayPal used to show the Bill Me Later banner.
showOnHomePage |	boolean |	Show the Bill Me Later banner on the main store page.
showBottomHome |	boolean |	If `showOnHomePage=true`, this flag specifies where on the main store page the banner should be shown. Value `true` means bottom of the page, while `false` means the top.
showOnProductListPage |	boolean |	Show the Bill Me Later banner on the product list page.
showBottomProductList |	boolean |	If `showOnProductListPage=true`, this flag specifies where on the product list page the banner should be shown. Value `true` means bottom of the page, while `false` means the top.
showOnProductDetailsPage |	boolean |	Show the Bill Me Later banner on the product page.
showOnCartPage |	boolean |	Show the Bill Me Later banner on the shopping cart page.

#### CustomTheme
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	string |	A unique ID of a theme.
displayName |	string |	The theme name shown to the user.
css |	string |	Theme's CSS code.

#### ShippingMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	string |	Unique id of this method.
name |	string |	Display name of this shipping method.
zone |	string *nullable* |	An optional ID of the zone this method is applicable to. See 'zones' property of the profile. The special value `WORLD` refers to the 'The World' zone.
deliverySpeed |	string *nullable* |	Delivery speed, in days.
orderBy |	number |	Position in the shipping method list.
enabled |	boolean |	True if the shipping method is visible to customers.
type |	string |	How the shipping rate gets calculated. One of the following:
 | `FLAT` |	Flat shipping rate or free shipping.
 | `TABLE` |	Shipping costs based on the number of items, total weight, or cart price.
 | `CARRIER` |	Receive shipping costs from the major shipping carrier companies (UPS, USPS, FedEx, Canada Post, Australia Post, EMS Russian Post).
rate |	number *nullable* |	Only for type=`FLAT`. Flat shipping rate.
unit |	string *nullable* |	Only for type=`FLAT`. Unit of the flat shipping rate. One of `CURRENCY`, `PERCENT`.
rangesOn |	string *nullable* |	Only for type=TABLE. What the rate rules depend on. One of the following:
 | `subtotal` |	Shipping rate rules depend on order subtotal.
 | `weight` |	Shipping rate rules depend on weight.
columns |	string *nullable* |	Only for type=TABLE. This specifies the rate calculation formula. One of the following:
 | `perOrder` |	Only per-order flat rate is specified for each rule.
 | `full` |	Per order + Per item + Percent charge + Per lbs
entries | Array\<[RateRule](http://google.com)\> |	Only for type=`TABLE`. Set of rules to calculate shipping rate. Each rule is only applicable to some subtotal or weight range (depending on 'rangesOn' property).
carrier |	string *nullable* |	Only for type=CARRIER. Sets which carrier to use for this shipping method. One of the following:
 | `AP` |	Australia Post
 | `BC` |	Brasil Correios
 | `CP` |	Canada Post
 | `DHL` |	DHL/Airborne
 | `EMS` |	EMS Russian Post
 | `FEDEX` |	FedEx
 | `MDS` |	MDS Collivery
 | `UPS` |	
 | `USPS` |	U.S.P.S.
methods	| Array\<[string](http://google.com)\> *nullable* |	Only for type=`CARRIER`. A list of shipping method codes that are enabled, ordered in the same way they should appear in customer frontend. These should correspond to the codes listed in `CarrierOnlineSettings`.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### TaxRule
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
zone |	string |	Unique zone ID. This should match one of the zones in 'zones' profile field. The special value `WORLD` refers to 'The World' zone.
tax |	number |	Tax value. in %, for this zone.

#### AustraliaPostConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
packageDimensions |	[Dimensions](http://google.com) |	
useDefaultAccount |	boolean |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like `FedEx`
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.

#### BrasilCorreiosConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountId |	string *nullable* |	
packageDimensions |	[Dimensions](http://google.com) |	
packagingType |	string *nullable* |	One of the following:
 | `BOX` |	Box
 | `ENVELOPE` |	Envelope
password |	string |	
restrictDelivery |	boolean |	
signatureConfirmation |	boolean |	
useDefaultAccount |	boolean |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like 'FedEx'
configured	| boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### CanadaPostConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
customerNumber	| string *nullable* |	
merchantId |	string *nullable* |	
options | Array\<string\> |	One of the following:
 | `SO` |	Signature
 | `COV` |	Coverage
 | `COD` |	
 | `PA18` |	Proof of Age Required - 18
 | `PA19` |	Proof of Age Required - 19
 | `HFP` |	Card for pickup
 | `DNS` |	Do not safe drop
 | `LAD` |	Leave at door - do not card
packageDimensions |	[Dimensions](http://google.com)	|
password |	string *nullable* |	
showOldSettings	| boolean *nullable* |	
useDefaultAccount |	boolean |	
username |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like `FedEx`
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### DHLConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountNumber |	string *nullable*	|
packageDimensions |	[Dimensions](http://google.com) |	
password |	string *nullable* |	
shippingKey |	string *nullable* |	
testEnvironment |	boolean |	
useDefaultAccount |	boolean |	
userID |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName	| string |	Shipping carrier name, like 'FedEx'
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### EMSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
internationalDeliveryType |	string | One of the following:
 | `doc` | Documents (max 2kg)
 | `att` |	Attachments
useDefaultAccount |	boolean |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\>	| Shipping methods.
carrierName |	string |	Shipping carrier name, like `FedEx`.
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.

#### FedExConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountNumber |	string *nullable* |	
dropoffType |	string |	One of the following:
 | `REGULARPICKUP`	| Regular Pickup
 | `REQUESTCOURIER` |	Request Courier
 | `DROPBOX` |	Drop Box
 | `BUSINESSSERVICECENTER` |	Business Service Center
 | `STATION` |	Station
meterNumber |	string *nullable* |	
packageDimensions |	[Dimensions](http://google.com)	|
rateRequestType |	string	| One of the following:
 | `LIST` |	Standard list rates
 | `ACCOUNT` |	Discounted rates
shipToResidence |	boolean |	
testAccount	| boolean |	
useDefaultAccount |	boolean |	
webAuthKey |	string *nullable* |	
webAuthPassword |	string *nullable* |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like `FedEx`
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### MDSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
clientID |	string *nullable* |	
defaultAddress |	string *nullable* |	
defaultContact |	string *nullable* |	
email |	string |	
packageType |	string *nullable* |	One of the following:
 | `MDS_ENVELOPE` | Envelope (documents less than 2Kg and A4 size)
 | `MDS_PACKAGE` |	Package (Parcel Exceeding 2Kg and any dimension above 20cm)
 | `MDS_DOCUMENTS` |	Tender Documents (Documents for lodging Tenders)
password |	string *nullable* |	
token |	string *nullable* |	
useDefaultAccount |	boolean |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like 'FedEx'
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### UPSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accessLicenseNumber |	string *nullable* |	
accountNumber |	string *nullable* |	
customerClassification |	string |	One of the following:
 | `CC01`	| Rates Associated with Shipper Number
 | `CC03`	| Daily Rates
 | `CC04`	| Retail Rates
 | `CC53`	| Standard List Rates
negotiatedRates |	boolean |	
packageDimensions |	[Dimensions](http://google.com) |	
password |	string *nullable* |	
testEnvironment |	boolean |	
useDefaultAccount |	boolean |	
userId |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string |	Shipping carrier name, like `FedEx`.
configured |	boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### USPSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
firstClassMailType |	string |	One of `LETTER`, `FLAT`, `PARCEL`.
intlMailType |	string |	One of the following:
 | `PACKAGE` |	Package
 | `POSTCARDS_OR_AEROGRAMMES`	| Postcards or aerogrammes
 | `MATTER_FOR_THE_BLIND` |	Matter for the blind
 | `ENVELOPE`	| Envelope
onlineRates |	boolean |	
packageDimensions |	[Dimensions](http://google.com) |	
size |	string |	One of the following:
 | `REGULAR` |	Regular (neither dimension exceeds 12 inches)
 | `LARGE` |	Large (any dimension exceeds 12 inches)
 | `OVERSIZE` |	Oversize (obsolete, same as large)
useDefaultAccount |	boolean |	
userId |	string *nullable* |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
carrierName |	string  |	Shipping carrier name, like `FedEx`
configured	| boolean |	True if the required fields are filled properly and the shipping service can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Dimensions
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
length |	number |	The length of a bundle or package to use when calculating rates, in meters.
width |	number |	The width of a bundle or package to use when calculating rates, in meters.
height |	number |	The height of a bundle or package to use when calculating rates, in meters.

#### CarrierCalculatedMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
name |	string |	The shipping method human-readable name, plain text.
code |	string |	The shipping method provider-specific unique code.
orderBy |	number |	Position in the resulting list of shipping methods shown to a customer.
maxWeight |	number |	Maximum weight of a package this method can serve, pounds.

#### RateRule
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
from |	number *nullable* |	Subtotal or weight range start.
to |	number |	Subtotal or weight range end. Unlimited if absent.
perOrder |	number *nullable* |	Flat shipping rate.
perWeight |	number *nullable* |	Shipping cost per weight unit. E.g. if the current weight unit is lbs, then this value specifies the cost per lbs.
perItem |	number *nullable* |	Shipping cost per order item.
percent	| number *nullable* |	Shipping cost as a % of order subtotal.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AuthorizeNetConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
MD5Hashvalue |	string *nullable* |	
emailReceipt |	boolean |	
endpointUrl |	string *nullable*	|
loginId |	string *nullable*  |
testAccount |	boolean |	
testMode |	boolean |	
transKey |	string *nullable* |	
transType |	string |	One of `AUTH_ONLY`, `AUTH_CAPTURE`.
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AuthorizeNetEmlConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
loginId |	string *nullable* |	
testMode |	boolean |	
transKey |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ESelectPlusConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
hppKey | string *nullable* |
psStoreId |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### SagePayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
encryptPswd |	string *nullable* |	
simulatorServer |	boolean |	
testMode |	boolean |	
txType |	string |	One of `PAYMENT`, `DEFERRED`, `AUTHENTICATE`
vendor |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### SageEVDConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
transactionType |	string |	One of the following:
 | `Auth` |	Authorization Only
 | `Sale` |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### BeanStreamConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
hashKey |	string *nullable* |	
merchantId |	string *nullable* |	
trnType |	string |	One of `PURCHASE_ONLY`, `PREAUTH_ONLY`
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### EWayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountType |	string *nullable*	| One of `AU`, `NZ`, `UK`
customerId |	string *nullable* |	
pageDescription |	string *nullable* |	
pageFooter |	string *nullable* |	
pageTitle |	string *nullable* |	
upgradedAU |	boolean |	True if the account was upgraded to use the newest EWay AU API.
userName |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### HSBCGlobalIrisConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId |	string |	
sharedSecret |	string *nullable* |	
subAccount |	string |	
transactionSettleType |	string |	One of `MANUAL`, `AUTOMATIC`
transactionType |	string	| One of `MANUAL`, `AUTOMATIC`
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayJunctionConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
storeId |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### SuomenVerkkomaksutConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantAuthHash |	string *nullable* |	
merchantId |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### IDEALMollieConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
banks |	string *nullable* |	
lastBanksUpdate |	number |	
partnerId |	string *nullable* |	
testMode |	boolean	|
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayOnlineConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId | string *nullable*	|
privateSecurityKey |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RobokassaConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
login | string *nullable*	|
password1 |	string *nullable* |	
password2 |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### IPaymentConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountId |	string *nullable* |	
applicationId |	string *nullable* |	
applicationPassword |	string *nullable* |	
securityKey |	string *nullable* |	
transactionType |	string |	One of the following:
 | `preauth` |	Delayed Payment Process/pre-authorization (preauth)
 | `auth` |	Instant Booking of a Payment (auth)
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PagSeguroConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
email |	string *nullable* |	
token |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### QiwiConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
login |	string *nullable* |	
password |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayPalStandardConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
businessId |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayPalPayflowLinkConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantLogin |	string *nullable* |	
partner |	string *nullable* |	
password |	string *nullable*	|
testMode |	boolean |	
transactionType |	string |	One of the following:
 | `AUTH` |	Authorization
 | `SALE` |	Sale
user |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### IPayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantCode |	string *nullable* |	
merchantKey |	string *nullable*	|
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### VCSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantPAM |	string *nullable* |	
secretWord	| string *nullable* |	
terminalId |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### MultiSafepayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
account |	string *nullable* |	
siteID |	string *nullable* |	
siteSecureCode |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ClickAndBuyConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantID |	string *nullable* |	
mmsSharedSecret |	string *nullable* |	
projectID |	string *nullable* |	
secretKey |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### TwoCheckoutConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
convertToUSD |	boolean |	
demo |	boolean |	
secretWord |	string *nullable* |	
sid |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### EPathConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
frequency |	string |	
url |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### BancomerConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantCode |	string *nullable* |	
secretCode |	string *nullable* |	
terminal |	string |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AmexConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
apiPassword |	string *nullable* |	
merchantId |	string *nullable*	|
transactionType |	string |	One of the following:
 | `AUTH` |	Authorize and Capture
 | `PAY` |	Purchase
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayFastConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
emailConfirmation |	boolean |	
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
pdtKey |	string *nullable* |	
testMode |	boolean |	
configured |	boolean	| True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayPalProConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
businessId |	string *nullable* |	
testMode |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GlobalGatewayE4Config
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
paymentPageId |	string |	
responseKey |	string |	
testMode |	boolean |	
transactionKey |	string |	
transactionType |	string |	One of `AUTH_CAPTURE`, `AUTH_ONLY`
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.

#### GoogleConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
allowAVSCodes |	string |	
allowCVNCodes |	string |	
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
sandbox |	boolean |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### PayPalConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
apiPassword |	string *nullable* |	
apiUsername |	string *nullable* |	
billMeLaterButton |	boolean |	
paymentAction |	string |	One of the following:
 | `ORDER` | Order
 | `AUTH` |	Authorization
 | `SALE` |	Sale
sandbox |	boolean |	
signature |	string *nullable*	|
subject |	string *nullable* |	
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Errors
**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |		| Store ID not found.


## Change profile

Returns store settings, including most of the settings configurable in the System Settings menu.

### URL

`GET http(s)://app.ecwid.com/api/v2/[STORE-ID]/profile?secure_auth_key=string`


### URL Parameters

**Name** |	**Type**	| **Description**
-------------- | -------------- | --------------
STORE-ID* |	number |	ID of the Ecwid store.
secure_auth_key |	string |	Product API secret key (can be found in the System Settings → API tab) or an OAuth authentication token. secure_auth_key allows access to the private profile fields. You should use HTTPS to pass this parameter. *Requires authentication*
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type `Profile` with the following fields:

#### Profile
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
storeDescription |	string *nullable*	| The description of a store which is shown when users browses to the store front page.
**System Settings → General → Store Profile** |
closed	| boolean	| `true` if the store is closed for maintenance and `false` if it is open.
enableIps | string *nullable*	| "Remain open for the IPs" (comma-separated): setting. *Requires authentication*
storeName |	string *nullable*	| Store name.
storeUrl |	string |	Store url.
timezone | string	| Timezone as set in General → Store Profile.
googleAnalyticsId |	string *nullable* |	General → Store Profile → "Google Analytics ID" setting.
useGoogleRemarketing |	boolean |	"Remarketing with Google Analytics" setting.
companyName	| string *nullable*	| The store company name.
companyEmail |	string *nullable*	| The store company email. *Requires authentication*
officeLocation	| [Address](http://google.com) |	Company address and phone.
invoiceLogoUrl	| string *nullable* |	Invoice Logo. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
**System Settings → General → Formats & Units** |
currency |	string |	Currency code, used in this store, as in ISO 4217 (`USD`, `CAD` etc.).
currencyPrefix |	string |	Prefix of the currency notation (e.g. $)
currencySuffix |	string |	Suffix of the currency notation
currencyGroupSeparator |	string |	A thousands separator. Possible values: space, dot("."), comma (","), or empty value.
currencyDecimalSeparator |	string |	A symbol used in the store to mark the boundary between the integral and the fractional parts in prices. Possible values: dot or comma, For example "." for $59.99 or "," for "34,50руб".
currencyTruncateZeroFractional |	boolean |	If "true", remove trailing zeros after decimal point.
currencyRate |	number |	Currency rate, the cost of the current currency in U.S. dollars, as set in the System General → Formats & Units.
weightUnit |	string |	Weight unit used in store. One of `CARAT`, `GRAM`, `OUNCE`, `POUND`, `KILOGRAM`.
weightGroupSeparator |	string |	A thousands separator. Possible values: space, dot("."), comma (","), or empty value.
weightDecimalSeparator |	string |	A symbol used in the store to mark the boundary between the integral and the fractional parts in prices. Possible values: dot or comma, For example "." for $59.99 or "," for "34,50руб".
weightTruncateZeroFractional |	boolean |	If "true", remove trailing zeros after decimal point.
dateFormat |	string |	Date format, e.g. "dd-MM-yyyy". See [Date and time patterns](http://google.com) for the meaning of the special characters.
timeFormat |	string |	Time format, e.g. "HH:mm:ss". See [Date and time patterns](http://google.com) for the meaning of the special characters.
**System Settings → General → Languages** |
enabledLanguages |	 Array\<string\> |	Languages, enabled in General → Languages. The first language in list is the default one.
**System Settings → General → Cart** |
hideOutOfStockProducts |	boolean |	Hide out of stock products.
showBuyNow |	boolean |	Show "Buy now" buttons on products list pages.
defaultProductSortOrder |	string |	Default Products Sort Order. One of the following:
 | `normal` 	|
 | `addedTimeDesc` | Date added
 | `priceAsc`	| Price: low to high
 | `priceDesc` | Price: high to low
 | `nameAsc` |	Name: A to Z
 | `nameDesc` |	Name: Z to A
minSubtotal	| number *nullable* |	Minimum subtotal allowed before a customer can checkout. Absent if not limited.
maxSubtotal	| number *nullable*	| Maximum subtotal allowed before a customer can checkout. Absent if not limited.
skipPaymentMethodSelectionWhenZeroTotal |	boolean |	Skip payment method selection, if order total is zero.
orderStatusWhenZeroTotal |	string *nullable* |	Set order status to this value when `orderStatusWhenZeroTotal==true`. One of `ACCEPTED`, `QUEUED`.
forceRegistrationOnCheckout |	boolean |	General → Cart → "Require customers to create accounts on checkout" setting.
requirePhoneOnCheckout |	boolean |	General → Cart → "Require phone number on checkout" setting.
askOptionsOnAddition |	boolean |	True to ask the customer to select product options when adding products to the cart from a product list. False to use default option values.
openBagOnAddition |	boolean |	General → Cart → 'Open bag when "Add to bag" is clicked' setting.
askCompanyName |	boolean |	General → Cart → "Ask for the company name" setting.
affiliateCodeEnabled |	boolean |	Tracking code on "Thank you for your order" page is enabled.
affiliateCode |	string *nullable* |	When `affiliateCodeEnabled==true`, this is a tracking code on "Thank you for your order" page.
billingAddressDuringCheckoutEnabled |	boolean |	Ask for a billing address during checkout.
showCompareToOnProductList |	boolean |	Display “Compare to” price on product list.
compareToPriceName |	string |	"Compare to" price name.
compareToPriceSaveUnit |	string |	Value of the "Show “Save” in" setting. One of `PERCENT`, `CURRENCY`, `NOTSHOW`
enableOrderNoted |	boolean |	True if order notes field is enabled.
orderNotedCaption |	string |	Order notes field caption.
requireTermsOnCheckout |	boolean |	True if the “Terms and Conditions” checkbox is enabled.
termsOnSeparateUrl |	boolean |	If `requireTermsOnCheckout==true`, this flag is true if you want to show an external URL as your terms.
externalTermsUrl |	string *nullable* |	If both requireTermsOnCheckout and termsOnSeparateUrl are true, this is the URL of your terms.
checkoutTerms |	string *nullable* |	If `requireTermsOnCheckout==true` and `termsOnSeparateUrl==false`, this is the terms text shown in a popup.
orderNumberSettings |	[OrderNumberSettings](http://google.com) |	Order number generation config, as in System Settings → General → Cart. *Requires authentication*
enableRelatedProductsOnCart |	boolean |	True if Related products are enabled on cart page.
**System Settings → General → E-goods** |
downloadConfig |	[DownloadConfig](http://google.com) |	E-goods download config, as in System Settings → General → E-goods. *Requires authentication*
**System Settings → General → Migrations** |
adaptiveDesignMigration |	boolean |	The 'Adaptive design for Product browser' flag.
newContinueButtonMigration |	boolean |	The 'New "Continue" buttons on the checkout pages' flag.
**System Settings → Zones** |
zones |	Array \<[Zone](http://google.com)\> |	Geographical zones settings. *Requires authentication*
**System Settings → Shipping** |
shippingSettings |	[ShippingSettings](http://google.com) |	Shipping settings.
carrierOnlineSettings |	[CarrierOnlineSettings](http://google.com) |	Configuration of online shipping rate services. *Requires authentication*
storeSameAsOffice |	boolean |	True, if the officeLocation is used as the 'from' address for shipping.
storeLocation |	[Address](http://google.com) *nullable* |	A separate address used to deliver items from. If `storeSameAsOffice == true`, the office address is used instead to calculate shipping cost.
**System Settings → Taxes** |
showTaxes |	boolean |	Taxes → "Show included taxes on product details page" setting.
taxes |	 Array\<[Tax](http://google.com)\> |	Taxes configuration.
**System Settings → Payment** |
paymentMethods | Array\<[PaymentMethod](http://google.com)\>	| Payment → Payment Methods configuration. Note that payment processor configuration is stored separately in the `paymentModulesConfiguration` field. *Requires authentication*
paymentModulesConfiguration |	[PaymentModulesConfiguration](http://google.com) |	Configuration of payment modules, including Google Wallet and PayPal Express Checkout.
**System Settings → Design** |
themeSettings |	[ThemeSettings](http://google.com) |	Storefront CSS theme settings as in System Settings → Design → Design Settings. *Requires authentication*
productThumbnailSize	| number |	Width and height of the box product thumbnails should fit in. Default in 160 pixels.
categoryThumbnailSize |	number |	Width and height of the box category thumbnails should fit in. Default in 160 pixels.
**System Settings → Mail** |
fromEmail |	string *nullable* |	System Settings → Mail → Customer notifications → "From" email address. *Requires authentication*
useCompanyEmail |	boolean |	True, if "same as company" is checked.
fromAdminEmail |	string *nullable* |	System Settings → Mail → Admin notifications → Send notifications to email. *Requires authentication*
useCompanyAdminEmail |	boolean |	True, if "same as company" is checked. *Requires authentication*
mailNotifications | Array\<[MailNotification](http://google.com)\>	| Notification email templates. *Requires authentication*
**System Settings → Social Tools → Share buttons** |
fbLikeButtonConfig	| [FBLikeButtonConfig](http://google.com) |	Facebook Like Button settings.
tumblrButtonConfig |	[TumblrButtonConfig](http://google.com)	| Tumblr configuration.
twitterButtonConfig |	[TwitterButtonConfig](http://google.com)	| Twitter configuration.
pinterestButtonConfig |	[PinterestButtonConfig](http://google.com)	| Pinterest configuration.
googleButtonConfig |	[GoogleButtonConfig](http://google.com) |	Google Plus configuration.
vkButtonConfig |	[VKButtonConfig](http://google.com) |	VKontakte button configuration.
**System Settings → Social Tools → FB Comments** |
fbCommentConfig |	[FBCommentConfig](http://google.com) |	Facebook comments settings.
**System Settings → Social Tools → Share Purchase** |
sharePurchaseConfig	| [SharePurchaseConfig](http://google.com) |	Share Purchase settings.
**System Settings → Social Tools → Ask Friends** |
enableAskForAdvice |	boolean |	Ask a customer to advise product.
**Promotions → Discounts** |
discounts | Array\<[Discount](http://google.com)\> |	Discounts Based on Subtotal. *Requires authentication*
billMeLaterConfig |	[BillMeLaterConfig](http://google.com) *nullable* |	Settings on the Promotion → Bill Me Later tab. Null if the Bill Me Later banner is disabled.
**Deprecated fields** |
groupSeparator |	string |	Deprecated as of API v2. Use currencyGroupSeparator or weightGroupSeparator instead.
decimalSeparator |	string |	Deprecated as of API v2. Use currencyDecimalSeparator or weightDecimalSeparator instead.
\* *All fields are optional. Missing fields do not affect existing field values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Address

**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
street |	string *nullable* |	A newline-separated street address. Up to two lines allowed.
city	| string *nullable* |	City name.
countryCode	| string *nullable*	| A two-letter ISO code of the country.
postalCode	| string *nullable* |	Postal code or ZIP code.
stateOrProvinceCode	| string *nullable* |	State code (e.g. `NY`). See list of supported state codes.
phone |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### OrderNumberSettings
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
nextNumber |	number	| Use this number as the next order number, if it is less then any existing order number.
numberLength |	number |	Pad order number to this length with zeroes `0`. `0` means no padding.
numberPrefix |	string	| Prefix every new order number with the given prefix.
numberSuffix |	string	| Add the given suffix to every generated order number.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### DownloadConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
timeToLiveHours |	number |	Number of hours the download link is valid. Zero means unlimited.
maxDownloads	| number	| Maximum number of downloads by customer. Zero means unlimited.
\* *All fields are optional. Missing fields do not affect existing field values*

#### Zone
**Field**	| **Type**	| **Description**
-------------- | -------------- | --------------
id* |	string |	Unique zone ID.
name* |	string |	Zone display name.
countryCodes	| Array\<string\> |	Country codes this zone contains.
stateOrProvinceCodes |	Array\<string\>	| State or province codes the zone contains.
postCodes | Array\<string\> |	Postcode (or zipcode) templates this zone contains.
\* *Fields marked with *  are mandatory.*

#### ShippingSettings
**Field**	| **Type**	| **Description**
-------------- | -------------- | --------------
entries | Array\<[ShippingMethod](http://google.com)\> |
* *All fields are optional. Missing fields do not affect existing field values*

#### CarrierOnlineSettings
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
AP |	[AustraliaPostConfig](http://google.com) |	The **Australia Post** shipping module configuration.
BC |	[BrasilCorreiosConfig](http://google.com) |	The **Brasil Correios** shipping module configuration.
CP |	[CanadaPostConfig](http://google.com) |	The **Canada Post** shipping module configuration.
DHL |	[DHLConfig](http://google.com) |	The **DHL/Airborne** shipping module configuration.
EMS |	[EMSConfig](http://google.com) |	The **EMS Russian Post** shipping module configuration.
FEDEX |	[FedExConfig](http://google.com) |	The **FedEx** shipping module configuration.
MDS |	[MDSConfig](http://google.com) |	The **MDS Collivery** shipping module configuration.
UPS	| [UPSConfig](http://google.com) |	The **UPS** shipping module configuration.
USPS |	[USPSConfig](http://google.com) |	The **U.S.P.S.** shipping module configuration.
\* *All fields are optional. Missing fields do not affect existing field values*

#### Tax
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id* |	number |	Unique ID of the tax.
name* |	string |	Display name of the tax.
enabled |	boolean |	True if the tax should apply.
includeInPrice |	boolean |	True is the tax should be included in the product price.
useShippingAddress |	boolean |	True to use shipping address for zone matching. False to use billing address. Note that e-goods are always taxed by the billing address.
taxShipping |	boolean |	True if the tax should apply to the shipping cost as well as the ordered items.
appliedByDefault |	boolean |	True if the tax should apply to all products. False enables per-product tax application. See property 'taxes' of the Product model.
rules | Array\<[TaxRule](http://google.com)\>	| Tax amount per geographical zone.
defaultTax |	number |	Tax value, in %, when none of the zones above match.
\* *Fields marked with *  are mandatory.*

#### PaymentMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
name* |	string |	Name of the payment method that is shown to customers, plain text.
instructions |	string |	An optional plain text note that is shown to the right from the payment method name.
enabled |	boolean |	True to show the method to customers.
paymentInstructionsTitle |	string *nullable* |	An optional plain text title of a separate block that is shown when the method is chosen.
paymentInstructions |	string *nullable* |	An optional HTML text shown in a separate block when the method is chosen.
processor |	string *nullable* |	The payment processor selected by the merchant in the payment method table. Null if not selected. One of the following:
 | `sagePayCC` |	Credit Card: SagePay
 | `payJunctionCC` |	Credit Card: PayJunction hosted checkout (QuickShop)
 | `suomenVerkkomaksutCC`	| Credit Card: Paytrail (Finnish Web Payments)
 | `beanStreamCC` |	Credit Card: BeanStream Hosted Payment Form 
 | `twoCheckoutCC` |	Credit Card: 2Checkout 
 | `authorizeNetCC` |	Credit Card: Authorize.Net SIM
 | `epath` |	Credit Card: e-Path
 | `sageEVD` |	Credit Card: Sage Exchange
 | `NMICC` |	Credit Card: Network Merchants
 | `HSBC` |	Credit Card: HSBC Secure ePayments
 | `HSBC_GLOBAL_IRIS` |	Credit Card: Realex Payments/Global Iris
 | `iPay` |	Credit Card: iPay88
 | `eSelectPlusCC` |	Credit Card: eSELECT Plus Hosted Paypage
 | `eWay` |	Credit Card: eWay Hosted Payment Page
 | `globalGatewayE4` |	Credit Card: First Data Global Gateway e4
 | `vcs` |	Credit Card: Virtual Card Services
 | `payFast` |	Credit Card: PayFast
 | `clickandbuy` |	ClickandBuy
 | `bancomer` |	Credit Card: BBVA Bancomer / eGlobal
 | `multiSafepay` |	MultiSafepay
 | `twoCheckoutECheck` |	ECheck: 2Checkout
 | `amex` |	Credit Card: American Express Payment Gateway
 | `authorizeNetECheck` |	ECheck: Authorize.Net SIM
 | `paypalStandard` |	PayPal Website Payments Standard
 | `paypalProHosted` |	PayPal Payments Pro Hosted
 | `paypalPayflowLink` |	Payflow Link
 | `paypalPayflowAdvanced` |	PayPal Payments Advanced
 | `paypalExpressCheckout` |	paypal
 | `iPayment` |	iPayment von 1 & 1
 | `pagSeguro` |	PagSeguro UOL
 | `robokassa`	Robokassa
 | `qiwi` |	QIWI Кошелек
 | `iDEALMollie` |	iDEAL / Mollie
 | `payOnline` |	PayOnline System
 | `offline` |	Offline Basic
 | `offlineCheck` |	Offline Check
 | `offlinePurchaseOrder` |	Purchase order
 | `demoAccept` |	Demo (accept all orders)
 | `demoDecline` |	Demo (decline all orders)
tag |	string *nullable* |	An optional tag which tags 'special' payment methods. One of `robokassa`, `qiwi`, `paypal`.
\* *Fields marked with *  are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as *nullable.*

#### PaymentModulesConfiguration
**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
Authorize.Net	| [AuthorizeNetConfig](http://google.com)  *nullable* |	The **Credit Card: Authorize.Net SIM** payment module configuration.
NetworkMerchants |	[AuthorizeNetEmlConfig](http://google.com)  *nullable* |	The **Credit Card: Network Merchants** payment module configuration.
ESelectPlus |	[ESelectPlusConfig](http://google.com)  *nullable* |	The **Credit Card: eSELECT Plus Hosted Paypage** payment module configuration.
SagePay |	[SagePayConfig](http://google.com) *nullable* |	The **Credit Card: SagePay** payment module configuration.
SageExchangeVirtualDesktop  |	[SageEVDConfig](http://google.com) *nullable* |	The **Credit Card: Sage Exchange** payment module configuration.
BeanStream |	[BeanStreamConfig](http://google.com)  *nullable* |	The **Credit Card: BeanStream Hosted Payment Form** payment module configuration.
eWay |	[EWayConfig](http://google.com) *nullable* |	The **Credit Card: eWay Hosted Payment Page** payment module configuration.
GlobalIris	| [HSBCGlobalIrisConfig](http://google.com) *nullable* |	The **Credit Card: Realex Payments/Global Iris** payment module configuration.
PayJunction |	[PayJunctionConfig](http://google.com) *nullable* |	The **Credit Card: PayJunction hosted checkout (QuickShop)** payment module configuration.
SuomenVerkkomaksut |	[SuomenVerkkomaksutConfig](http://google.com) *nullable* |	The **Credit Card: Paytrail (Finnish Web Payments)** payment module configuration.
IDEALMollie |	[IDEALMollieConfig](http://google.com) *nullable* |	The **iDEAL / Mollie** payment module configuration.
PayOnline |	[PayOnlineConfig](http://google.com) *nullable* |	The **PayOnline System** payment module configuration.
Robokassa |	[RobokassaConfig](http://google.com) *nullable* |	The **Robokassa** payment module configuration.
iPayment |	[IPaymentConfig](http://google.com) *nullable* |	The **iPayment von 1 & 1** payment module configuration.
pagSeguro |	[PagSeguroConfig](http://google.com) *nullable* |	The **PagSeguro UOL** payment module configuration.
Qiwi |	[QiwiConfig](http://google.com) *nullable* |	The **QIWI Кошелек** payment module configuration.
PayPalStandard |	[PayPalStandardConfig](http://google.com) *nullable* |	The **PayPal Website Payments Standard** payment module configuration.
PayPalPayflowLink |	[PayPalPayflowLinkConfig](http://google.com) *nullable* |	The **Payflow Link** payment module configuration.
IPay |	[IPayConfig](http://google.com) *nullable* |	The **Credit Card: iPay88** payment module configuration.
VCS	| [VCSConfig](http://google.com) *nullable* |	The **Credit Card: Virtual Card Services** payment module configuration.
MultiSafepay |	[MultiSafepayConfig](http://google.com) *nullable* |	The **MultiSafepay** payment module configuration.
ClickAndBuy |	[ClickAndBuyConfig](http://google.com) *nullable* |	The **ClickandBuy** payment module configuration.
2Checkout.com |	[TwoCheckoutConfig](http://google.com) *nullable* |	The **Credit Card: 2Checkout** payment module configuration.
e-Path |	[EPathConfig](http://google.com) *nullable* |	The **Credit Card: e-Path** payment module configuration.
Bancomer |	[BancomerConfig](http://google.com) *nullable* |	The **Credit Card: BBVA Bancomer / eGlobal** payment module configuration.
Amex |	[AmexConfig](http://google.com) *nullable* |	The **Credit Card: American Express Payment Gateway** payment module configuration.
PayFast |	[PayFastConfig](http://google.com) *nullable* |	The **Credit Card: PayFast** payment module configuration.
PayPalPro	| [PayPalProConfig](http://google.com) *nullable* |	The **PayPal Payments Pro Hosted** payment module configuration.
GlobalGatewayE4 |	[GlobalGatewayE4Config](http://google.com) *nullable* |	The **Credit Card: First Data Global Gateway e4** payment module configuration.
google |	[GoogleConfig](http://google.com) *nullable* |	The **Google Checkout** payment module configuration.
paypal |	[PayPalConfig](http://google.com) *nullable* |	The **PayPal Checkout** payment module configuration.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### ThemeSettings
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
customThemes | Array\<[CustomTheme](http://google.com)\> |	CSS themes developed by store owner.
activeThemeId |	string |	An identifier of an active theme, either custom or built-in. Build-id themes are "Standard.css", "Red.css", and "Beige.css"
\* *All fields are optional. Missing fields do not affect existing field values.*

#### MailNotification
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
type* |	string |	Notification type. One of the following:
 | `ADMIN_ACTIVATION` |	Welcome to Ecwid!
 | `ADMIN_VALIDATION` |	!MailNotification.admin_validation!
 | `NEW_ORDER_ADMIN` |	New order
 | `ORDER_PAID_ADMIN` |	Order is paid
 | `ORDER_FAILED_ADMIN` |	Order payment failed
 | `STOCK_ADMIN` |	Stock notification
 | `PASSWORD` |	Password reminder
 | `REGISTRATION` |	Successful registration
 | `ORDER_COMPLETED` |	Order is completed
 | `ORDER_REJECTED` |	Order is rejected
 | `EGOODS` |	Egoods download
 | `SHIPPING` |	Order shipped
enabled |	boolean |
subjectTemplate* |	string |	
bodyTemplate* |	string | 
\* *Fields marked with *  are mandatory.*

#### FBLikeButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show	| boolean |	Show Like button.
display |	string |	Like button position. One of `DETAILS`, `LIST_DETAILS`.
sendButton |	boolean |	Show Send button.
colorScheme |	string |	Color Scheme. One of `light`, `dark`
font |	string |	Font used for the button text (e.g. `Arial` or `Lucida`).
\* *All fields are optional. Missing fields do not affect existing field values.*

#### TumblrButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Tumblr button.
display |	string |	Button design type. One of `tumblr_1`, `tumblr_1T`, `tumblr_2`, `tumblr_2T`, `tumblr_4`, `tumblr_4T`.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### TwitterButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Twitter button.
displayCounter |	boolean |	True to show share counter.
viaAccount |	string *nullable* |	Twitter account
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PinterestButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Pinterest button.
displayCounter |	boolean |	True to show share counter.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### GoogleButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show Google Plus button.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### VKButtonConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show VKontakte button.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### FBCommentConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
show |	boolean |	True to show FB comments.
colorScheme |	string |	Color Scheme. One of `light`, `dark`.
posts |	number |	Number of posts
width |	number |	Width, px
appId |	string |	Your FB app id
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### SharePurchaseConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
sharePurchase |	boolean |	Ask a customer to share his purchase.
shareTwitterAccount |	string *nullable* |	Your store's Twitter account
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Discount
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
base* |	string |	Specifies condition when this discount is valid. *One of the following:*
 | `ON_TOTAL` |	Order total should be at least the one specified in the 'orderTotal' field
 | `ON_MEMBERSHIP` |	Customer should be a member of a group with ID membershipId
 | `ON_TOTAL_AND_MEMBERSHIP` |	Both order total and customer's membership conditions apply
orderTotal* |	number |	Minimal order total required for this discount to be applicable.
membershipId |	number |	An ID of the customer group this discount is applicable to.
value* |	number |	Discount value, in % or currency, depending on the 'type' field.
type* |	string |	The type of the 'value' field: % or currency. One of `ABS`, `PERCENT`.
\* *Fields marked with * are mandatory.*

#### BillMeLaterConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
publisherId |	string |	An internal ID retrieved from PayPal used to show the Bill Me Later banner.
showOnHomePage |	boolean |	Show the Bill Me Later banner on the main store page.
showBottomHome |	boolean |	If `showOnHomePage=true`, this flag specifies where on the main store page the banner should be shown. Value `true` means bottom of the page, while `false` means the top.
showOnProductListPage |	boolean |	Show the Bill Me Later banner on the product list page.
showBottomProductList |	boolean |	If `showOnProductListPage=true`, this flag specifies where on the product list page the banner should be shown. Value `true` means bottom of the page, while `false` means the top.
showOnProductDetailsPage |	boolean |	Show the Bill Me Later banner on the product page.
showOnCartPage |	boolean |	Show the Bill Me Later banner on the shopping cart page.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### CustomTheme
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id* |	string |	A unique ID of a theme.
displayName* |	string |	The theme name shown to the user.
css* |	string |	Theme's CSS code.
\* *Fields marked with * are mandatory.*

#### ShippingMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id* |	string |	Unique id of this method.
name* |	string |	Display name of this shipping method.
zone |	string *nullable* |	An optional ID of the zone this method is applicable to. See 'zones' property of the profile. The special value `WORLD` refers to the 'The World' zone.
deliverySpeed |	string *nullable* |	Delivery speed, in days.
orderBy |	number |	Position in the shipping method list.
enabled |	boolean |	True if the shipping method is visible to customers.
type* |	string |	How the shipping rate gets calculated. One of the following:
 | `FLAT` |	Flat shipping rate or free shipping.
 | `TABLE` |	Shipping costs based on the number of items, total weight, or cart price.
 | `CARRIER` |	Receive shipping costs from the major shipping carrier companies (UPS, USPS, FedEx, Canada Post, Australia Post, EMS Russian Post).
rate |	number *nullable* |	Only for `type=FLAT`. Flat shipping rate.
unit |	string *nullable* |	Only for `type=FLAT`. Unit of the flat shipping rate. One of `CURRENCY`, `PERCENT`.
rangesOn |	string *nullable* |	Only for type=TABLE. What the rate rules depend on. One of the following:
 | `subtotal` |	Shipping rate rules depend on order subtotal.
 | `weight` |	Shipping rate rules depend on weight.
columns |	string *nullable* |	Only for type=TABLE. This specifies the rate calculation formula. One of the following:
 | `perOrder` |	Only per-order flat rate is specified for each rule.
 | `full` |	Per order + Per item + Percent charge + Per lbs
entries | Array\<[RateRule](http://google.com)\> |	Only for `type=TABLE`. Set of rules to calculate shipping rate. Each rule is only applicable to some subtotal or weight range (depending on 'rangesOn' property).
carrier |	string *nullable* |	Only for `type=CARRIER`. Sets which carrier to use for this shipping method. One of the following:
 | `AP` |	Australia Post
 | `BC` |	Brasil Correios
 | `CP` |	Canada Post
 | `DHL` |	DHL/Airborne
 | `EMS` |	EMS Russian Post
 | `FEDEX` |	FedEx
 | `MDS` |	MDS Collivery
 | `UPS` |	
 | `USPS` |	U.S.P.S.
methods	| Array\<[string](http://google.com)\> *nullable* |	Only for `type=CARRIER`. A list of shipping method codes that are enabled, ordered in the same way they should appear in customer frontend. These should correspond to the codes listed in CarrierOnlineSettings.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### TaxRule
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
zone* |	string |	Unique zone ID. This should match one of the zones in 'zones' profile field. The special value `WORLD` refers to 'The World' zone.
tax* |	number |	Tax value. in %, for this zone.
\* *Fields marked with * are mandatory.*

#### AustraliaPostConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
packageDimensions |	[Dimensions](http://google.com) |	
useDefaultAccount |	boolean |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### BrasilCorreiosConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountId |	string *nullable* |	
packageDimensions |	[Dimensions](http://google.com) |	
packagingType |	string *nullable* |	One of the following:
 | `BOX` |	Box
 | `ENVELOPE` |	Envelope
password |	string |	
restrictDelivery |	boolean |	
signatureConfirmation |	boolean |	
useDefaultAccount |	boolean |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### CanadaPostConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
customerNumber	| string *nullable* |	
merchantId |	string *nullable* |	
options | Array\<string\> |	One of the following:
 | `SO` |	Signature
 | `COV` |	Coverage
 | `COD` |	
 | `PA18` |	Proof of Age Required - 18
 | `PA19` |	Proof of Age Required - 19
 | `HFP` |	Card for pickup
 | `DNS` |	Do not safe drop
 | `LAD` |	Leave at door - do not card
packageDimensions |	[Dimensions](http://google.com)	|
password |	string *nullable* |	
showOldSettings	| boolean *nullable* |	
useDefaultAccount |	boolean |	
username |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### DHLConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountNumber |	string *nullable*	|
packageDimensions |	[Dimensions](http://google.com) |	
password |	string *nullable* |	
shippingKey |	string *nullable* |	
testEnvironment |	boolean |	
useDefaultAccount |	boolean |	
userID |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *Some fields can have null value or be absent, in which case they are marked as `nullable`.*

#### EMSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
internationalDeliveryType |	string | One of the following:
 | `doc` | Documents (max 2kg)
 | `att` |	Attachments
useDefaultAccount |	boolean |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\>	| Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### FedExConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountNumber |	string *nullable* |	
dropoffType |	string |	One of the following:
 | `REGULARPICKUP`	| Regular Pickup
 | `REQUESTCOURIER` |	Request Courier
 | `DROPBOX` |	Drop Box
 | `BUSINESSSERVICECENTER` |	Business Service Center
 | `STATION` |	Station
meterNumber |	string *nullable* |	
packageDimensions |	[Dimensions](http://google.com)	|
rateRequestType |	string	| One of the following:
 | `LIST` |	Standard list rates
 | `ACCOUNT` |	Discounted rates
shipToResidence |	boolean |	
testAccount	| boolean |	
useDefaultAccount |	boolean |	
webAuthKey |	string *nullable* |	
webAuthPassword |	string *nullable* |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### MDSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
clientID |	string *nullable* |	
defaultAddress |	string *nullable* |	
defaultContact |	string *nullable* |	
email |	string |	
packageType |	string *nullable* |	One of the following:
 | `MDS_ENVELOPE` | Envelope (documents less than 2Kg and A4 size)
 | `MDS_PACKAGE` |	Package (Parcel Exceeding 2Kg and any dimension above 20cm)
 | `MDS_DOCUMENTS` |	Tender Documents (Documents for lodging Tenders)
password |	string *nullable* |	
token |	string *nullable* |	
useDefaultAccount |	boolean |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### UPSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accessLicenseNumber |	string *nullable* |	
accountNumber |	string *nullable* |	
customerClassification |	string |	One of the following:
 | `CC01`	| Rates Associated with Shipper Number
 | `CC03`	| Daily Rates
 | `CC04`	| Retail Rates
 | `CC53`	| Standard List Rates
negotiatedRates |	boolean |	
packageDimensions |	[Dimensions](http://google.com) |	
password |	string *nullable* |	
testEnvironment |	boolean |	
useDefaultAccount |	boolean |	
userId |	string *nullable* |	
methods |	 Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### USPSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
firstClassMailType |	string |	One of `LETTER`, `FLAT`, `PARCEL`.
intlMailType |	string |	One of the following:
 | `PACKAGE` |	Package
 | `POSTCARDS_OR_AEROGRAMMES`	| Postcards or aerogrammes
 | `MATTER_FOR_THE_BLIND` |	Matter for the blind
 | `ENVELOPE`	| Envelope
onlineRates |	boolean |	
packageDimensions |	[Dimensions](http://google.com) |	
size |	string |	One of the following:
 | `REGULAR` |	Regular (neither dimension exceeds 12 inches)
 | `LARGE` |	Large (any dimension exceeds 12 inches)
 | `OVERSIZE` |	Oversize (obsolete, same as large)
useDefaultAccount |	boolean |	
userId |	string *nullable* |	
methods | Array\<[CarrierCalculatedMethod](http://google.com)\> |	Shipping methods.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Dimensions
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
length |	number |	The length of a bundle or package to use when calculating rates, in meters.
width |	number |	The width of a bundle or package to use when calculating rates, in meters.
height |	number |	The height of a bundle or package to use when calculating rates, in meters.
\* *All fields are optional. Missing fields do not affect existing field values.*

#### CarrierCalculatedMethod
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
name* |	string |	The shipping method human-readable name, plain text.
code* |	string |	The shipping method provider-specific unique code.
orderBy |	number |	Position in the resulting list of shipping methods shown to a customer. Default is 0.
\* *Fields marked with * are mandatory.*

#### RateRule
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
from* |	number *nullable* |	Subtotal or weight range start.
to |	number *nullable* |	Subtotal or weight range end. Unlimited if absent.
perOrder |	number *nullable* |	Flat shipping rate.
perWeight |	number *nullable* |	Shipping cost per weight unit. E.g. if the current weight unit is lbs, then this value specifies the cost per lbs.
perItem |	number *nullable* |	Shipping cost per order item.
percent	| number *nullable* |	Shipping cost as a % of order subtotal.
\* *Fields marked with * are mandatory.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### AuthorizeNetConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
MD5Hashvalue |	string *nullable* |	
emailReceipt |	boolean |	
endpointUrl |	string *nullable*	|
loginId |	string v |
testAccount |	boolean |	
testMode |	boolean |	
transKey |	string *nullable* |	
transType |	string |	One of `AUTH_ONLY`, `AUTH_CAPTURE`
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### AuthorizeNetEmlConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
loginId |	string *nullable* |	
testMode |	boolean |	
transKey |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### ESelectPlusConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
hppKey | string *nullable* |
psStoreId |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*
** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### SagePayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
encryptPswd |	string *nullable* |	
simulatorServer |	boolean |	
testMode |	boolean |	
txType |	string |	One of `PAYMENT`, `DEFERRED`, `AUTHENTICATE`
vendor |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### SageEVDConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
transactionType |	string |	One of the following:
 | `Auth` |	Authorization Only
 | `Sale` |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### BeanStreamConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
hashKey |	string *nullable* |	
merchantId |	string *nullable* |	
trnType |	string |	One of `PURCHASE_ONLY`, `PREAUTH_ONLY`
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### EWayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountType |	string *nullable*	| One of `AU`, `NZ`, `UK`
customerId |	string *nullable* |	
pageDescription |	string *nullable* |	
pageFooter |	string *nullable* |	
pageTitle |	string *nullable* |	
upgradedAU |	boolean |	True if the account was upgraded to use the newest EWay AU API.
userName |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### HSBCGlobalIrisConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId |	string |	
sharedSecret |	string *nullable* |	
subAccount |	string |	
transactionSettleType |	string |	One of `MANUAL`, `AUTOMATIC`.
transactionType |	string	| One of `MANUAL`, `AUTOMATIC`.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayJunctionConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
storeId |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### SuomenVerkkomaksutConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantAuthHash |	string *nullable* |	
merchantId |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### IDEALMollieConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
banks |	string *nullable* |	
lastBanksUpdate |	number |	
partnerId |	string *nullable* |	
testMode |	boolean	|
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayOnlineConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantId | string *nullable*	|
privateSecurityKey |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### RobokassaConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
login | string *nullable*	|
password1 |	string *nullable* |	
password2 |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### IPaymentConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
accountId |	string *nullable* |	
applicationId |	string *nullable* |	
applicationPassword |	string *nullable* |	
securityKey |	string *nullable* |	
transactionType |	string |	One of the following:
 | `preauth` |	Delayed Payment Process/pre-authorization (preauth)
 | `auth` |	Instant Booking of a Payment (auth)
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PagSeguroConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
email |	string *nullable* |	
token |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### QiwiConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
login |	string *nullable* |	
password |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayPalStandardConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
businessId |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayPalPayflowLinkConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantLogin |	string *nullable* |	
partner |	string *nullable* |	
password |	string *nullable*	|
testMode |	boolean |	
transactionType |	string |	One of the following:
 | `AUTH` |	Authorization
 | `SALE` |	Sale
user |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### IPayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantCode |	string *nullable* |	
merchantKey |	string *nullable*	|
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### VCSConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantPAM |	string *nullable* |	
secretWord	| string *nullable* |	
terminalId |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### MultiSafepayConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
account |	string *nullable* |	
siteID |	string *nullable* |	
siteSecureCode |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### ClickAndBuyConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantID |	string *nullable* |	
mmsSharedSecret |	string *nullable* |	
projectID |	string *nullable* |	
secretKey |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### TwoCheckoutConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
convertToUSD |	boolean |	
demo |	boolean |	
secretWord |	string *nullable* |	
sid |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### EPathConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
frequency |	string |	
url |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### BancomerConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
merchantCode |	string *nullable* |	
secretCode |	string *nullable* |	
terminal |	string |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### AmexConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
apiPassword |	string *nullable* |	
merchantId |	string *nullable*	|
transactionType |	string |	One of the following:
 | `AUTH` |	Authorize and Capture
 | `PAY` |	Purchase
configured |	boolean |	True if the required fields are filled properly and the payment module can be used. It is allowed to fill the object only partially and save.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayFastConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
emailConfirmation |	boolean |	
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
pdtKey |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayPalProConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
businessId |	string *nullable* |	
testMode |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### GlobalGatewayE4Config
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
paymentPageId |	string |	
responseKey |	string |	
testMode |	boolean |	
transactionKey |	string |	
transactionType |	string |	One of `AUTH_CAPTURE`, `AUTH_ONLY`
\* *All fields are optional. Missing fields do not affect existing field values.*

#### GoogleConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
allowAVSCodes |	string |	
allowCVNCodes |	string |	
merchantId |	string *nullable* |	
merchantKey |	string *nullable* |	
sandbox |	boolean |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### PayPalConfig
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
apiPassword |	string *nullable* |	
apiUsername |	string *nullable* |	
billMeLaterButton |	boolean |	
paymentAction |	string |	One of the following:
 | `ORDER` | Order
 | `AUTH` |	Authorization
 | `SALE` |	Sale
sandbox |	boolean |	
signature |	string *nullable*	|
subject |	string *nullable* |	
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |		| Store ID not found.


# Product

## Get a product

### URL

`GET /storeId/products/[productId]?token=string`

### URL Parameters

**Name** |	**Type**	| **Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
productId | number |	Идентификатор запрашиваемого продукта.
token* |	string |	Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'Product' with the following fields:

#### Product
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	number |	A unique integer product ID.
sku |	string |	Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
thumbnailUrl |	string *nullable* |	An URL of the product thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
quantity |	number *nullable* |	Amount of the product in stock as an integer value. Absent for unlimited products.
inStock |	boolean |	True if any of the product combinations or the product itself has positive quantity or is unlimited.
name |	string |	Product name as a plain text.
price |	number |	Basic product price.
listPrice |	number |	The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs.
compareToPrice |	number *nullable* |	'Compare To' price shown strike-out in the customer frontend.
weight |	number |	Product weight, in the store units. Absent for intangible products.
url |	string |	URL of the product's description web page.
created	| string |	Product creation date/time.
lastUpdateTime |	string *nullable* |	Product last update date/time. Can be null for products that were created before this.
productClassId |	number |	Id of a product class this product belongs to (like 'Books'). Zero '0' value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled |	boolean |	'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> |	A list of the product options. Empty if no options are specified for the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly |	boolean |	True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate |	number |	For `fixedShippingRateOnly=true`, this value is used instead of the shipping. For `fixedShippingRateOnly=false`, this value adds to the shipping cost.
defaultCombinationId |	number |	Id of a combination corresponding to the default product option values. E.g. if the default t-shirt color is 'white', and there is a separate combination for the white t-shirts, that combination is returned.
imageUrl |	string *nullable* |	An URL of a product image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. This is either an URL of an image uploaded to the /api/v2/STORE-ID/images or an URL of an external resource.
smallThumbnailUrl |	string *nullable* |	An URL of the product thumbnail fitted in the 80x80 box.
originalImageUrl |	string *nullable* |	An URL of an original product image that was uploaded for this product.
description	| string *nullable* |	Product description in HTML.
galleryImages | Array\<[GalleryImage](http://google.com)\> |	A list of gallery images.
categoryIds | Array\<number\> |	A list of categories which this product belongs to.
defaultCategoryId |	number *nullable* |	Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> |	If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor.
files | Array\<[ProductFile](http://google.com)\> |	E-goods attached to the product. This field is only available for authorized requests.
relatedProducts |	[RelatedProducts](http://google.com) *nullable* |	The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
combinations | Array\<[Combination](http://google.com)\> |	This can only be used when product retrieval. This field is absent on saving a product.
* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### WholesalePrice
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
quantity |	number |	Number of items for which the special price is eligible.
price |	number |	Special price for the product when ordered more the 'quantity' items.

#### ProductOption
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
type |	string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
name |	string |	Option name, like 'Color', as a plain text.
choices | Array\<[ProductOptionChoice](http://google.com)\> |	All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty
defaultChoice |	number *nullable* |	The number, starting from `0`, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required |	boolean |	"true" if this option is required, "false" otherwise. Default is false
* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
alt |	string |	The image description, displayed in 'alt' image attribute, as a plain text.
url |	string |	The image url.
thumbnail |	string *nullable* | An URL of the image thumbnail fit into the 46x42 box.
width |	number |	Width of the image.
height |	number |	Height of the image.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	number |	Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
name |	string |	The attribute's printable name
value |	string *nullable* |	The attribute value. Set to null in product update request to remove the attribute.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	number |	Unique integer file ID.
name |	string |	A plain-text file name.
description |	string |	A plain-text file description.
size |	number |	File size, in bytes, as a 64-bit integer.

#### RelatedProducts
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
productIds | Array\<number\> *nullable*	| IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory	| [RelatedCategory](http://google.com) *nullable* |	Specifies the random number of related products from a given category.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Combination
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
id |	number |	A unique integer combination ID.
combinationNumber |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> |	Set of options which identifies this combination. An array of {name:, value:} objects.
sku |	string *nullable* |	If present, combination SKU, unique code. If null, product sku is assumed.
smallThumbnailUrl |	string *nullable* |	An URL of the product combination thumbnail fitted in the 80x80 box. If null, product thumbnail is assumed.
thumbnailUrl |	string *nullable* |	An URL of the product combination thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. If null, product thumbnail is assumed.
imageUrl |	string *nullable* |	An URL of a combination image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. If null, product image is assumed.
originalImageUrl |	string *nullable* |	An URL of a non-resized combination image that was uploaded for this combination. If null, product image is assumed.
quantity |	number *nullable* |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price |	number *nullable* |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place.
weight |	number *nullable* |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean *nullable* |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
enabled |	boolean |	Флаг включенности выбора связанных товаров из категории
categoryId |	number |	Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |	number |	Number of random products from a given category (or from all store, if `categoryId==0`), which should be shown as a related products of a given product.

#### OptionValue
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
name |	string |	Option name, as in Product.options[i].name
value |	string |	Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
text |	string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier |	number |	Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`
priceModifierType |	string |	Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT`. Default is `ABSOLUTE`.

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |	[NotFoundError](#notfounderror) |	Возвращается в случае, когда продукт не найден по заданному идентификатору.
500 |	[InternalError](#internalerror) |	Невозможно получить продукт произошла внутренняя ошибка сервера.


## Add a product

Add a product

### URL

`POST /storeId/products?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Product' with the following fields:

#### Product
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
sku* |	string |	Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
quantity |	number |	Amount of the product in stock as an integer value. Absent for unlimited products.
inStock* |	boolean |	True if any of the product combinations or the product itself has positive quantity or is unlimited.
name* |	string |	Product name as a plain text.
price* |	number |	Basic product price.
listPrice* |	number |	The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. Default is empty.
compareToPrice |	number *nullable* |	'Compare To' price shown strike-out in the customer frontend.
weight* |	number |	Product weight, in the store units. Absent for intangible products.
created* |	string |	Product creation date/time.
lastUpdateTime |	string *nullable* |	Product last update date/time. Can be null for products that were created before this.
productClassId* |	number |	Id of a product class this product belongs to (like 'Books'). Zero `0` value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled* |	boolean |	'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> |	A list of the product options. Empty if no options are specified for the product. Default is empty.
warningLimit |	number |	The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly* |	boolean *nullable* |	True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate* |	number |	For fixedShippingRateOnly=true, this value is used instead of the shipping. For `fixedShippingRateOnly=false`, this value adds to the shipping cost.
description |	string *nullable* |	Product description in HTML.
categoryIds | Array\<number\> |	A list of categories which this product belongs to. Default is empty.
defaultCategoryId |	number  *nullable* |	Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> |	If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor. Default is empty.
relatedProducts |	RelatedProducts |	The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### WholesalePrice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
quantity* |	number |	Number of items for which the special price is eligible.
price* |	number |	Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

#### ProductOption
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
type |	string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`. Default is `SELECT`.
name* |	string |	Option name, like 'Color', as a plain text.
choices | Array\<[ProductOptionChoice](http://google.com)> |	All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty.
defaultChoice |	number *nullable* |	The number, starting from 0, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required* |	boolean |	"true" if this option is required, "false" otherwise. Default is false
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
alt |	string *nullable* |	The image description, displayed in 'alt' image attribute, as a plain text.
url* |	string |	The image url.
thumbnail |	string *nullable* |	An URL of the image thumbnail fit into the 46x42 box.
width* |	number |	Width of the image.
height* |	number |	Height of the image.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id |	number |	Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
value |	string *nullable* |	The attribute value. Set to null in product update request to remove the attribute.
Fields marked with  are mandatory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id* |	number |	Unique integer file ID.
name* |	string |	A plain-text file name.
description* |	string |	A plain-text file description.
size* |	number |	File size, in bytes, as a 64-bit integer.
\* *Fields marked with * are mandatory.*

#### RelatedProducts
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
productIds | Array\<number\> *nullable* |	IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory |	[RelatedCategory](http://google.com) *nullable* |	Specifies the random number of related products from a given category.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Combination
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
combinationNumber* |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<OptionValue\> |	Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku |	string *nullable* |	If present, combination SKU, unique code. If null, product sku is assumed.
quantity |	number *nullable*  |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price |	number *nullable* |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |	number *nullable* |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean *nullable* |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |	number |	Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
enabled |	boolean |	Флаг включенности выбора связанных товаров из категории
categoryId |	number |	Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |	number |	Number of random products from a given category (or from all store, if categoryId==0), which should be shown as a related products of a given product.
\* *Fields marked with * are mandatory.*

#### OptionValue
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string |	Option name, as in Product.options[i].name
value |	string |	Option value one of Product.options[i].choices[j].text
\* *Fields marked with * are mandatory.*

#### ProductOptionChoice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
text* |	string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* | number |	Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`
priceModifierType* | string |	Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT`. Default is `ABSOLUTE`.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошло создание сущности
success |	boolean | Успешно ли прошло создание

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
409 |	[NonUniqueError](#nonuniquerror) |	Продукт с таким sku уже существует
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана
404	| [NotFoundError](#notfounderror) |	Сущность, на которую есть ссылка в продукте, не существует(например на продуктовый класс)


## Update a product

Update a product

### URL

`PUT /[storeId]/products/[productId]?token=string`

### URL Parameters

**Name** |	**Type** | **Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
productId* |	number |	Идентификатор изменяемого продукта
token* |	string |	Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Product' with the following fields:

#### Product
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
sku |	string |	Product SKU, that is, a unique code of the inventory item. Items with different options can have different SKUs, which are specified in the embedded Combination objects.
quantity |	number *nullable* |	Amount of the product in stock as an integer value. Absent for unlimited products.
inStock |	boolean |	True if any of the product combinations or the product itself has positive quantity or is unlimited.
name |	string |	Product name as a plain text.
price |	number |	Basic product price.
listPrice |	number |	The price shown in the product list, which may be different from the basic price if the default product combination overrides the basic price.
wholesalePrices | Array\<[WholesalePrice](http://google.com)/> |	The sorted array of (quantity limit, price) pairs.
compareToPrice |	number *nullable* |	'Compare To' price shown strike-out in the customer frontend.
weight |	number |	Product weight, in the store units. Absent for intangible products.
created |	string |	Product creation date/time.
lastUpdateTime |	string *nullable* |	Product last update date/time. Can be null for products that were created before this.
productClassId |	number |	Id of a product class this product belongs to (like 'Books'). Zero '0' value means 'General' class, which is the default for new products. Product classes have additional attributes you can see on the 'Attributes' tab in the product editor.
enabled |	boolean |	'true' if product is enabled, 'false' otherwise. Disabled products do not show in the customer frontend.
options | Array\<[ProductOption](http://google.com)\> |	A list of the product options. Empty if no options are specified for the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field.
fixedShippingRateOnly |	boolean |	True if the shipping is calculated as 'Fixed rate per item' (see Tax and Shipping / Shipping freight in the product editor). With this option on, global shipping settings do not affect the shipping rate of the item. The fixedShippingRate field is than specifies the shipping cost.
fixedShippingRate |	number |	For fixedShippingRateOnly=true, this value is used instead of the shipping. For fixedShippingRateOnly=false, this value adds to the shipping cost.
description |	string |	Product description in HTML.
categoryIds | Array\<number\> |	A list of categories which this product belongs to.
defaultCategoryId |	number *nullable* |	Id of a category marked by a store owner as 'default' for this product. Default category shows up in a product page when no category id is given in the URL.
attributes | Array\<[AttributeValue](http://google.com)\> |	If present, contains product's attributes values (see the description of object Attribute below). You can edit the attribute values on the 'Attributes' tab in the product editor.
relatedProducts |	[RelatedProducts](http://google.com) *nullable* |	The configuration of related products, as shown in the 'Related Products' tab of the Product Editor.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.**

#### WholesalePrice
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
quantity* |	number |	Number of items for which the special price is eligible.
price* |	number |	Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

#### ProductOption
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
type |	string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`. Default is `SELECT`.
name* |	string |	Option name, like 'Color', as a plain text.
choices	| Array\<[ProductOptionChoice](http://google.com)\> |	All possible option choices, if the type is `SELECT`, `CHECKBOX` or `RADIO`. Absent otherwise. Default is empty.
defaultChoice |	number *nullable* |	The number, starting from `0`, of the default choice. Only present if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required* |	boolean |	"true" if this option is required, "false" otherwise. Default is false
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### GalleryImage
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
alt | string *nullable* |	The image description, displayed in 'alt' image attribute, as a plain text.
url* |	string |	The image url.
thumbnail |	string *nullable* |	An URL of the image thumbnail fit into the 46x42 box.
width* |	number |	Width of the image.
height* |	number |	Height of the image.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### AttributeValue
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
id* |	number |	Unique attribute ID, as found in the /api/v3/[STORE-ID]/classes/[ID].
value |	string *nullable*  |	The attribute value. Set to null in product update request to remove the attribute.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### ProductFile
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
id* |	number |	Unique integer file ID.
name* |	string |	A plain-text file name.
description* |	string |	A plain-text file description.
size* |	number |	File size, in bytes, as a 64-bit integer.
\* *Fields marked with * are mandatory.*

#### RelatedProducts
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
productIds	| Array\<number\> *nullable* |	IDs of the related products. May contain ids of removed products, in which case the removed ids should be disregarded.
relatedCategory |	[RelatedCategory](http://google.com) *nullable* |	Specifies the random number of related products from a given category.
\* *All fields are optional. Missing fields do not affect existing field values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Combination
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
combinationNumber* |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> |	Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty.
sku |	string *nullable* |	If present, combination SKU, unique code. If null, product sku is assumed.
quantity |	number *nullable* |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited* |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price |	number *nullable* |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty.
weight |	number *nullable* |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean *nullable* |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |	number *nullable* |	Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### RelatedCategory
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
enabled |	boolean |	Флаг включенности выбора связанных товаров из категории
categoryId |	number |	Id of a category whose products you wish to add as related products. Zero value means "any category", that is, just random products.
productCount |	number |	Number of random products from a given category (or from all store, if `categoryId==0`), which should be shown as a related products of a given product.
\* *All fields are optional. Missing fields do not affect existing field values*

#### OptionValue
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
name* |	string |	Option name, as in Product.options[i].name
value* |	string |	Option value one of Product.options[i].choices[j].text
\* *Fields marked with * are mandatory.*

#### ProductOptionChoice
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
text* |	string | A text displayed as a choice in a drop-down or a radio box, e.g. 'Green'.
priceModifier* |	number |	Number of percents or currency units to add to the product price when this choice is selected. May be negative or zero. Default is `0`.
priceModifierType* |	string |	Specifies the way the product price is modified. One of `PERCENT` or `ABSOLUTE`. If `PERCENT`, then priceModifier is a number of percents to add to the price. If `ABSOLUTE`, then priceModifier is a number of currency units to add to the price. One of `ABSOLUTE`, `PERCENT` Default is `ABSOLUTE`.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** |	**Type** | **Description**
-------------- | -------------- | --------------
message	 | string | Детальное сообщение о том, как прошел апдейт
updateCount |	number | Количество обновленных сущностей
success |	boolean | Успешно ли прошел апдейт

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
409 |	[NonUniqueError](#nonuniqueerror) |	Продукт с таким sku уже существует
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана
404 |	[NotFoundError](#notfounderror) |	Сущность, на которую есть ссылка в продукте, не существует (например на продуктовый класс)


## Delete a product

Delete a product

### URL

`DELETE /[storeId]/products/[productId]?token=string`

### URL Parameters

**Name** |	**Type** | **Description**
-------------- | -------------- | --------------
storeId*	| number |	ID of the Ecwid store.
productId* |	number |	Идентификатор удаляемого продукта
token* |	string |	Oauth токен для доступа к данной функциональности
* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

# Categories

## Get categories

Returns an array of immediate subcategories of a given parent category. If the parent parameter is absent, returns all categories. If parent=0, returns a list of root categories. Disabled categories are not returned, but enabled subcategories of disabled categories are.

### URL

`GET /[storeId]/categories?token=string&parent=number&hidden_categories=boolean&productIds=boolean`

### URL Parameters

**Name** | **Type** | **Description**
-------------- | -------------- | --------------
storeId* | number | ID of the Ecwid store.
token* | string | Oauth токен для доступа к данной функциональности.
parent | number | Идентификатор категории-родителя, чьих детей надо получить
hidden_categories | boolean | Флаг указывающий на то, нужно ли возвращать в выдаче кроме разрешенных категорий еще и запрещенные.
productIds | boolean | Показывать ли для категорий список идентификаторов продуктов, принадлежащих им. Default is false.
\* *Parameters marked with * are mandatory.*

### Response

A JSON array of objects of type 'Category' with the following fields:

#### Category

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id | number | A unique integer category ID.
parentId | number *nullable* | An ID of the parent category, if any. This key is absent for root categories.
orderBy | number | Position of this category in the parent category. OrderBys may not be sequential. Categories are returned in ascending order.
thumbnailUrl | string *nullable* | An URL of the category thumbnail. The thumbnail size is specified in the store profile. This is either an URL of an image uploaded to the `/api/v2/STORE-ID/images` or an URL of an external resource.
originalImageUrl | string *nullable* | An URL of the non-resized category image originally uploaded as a thumbnail. This is either an URL of an image uploaded to the `/api/v2/STORE-ID/images` or an URL of an external resource.
name | string | Category name, plain text.
url | string | URL of the category.
productCount | number | Number of products in the category and its subcategories.
description | string *nullable* | The category description in HTML. Null in category list request (/categories). Can also be null if no description is set for the category.
enabled | boolean | "true" if the category is enabled, "false" otherwise. Enabled categories show in a category list in storefront.
productIds | Array\<number\> *nullable* | Products that should be included in the category. This field can be null, if category products should not be returned or changed.
\* *Some fields can have null value or be absent, in which case they are marked as nullable*.


## Get a category

Returns a single category with the given id. Disabled categories are not returned, unless queried with authentication.

### URL

`GET /[storeId]/categories/[id]?token=string&productIds=boolean`

### URL Parameters

**Name** | **Type** | **Description**
-------------- | -------------- | --------------
storeId* | number | ID of the Ecwid store.
id* | number | Уникальный идентификатор категории.
token* |	string |	Oauth токен для доступа к данной функциональности
productIds | boolean | Показывать ли в результате список идентификаторов продуктов, принадлежащих данной категории.
\* *Parameters marked with * are mandatory*.

### Response

A JSON object of type 'Category' with the following fields:

#### Category

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id | number | A unique integer category ID.
parentId | number *nullable* | An ID of the parent category, if any. This key is absent for root categories.
orderBy | number | Position of this category in the parent category. OrderBys may not be sequential. Categories are returned in ascending order.
thumbnailUrl | string *nullable* | An URL of the category thumbnail. The thumbnail size is specified in the store profile. This is either an URL of an image uploaded to the `/api/v2/STORE-ID/images` or an URL of an external resource.
originalImageUrl | string *nullable* | An URL of the non-resized category image originally uploaded as a thumbnail. This is either an URL of an image uploaded to the `/api/v2/STORE-ID/images` or an URL of an external resource.
name | string | Category name, plain text.
url | string | URL of the category.
productCount | number | Number of products in the category and its subcategories.
description | string *nullable* | The category description in HTML. Null in category list request (/categories). Can also be null if no description is set for the category.
enabled | boolean | "true" if the category is enabled, "false" otherwise. Enabled categories show in a category list in storefront.
productIds | Array\<number\> *nullable* | Products that should be included in the category. This field can be null, if category products should not be returned or changed.
\* *Some fields can have null value or be absent, in which case they are marked as nullable*.

### Errors

HTTP Status | Response JSON	| Description
-------------- | -------------- | --------------
404 | [NotFoundError](#notfounderror) | Either Store ID or category ID not found.


## Add new category

Adds a category to a store under the specified subcategory (parentId) or as a root category (when parentId=0).

### URL

`POST /[storeId]/categories?token=string`

### URL Parameters

**Name** | **Type** | **Description**
-------------- | -------------- | --------------
storeId* | number | ID of the Ecwid store.
token*	| string | Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Category' with the following fields:

#### Category

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
parentId |	number *nullable* |	An ID of the parent category, if any. This key is absent for root categories.
orderBy* |	number |	Position of this category in the parent category. OrderBys may not be sequential. Categories are returned in ascending order.
name*	| string	| Category name, plain text.
description |	string *nullable*	| The category description in HTML. Null in category list request (/categories). Can also be null if no description is set for the category.
enabled	| boolean	| "true" if the category is enabled, "false" otherwise. Enabled categories show in a category list in storefront.Default is true
productIds	| Array\<numbеr\> *nullable*	| Products that should be included in the category. This field can be null, if category products should not be returned or changed.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

### Response

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus

**Field**	| **Type** |	**Description**
-------------- | -------------- | --------------
message |	string |	Детальное сообщение о том, как прошло создание сущности.
success	| boolean	| Успешно ли прошло создание.

### Errors

**HTTP Status** |	**Response** | **JSON Description**
-------------- | -------------- | --------------
449 |	[ImportInProgressError](#importinprogresserror) |	Import is in progress, cannot modify the store. Retry later.
402 |	[LimitError](#limiterror) |	Попытка создать больше категорий, чем это задано ограничением текущего плана
409	| [ValidationError](#validationerror) |	Введенные данные не прошли валидацию.
409 |	[RetryError](#retryerror) |	There was a conflict modifying the store. Retry later.


## Change a category

Changes a category identified with id. To reorder categories, change their orderBy. To move a category to another parent category, change its parentId.

### URL

`PUT /[storeId]/categories/[id]?token=string`

### URL Parameters

**Name**	| **Type**	| **Description**
-------------- | -------------- | --------------
storeId*	| number	| ID of the Ecwid store.
id*	| number	| Id of the category to change.
token*	| string	| Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory*.

### Request body

A JSON object of type 'Category' with the following fields:

#### Category

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
parentId |	number *nullable*	| An ID of the parent category, if any. This key is absent for root categories.
orderBy	| number |	Position of this category in the parent category. OrderBys may not be sequential. Categories are returned in ascending order.
thumbnailUrl |	string *nullable*	| An URL of the category thumbnail. The thumbnail size is specified in the store profile. This is either an URL of an image uploaded to the `/api/v2/STORE-ID/images` or an URL of an external resource.
name	| string	| Category name, plain text.
description	| string *nullable*	| The category description in HTML. Null in category list request (/categories). Can also be null if no description is set for the category.
enabled	| boolean	| "true" if the category is enabled, "false" otherwise. Enabled categories show in a category list in storefront.
productIds	| Array\<number\>	*nullable* | Products that should be included in the category. This field can be null, if category products should not be returned or changed.
\* *All fields are optional. Missing fields do not affect existing field values*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** |	**Type**	| **Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошел апдейт.
updateCount |	number | Количество обновленных сущностей.
success |	boolean | Успешно ли прошел апдейт.

### Errors

**HTTP Status**	| **Response JSON** |	**Description**
-------------- | -------------- | --------------
404	| [ImportInProgressError](#importinprogresserror)	| Import is in progress, cannot modify the store. Retry later.
409	| [RetryError](#retryerror)	| There was a conflict modifying the store. Retry later.
449	| [ValidationError](#validationerror)	| Введенные данные не прошли валидацию.


## Delete a category

Deletes a category with the given id and its subcategories. No products are removed.

### URL

`DELETE /[storeId]/categories/[id]?token=string`

### URL Parameters

**Name** |	**Type**	| **Description**
-------------- | -------------- | --------------
storeId*	| number	| ID of the Ecwid store.
id* |	number	| Идентификатор категории, которую нужно удалить.
token* |	string	| Oauth токен для доступа к данной функциональности.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |	[NotFoundError](#notfounderror) |	Удаляемая категория не найдена
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка
449	| [ImportInProgressException](#importinprogressexception) |	Import is in progress, cannot modify the store. Retry later.

# Classes

## Get product classes

List all product classes in a store.

### URL

`GET /[storeId]/classes?token=string`

### URL Parameters

**Name** |	**Type**	| **Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON array of objects of type 'ProductClass' with the following fields:

#### ProductClass
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number |	Unique integer product class ID. Zero `0` for the built-in 'General' class applied to products by default.
name |	string |	The name of the product class. This field is absent for the 'General' product class.
attributes |	Array\<[Attribute](#attribute)\> |	An array of product class attributes, e.g. 'ISBN' for Books.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### attribute
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number |	Unique integer attribute ID.
name |	string |	The name of the attribute, like 'ISBN', as shown in the store front-end. Plain text.
type |	string |	 Attribute type. `CUSTOM` attributes can be added or removed. Other types are built-ins, thus you cannot remove those fields. One of `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show |	string |	Controls the visibility and location of the attribute value on the product page. One of `NOTSHOW`, `DESCR`, `PRICE`.


## Get a product class

Return information about a single product class.

### URL

`GET /[storeId]/classes/[id]?token=string`

### URL Parameters

**Name** |	**Type**	| **Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
id* |	number |	Идентификатор продуктового класса, который нужно получить
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'ProductClass' with the following fields:

#### ProductClass
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number |	Unique integer product class ID. Zero `0` for the built-in 'General' class applied to products by default.
name |	string *nullable* |	The name of the product class. This field is absent for the 'General' product class.
attributes | Array\<[Attribute](http://google.com)\> |	An array of product class attributes, e.g. 'ISBN' for Books.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Attribute
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number |	Unique integer attribute ID.
name |	string |	The name of the attribute, like 'ISBN', as shown in the store front-end. Plain text.
type |	string |	Attribute type. `CUSTOM` attributes can be added or removed. Other types are built-ins, thus you cannot remove those fields. One of `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show |	string |	Controls the visibility and location of the attribute value on the product page. One of `NOTSHOW`, `DESCR`, `PRICE`.

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	[NotFoundError](#notfounderror) |	Продуктовый класс с данным идентификатором не найден


## Delete a product class

Remove a product class (product type) from the store. Does not remove any products. Products of this class move to the default 'General' class.

### URL

`DELETE /[storeId]/classes/id?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
id* |	number |	Идентификатор продуктового класса, который нужно удалить
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	[NotFoundError](#notfounderror) |	Удаляемый продуктовый класс не найден
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка


## Update a product class

Changes an existing product class (product type) to the store. Returns the ProductClass including its attributes object with the 'id' field filled in.

### URL

`PUT /[storeId]/classes/[id]?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
id* |	number |	Идентификатор обновляемого продуктового класса
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'ProductClass' with the following fields:

#### ProductClass
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string *nullable* |	The name of the product class. This field is absent for the 'General' product class.
attributes |	Array\<[Attribute](http://google.com)\> |	An array of product class attributes, e.g. 'ISBN' for Books.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### Attribute
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name* |	string | The name of the attribute, like 'ISBN', as shown in the store front-end. Plain text.
type* |	string | Attribute type. `CUSTOM` attributes can be added or removed. Other types are built-ins, thus you cannot remove those fields. One of `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show |	string |	Controls the visibility and location of the attribute value on the product page. One of `NOTSHOW`, `DESCR`, `PRICE`. Default is `NOTSHOW`.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том, как прошел апдейт
updateCount |	number | Количество обновленных сущностей
success |	boolean | Успешно ли прошел апдейт

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[InternalError](http://google.com) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка

#### InternalError
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
errorMessage |	string *nullable* |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

## Create a product class

Adds new product class (product type) to the store. Returns the ProductClass including its attributes object with the 'id' field filled in.

### URL

`POST /[storeId]/classes?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'ProductClass' with the following fields:

#### ProductClass
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	The name of the product class. This field is absent for the 'General' product class.
attributes | Array\<[Attribute](http://google.com)\> |	An array of product class attributes, e.g. 'ISBN' for Books. Default is empty.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Attribute
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name* |	string |	The name of the attribute, like 'ISBN', as shown in the store front-end. Plain text.
type* |	string |	Attribute type. `CUSTOM` attributes can be added or removed. Other types are built-ins, thus you cannot remove those fields. One of `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show |	string |	Controls the visibility and location of the attribute value on the product page. One of `NOTSHOW`, `DESCR`, `PRICE`. Default is `NOTSHOW`.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том, как прошло создание сущности
success |	boolean | Успешно ли прошло создание

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка

# Combinations

## Delete product combinations

Удаление всех продуктовых комбинаций продукта

### URL

`DELETE /[storeId]/products/[id]/combinations?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, комбинации которого нужно удалить
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

HTTP Status |	Response JSON |	Description
-------------- | -------------- | --------------
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на текущем плане
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан


## Create a product combination

Создание продуктовой комбинации

### URL

`POST /[storeId]/products/[id]/combinations?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, которому мы добавляем комбинацию
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Combination' with the following fields:

#### Combination
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
combinationNumber* |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array\<[OptionValue](http://google.com)\> |	Set of options which identifies this combination. An array of {name:, value:} objects. Default is empty
sku |	string *nullable* |	If present, combination SKU, unique code. If null, product sku is assumed.
quantity |	number *nullable* |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited* |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price |	number *nullable* |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place. Default is empty
weight |	number *nullable* |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean *nullable* |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |	number |	Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OptionValue
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name* |	string |	Option name, as in Product.options[i].name
value* |	string |	Option value one of Product.options[i].choices[j].text
\* *Fields marked with * are mandatory.*

#### WholesalePrice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
quantity* |	number |	Number of items for which the special price is eligible.
price* |	number |	Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошло создание сущности
success |	boolean | Успешно ли прошло создание

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |	[NotFoundError](#notfounderror) |	Продукт, которому создается комбинация не найден
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на текущем плане
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
409 |	[NonUniqueError](#nonuniqueerror) |	Либо комбинация неуникальная либо существуют продукт и комбинация с одинаковым sku и разным стоком


## Delete a product combination

Удаление продуктовой комбинации

### URL

`DELETE /[storeId]/products/[id]/combinations/[combinationId]?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, чью комбинацию нужно удалить
combinationId* |	number |	Идентификатор комбинации, которую нужно удалить
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string |	 Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

HTTP Status |	Response JSON |	Description
-------------- | -------------- | --------------
404 |	[NotFoundError](#notfounderror) |	Удаляемая комбинация не найдена
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на текущем плане


## Get a product combination

Получение продуктовой комбинации по ее айдишнику

### URL

`GET /[storeId]/products/[id]/combinations/[combinationId]?token=string`

### URL Parameters

Name |	Type |	Description
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, комбинацию которого мы хотим получить
combinationId* |	number |	Идентификатор комбинации, которую мы хотим получить
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'Combination' with the following fields:

#### Combination
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id |	number |	A unique integer combination ID.
combinationNumber |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options |	Array\<[OptionValue](http://google.com)\>	| Set of options which identifies this combination. An array of {name:, value:} objects.
sku |	string *nullable* |	If present, combination SKU, unique code. If null, product sku is assumed.
smallThumbnailUrl |	string *nullable* |	An URL of the product combination thumbnail fitted in the 80x80 box. If null, product thumbnail is assumed.
thumbnailUrl |	string *nullable* |	An URL of the product combination thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. If null, product thumbnail is assumed.
imageUrl |	string *nullable* |	An URL of a combination image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. If null, product image is assumed.
originalImageUrl |	string *nullable* |	An URL of a non-resized combination image that was uploaded for this combination. If null, product image is assumed.
quantity |	number *nullable* |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price |	number *nullable* |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place.
weight |	number *nullable* |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean *nullable* |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number *nullable* |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OptionValue

**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string |	Option name, as in Product.options[i].name
value |	string |	Option value one of Product.options[i].choices[j].text

#### WholesalePrice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
quantity |	number |	Number of items for which the special price is eligible.
price |	number |	Special price for the product when ordered more the 'quantity' items.

### Errors

HTTP Status |	Response JSON |	Description
-------------- | -------------- | --------------
404 |	[NotFoundError](#notfounderror) |	Комбинация не найдена
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на данном плане


## Get product combinations

Получение всех комбинаций продукта

### URL

`GET /[storeId]/products/[id]/combinations?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id |	number |	Идентификатор продукта, комбинации которого нужно получить

\* *Parameters marked with * are mandatory.*

### Response

A JSON array of objects of type 'Combination' with the following fields:

#### Combination
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
id |	number |	A unique integer combination ID.
combinationNumber |	number	| A positive integer number, unique to the product, shown in the combinations table in the product editor.
options | Array<[OptionValue](http://google.com)> |	Set of options which identifies this combination. An array of {name:, value:} objects.
sku |	string |	If present, combination SKU, unique code. If null, product sku is assumed.
smallThumbnailUrl |	string |	An URL of the product combination thumbnail fitted in the 80x80 box. If null, product thumbnail is assumed.
thumbnailUrl |	string |	An URL of the product combination thumbnail. The thumbnail size is specified in the store profile and may be different from the category thumbnail size. If null, product thumbnail is assumed.
imageUrl |	string |	An URL of a combination image that must be shown to the user. If the original image is greater then 500x500 pixels, it is resized to make it smaller. The original image is always available under the originalImageUrl field of a Product. If null, product image is assumed.
originalImageUrl |	string |	An URL of a non-resized combination image that was uploaded for this combination. If null, product image is assumed.
quantity |	number |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited |	boolean |	"true", if the combination is unlimited (that is, never runs out).
price | number |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices | Array<[WholesalePrice](http://google.com)> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place.
weight |	number |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OptionValue
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string |	Option name, as in Product.options[i].name
value |	string |	Option value one of Product.options[i].choices[j].text

#### WholesalePrice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
quantity |	number |	Number of items for which the special price is eligible.
price |	number |	Special price for the product when ordered more the 'quantity' items.

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на данном плане


## Update a product combination

Изменение продуктовой комбинации

### URL

`PUT /[storeId]/products/[id]/combinations/[combinationId]?token=string`

### URL Parameters

Name |	Type |	Description
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, комбинация которого изменяется
combinationId* |	number |	Идентификатор комбинации, которая изменяется
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'Combination' with the following fields:

#### Combination
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
combinationNumber |	number |	A positive integer number, unique to the product, shown in the combinations table in the product editor.
options |	Array\<[OptionValue](http://google.com)\>	| Set of options which identifies this combination. An array of {name:, value:} objects.
sku |	string |	If present, combination SKU, unique code. If null, product sku is assumed.
quantity |	number |	Amount of the product with the given combination of option values in stock. Null if the quantity is the same as the 'quantity' field in the product.
unlimited |	boolean	| "true", if the combination is unlimited (that is, never runs out).
price |	number |	Price of the product having the specified option values. If null, basic product price is assumed.
wholesalePrices |	Array\<[WholesalePrice](http://google.com)\> |	The sorted array of (quantity limit, price) pairs. If null, no wholesale prices are assumed and 'price' field takes place.
weight |	number |	Product weight, in the store units. If null, the weight is inherited from the product.
tangible |	boolean |	True if the combination has its own weight that overrides the product's weight. False if the combination is intangible (no shipping required). Null if the weight should be inherited from the product.
warningLimit |	number |	The value of the 'Send me a note when quantity in stock reaches' field. If null, product's limit is used.
inventoryDelta |	number |	Specifies amount by which to increase the combination's inventory in stock (for PUT requests). Negative number decreases inventory.
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### OptionValue
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string |	Option name, as in Product.options[i].name
value |	string |	Option value one of Product.options[i].choices[j].text
\* *Fields marked with * are mandatory.*

#### WholesalePrice
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
quantity |	number |	Number of items for which the special price is eligible.
price |	number |	Special price for the product when ordered more the 'quantity' items.
\* *Fields marked with * are mandatory.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошел апдейт
updateCount |	number | Количество обновленных сущностей
success |	boolean | Успешно ли прошел апдейт

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
402 |	[PaidFeatureError](#paidfeatureerror) |	Данная функциональность не доступна на текущем плане
400 |	[IllegalParameterError](#illegalparametererror) | Некоторые парамеры в запросе заданы неверно

# Discounts

## Get a discount coupon

Get discount coupon by code

### URL

`GET /[storeId]/discount_coupons/[code]?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
code* |	string |	Уникальный код купона
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DiscountCoupon' with the following fields:

#### DiscountCoupon
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string | Название купона
code |	string | Код купона. Должен быть уникальным
discountType |	string | Discount type (ABS, PERCENT, SHIPPING). One of `ABS`, `PERCENT`, `SHIPPING`
status |	string | Type of discount coupon (ACTIVE, PAUSED, EXPIRED, USEDUP). One of `ACTIVE`, `PAUSED`, `EXPIRED`, `USEDUP`.
discount |	number | Размер скидки.
launchDate |	string | Дата запуска купона
expirationDate |	string *nullable* | Дата экспирации купона
totalLimit |	number *nullable* |	
usesLimit |	string | Limit of using coupon (UNLIMITED, ONCEPERCUSTOMER, SINGLE). One of `UNLIMITED`, `ONCEPERCUSTOMER`, `SINGLE`.
repeatCustomerOnly |	boolean |	Флаг показывающий, что купон может применяться только для покупателей ранее делавших покупки.
creationDate |	string |	Дата создания купона
orderCount |	number |	Число применений купона
catalogLimit |	[DiscountCouponCatalogLimit](http://google.com) *nullable* |	Ограничение применения купона по товарам и категориям
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### DiscountCouponCatalogLimit
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
products | Array\<number\> *nullable* |	Список идентификаторов товаров, перечисленных через запятую, к которым может быть применен купон.
categories | Array\<number\> *nullable* |	Список идентификаторов категорий, перечисленных через запятую, к товарам которых может быть применен купон.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
404 |	[NotFoundError](http://google.com) |	Купон не найден
400 |	[IllegalParameterError](http://google.com) |	Некоторые парамеры в запросе заданы неверно


## Get discount coupons

Получение списка купов магазина
## URL

`GET /[storeId]/discount_coupons?[code]=string​&discount_type=string​&availability=string​&token=string`

### URL Parameters

**Name** | **Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
code |	string |	Уникальный код купона
discount_type |	string |	Comma separated list of discount types e.g. discountType=`ABS`,`PERCENT`
availability |	string |	Comma separated list of availability statuses e.g. availability=`ACTIVE`,`EXPIRED`
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON array of objects of type 'DiscountCoupon' with the following fields:

#### DiscountCoupon
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string | Название купона
code |	string | Код купона. Должен быть уникальным
discountType |	string | Discount type(ABS, PERCENT, SHIPPING). One of `ABS`, `PERCENT`, `SHIPPING`
status |	string | Type of discount coupon(ACTIVE, PAUSED, EXPIRED, USEDUP). One of `ACTIVE`, `PAUSED`, `EXPIRED`, `USEDUP`
discount |	number | Размер скидки.
launchDate |	string | Дата запуска купона
expirationDate |	string *nullable* | Дата экспирации купона
totalLimit |	number *nullable* |	
usesLimit |	string | Limit of using coupon(UNLIMITED, ONCEPERCUSTOMER, SINGLE). One of `UNLIMITED`, `ONCEPERCUSTOMER`, `SINGLE`
repeatCustomerOnly |	boolean |	Флаг показывающий, что купон может применяться только для покупателей ранее делавших покупки
creationDate |	string |	Дата создания купона
orderCount |	number |	Число применений купона
catalogLimit |	[DiscountCouponCatalogLimit](http:/google.com) *nullable* |	Ограничение применения купона по товарам и категориям
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### DiscountCouponCatalogLimit
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
products | Array\<number\> *nullable* |	Список идентификаторов товаров, перечисленных через запятую, к которым может быть применен купон
categories | Array\<number\> *nullable* |	Список идентификаторов категорий, перечисленных через запятую, к товарам которых может быть применен купон
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно


## Delete a discount coupon

Удаление купона по его коду
URL

`DELETE /[storeId]/discount_coupons/[code]?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
code* |	string |	Уникальный код купона
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
400	| [IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно


## Update a discount coupon

Изменение купона

### URL

`PUT /[storeId]/discount_coupons/[code]?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
code* |	string |	Уникальный код купона
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'DiscountCoupon' with the following fields:

#### DiscountCoupon
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name |	string | Название купона
code |	string | Код купона. Должен быть уникальным
discountType |	string | Discount type (ABS, PERCENT, SHIPPING). One of `ABS`, `PERCENT`, `SHIPPING`
status |	string | Type of discount coupon(ACTIVE, PAUSED, EXPIRED, USEDUP). One of `ACTIVE`, `PAUSED`, `EXPIRED`, `USEDUP`
discount |	number | Размер скидки.
launchDate |	string | Дата запуска купона
expirationDate |	string *nullable* | Дата экспирации купона
totalLimit |	number *nullable* |	
usesLimit |	string | Limit of using coupon(UNLIMITED, ONCEPERCUSTOMER, SINGLE). One of `UNLIMITED`, `ONCEPERCUSTOMER`, `SINGLE`
repeatCustomerOnly |	boolean |	Флаг показывающий, что купон может применяться только для покупателей ранее делавших покупки
catalogLimit |	[DiscountCouponCatalogLimit](http://google.com) *nullable* |	Ограничение применения купона по товарам и категориям
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

#### DiscountCouponCatalogLimit
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
products | Array\<number\> *nullable* |	Список идентификаторов товаров, перечисленных через запятую, к которым может быть применен купон
categories | Array\<number\> *nullable* |	Список идентификаторов категорий, перечисленных через запятую, к товарам которых может быть применен купон
\* *All fields are optional. Missing fields do not affect existing field values.*

** *Some fields can be explicitly set to null using the {"field":null} syntax, in which case they are marked as nullable.*

### Response

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошел апдейт
updateCount |	number | Количество обновленных сущностей
success |	boolean | Успешно ли прошел апдейт

### Errors

**HTTP Status** |	**Response JSON**	| **Description**
-------------- | -------------- | --------------
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
409	| [InternalError](#internalerror) |	Не удалось провести обновление купона. Внутренняя ошибка сервера


## Create a discount coupon

Создание купона

### URL

`POST /[storeId]/discount_coupons?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
-------------- | -------------- | --------------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
\* *Parameters marked with * are mandatory.*

### Request body

A JSON object of type 'DiscountCoupon' with the following fields:

#### DiscountCoupon
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
name* |	string | Название купона
code* |	string | Код купона. Должен быть уникальным.
discountType |	string | Discount type (ABS, PERCENT, SHIPPING). One of `ABS`, `PERCENT`, `SHIPPING`. Default is `ABS`.
status |	string | Type of discount coupon(ACTIVE, PAUSED, EXPIRED, USEDUP). One of `ACTIVE`, `PAUSED`, `EXPIRED`, `USEDUP`. Default is `ACTIVE`.
discount |	number | Размер скидки. Default is `0`.
launchDate* |	string | Дата запуска купона
expirationDate |	string *nullable* | Дата экспирации купона
totalLimit |	number *nullable*	|
usesLimit |	string | Limit of using coupon(UNLIMITED, ONCEPERCUSTOMER, SINGLE). One of `UNLIMITED`, `ONCEPERCUSTOMER`, `SINGLE`. Default is `UNLIMITED`.
repeatCustomerOnly |	boolean |	Флаг показывающий, что купон может применяться только для покупателей ранее делавших покупки. Default is false.
catalogLimit |	[DiscountCouponCatalogLimit](http://google.com) *nullable* |	Ограничение применения купона по товарам и категориям. 
\* *Fields marked with * are mandatory.*

** *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### DiscountCouponCatalogLimit
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
products |	Array\<number\> *nullable* |	Список идентификаторов товаров, перечисленных через запятую, к которым может быть применен купон
categories | Array\<number\> *nullable* |	Список идентификаторов категорий, перечисленных через запятую, к товарам которых может быть применен купон
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*


### Response

A JSON object of type 'CreateStatus' with the following fields:
#### CreateStatus
**Field** |	**Type** |	**Description**
-------------- | -------------- | --------------
message |	string | Детальное сообщение о том, как прошло создание сущности
success |	boolean | Успешно ли прошло создание

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
-------------- | -------------- | --------------
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
409 |	[NonUniqueError](#nonuniqueerror) |	Купон с таким кодом уже создан

# Images

## Delete category image

Удаление картинки категории

### URL

`DELETE /[storeId]/categories/[id]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор категории, у которой удаляем картинку
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Категория, у которой удаляем картинку, не найдена
403	| [AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан

## Delete a product combination image

Удаление картинки продуктовой комбинации

### URL

`DELETE /[storeId]/products/[id]/combinations/[combinationId]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, у комбинации которого удаляется картинка
combinationId* |	number |	Идентификатор продуктовой комбинации, у которой удаляется картинка
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	[NotFoundError](#notfounderror) |	Продукт или комбинация, у которой удаляем картинку, не найдены
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан

## Delete a product gallery image

Удаление картинки из галереи продукта

### URL

`DELETE /[storeId]/products/[id]/gallery/fileId?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, у которого удаляем картинку из галереи
fileId* |	number |	Идентификатор картинки, удаляемой из галереи продукта
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, у которого из галереи удаляется продукт, не найден
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#iilegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана

## Delete product image

Удаление картинки продукта

### URL

`DELETE /[storeId]/products/[id]/image?token=string`

### URL Parameters

Name |	Type |	Description
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, чью картинку удаляем
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount	| number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

HTTP Status |	Response JSON |	Description
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, у которого из галереи удаляется продукт, не найден
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана

## Clear product egoods

Удаление всех egoods продукта

### URL

`DELETE /[storeId]/products/[id]/files?token=string`

### URL Parameters

Name |	Type |	Description
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, у которого нужно удалить все egoods
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[UploadFileError](#uploadfileerror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, у которого удаляем все egoods, не найден
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана

## Clear product gallery

Удаление всех картинок из галереи продукта

### URL

`DELETE /[storeId]/products/[id]/gallery?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, у которого удаляем все картинки из галереи
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
message |	string | Детальное сообщение о том как прошло удаление
deleteCount |	number | Количество удаленных сущностей
success |	boolean | Успешно ли прошло удаление

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[UploadFileError](#uploadfileerror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, у которого удаляем все картинки из галереи, не найден
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана


## Upload category image

Загрузка картинки категории на сервер

### URL

`POST /[storeId]/categories/[id]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор категории, для которой загружаем картинку
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка
404 |	[NotFoundError](#notfounderror)	| Категория, для которой загружаем картинку, не найдена
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан


## Upload category image

Загрузка картинки категории на сервер

### URL

`POST /[storeId]/categories/[id]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор категории, для которой загружаем картинку
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка
404 |	[NotFoundError](#notfounderror)	| Категория, для которой загружаем картинку, не найдена
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан


## Upload gallery image

Загрузка картинки галереи на сервер

### URL

`POST /[storeId]/products/[id]/gallery?token=string&fileName=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
fileName* |	string |	Имя файла картинки загружаемой в галерею продукта
id* |	number |	Идентификатор продукта, для которого загружаем картинку в галерею
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

HTTP Status | Response JSON |	Description
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, для которого загружается картинка не найден
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана

## Upload a product combination image

Загрузка картинки продуктовой комбинации на сервер

### URL

`POST /[storeId]/products/[id]/combinations/[combinationId]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, для комбинации которого заливается картинка
combinationId* |	number |	Идентификатор комбинации, для которой заливается картинка
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

HTTP Status |	Response JSON |	Description
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
404 |	[NotFoundError](#notfounderror) |	Продукт или комбинация, для которой загружается картинка, не найдены
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка


## Upload product file

Загрузка на сервер egoods продукта

### URL

`POST /[storeId]/products/[id]/files?token=string&fileName=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатора продукта для которого заливаем egood
fileName* |	string |	Название заливаемого egood-файла
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
404 |	[NotFoundError](#notfounderror) |	Продукт, для которого загружается файл не найден
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
403 |	[AuthError](#autherror) |	Для данного токена нет доступа для данной функциональности, либо токен не верен или не передан
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана


## Upload product image

Загрузка на сервер картинки товара

### URL

`POST /[storeId]/products/[id]/image?token=string`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
storeId* |	number |	ID of the Ecwid store.
token* |	string |	Oauth токен для доступа к данной функциональности
id* |	number |	Идентификатор продукта, картинка которого будет загружена
\* *Parameters marked with * are mandatory.*

### Request body

Binary data.

### Response

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
id |	number | Айдишник залитого к нам файла

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
500 |	[FileUploadError](#fileuploaderror) |	Ошибка загрузки файла
500 |	[InternalError](#internalerror) |	Запрос не получилось выполнить, на сервере произошла внутренняя ошибка
404 |	[NotFoundError](#notfounderror) |	Продукт, для которого загружается картинка не найден
413 |	[EntityTooLongError](#entitytoolongerror) |	Загружаемый файл слишком велик
400 |	[IllegalParameterError](#illegalparametererror) |	Некоторые парамеры в запросе заданы неверно
402 |	[PaidFeatureError](#paidfeatureerror) |	Запрошена функциональность не доступная для данного плана
402 |	[LimitError](#limiterror) |	Уперлись в лимит на количество товаров для данного плана


# Orders

## Create orders

### URL

`POST https://app.ecwid.com//api/v<VERSION>/[STOREID]>/order?secure_auth_key=<ORDERAPIKEY>&order=<ORDERNUMBER>`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
STORE-ID* |	number |	ID of the Ecwid store.
secure_auth_key* |	string |	Product API secret key (can be found in the System Settings → API tab) or an OAuth authentication token.
date |	string |	All orders placed this day. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_date |	string |	All orders placed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
to_date |	string |	All orders placed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_update_date |	string |	All orders changed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
to_update_date |	string |	All orders changed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
order |	string |	Order number. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
from_order |	string |	All orders with numbers bigger than or equal to <value>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
to_order |	string |	All orders with numbers smaller than or equal to \<value\>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
customer_id |	string |	Unique numeric customer identifier or null for anonymous orders.
customer_email |	string |	Customer email or null for orders with empty or absent emails.
statuses |	string |	Payment and/or fulfillment comma-separated status names. Payment statuses: `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`, `INCOMPLETE`. Fulfillment statuses: `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
limit |	number |	Number of orders returned in response. The default and maximal value is 200, any greater value is reset to 200.
offset |	number |	How many orders skip from beginning.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'OrderResponse' with the following fields:

#### OrderResponse
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
count |	number |	The number of orders returned in the 'orders' field.
total |	number |	The number of orders satisfying the conditions specified in the request URL.
orders | Array\<[Order](http://google.com)\> |	No more then limit orders starting from the given offset ordered by time descending.
nextUrl |	string *nullable* |	URL of the API request for the next page or null if there if not next page.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Order
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
number |	number |	A unique order number.
vendorNumber |	string |	Admin-defined order numbers with prefix and suffix, e.g. 2011-345-q.
externalTransactionId |	string *nullable* |	Transaction identifier returned by payment system (PayPal for example.
shippingTrackingCode |	string *nullable* |	Shipping tracking code.
created |	date |	The date/time of order placement.
lastChangeDate |	date |	The date/time of the last order change. *
paymentStatus |	string |	Payment status. One of `INCOMPLETE`, `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`.
fulfillmentStatus |	string |	Fulfillment status. One of `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
shippingMethod |	string *nullable* |	Shipping method name.
shippingPerson |	[Person](http://google.com) |	Receiver name and address.
paymentMethod |	string *nullable*|	Payment method name.
billingPerson |	[Person](http://google.com) |	The billing person name and address.
paymentParameters | Map\<string,string\> |	Additional payment parameters entered by customer on checkout.
avsMessage |	string *nullable* |	Address verification status returned by the payment system.
cvvMessage |	string *nullable* |	Credit card verification status returned by the payment system.
customerId |	number *nullable* |	Unique customer identification, when the order is made by a registered user.
customerName |	string *nullable* |	Customer name.
customerEmail |	string *nullable* |	Customer email address.
customerIP |	string *nullable* |	Customer IP address.
customerCountryCodeByIP |	string *nullable* |	Country code determined by customer IP address (if possible).
discountCoupon |	string *nullable* |	Discount coupon code (e.g. 'AX-545DF-DD').
subtotalCost |	number |	Subtotal (products) cost.
discountCost |	number |	Discount cost (monetary sum of all discounts applied to this order).
shippingCost |	number |	Shipping cost.
taxCost |	number |	Tax cost.
totalCost |	number |	Total order cost.
affiliateId |	string *nullable* |	Affiliate ID.
discountType |	string *nullable* |	Type of discount coupon. One of `ABS`, `PERCENT`, `SHIPPING`.
orderComments |	string *nullable* |	Order comments.
items | Array\<[OrderItem](http://google.com)\> |	Order items.
volumeDiscountValue |	number *nullable* |	Discount granted to the customer based on the volume ordered either in percents or in currency, based on the volumeDiscountType field (see below).
volumeDiscountCost |	number |	Discount in currency granted to the customer based on the volume ordered. Same as volumeDiscountValue if volumeDiscountType == `ABS`.
volumeDiscountType |	string *nullable* |	Specifies the type of discount. One of `ABS`, `PERCENT`.
couponDiscountCost |	number |	Discount in currency granted to the customer based on the coupon entered.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Person
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string *nullable* |	Person full nam.
companyName |	string *nullable* |	Company nam.
street |	string *nullable* |	A newline-separated street address. Up to two lines allowed.
city |	string *nullable* |	City name.
countryCode |	string *nullable* |	A two-letter ISO code of the country.
postalCode |	string *nullable* |	Postal code or ZIP code.
stateOrProvinceCode |	string *nullable* |	State code (e.g. 'NY'). See list of supported state codes.
stateName |	string *nullable* |	State/region geographical name.
countryName |	string *nullable* |	Country name.
phone |	string *nullable* |	
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OrderItem
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
sku |	string |	Product SKU.
name |	string	Product name.
quantity |	number |	Count of purchased products.
price |	number |	Product price.
weight |	number *nullable* |	Product weight.
productId |	number *nullable* |	Product internal ID.
categoryId |	number *nullable* |	Default category ID for this product (0, if no default category has been set for the product).
taxes |	 Array\<[OrderItemTax](http://google.com)\> |	Array of taxes, applied to this order item.
options | Array\<[OrderItemOption](http://google.com)\> |	Product options selected by the customer (e.g. color, size).
files | Array\<[OrderItemProductFile](http://google.com)\> |	Files, attached to this order item
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OrderItemTax
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	Tax name.
value |	number |	Tax value in percents. May depends on shipping or billing person.
total |	number | Tax cost for order item. May depends on shipping or billing person and tax settings.

#### OrderItemOption
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	Option name.
type |	string |	Option type. One of `SELECT`, `CHECKBOX`, `TEXT`, `DATE`, `FILE`.
value |	string |	Contain text value for `SELECT`, `DATE` and `TEXT` option types.
value | Array\<[OrderItemOrderFile](http://google.com)\> |	Contain Array\<OrderItemOrderFile\> in case option type is `FILE`.

#### OrderItemProductFile
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	File name.
description |	string |	File description.
url |	string |	URL.
size |	number |	File size in bytes.
maxDownloads |	number |	Max number of allowed downloads.
remainingDownloads |	number |	Remaining number of allowed downloads.
expires |	date |	File link expiration date/time

#### OrderItemOrderFile
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	File name.
size |	number |	File size in bytes.
url |	string |	File URL.

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	| Store ID not found.
400 |	[OrderException](#orderexception) |	Wrong URL parameters. Also this error will appear if you try to use the HTTP endpoint. All requests have to be sent over HTTPS protocol only.
405 |	[OrderException](#orderexception) |	Incorrect HTTP method (GET instead of POST, for example).
403 |	[OrderException](#orderexception) |	Ecwid account type does not allow this kind of requests. Consider upgrading your account.

#### OrderException
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
error |	string |	Error code.
errorMessage |	string |	Error description, in English.

## Retrieve orders

The Order API returns an object OrderResponse containing array of Orders and some additional information. The number of returned orders can not exceed 200. To retrieve more orders you have to send several requests with specified paging parameters (see 'limit' and 'offset' parameters below).
Examples

`https://app.ecwid.com/api/v2/1003/orders?secure_auth_key=XXXXXX&order=4000,4001,4002`
`https://app.ecwid.com/api/v2/1003/orders?secure_auth_key=XXXXXX&from_date=2011-01-01&to_date=2011-02-01`
`https://app.ecwid.com/api/v2/1003/orders?secure_auth_key=XXXXXX&statuses=QUEUED,SHIPPED&offset=200&limit=100`

### URL

`GET https://app.ecwid.com/api/v2/[STORE-ID]/orders?secure_auth_key=string&date=string&from_date=string&to_date=string&from_update_date=string&to_update_date=string&order=string&from_order=string&to_order=string&customer_id=string&customer_email=string&statuses=string&limit=number&offset=number`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
STORE-ID* |	number |	ID of the Ecwid store.
secure_auth_key* |	string |	Product API secret key (can be found in the System Settings → API tab) or an OAuth authentication token.
date |	string |	All orders placed this day. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_date |	string |	All orders placed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
to_date |	string |	All orders placed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_update_date |	string |	All orders changed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
to_update_date |	string |	All orders changed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
order |	string |	Order number. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
from_order |	string |	All orders with numbers bigger than or equal to \<value\>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
to_order |	string |	All orders with numbers smaller than or equal to \<value\>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
customer_id |	string |	Unique numeric customer identifier or null for anonymous orders.
customer_email |	string |	Customer email or null for orders with empty or absent emails.
statuses |	string |	Payment and/or fulfillment comma-separated status names. Payment statuses: `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`, `INCOMPLETE`. Fulfillment statuses: `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
limit |	number |	Number of orders returned in response. The default and maximal value is 200, any greater value is reset to 200.
offset |	number |	How many orders skip from beginning.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'OrderResponse' with the following fields:

#### OrderResponse
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
count |	number |	The number of orders returned in the 'orders' field.
total |	number |	The number of orders satisfying the conditions specified in the request URL.
orders | Array\<[Order](http://google.com)\> |	No more then limit orders starting from the given offset ordered by time descending.
nextUrl |	string *nullable* |	URL of the API request for the next page or null if there if not next page.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Order
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
number |	number |	A unique order number.
vendorNumber |	string |	Admin-defined order numbers with prefix and suffix, e.g. 2011-345-q.
externalTransactionId |	string *nullable* |	Transaction identifier returned by payment system (PayPal for example.
shippingTrackingCode |	string *nullable* |	Shipping tracking code.
created |	date |	The date/time of order placement.
lastChangeDate |	date |	The date/time of the last order change.
paymentStatus |	string |	Payment status. One of `INCOMPLETE`, `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`.
fulfillmentStatus |	string |	Fulfillment status. One of `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
shippingMethod |	string *nullable* |	Shipping method name.
shippingPerson |	[Person](http://google.com) |	Receiver name and address.
paymentMethod |	string *nullable*|	Payment method name.
billingPerson |	[Person](http://google.com) |	The billing person name and address.
paymentParameters | Map\<string,string\> |	Additional payment parameters entered by customer on checkout.
avsMessage |	string *nullable* |	Address verification status returned by the payment system.
cvvMessage |	string *nullable* |	Credit card verification status returned by the payment system.
customerId |	number *nullable* |	Unique customer identification, when the order is made by a registered user.
customerName |	string *nullable* |	Customer name.
customerEmail |	string *nullable* |	Customer email address.
customerIP |	string *nullable* |	Customer IP address.
customerCountryCodeByIP |	string *nullable* |	Country code determined by customer IP address (if possible).
discountCoupon |	string *nullable* |	Discount coupon code (e.g. 'AX-545DF-DD').
subtotalCost |	number |	Subtotal (products) cost.
discountCost |	number |	Discount cost (monetary sum of all discounts applied to this order).
shippingCost |	number |	Shipping cost.
taxCost |	number |	Tax cost.
totalCost |	number |	Total order cost.
affiliateId |	string *nullable* |	Affiliate ID.
discountType |	string *nullable* |	Type of discount coupon. One of `ABS`, `PERCENT`, `SHIPPING`.
orderComments |	string *nullable* |	Order comments.
items | Array\<[OrderItem](http://google.com)\> |	Order items.
volumeDiscountValue |	number *nullable* |	Discount granted to the customer based on the volume ordered either in percents or in currency, based on the volumeDiscountType field (see below).
volumeDiscountCost |	number |	Discount in currency granted to the customer based on the volume ordered. Same as volumeDiscountValue if volumeDiscountType == `ABS`.
volumeDiscountType |	string *nullable* |	Specifies the type of discount. One of `ABS`, `PERCENT`.
couponDiscountCost |	number |	Discount in currency granted to the customer based on the coupon entered.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### Person
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string *nullable* |	Person full nam.
companyName |	string *nullable* |	Company nam.
street |	string *nullable* |	A newline-separated street address. Up to two lines allowed.
city |	string *nullable* |	City name.
countryCode |	string *nullable* |	A two-letter ISO code of the country.
postalCode |	string *nullable* |	Postal code or ZIP code.
stateOrProvinceCode |	string *nullable* |	State code (e.g. 'NY'). See list of supported state codes.
stateName |	string *nullable* |	State/region geographical name.
countryName |	string *nullable* |	Country name.
phone |	string *nullable* |	
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OrderItem
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
sku |	string |	Product SKU.
name |	string	Product name.
quantity |	number |	Count of purchased products.
price |	number |	Product price.
weight |	number *nullable* |	Product weight.
productId |	number *nullable* |	Product internal ID.
categoryId |	number *nullable* |	Default category ID for this product (0, if no default category has been set for the product).
taxes |	 Array\<[OrderItemTax](http://google.com)\> |	Array of taxes, applied to this order item.
options | Array\<[OrderItemOption](http://google.com)\> |	Product options selected by the customer (e.g. color, size).
files | Array\<[OrderItemProductFile](http://google.com)\> |	Files, attached to this order item
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### OrderItemTax
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	Tax name.
value |	number |	Tax value in percents. May depends on shipping or billing person.
total |	number | Tax cost for order item. May depends on shipping or billing person and tax settings.

#### OrderItemOption
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	Option name.
type |	string |	Option type. One of `SELECT`, `CHECKBOX`, `TEXT`, `DATE`, `FILE`.
value |	string |	Contain text value for `SELECT`, `DATE` and `TEXT` option types.
value | Array\<[OrderItemOrderFile](http://google.com)\> |	Contain Array\<OrderItemOrderFile\> in case option type is `FILE`.

#### OrderItemProductFile
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	File name.
description |	string |	File description.
url |	string |	URL.
size |	number |	File size in bytes.
maxDownloads |	number |	Max number of allowed downloads.
remainingDownloads |	number |	Remaining number of allowed downloads.
expires |	date |	File link expiration date/time

#### OrderItemOrderFile
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
name |	string |	File name.
size |	number |	File size in bytes.
url |	string |	File URL.

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	| Store ID not found.
400 |	[OrderException](#orderexception) |	Wrong URL parameters. Also this error will appear if you try to use the HTTP endpoint. All requests have to be sent over HTTPS protocol only.
405 |	[OrderException](#orderexception) |	Incorrect HTTP method (GET instead of POST, for example).
403 |	[OrderException](#orderexception) |	Ecwid account type does not allow this kind of requests. Consider upgrading your account.

#### OrderException
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
error |	string |	Error code.
errorMessage |	string |	Error description, in English.

## Change orders

You can modify payment status, fulfillment status and shipping tracking code via POST request with specified parameters. You define orders which need to be changed, define new state (payment/fulfillment/tracking code) for these orders and send request to Ecwid. We process your request and return information (in JSON format) about changed orders. One request can change many orders at once.
For example, you can change payment status `QUEUED`->`ACCEPTED` for orders placed in last two days. Or you can change fulfillment status `NEW`->`DELIVERED` for all orders of customer John Smith.

### Debugging your queries

Requests can be executed in debug mode. No real order changes are made in this mode. Ecwid will emulate requests and return the same response as if you executed this request without debugging. Just add "debug=yes" to request parameters in order to execute this request in debug mode.
Why do you need this? You can easily debug your API requests in browser using simple GET requests (no need to create HTTP form or use some language/tool to send POST request). Just open URL like this in your browser (use your own secure_auth_key):

`https://app.ecwid.com/api/v2/1003/orders?secure_auth_key=XXXXX&order=123&new_payment_status=ACCEPTED&debug=yes`

and you will see which orders will be changed by this request in real mode.

### Examples

Change order #123 payment status to `ACCEPTED`
`<form action="https://app.ecwid.com/api/v2/1003/orders" method="post">
	<input type="text" name="secure_auth_key" value="XXXXX" />
	<input type="text" name="order" value="123" />
	<input type="text" name="new_payment_status" value="ACCEPTED" />
	<input type="submit" />
</form>`

Here is the debug request with the same parameters. This request doesn't change any order:

`https://app.ecwid.com/api/v2/1003/orders?secure_auth_key=XXXXX&order=123&new_payment_status=ACCEPTED&debug=yes`

### URL

`POST https://app.ecwid.com/api/v2/[STORE-ID]/orders?secure_auth_key=string​&date=string​&from_date=string​&to_date=string​&from_update_date=string​&to_update_date=string​&order=string​&from_order=string​&to_order=string​&customer_id=string​&customer_email=string​&statuses=string​&limit=number​&offset=number​&new_payment_status=string​&new_fulfillment_status=string​&new_shipping_tracking_code=string​&debug=boolean`

### URL Parameters

**Name** |	**Type** |	**Description**
--------- | -----------| -----------
STORE-ID* |	number |	ID of the Ecwid store.
secure_auth_key* |	string |	Product API secret key (can be found in the System Settings → API tab) or an OAuth authentication token.
date |	string |	All orders placed this day. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_date |	string |	All orders placed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
to_date |	string |	All orders placed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp.
from_update_date |	string |	All orders changed after this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
to_update_date |	string |	All orders changed before this date. Two data formats are supported: YYYY-MM-DD and Unix timestamp. For new orders update date is equal to creation date.
order |	string |	Order number. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
from_order |	string |	All orders with numbers bigger than or equal to <value>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
to_order |	string |	All orders with numbers smaller than or equal to <value>. Two order number formats are supported: ordinary order number (numeric) and vendor order number (order number with prefix/suffix).
customer_id |	string |	Unique numeric customer identifier or null for anonymous orders.
customer_email |	string |	Customer email or null for orders with empty or absent emails.
statuses |	string |	Payment and/or fulfillment comma-separated status names. Payment statuses: `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`, `INCOMPLETE`. Fulfillment statuses: `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
limit |	number |	Number of orders returned in response. The default and maximal value is 200, any greater value is reset to 200.
offset |	number |	How many orders skip from beginning.
new_payment_status |	string |	New payment status. One of `INCOMPLETE`, `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`.
new_fulfillment_status |	string |	New fulfillment status. One of `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
new_shipping_tracking_code |	string |	New shipping tracking code. Change of shipping tracking number will also change the order's fulfillment status to `SHIPPED`.
debug |	boolean | If set, this flag prevents orders from being changed, while the rest behaviour remains intact.
\* *Parameters marked with * are mandatory.*

### Response

A JSON object of type 'ChangedOrderResponse' with the following fields:

#### ChangedOrderResponse
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
count |	number |	The number of orders returned in the 'orders' field.
total |	number |	The number of orders satisfying the conditions specified in the request URL.
orders | Array<[ChangedOrder](http://google.com)> |	No more then the limit of the changed orders starting from the given offset ordered by time descending.

#### ChangedOrder
**Field** |	**Type** |	**Description**
--------- | -----------| -----------
number |	number |	A unique order number.
vendorNumber |	string *nullable* |	Admin-defined order numbers with prefix and suffix, e.g. 2011-345-q4.
oldPaymentStatus |	string *nullable* |	Old payment status. One of `INCOMPLETE`, `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`.
oldFulfillmentStatus |	string *nullable* |	Old fulfillment status. One of `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
paymentStatus |	string *nullable* |	New payment status. One of `INCOMPLETE`, `ACCEPTED`, `DECLINED`, `CANCELLED`, `QUEUED`, `CHARGEABLE`.
fulfillmentStatus |	string *nullable* |	New fulfillment status. One of `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
shippingTrackingCode |	string *nullable* |	New shipping tracking code. Order fulfillment status changed to `SHIPPED` every time you set shipping tracking code.
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

### Errors

**HTTP Status** |	**Response JSON** |	**Description**
--------- | -----------| -----------
404 |	| Store ID not found.
400	| [OrderException](#orderexception) |	Wrong URL parameters. Also this error will appear if you try to use the HTTP endpoint. All requests have to be sent over HTTPS protocol only.
405 |	[OrderException](#orderexception) |	Incorrect HTTP method (GET instead of POST, for example).
403|	[OrderException](#orderexception) |	Ecwid account type does not allow this kind of requests. Consider upgrading your account.

## Instant Order Notifications

Ecwid can notify another application about important store events as they happen in near real-time. A developer can use this API to extend and customize your checkout process. For example send a custom e-mail notification, inform your supplier about a sale, generate a pin code or a license key for a sold software, notify your IM client when you are offline, send a text message, add a new order to your accounting software or subscribe a new customer to your newsletter.

### How it works
All you have to do is provide a URL and Ecwid will call this URL (via HTTP POST request) as soon as things happen.
The following events are supported:
\* **New order has been placed.**
\* **Order status has been changed.**
 
This technology is called "Webhooks". For general reading on Webhooks, please refer to  their Wiki. 
 
 
### How to configure
1. [Log into your Ecwid account](https://my.ecwid.com/).
2. Go to the **System settings → API** page. 
3. Find the **Instant Order Notifications** section.
4. Enter a valid URL for Ecwid to contact. Ecwid will send a request to this URL each time a supported event occurs.  
 
### API Details
The following parameters are sent in an HTTP POST request to the endpoint URL as soon as one of the supported events occurs: 
 
**Name** |	**Type** |	**Description**
--------- | -----------| -----------
owner_id | Integer | Store ID, where the event occurred.
event_type | Text | Type of the occurred event. Possible values: `new_order` or `order_status_change`. 
date | Date | Order placement date or date of the order status change. Format is YYYY-MM-DD hh:mm:ss
order_id | Integer | Order ID without custom suffix and prefix. 
payment_status | Text | New payment status. If event is "new_order", then possible values are `QUEUED` or `ACCEPTED`. If "order_status_change", then `QUEUED`, `ACCEPTED`, `CHARGEABLE`, `DECLINED`, `CANCELLED`.
fulfillment_status |	Text | New fulfillment status. If event is "new_order", then it will be equal to `NEW` (default fulfillment status). If "order_status_change", then possible values are `NEW`, `PROCESSING`, `SHIPPED`, `DELIVERED`, `WILL_NOT_DELIVER`.
old_payment_status | Text | The payment status before the update. This parameter will be sent, only if event type is "order_status_change". 
old_fulfillment_status | Text | The fulfillment status before the update. This parameter will be sent, only if event type is "order_status_change". 

If the request fails to connect (wrong URL or problems on your server), Ecwid will attempt to re-send it using the following backoff logic: 1 minute, 5 minutes, 10 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, 5 hours, 12 hours, 24 hours, 36 hours, 48 hours, 60 hours, 72 hours. If all attempts were not successful, a message gets removed from the queue as an undelivered one.
 
The request is considered successful if an endpoint/URL returns HTTP 200 or HTTP 201 status header. 
  
### Securing Instant Order Notifications and Correct Workflow

The correct workflow is as follows: 
Your script gets a notification about an event. Only the necessary information like order status, order and store IDs is sent. No private sensitive information is sent.
Then your script should use [Order API](#orders) to validate and get more information about this event. I.e. check that the placed/updated order exists and gets necessary sensitive order details. If no such order exists in a database or it exists, but its current order status doesn't match a status in the notification, then the notification should be ignored as a fake one. 
 
This approach makes the whole process to be secure by design. For example:
1. If you set the incorrect endpoint URL or use a 3d-party URL (e.g. from [RequestBin](http://requestb.in/)) to test notifications, they will not get a private information about your customers, because they don't know your Order API secret key. 
2. This design forces a developer to always verify each notification request which comes to the endpoint. So even if somebody tries to "fake" a notification, it will not be validated and will be ignored.
 
 
### How to test
For testing notifications use the **"Test endpoint"** link on the **"API"** page. It allows to send custom notifications with any data you want, so it simplifies testing of your scripts. 
 
Also we suggest to use the [RequestBin tool](http://requestb.in/). It is an awesome utility to help see data come across as events happen in your system. Make a new bin and use its URL as the endpoint one. All notifications will appear in the same RequestBin page.
 
### What user agent string does Ecwid use for notifications? 
Ecwid uses the "Ecwid ION Cannon" user agent string. **"ION"** stands for Instant Order Notifications. So the thing  that "shoots" notifications at endpoints is [ION Cannon](http://www.youtube.com/watch?v=UN8YIR60Ij0). 

#### orderexception
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Error description, in English.

#### entitytoolongerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### notfounderror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### illegalparametererror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### internalerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### limiterror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### paidfeatureerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### autherror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### fileuploaderror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### importinprogresserror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### validationerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### retryerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*

#### nonuniqueerror
Field |	Type |	Description
--------- | -----------| -----------
errorMessage |	string |	Детальное сообщение об ошибке
\* *Some fields can have null value or be absent, in which case they are marked as nullable.*
