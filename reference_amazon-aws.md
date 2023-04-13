Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Amazon Web Services (AWS)

Share Feedback

On this page

  * Synopsis
  * Cluster Configuration Options
  * Amazon Availability Zones
  * Integrations
  * More Information

## Synopsis

Atlas supports deploying clusters and serverless instances onto Amazon Web
Services (AWS). Atlas supports all AWS regions other than some regions in
China and US GovCloud.

Atlas supports the following AWS regions. While all of the following regions
support `M10+` clusters, some regions don't support `M0` clusters, `M2/M5`
clusters, or serverless instances. A check mark indicates support for `M0`
clusters, `M2/M5` clusters, or serverless instances. The Atlas Region is the
corresponding region name used by the Atlas API.

Americas

Asia Pacific

Europe

Middle East and Africa

AWS Region

|

Location

|

Atlas Region

|

`M0` Support

|

`M2/M5` Support

|

Serverless Instance Support  
  
|||||  
  
`us-east-1`

|

Northern Virginia, USA

|

`US_EAST_1`

|

 __

|

 __

|

 __  
  
`us-west-2`

|

Oregon, USA

|

`US_WEST_2`

|

 __

|

 __

|

 __  
  
`ca-central-1`

|

Montreal, QC, Canada

|

`CA_CENTRAL_1`

|

|

|  
  
`us-east-2`

|

Ohio, USA

|

`US_EAST_2`

|

|

|  
  
`us-west-1`

|

Northern California, USA

|

`US_WEST_1`

|

|

|  
  
`sa-east-1`

|

Sao Paulo, Brazil

|

`SA_EAST_1`

|

 __

|

 __

|  
  
This page provides reference material related to Atlas cluster deployments on
AWS. The following options do not apply to serverless instances.

## Cluster Configuration Options

Each Atlas cluster tier comes with a default set of resources. Atlas provides
the following resource configuration options:

Custom Storage Size

    

The size of the server root volume. Atlas clusters deployed onto AWS use
general purpose SSDs [1].

## Note

### RAM Availability

The actual amount of RAM available to each cluster tier might be slightly less
than the stated amount, due to memory that the kernel reserves.

The following cluster tiers are available:

Instance Size

|

Default Storage

|

Default RAM  
  
||  
  
M0

|

.5 GB

|

Shared  
  
M2

|

2 GB

|

Shared  
  
M5

|

5 GB

|

Shared  
  
M10 __

|

10 GB

|

2 GB  
  
M20 __

|

20 GB

|

4 GB  
  
M30 __

|

40 GB

|

8 GB  
  
M40 __

|

80 GB

|

16 GB  
  
R40 __

|

80 GB

|

16 GB  
  
M40_NVME

|

380 GB

|

15.25 GB  
  
M50 __

|

160 GB

|

32 GB  
  
R50 __

|

160 GB

|

32 GB  
  
M50_NVME

|

760 GB

|

30.5 GB  
  
M60 __

|

320 GB

|

64 GB  
  
R60 __

|

320 GB

|

64 GB  
  
M60_NVME

|

1.6 TB

|

61 GB  
  
M80 __

|

760 GB

|

131 GB  
  
R80 __

|

750 GB

|

122 GB  
  
M80_NVME

|

1.6 TB

|

122 GB  
  
M100

|

1 TB

|

160 GB  
  
M140 __

|

1 TB

|

192 GB  
  
M200 __

|

1.5 TB

|

256 GB  
  
R200 __

|

1.5 TB

|

256 GB  
  
M200_NVME

|

3.1 TB

|

244 GB  
  
M300 ____

|

2 TB

|

384 GB  
  
R300 __

|

2 TB

|

384 GB  
  
R400 __

|

3 TB

|

488 GB  
  
M400_NVME

|

4 TB

|

512 GB  
  
R700

|

4 TB

|

768 GB  
  
 __Can use this tier for a multi-cloud cluster.

 __Unavailable in the **AP_SOUTHEAST_2** region.

## Note

### Cluster Tier & API Naming Conventions

For purposes of management with the Atlas Administration API, cluster tier
names that are prepended with `R` instead of an `M` (`R40` for example) run a
low-CPU version of the cluster. When creating or modifying a cluster with the
API, be sure to specify your desired cluster class by name with the
`providerSettings.instanceSizeName` attribute.

## Important

### Multi-Cloud Low-CPU clusters

Low-CPU cluster tiers (R40, R50, R60, etc) are available in multi-cloud
cluster configurations as long as the cluster tier is available for all the
regions that the cluster uses.

Workloads typically require less than `2TB`.

Custom Storage Speed

    

The input/output operations per second (IOPS) the system can perform.

Each cluster has a default IOPS rate. You can also choose to provision your
tier's IOPS rate to meet your particular needs.

The selected cluster tier and custom storage size dictate the maximum IOPS for
each storage speed.

Encrypted Storage Volumes

    Encrypts the root volume for data at rest inside the volume and all data moving between the volume and the cluster. Atlas uses Amazon EBS encryption.

## Amazon Availability Zones

Each AWS region includes a set number of independent availability zones.
Availability Zones consist of one or more discrete data centers, each with
redundant power, networking and connectivity, housed in separate facilities.
For regions that have at least three availability zones (3AZ), Atlas deploys
clusters across three availability zones. For regions that only have two
availability zones (2AZ), Atlas deploys clusters across two availability
zones.

The Atlas Add New Cluster form marks regions that support at least three
availability zones as Recommended, as they provide higher availability.

The number of availability zones in a region has no effect on the number of
MongoDB nodes Atlas can deploy. MongoDB Atlas clusters are always made of
replica sets with a minimum of three MongoDB nodes.

For more information on the number of availability zones in a given region,
see the Amazon documentation on global infrastructure.

For more information on AWS regions and availability zones, see the Amazon
documentation on using regions and availability zones

### Regions with at Least Three Availability Zones

Atlas clusters deployed in regions with at least three availability zones are
split across three availability zones. For example, a three node replica set
cluster would have one node deployed onto each availability zone.

click to enlarge

3AZ clusters have higher availability compared to 2AZ clusters. However, not
all regions support 3AZ clusters.

### Regions with Only Two Availability Zones

Atlas clusters deployed in regions with two availability zones are split
across the two availability zones. For example, a three node replica set
cluster would have two nodes deployed to one availability zone and the
remaining node deployed to the other availability zone.

click to enlarge

2AZ clusters have a higher chance of loss of availability in the event of the
loss of an availability zone than 3AZ clusters. However, where latency or
location are a priority, a region that supports 2AZ clusters may be preferred.

[1]|  For detailed documentation on Amazon storage options, see Amazon EBS
Volume Types  
|  
  
## Integrations

Along with global region support, the following product integrations enable
applications running on AWS, such as Amazon EC2, AWS Lambda, and Amazon
Elastic Container Service (ECS), to use Atlas instances easily and securely.

### Networking Services

  * AWS PrivateLink: Set up private endpoints with AWS

  * AWS Virtual Private Cloud (VPC): Set up network peering connections with AWS

### Security and Identity Services

  * AWS Identity Access Management (IAM) Configure database users with IAM authentication

  * AWS Key Management Service (KMS):

    * Configure Atlas disk encryption with KMS

    * Configure client-side field level encryption with KMS

  * AWS SSO: Configure federated authentication to the MongoDB UI

### Other AWS Services

  * AWS CloudFormation: Deploy and manage Atlas from CloudFormation

  * AWS EventBridge: Send Atlas trigger events to AWS EventBridge

  * Amazon Kinesis: Send data to Atlas via Kinesis Data Firehose

  * AWS S3: Configure Atlas Data Federation to query data from S3

### Procurement

  * AWS Marketplace: Pay for Atlas usage via AWS

## More Information

For more information on how to use AWS with Atlas most effectively, review the
following best practices, guides, and case studies:

  * AWS App Runner: Build Applications and APIs Faster with MongoDB Atlas and AWS App Runner

  * AWS Lambda: Best Practices Connecting from AWS Lambda

← Cloud ProvidersGoogle Cloud Platform (GCP) →

