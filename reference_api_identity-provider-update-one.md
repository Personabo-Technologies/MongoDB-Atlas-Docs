Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Connected Identity Provider

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `federationSettings` resource allows you to update one identity provider
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

    
    
    PATCH /federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}  
      
  
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
  
`IDP-ID`

|

string

|

Unique 20-hexadecimal digit string that identifies the IdP.  
  
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

Name

|

Type

|

Description

|

Required  
  
|||  
  
`associatedDomains`

|

array

|

List that contains the domains associated with the identity provider.

|  
  
`displayName`

|

string

|

Human-readable label that identifies the identity provider.

|  
  
`issuerUri`

|

string

|

Unique string that identifies the issuer of the SAML Assertion.

|  
  
`pemFileInfo`

|

array

|

List that contains the PEM file information for the identity provider's
certificates.

|  
  
`requestBinding`

|

string

|

SAML Authentication Request Protocol HTTP method binding (POST or REDIRECT)
that Federated Authentication uses to send the authentication request.

Valid values include `HTTP-POST` and `HTTP-REDIRECT`.

|  
  
`responseSignatureAlgorithm`

|

string

|

Signature algorithm that Federated Authentication uses to encrypt the identity
provider signature.

Valid values include `SHA-1` and `SHA-256`.

|  
  
`ssoDebugEnabled`

|

boolean

|

Flag that indicates whether the identity provider has SSO debug enabled.

|

Required  
  
`ssoUrl`

|

string

|

Unique string that identifies the intended audience of the SAML assertion.

|  
  
`status`

|

string

|

String enum that indicates whether the identity provider is active or not.

Accepted values are `ACTIVE` or `INACTIVE`.

|  
  
## Response

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
         --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}"  
         --data {  
                 "associatedDomains": [],  
                 "displayName": "Test",  
                 "issuerUri": "urn:123456789000.us.provider.com",  
                 "pemFileInfo": [  
                   {  
                     "certificates": [  
                       {  
                         "content": "string",  
                         "notAfter": "2035-09-29T15:03:55Z",  
                         "notBefore": "2022-01-20T15:03:55Z"  
                       }  
                     ],  
                     "fileName": "file.pem"  
                   }  
                 ],  
                 "requestBinding": "HTTP-POST",  
                 "responseSignatureAlgorithm": "SHA-256",  
                 "ssoDebugEnabled": true,  
                 "ssoUrl": "https://123456789000.us.provider.com/samlp/12345678901234567890123456789012",  
                 "status": "INACTIVE"  
               }  
  
## Example Response

    
    
     {  
      
       "acsUrl": "https://example.mongodb.com/sso/saml2/12345678901234567890",  
       "associatedDomains": [],  
       "associatedOrgs": [  
         {  
           "domainAllowList": [  
             "domain.com"  
           ],  
           "domainRestrictionEnabled": true,  
           "identityProviderId": "0oa8i0grsgbwDiIyw453",  
           "orgId": "5df7a168f10fab3a149357fb",  
           "postAuthRoleGrants": [  
             "ORG_OWNER"  
           ],  
           "roleMappings": [  
             {  
               "externalGroupName": "example",  
               "id": "61e89721b827b56c845ff44c",  
               "roleAssignments": [  
                     {  
                      "groupId": null,  
                      "orgId": "5df7a168f10fab3a149357fb",  
                      "role": "ORG_OWNER"  
                     }  
               ]  
             }  
           ],  
           "userConflicts": [  
             {  
               "emailAddress": "someone@example.com",  
               "firstName": "John",  
               "id": "59db8d1d87d9d6420df0613a",  
               "lastName": "Smith",  
               "userId": "59db8d1d87d9d6420df0613a"  
             }  
           ]  
         }  
       ],  
       "audienceUri": "https://www.example.com/saml2/service-provider/abcdefghij1234567890",  
       "displayName": "Test",  
       "issuerUri": "urn:123456789000.us.provider.com",  
       "oktaIdpId": "0oa8i0grsgbwDiIyw453",  
       "pemFileInfo": [  
         {  
           "certificates": [  
             {  
               "notAfter": "2035-09-29T15:03:55Z",  
               "notBefore": "2022-01-20T15:03:55Z"  
             }  
           ],  
           "fileName": "file.pem"  
         }  
       ],  
       "requestBinding": "HTTP-POST",  
       "responseSignatureAlgorithm": "SHA-256",  
       "ssoDebugEnabled": true,  
       "ssoUrl": "https://123456789000.us.provider.com/samlp/12345678901234567890123456789012",  
       "status": "INACTIVE"  
     }  
  
What is MongoDB Atlas? →

