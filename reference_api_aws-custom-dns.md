Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Custom DNS for Atlas Clusters Deployed to AWS

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `awsCustomDNS` resource lets you retrieve and update the custom DNS
configuration of an Atlas project's clusters deployed to AWS. The resource
requires your Project ID.

Enable custom DNS if you use the VPC peering on AWS and you use your own DNS
servers instead of Amazon Route 53.

## Tip

### See also:

How does this affect AWS VPC peering when I use custom DNS?

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/awsCustomDNS

|

Retrieve the custom DNS configuration of an Atlas project's clusters deployed
to AWS.  
  
`PATCH`

|

/groups/{GROUP-ID}/awsCustomDNS

|

Update the custom DNS configuration of an Atlas project's clusters deployed to
AWS.  
  
What is MongoDB Atlas? →

