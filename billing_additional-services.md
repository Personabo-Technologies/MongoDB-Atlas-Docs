Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Additional Services

Share Feedback

On this page

  * Advanced Security
  * Private Endpoints
  * Database Auditing
  * Atlas App Services
  * Charts for Atlas
  * Atlas Online Archive
  * Support Plan

## Advanced Security

## Note

Atlas doesn't support advanced security options for serverless instances.

Atlas supports Encryption at Rest via customer KMS and LDAP User
Authentication and Authorization in Atlas projects and clusters.

Excluding MongoDB Atlas Enterprise and MongoDB Atlas Platinum customers, Atlas
charges a 15% uplift to the cost of each cluster with **LDAP User
Authentication and Authorization** and/or **Encryption at Rest via customer
KMS** enabled.

Configuring **LDAP User Authentication and Authorization** for a project
enables the feature for all clusters in the project. Configuring **Encryption
at Rest via customer KMS** for a project allows enabling/disabling the feature
on per cluster basis.

## Private Endpoints

MongoDB Atlas supports private endpoints.

AWS PrivateLink

Azure Private Link

Private Service Connect

MongoDB Atlas supports private endpoints on AWS using the AWS PrivateLink
feature.

Atlas charges you based on your usage across these dimensions:

  * Atlas Private Endpoint: The sum of the hourly costs incurred to host private endpoints in all AWS regions.

  * Atlas Private Endpoint Capacity Units: The sum of the hourly costs incurred to process traffic to private endpoints.

In addition to the costs Atlas charges you, AWS charges you for each VPC
interface endpoint you create. To ensure cluster availability in the event of
a widespread network outage, create VPC interface endpoints in at least two
availability zones per region. AWS also charges you for the data volume each
VPC interface endpoint processes.

## Tip

### See also:

AWS PrivateLink Pricing.

### Atlas Private Endpoint

Atlas charges hourly for each region to which you deploy a private endpoint.
The hourly cost varies by region.

### Atlas Private Endpoint Capacity Units

Additionally, Atlas charges you per hour based on the traffic that your
private endpoint processes. The hourly cost varies based on the amount of
traffic and the region to which your private endpoint is deployed.

Atlas private endpoint capacity units measure the dimensions on which the
Atlas private endpoint processes your traffic. The dimensions measured are:

  *  **New connections or flows** : Number of newly established connections or flows per second.

  *  **Active connections or flows** : Peak concurrent connections or flows, sampled per minute.

  *  **Processed bytes** : The number of bytes processed by the private endpoint in Gigabytes (GB).

For TCP traffic, an Atlas private endpoint capacity unit contains:

  *  **New connections or flows** : 800 new TCP connections per second.

  *  **Active connections or flows** : 100,000 active TCP connections (sampled per minute).

  *  **Processed bytes** : 1 GB per hour.

For UDP traffic, an Atlas private endpoint capacity unit contains:

  *  **New connections or flows** : 400 new UDP flows per second.

  *  **Active connections or flows** : 50,000 active UDP flows (sampled per minute).

  *  **Processed bytes** : 1 GB per hour.

For TLS traffic, an Atlas private endpoint capacity unit contains:

  *  **New connections or flows** : 50 new TLS connections or flows per second.

  *  **Active connections or flows** : 3,000 active TLS connections or flows (sampled per minute).

  *  **Processed bytes** : 1 GB per hour.

Atlas charges you only for the dimension that has the highest usage during
each hour across all traffic types.

## Example

This provides a breakdown of costs for one hour of TLS network traffic to a
private endpoint in the `us-east-1` region:

Dimension

|

Amount

|

Atlas Private Endpoint Capacity Units Consumed  
  
||  
  
New connections or flows

|

25

|

.50  
  
Active connections or flows

|

1500

|

.50  
  
Processed bytes

|

2.5 GB

|

2.5  
  
The **Processed bytes** dimension has the largest capacity unit consumption
rate. For this hour, Atlas charges you the following for using Atlas private
endpoint capacity units in the `us-east-1` region:

Capacity Units

|

Region Rate per Capacity Unit

|

Total  
  
||  
  
2.5

|

$0.0450

|

$0.1125  
  
### AWS PrivateLink Rates by Region

Atlas rates for using the AWS PrivateLink feature vary by region:

## Note

The rates listed below are in addition to what AWS charges you for each VPC
interface endpoint you create.

## Tip

### See also:

AWS PrivateLink Pricing.

AWS region

|

Hourly Cost per Private Endpoint

|

Cost per Atlas Private Endpoint Capacity Unit  
  
||  
  
`us-east-1` N. Virginia

|

$0.0450

|

$0.0120  
  
`us-east-2` Ohio

|

$0.0450

|

$0.0120  
  
`us-west-1` N. California

|

$0.0504

|

$0.0120  
  
`us-west-2` Oregon

|

$0.0450

|

$0.0120  
  
`ca-central-1` Canada

|

$0.0495

|

$0.0132  
  
`sa-east-1` Sao Paulo

|

$0.0680

|

$0.0165  
  
`eu-north-1` Stockholm

|

$0.0479

|

$0.0114  
  
`eu-west-1` Ireland

|

$0.0504

|

$0.0120  
  
`eu-west-2` London

|

$0.0529

|

$0.0120  
  
`eu-west-3` Paris

|

$0.0529

|

$0.0126  
  
`eu-central-1` Frankfurt

|

$0.0540

|

$0.0120  
  
`me-south-1` Bahrain

|

$0.0554

|

$0.0132  
  
`ap-northeast-1` Tokyo

|

$0.0486

|

$0.0120  
  
`ap-northeast-2` Seoul

|

$0.0450

|

$0.0120  
  
`ap-south-1` Mumbai

|

$0.0478

|

$0.0120  
  
`ap-southeast-1` Singapore

|

$0.0504

|

$0.0120  
  
`ap-southeast-2` Sydney

|

$0.0504

|

$0.0120  
  
`ap-east-1` Hong Kong

|

$0.0554

|

$0.0132  
  
## Database Auditing

Atlas supports database auditing. To learn more, see Set up Database Auditing.

Excluding MongoDB Atlas Enterprise and MongoDB Atlas Platinum customers, Atlas
charges a 10% uplift in the hourly cost of all dedicated clusters for projects
using Database Auditing.

## Atlas App Services

Atlas App Services applications may incur data transfer and compute costs for
each application in a project. If you have App Services applications in your
organization, your invoice includes these costs as a line item.

## Tip

### See also:

Atlas App Services Billing

## Charts for Atlas

Charts on Atlas is billed based on the volume of data transferred from the
Charts web server to web browser clients. Each Charts instance comes with a
free `1 GB` of data transfers per month. Once the `1 GB` of free data usage
has been consumed, all subsequent GBs of data transfers are billed at a fixed
rate.

## Tip

### See also:

Charts on Atlas Pricing.

## Atlas Online Archive

You may incur data transfer and compute costs for each Online Archive on your
Atlas cluster. If you have Online Archive configured on your cluster, your
Atlas invoice includes these costs as a line item.

## Tip

### See also:

Atlas pricing page

## Support Plan

If you have an upgraded support plan, the total support cost for the month is
listed in the Summary section of your invoice. Support cost line items are
listed in the Details section.

← GCP Self-Serve MarketplaceInternational Usage and Taxation →

