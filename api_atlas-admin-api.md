Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Deployments with the Atlas Administration API

Share Feedback

On this page

  * Atlas Administration API Features
  * HTTP Methods
  * JSON
  * Linking
  * Lists
  * Envelopes
  * Pretty Printing
  * Response Codes
  * Errors
  * Project ID
  * Authentication
  * Rate Limiting

Manage your Atlas environment through the command line or automate with the
Atlas Administration API. Atlas Administration API resources add, edit, or
delete administrative objects within Atlas, including projects, users, and
database deployments.

You can't read or write data using the Atlas Administration API. To read and
write data in Atlas, use the Data API.

Use these resources and the following sections to learn more about the Atlas
Administration API:

  * Get Started with the Atlas Administration API

  * Atlas Administration API Specification

  * Atlas Administration API Error Codes

## Atlas Administration API Features

The Atlas Administration API follows the principles of the REST architectural
style to expose a number of internal resources which enable programmatic
access to Atlas's features.

As with changes made through the Atlas web interface, changes made through the
API are subject to Atlas billing. If you incur charges, you must have a valid
credit card on file with Atlas or risk having your account locked.

The API has the following features:

JSON entities

    All entities are expressed in JSON.
Key-based access

    Each Atlas user or application needing to connect to Atlas must generate an API key before accessing the Atlas Administration API.
Digest authentication

    To ensure that your API key is never sent over the network, API requests are authenticated using HTTP Digest Authentication.
Browsable interface

    Using a consistent linking mechanism, you can browse the entire API by starting at the root resource and following links to related resources.
HTTPS-Only

    You can only access the API via HTTPS, ensuring all data sent over the network is fully encrypted using TLS.
User Access Control

    

Each Atlas user's API capabilities match the permissions granted by their
Atlas Atlas User Roles.

## Example

A user with the `Project Read Only` in a Atlas project can't modify any
resource within that project whether through the Atlas user interface or the
API.

API Network Access List

    

Atlas secures access to its API through an access list. This list restricts
access to the API to specific IP or CIDR addresses. Each Programmatic API Key
has its own API access list. Each API Key must make any API requests from an
IP address on the API access list.

## Tip

### See also:

Get Started with the Atlas Administration API.

## HTTP Methods

All resources support a subset of these common HTTP Methods:

Method

|

Purpose  
  
|  
  
`GET`

|

Retrieve the JSON representation of a resource.  
  
`POST`

|

Create a new resource using the provided JSON representation.  
  
`PUT`

|

Replace a resource with the provided JSON representation.  
  
`PATCH`

|

Update the specified fields in a resource using the provided JSON
representation.  
  
`DELETE`

|

Remove a resource.  
  
`HEAD`

|

Returns the response header without the JSON representation of the resource.  
  
## JSON

All entities are represented in JSON. The following rules and conventions
apply:

  *  **Content Type Request Header**

When sending JSON to the server via `POST` or `PUT`, make sure to specify the
correct content type request header: `Content-Type: application/json`

  *  **Invalid Fields**

Invalid fields are _rejected_ rather than _ignored_. For example, if you
attempt to create a new entity and misspell one of the fields, or attempt to
update an existing entity and include a field that can't be modified, the
server responds with a 400 status code and an error message stating which
field is invalid.

  *  **ISO-8601-Formatted Dates**

All dates are returned as ISO-8601-formatted strings designated in UTC. When
sending dates to the server (i.e., as query parameters or fields in `POST` or
`PATCH` request entities), use ISO-8601-formatted dates. If you do not specify
a time zone, UTC is assumed. However, it is highly recommended that you
include a time zone designator to avoid any ambiguity.

  *  **BSON Timestamps**

In some cases, a timestamp is returned as a BSON timestamp, most notably in
the backup resources. These are represented in JSON documents as an object
with two fields: `date`, which is an ISO-8601-formatted date string in UTC
with granularity to the second, and `increment` a 32-bit integer.

  *  **Field Names for Fields with Numbers**

Fields that contain numeric values in a particular unit will be named so as to
disambiguate the unit being used.

  *  **Empty Fields**

Fields that do not have a current value are returned with an appropriate
default value.

Fields that do not have a sensible default value are omitted from the entity.

  *  **Field Order**

The fields in the JSON documents returned by the server are in no particular
order, and the order may change. Do not depend on the order of the fields.

## Linking

Each resource includes one or more links to sub-resources and/or related
resources. Links are placed in the `links` field of an entity, which is an
array of link relation objects. Each link relation has two fields:

Field

|

Description  
  
|  
  
`rel`

|

Name (or type) of the relation. Many of these are considered Extension
Relation Types and are prefixed by `http://mms.mongodb.com`.  
  
`href`

|

The target URL.  
  
All entities include at least one link relation called `self`, which is simply
its own URL. When an entity is part of a list, then it only includes the
`self` link relation.

For more information, refer to the Web Linking Specification. Note that
although the specification describes a format for including links in the HTTP
response headers, doing so is not a requirement. To make the API easily
browsable, it includes the links in the response body rather than in the
response headers.

## Lists

Some resources return a list of entities. When a list of entities is expected
in a response, the results are returned in batches bounded by the following
query parameters:

Field

|

Description  
  
|  
  
`pageNum`

|

Page number (1-based). Defaults to `1` if not specified.  
  
`itemsPerPage`

|

Number of items to return per page, up to a maximum of 500. Defaults to `100`
if not specified.  
  
`includeCount`

|

Specifies whether the response returns the `totalCount` field. Defaults to
`true` if not specified.  
  
The response entity contains three fields:

Field

|

Description  
  
|  
  
`totalCount`

|

The total number of items in the entire result set.  
  
`results`

|

The result set, which is an array of entity documents.  
  
`links`

|

Contains one to three link relations: `previous` for the previous page of
results (omitted for the first page); `next` for the next page of results
(omitted for the last page); and `self` for the current page (always present).  
  
If you make a request for a list of entities and there are no results, then
the API responds with a 200 status code and the `results` array is empty. It
does _not_ respond with a 404 in this case, since the list of entities may not
be empty at some point in the future. However, if you request a list of
entities in a context that does not exist (e.g., the list of hosts for a non-
existent project), then this _does_ result in a 404 response status.

## Envelopes

Some clients might not be able to access the HTTP response headers and/or
status code. In that case, you can request that the response include an
"envelope," which is simply an extra layer of information in the JSON document
and contains any relevant details that would normally be in the response
headers. By default, the API does _not_ include the response in an envelope.
To request one, simply add the query parameter `envelope=true`.

For responses that contain a single entity, the envelope contains two fields:

Field

|

Description  
  
|  
  
`status`

|

The HTTP status code.  
  
`content`

|

The requested entity.  
  
For responses that contain a list of entities, there is already an envelope
that wraps the results, so specifying `envelope=true` only adds the `status`
field to the existing envelope.

## Pretty Printing

By default, extraneous whitespace is stripped from the JSON returned by the
server. To ask for pretty-printed JSON, simply append the `pretty=true` query
parameter to any request:

    
    
    curl --user '{USERNAME}:{APIKEY}' --digest \  
      
      --header 'Accept: application/json' \  
      --include \  
      --request GET "https://cloud.mongodb.com/api/atlas/v1.0?pretty=true"  
  
## Response Codes

Responses use the standard HTTP response codes, including:

Code

|

Meaning

|

Notes  
  
||  
  
200

|

OK

|

The request was successful. This is typically the response to a successful
`GET` request.  
  
201

|

Created

|

A new resource was created. This is typically the response to a successful
`POST` request.  
  
202

|

Accepted

|

A request for an asynchronous operation was accepted.  
  
400

|

Bad Request

|

Something was wrong with the client request.  
  
401

|

Unauthorized

|

Authentication is required but was not present in the request. Typically this
means that the digest authentication information was omitted from the request,
the provided credentials are incorrect, or the user associated with the given
API key is not allowed to access the requested resource.  
  
403

|

Forbidden

|

Access to the specified resource is not permitted.  
  
404

|

Not Found

|

The requested resource does not exist.  
  
405

|

Method Not Allowed

|

The HTTP method is not supported for the specified resource. Keep in mind that
each resource may only support a subset of HTTP methods.

## Example

### You can't DELETE the root resource.  
  
409

|

Conflict

|

This is the response to a request to create or modify a property of an entity
that is unique when an existing entity already exists with the same value for
that property.  
  
5xx

|

Various server errors

|

Something unexpected went wrong. Try again later and consider notifying Atlas
Support.  
  
## Errors

When a request returns an error, the response body contains a JSON document.
This document includes details about why the API request failed. The document
contains five parameters:

Parameter

|

Data Type

|

Description  
  
||  
  
detail

|

string

|

Human-readable description that Atlas returns for the errant API request.  
  
error

|

integer

|

Status code returned in the header of the HTTP response.  
  
errorCode

|

string

|

Named constant that represents the errant API request. To learn about these
constants, see Atlas Administration API Error Codes.  
  
parameters

|

array

|

List of parameters included in the API request.  
  
reason

|

string

|

Status code definition returned in the header of the HTTP response.  
  
## Example

Atlas returns the following response body when you make a request in the
incorrect format:

    
    
    1| {  
    |  
    2|   "detail" : "Cannot find resource /api/atlas/v1.0/softwareComponents/version.",  
    3|   "error" : 404,  
    4|   "errorCode" : "RESOURCE_NOT_FOUND",  
    5|   "parameters" : [ "/api/atlas/v1.0/softwareComponents/version" ],  
    6|   "reason" : "Not Found"  
    7| }  
  
## Project ID

Your Project ID is a string value that uniquely identifies a Atlas project.

Atlas projects were previously identified as "groups". Some Atlas endpoints
reference `group` or `{GROUP-ID}` as part of the request path, query, or body
parameters. For any endpoint that requires your `{GROUP-ID}`, specify your
Project ID instead.

To retrieve your project ID:

1

### Navigate to the Settings page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Next to the Projects menu, expand the Options menu, then click Project Settings.

2

### Copy the string listed under the Project ID heading.

## Authentication

As previously mentioned, the Atlas Administration API uses HTTP Digest
Authentication. The details of digest authentication are beyond the scope of
this document. Digest authentication requires a username and a password. The
Atlas hashes these values using a unique value called a **nonce**. The API
public key serves as the username. Its corresponding API private key serves as
the password.

Keep the following points in mind:

  * The Atlas-generated nonce is used by the client to hash the username and password before sending them back to the Atlas to authenticate a request. The nonce is only valid for a short amount of time as per the digest authentication specification. This is to prevent replay attacks, so you can't cache a nonce and use it forever.

  * Using digest authentication with HTTPS adds an extra layer of security. The API request never sends the password to the Atlas.

  * Some resource require additional security. These resources deny access to any request not made from an IP address on an API access list. Each organization may have one or more API keys, each with their own API access list. An API key can access an API resource only from an IP address on its API access list.

  * Atlas roles limit which operations an API key can perform. The API resources enforce the same privileges. The resources and methods that an API key use the same roles as an Atlas user.

  * Atlas binds many resources to a project. Many API resource URLs follow the format of `/api/atlas/v1.0/groups/<GROUP-ID>/`. For these resources, the API key must be a member of the organization that hosts the project. Otherwise, the Atlas responds with a 401 error.

## Rate Limiting

Certain resources limit how many requests they can process per minute.

For these resources, Atlas allows up to 100 requests per minute _per project_.
API keys belong to an organization, but can be granted access multiple
projects.

## Example

Consider two users: A and B. User A belongs to project X, and user B belongs
to projects X and Y.

  * At 1:00:00pm, User A makes 50 requests to a rate limited resource in project X, all of which are complete by 1:00:20pm.

  * At 1:00:30pm, User B attempts to make 60 requests to a rate limited resource in project X.

Since User A has already used up 50 requests within the 1:00pm minute for
project X, the last 10 requests User B attempts to make are rejected.

However, User B can make requests to a rate limited resource in project Y,
since each project maintains a separate request counter.

  * At 1:01:00pm, requests to project X may proceed, because the request counter used for rate limiting resets each minute.

If you exceed the rate limit, the API returns a 429 (Too Many Requests) HTTP
status code.

← APIsGet Started with the Atlas Administration API →

