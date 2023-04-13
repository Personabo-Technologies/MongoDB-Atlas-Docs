Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Organization Invoice

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Request Headers
  * Response
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /orgs/{ORG-ID}/invoices/{INVOICE-ID}  
      
  
### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`ORG-ID`

|

string

|

Unique identifier of the organization.  
  
`INVOICE-ID`

|

string

|

Unique identifier of the invoice. Charges are typically posted the next day.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

### Request Headers

This endpoint can return its content in JSON or CSV format. Use the `Accept`
request header to specify your desired the content type.

  * For JSON, use `"Accept: application/json"`;

  * For CSV, use `"Accept: text/csv"`

## Response

JSON

CSV

If you specify `Accept: application/json` in the request headers, the HTTP
response is a JSON document that includes the following fields:

Name

|

Type

|

Description  
  
||  
  
`amountBilledCents`

|

number

|

Amount billed in this invoice, calculated as **subtotalCents** \+
**salesTaxCents** \- **startingBalanceCents**  
  
`amountPaidCents`

|

number

|

Amount paid for this invoice.  
  
`created`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when this invoice was
created.  
  
`creditsCents`

|

number

|

Amount credited by MongoDB, in USD cents.  
  
`endDate`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the billing period for
this invoice ended.  
  
`groupId`

|

string

|

Unique identifier of the project with which the invoice is associated. _Does
not appear on all invoices._  
  
`id`

|

string

|

Unique identifier for this invoice.  
  
`lineItems`

|

object array

|

Line items in the invoice. This information is also found in the Usage Details
section of the Invoice page in the Atlas UI.

Each object in the array includes the following fields:

|

Item

|

Description  
  
|  
  
`clusterName`

|

The name of the cluster that incurred the charge  
  
`created`

|

Timestamp in ISO 8601 date and time format in UTC when the line item was
posted to the invoice.  
  
`endDate`

|

Timestamp in ISO 8601 date and time format in UTC when the period for which
the line item applies ended.  
  
`discountCents`

|

Amount discounted, in USD cents. _Displays when applicable._  
  
`groupId`

|

ID of the project with which the line item is associated.  
  
`note`

|

Note regarding the line item.  
  
`percentDiscount`

|

Percent of discount. _Displays when applicable._  
  
`quantity`

|

Number of units of the line item (e.g. GB, hours, etc.).  
  
`sku`

|

Description of the line item. This could be the instance type, a support
charge, advanced security, etc.  
  
`startDate`

|

Timestamp in ISO 8601 date and time format in UTC when the period for which
the line item applies began.  
  
`stitchAppName`

|

Name of the Atlas App Services app associated with the line item.  
  
`tierLowerBound`

|

The lower bound of the specific tier used for the line item.  
  
`tierUpperBound`

|

The upper bound of the specific tier used for the line item.

## Note

`tierLowerBound` and `tierUpperBound` only appear if your `sku` is tiered.  
  
`totalPriceCents`

|

Total price for the line item, in USD cents. Equal to

    
    
    |  unitPriceDollars * quantity * 100  
      
  
`unit`

|

Unit of measure (e.g. GB, hours, etc.)  
  
`unitPriceDollars`

|

Cost of the item, in dollars.  
  
`links`

|

object array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
`orgId`

|

string

|

Unique identifier for the organization that received this invoice.  
  
`payments`

|

object array

|

Payments applied to the invoice. Objects in the `payments` array include the
following fields:

|

Field

|

Description  
  
|  
  
`amountBilledCents`

|

The amount of the invoice, in USD cents.  
  
`amountPaidCents`

|

The amount that the customer paid, in USD cents.  
  
`created`

|

Timestamp in ISO 8601 date and time format in UTC when the payment was
recorded.  
  
`id`

|

Unique identifier of the payment.  
  
`salesTaxCents`

|

Amount of sales tax paid, in USD cents.  
  
`statusName`

|

State of the payment.

|

Status

|

Description  
  
|  
  
`CANCELLED`

|

The payment has been cancelled.  
  
`FAILED`

|

The attempt to charge the credit card failed.  
  
`FORGIVEN`

|

The payment was created, but was subsequently forgiven.  
  
`NEW`

|

The payment has been created, but no attempt has been made to charge the
credit card.  
  
`PAID`

|

The payment was successful.  
  
`subtotalCents`

|

Sum of all positive invoice line items, in USD cents.  
  
`updated`

|

Timestamp in ISO 8601 date and time format in UTC when the object was last
updated.  
  
`refunds`

|

object array

|

Refunds issued for the invoice. Objects in the `refunds` array include the
following fields:

|

Field

|

Description  
  
|  
  
`amountCents`

|

The amount of the refund, in USD cents.  
  
`created`

|

Timestamp in ISO 8601 date and time format in UTC when the refund was
recorded.  
  
`reason`

|

Reason for the refund.  
  
`paymentId`

|

Unique identifier of the payment.  
  
`salesTaxCents`

|

number

|

Amount of taxes levied on **subtotalCents**.  
  
`startDate`

|

string

|

Timestamp in ISO 8601 date and time format in UTC of the starting date for
this invoice.  
  
`statusName`

|

string

|

State of this invoice. Accepted values are:

|

Status

|

Description  
  
|  
  
`INVOICED`

|

The customer received an invoice for their subscription.  
  
`PAID`

|

The funds have been transferred to MongoDB.  
  
`PREPAID`

|

The customer has purchased credit from MongoDB sales, so the customer is not
charged.  
  
`FREE`

|

The amount turned out to be zero, so the customer is not charged.  
  
`PENDING`

|

Includes charges for the current subscription cycle. An organization should
never have more than one invoice in this state.  
  
`FORGIVEN`

|

The charge has been forgiven. If the charge succeeded, it has been refunded.  
  
`FAILED`

|

An attempt to charge the credit card for the amount due failed.  
  
`CLOSED`

|

All charges for the subscription cycle have been finalized, the balance is
more than zero, and the customer has not been charged yet.  
  
`subtotalCents`

|

number

|

Sum of all positive invoice line items in USD cents.  
  
`updated`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the invoice was last
updated.  
  
If you set the query element `envelope` to `true`, the response is wrapped by
the `content` object.

## Example Request

JSON

CSV

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/{INVOICE-ID}"  
  
## Example Response

JSON

CSV

## Note

In the following sample response, the `lineItems` array has been truncated for
ease of viewing.

    
    
    {  
      
      "amountBilledCents" : 240,  
      "amountPaidCents" : 240,  
      "created" : "2018-04-01T06:14:31Z",  
      "endDate" : "2018-05-01T00:00:00Z",  
      "id" : "{INVOICE-ID}",  
      "lineItems" : [ {  
        "clusterName" : "{CLUSTER-NAME}",  
        "created" : "2018-05-01T04:05:31Z",  
        "endDate" : "2018-05-01T00:00:00Z",  
        "groupId" : "{GROUP-ID}",  
        "quantity" : 72.0,  
        "sku" : "ATLAS_INSTANCE_M0",  
        "startDate" : "2018-04-30T00:00:00Z",  
        "totalPriceCents" : 0,  
        "unit": "server hours",  
        "unitPriceDollars" : 0.0  
      }, {  
        "clusterName" : "{CLUSTER-NAME}",  
        "created" : "2018-04-30T04:05:19Z",  
        "endDate" : "2018-04-30T00:00:00Z",  
        "groupId" : "{GROUP-ID}",  
        "quantity" : 72.0,  
        "sku" : "ATLAS_INSTANCE_M0",  
        "startDate" : "2018-04-29T00:00:00Z",  
        "totalPriceCents" : 0,  
        "unit": "server hours",  
        "unitPriceDollars" : 0.0  
      },  
      ... ,  
      {  
        "clusterName" : "{CLUSTER-NAME}",  
        "created" : "2018-04-02T06:05:07Z",  
        "endDate" : "2018-04-02T00:00:00Z",  
        "groupId" : "{GROUP-ID}",  
        "quantity" : 72.0,  
        "sku" : "ATLAS_INSTANCE_M0",  
        "startDate" : "2018-04-01T00:00:00Z",  
        "totalPriceCents" : 0,  
        "unit": "server hours",  
        "unitPriceDollars" : 0.0  
      } ],  
      "links" : [ {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}",  
        "rel" : "http://mms.mongodb.com/org"  
      }, {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/{INVOICE-ID}",  
        "rel" : "self"  
      } ],  
      "orgId" : "{ORG-ID}",  
      "payments" : [ {  
        "amountBilledCents" : 240,  
        "amountPaidCents" : 240,  
        "created" : "2018-05-01T04:05:14Z",  
        "id" : "{PAYMENT-ID}",  
        "salesTaxCents" : 19,  
        "statusName" : "PAID",  
        "subtotalCents" : 221,  
        "updated" : "2018-05-01T07:00:46Z"  
      } ],  
      "refunds" : [ ],  
      "salesTaxCents" : 19,  
      "startDate" : "2018-04-01T00:00:00Z",  
      "startingBalanceCents" : 0,  
      "statusName" : "PAID",  
      "subtotalCents" : 221,  
      "updated" : "2018-05-01T07:00:46Z"  
  
What is MongoDB Atlas? →

