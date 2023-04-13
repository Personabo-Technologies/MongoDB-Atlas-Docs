Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return One Identity Provider's Metadata

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

The `federationSettings` resource allows you to return the contents of the
SAML metadata XML file for one identity provider in the specified federation.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}/metadata.xml  
      
  
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

This endpoint does not use HTTP request body parameters.

## Response

File Type

|

Description  
  
|  
  
XML

|

Metadata for the IdP.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/xml" \  
         --header "Content-Type: application/xml" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}/metadata.xml?pretty=true"  
  
## Example Response

    
    
    <?xml version="1.0" encoding="UTF-8"?>  
      
    <md:EntityDescriptor entityID="https://www.example.com/saml2/service-provider/sptikhtmphyefhvhjmkt" xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata"><md:SPSSODescriptor AuthnRequestsSigned="true" WantAssertionsSigned="true" protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"><md:KeyDescriptor use="encryption"><ds:KeyInfo xmlns:ds="http://www.w3.org/2000/09/xmldsig#"><ds:X509Data><ds:X509Certificate>MIIDpjCCAo6gAwIBAgIGAWqTiVlwMA0GCSqGSIb3DQEBCwUAMIGTMQswCQYDVQQGEwJVUzETMBEG  
    A1UECAwKQ2FsaWZvcm5pYTEWMBQGA1UEBwwNU2FuIEZyYW5jaXNjbzENMAsGA1UECgwET2t0YTEU  
    MBIGA1UECwwLU1NPUHJvdmlkZXIxFDASBgNVBAMMC21vbmdvZGItZGV2MRwwGgYJKoZIhvcNAQkB  
    Fg1pbmZvQG9rdGEuY29tMB4XDTE5MDUwNzE4MjIzM1oXDTI5MDUwNzE4MjMzM1owgZMxCzAJBgNV  
    BAYTAlVTMRMwEQYDVQQIDApDYWxpZm9ybmlhMRYwFAYDVQQHDA1TYW4gRnJhbmNpc2NvMQ0wCwYD  
    VQQKDARPa3RhMRQwEgYDVQQLDAtTU09Qcm92aWRlcjEUMBIGA1UEAwwLbW9uZ29kYi1kZXYxHDAa  
    BgkqhkiG9w0BCQEWDWluZm9Ab2t0YS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIB  
    AQCXHOJx/t+zFgbJzloBRpGhMFxccmvMShn2OQHinrW/s7J49YGbkj0NBWpW+Y6yTZfzGm04mYe+  
    /1+m7+ERJpypvlF+tkNcevMmYtxTPjYvGk+GslkjdfDJFSygbtiQkLCQTbpPnGTtVvx+YSg83Rq0  
    a7QPQ0QeU7utE2NiTOGakIzTLd6Okb2VjBb/cv92P1fcrrY7aDbb27V2+ZBsdv8fg55xrwlMm2uv  
    m32ZSRWfWwYgOoUtYZxEQZoOv45MPKf0O5Ok7ICyNZAd5+zI+gS+7keKAE6mF9ux7MfokashORgf  
    UN2K77/xYk/1y4XSlKF1vb6+yfZr9MTkyrSCaS/tAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAH+k  
    iR2cvXUlxOLG6gpMCuZlDdvkayBBwRNprawhEr2LLI8yGV3hRsWxsi2GoXXOCHZ62/rsn3Lg8mvQ  
    YAW3knId2ZsEh6mWlUljIjAtUZ5s6067KQV4u/70sO3wBQ0kcs/WnJPfz3Obb7uQ8cv0aa68IJrb  
    u8w5NqwWqA3FP1iuG3mfHNh6GI7DhzaVnzm9F5m7pL6hohKHMxF7n/dtuRMPTpc+UvpbnNAz/0kS  
    2d9fEHuMo4DXuzFZMy2ZKyFNnsVAwasAN3vdWY2S9ysGoUmCr98dS+nh4mMPSUHoPWj2myP53E08  
    +ZRsuZ13zI2C25+U4rgerB8XsxU7OER2CEk=</ds:X509Certificate></ds:X509Data></ds:KeyInfo><md:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc"/><md:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes192-cbc"/><md:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/><md:EncryptionMethod Algorithm="http://www.w3.org/2009/xmlenc11#aes128-gcm"/><md:EncryptionMethod Algorithm="http://www.w3.org/2009/xmlenc11#aes256-gcm"/><md:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#tripledes-cbc"/></md:KeyDescriptor><md:KeyDescriptor use="signing"><ds:KeyInfo xmlns:ds="http://www.w3.org/2000/09/xmldsig#"><ds:X509Data><ds:X509Certificate>MIIDpjCCAo6gAwIBAgIGAWqTiVlwMA0GCSqGSIb3DQEBCwUAMIGTMQswCQYDVQQGEwJVUzETMBEG  
    A1UECAwKQ2FsaWZvcm5pYTEWMBQGA1UEBwwNU2FuIEZyYW5jaXNjbzENMAsGA1UECgwET2t0YTEU  
    MBIGA1UECwwLU1NPUHJvdmlkZXIxFDASBgNVBAMMC21vbmdvZGItZGV2MRwwGgYJKoZIhvcNAQkB  
    Fg1pbmZvQG9rdGEuY29tMB4XFKDLJFHwNzE4MjIzM1oXDTI5MDUwNzE4MjMzM1owgZMxCzAJBgNV  
    BAYTAlVTMRMwEQYDVQQIDApDYWxpZm9ybmlhMRYwFAYDVQQHDA1TYW4gRnJhbmNpc2NvMQ0wCwYD  
    VQQKDARPa3RhMRQwEgYDVQQLDAtTU09Qcm92aWRlcjEUMBIGA1UEAwwLbW9uZ29kYi1kZXYxHDAa  
    BgkqhkiG9w0BCQEWDWluZm9Ab2t0YS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIB  
    AQCXHOJx/t+zFgbJzloBRpGhMFxccmvMShn2OQHinrW/s7J49YGbkj0NBWpW+Y6yTZfzGm04mYe+  
    /1+m7+ERJpypvlF+tkNcevMmYtxTPjYvGk+GQmZSLKJDJAygbtiQkLCQTbpPnGTtVvx+YSg83Rq0  
    a7QPQ0QeU7utE2NiTOGakIzTLd6Okb2VjBb/cv92P1fcrrY7aDbb27V2+ZBsdv8fg55xrwlMm2uv  
    m32ZSRWfWwYgOoUtYZxEQZoOv45MPKf0O5Ok7ICyNZAd5+zI+gS+7keKAE6mF9ux7MfokashORgf  
    UN2K77/xYk/1y4XSlKF1vb6+yfZr9MTkyrSCaS/tAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAH+k  
    iR2cvXUlxOLG6gpMCuZlDdvkayBBwRNprawhEr2LLI8yGV3hRsWxsi2GoXXOCHZ62/rsn3Lg8mvQ  
    YAW3knId2ZsEh6mWlUljIjAtUZ5s6067KQV4u/70sO3wBQ0kcs/WnJPfz3Obb7uQ8cv0aa68IJrb  
    u8w5NqwWqA3FP1iuG3mfHNh6GI7DhzaVnzm9F5m7pL6hohKHMxF7n/dtuRMPTpc+UvpbnNAz/0kS  
    2d9fEHuMo4DXuzFZMy2ZKyFNnsVAwasAN3vdWY2S9ysGoUmCr98dS+nh4mMPSUHoPWj2myP53E08  
    l:lang="en">http://www.mongodb.com/</md:OrganizationURL></md:Organization>  
  
What is MongoDB Atlas? →

