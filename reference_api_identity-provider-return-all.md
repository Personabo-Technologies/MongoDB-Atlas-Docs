Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return All Connected Identity Providers

Share Feedback

On this page

  * Required Roles
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

The `federationSettings` resource allows you to return all identity providers
for a federated authentication configuration.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role for at least one connected
organization in the federation configuration to call this endpoint.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/  
      
  
### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`FEDERATION-SETTINGS-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the federated
authentication configuration.  
  
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

Each document in the `results` array contains the federated authentication
configuration for each connected organization.

Name

|

Type

|

Description  
  
||  
  
acsUrl

|

string

|

Assertion consumer service URL to which the IdP sends the SAML response.  
  
associatedDomains

|

array

|

List that contains the configured domains from which users can log in for this
IdP.  
  
associatedOrgs

|

array

|

List that contains the organizations from which users can log in for this IdP.  
  
audienceUri

|

string

|

Identifier for the intended audience of the SAML Assertion.  
  
displayName

|

string

|

Human-readable label that identifies the IdP.  
  
issuerUri

|

string

|

Identifier for the issuer of the SAML Assertion.  
  
oktaIdpId

|

string

|

Unique 20-hexadecimal digit string that identifies the IdP.  
  
pemFileInfo

|

array

|

List that contains the file information, including: start date, and expiration
date for the identity provider's PEM-encoded public key certificate.

|

Name

|

Type

|

Description  
  
||  
  
certificates

|

array

|

List that contains the start date and expiration date for the identity
provider's PEM-encoded public key certificate.  
  
fileName

|

string

|

Label that identifies the file containing the identity provider's PEM-encoded
public key certificate.  
  
requestBinding

|

string

|

SAML Authentication Request Protocol binding used to send the AuthNRequest.
Atlas supports the following binding values:

  * `HTTP POST`

  * `HTTP REDIRECT`

  
  
responseSignatureAlgorithm

|

string

|

Algorithm used to encrypt the IdP signature. Atlas supports the following
signature algorithm values:

  * `SHA-1`

  * `SHA-256`

  
  
ssoDebugEnabled

|

boolean

|

Flag that indicates whether the IdP has enabled **Bypass SAML Mode**. Enabling
this mode generates a URL that allows you bypass SAML and login to your
organizations at any point. You can authenticate with this special URL only
when Bypass Mode is enabled. Set this parameter to `true` during testing. This
keeps you from getting locked out of MongoDB.  
  
ssoUrl

|

string

|

URL of the receiver of the SAML AuthNRequest.  
  
status

|

string

|

Label that indicates whether the identity provider is active. The IdP is
Inactive until you map at least one domain to the IdP.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders"  
  
## Example Response

    
    
    {  
      
     "links": [  
         {  
             "links" : [ {  
     "href" : "https://cloud.mongodb.com/api/public/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders?pretty=true&pageNum=1&itemsPerPage=100",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "acsUrl" : "https://example.mongodb.com/sso/saml2/12345678901234567890",  
             "associatedDomains" : [ ],  
             "associatedOrgs" : [ ],  
             "audienceUri" : "https://www.example.com/saml2/service-provider/abcdefghij1234567890",  
             "displayName" : "Test",  
             "issuerUri" : "urn:123456789000.us.provider.com",  
             "oktaIdpId" : "1234567890abcdefghij",  
             "pemFileInfo" : {  
                 "certificates" : [ {  
                    "notAfter" : "2035-09-29T15:03:55Z",  
                    "notBefore" : "2022-01-20T15:03:55Z"  
                 } ],  
                 "fileName" : "file.pem"  
             },  
             "requestBinding" : "HTTP-POST",  
             "responseSignatureAlgorithm" : "SHA-256",  
             "ssoDebugEnabled" : true,  
             "ssoUrl" : "https://123456789000.us.provider.com/samlp/12345678901234567890123456789012",  
             "status" : "INACTIVE"  
         } ],  
     "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

