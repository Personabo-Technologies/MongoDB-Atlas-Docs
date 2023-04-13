Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return the Latest Targets for Prometheus

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * labels Embedded Document
  * Example Request
  * Example Response

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/prometheus/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/discovery  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`{GROUP-ID}`

|

Required

|

Project identifier.  
  
### Request Query Parameters

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
  
targetScheme

|

TargetScheme

|

Optional

|

Type of targets to return. Values include:

  * `PUBLIC`: Public internet accessible targets.

  * `PRIVATE`: Private IP for VPC peering compatible targets.

|

`PUBLIC`  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of your latest **targets** from
which to scrape and a document containing their **labels**.

Name

|

Type

|

Description  
  
||  
  
`targets`

|

array of objects

|

Each `host` and `port` from which to scrape metrics.  
  
`labels`

|

document

|

Document that contains the label and value that differentiates your metrics.  
  
### labels Embedded Document

Label

|

Description  
  
|  
  
`group_id`

|

Unique hexadecimal digit string that identifies the project.  
  
`group_name`

|

Human-readable label that identifies the project.  
  
`org_id`

|

Unique hexadecimal digit string that identifies the organization.  
  
`cluster_name`

|

Human-readable label that identifies the cluster.  
  
`replica_set_name`

|

Human-readable label that identifies the replica set.  
  
## Example Request

    
    
    curl --header 'Accept: application/json'  
      
    # Sets the `Authorization` header on every scrape request with the  
    # configured username and password.  
    --user prom_user_618d48e05277a606ed2496fe:fSIMUngfTmOTVEB4  
    # The URL that Prometheus fetches the targets from.  
    --request GET "https://cloud.mongodb.com/prometheus/v1.0/groups/618d48e05277a606ed2496fe/discovery"  
  
## Example Response

    
    
    [  
      
      {  
          "targets":[  
            "cluster1-shard-00-02.lvfy8.mongodb-dev.net:27018",  
            "cluster1-shard-00-00.lvfy8.mongodb-dev.net:27018",  
            "cluster1-shard-00-01.lvfy8.mongodb-dev.net:27018"  
          ],  
          "labels":{  
            "cluster_name":"Cluster1",  
            "group_id":"618d48e05277a606ed2496fe",  
            "group_name":"Cloud-Testing",  
            "org_id":"618d48ba5277a606ed2495ce",  
            "replica_set_name":"atlas-74dujs-shard-0"  
          }  
      }  
    ]  
  
← More API ResourcesCustom Role Actions →

