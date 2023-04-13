Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Invoices

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Use the `invoices` resource to view invoices for a Atlas organization.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/orgs/{ORG-ID}/invoices/

|

Get all invoices for the Atlas organization identified by `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/invoices/{INVOICE-ID}

|

Get the invoice identified by `{INVOICE-ID}` for the Atlas organization
identified by `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/invoices/pending

|

Get the pending invoice for the Atlas organization identified by `{ORG-ID}`.  
  
What is MongoDB Atlas? →

