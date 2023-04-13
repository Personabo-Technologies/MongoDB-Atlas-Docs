Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Invoices for One Organization

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
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

    
    
    GET /orgs/{ORG-ID}/invoices/  
      
  
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
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

Each document in the `result` array represents one invoice. Charges are
typically posted the next day.

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

Amount billed in this invoice, calculated as `subtotalCents` \+
`salesTaxCents` \- `startingBalanceCents`.  
  
`amountPaidCents`

|

number

|

Amount paid for this invoice, in USD cents.  
  
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
  
`id`

|

string

|

Unique identifier for this invoice.  
  
`links`

|

object array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
`groupId`

|

string

|

Unique identifier of the project with which the invoice is associated. _Does
not appear on all invoices._  
  
`orgId`

|

string

|

Unique identifier for the organization that received this invoice.  
  
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
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/?pretty=true"  
  
## Example Response

    
    
    {  
      
       "links" : [ {  
         "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/?pretty=true&pageNum=1&itemsPerPage=100",  
         "rel" : "self"  
       } ],  
       "results" : [ {  
         "amountBilledCents" : 0,  
         "amountPaidCents" : 0,  
         "created" : "2018-06-01T04:05:10Z",  
         "endDate" : "2018-07-01T00:00:00Z",  
         "id" : "{INVOICE-ID}",  
         "links" : [ {  
           "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/{INVOICE-ID}",  
           "rel" : "self"  
         } ],  
         "orgId" : "{ORG-ID}",  
         "salesTaxCents" : 0,  
         "startDate" : "2018-06-01T00:00:00Z",  
         "startingBalanceCents" : 0,  
         "statusName" : "PENDING",  
         "subtotalCents" : 0,  
         "updated" : "2018-06-01T04:05:10Z"  
       }, {  
         "amountBilledCents" : 726,  
         "amountPaidCents" : 726,  
         "created" : "2018-02-01T06:05:04Z",  
         "endDate" : "2018-03-01T00:00:00Z",  
         "id" : "{INVOICE-ID}",  
         "links" : [ {  
           "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/invoices/{INVOICE-ID}",  
           "rel" : "self"  
         } ],  
         "orgId" : "{ORG-ID}",  
         "salesTaxCents" : 57,  
         "startDate" : "2018-02-01T00:00:00Z",  
         "startingBalanceCents" : 0,  
         "statusName" : "PAID",  
         "subtotalCents" : 669,  
         "updated" : "2018-03-01T07:00:54Z"  
       } ],  
       "totalCount" : 16  
    }  
  
What is MongoDB Atlas? →

