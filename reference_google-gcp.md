Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Google Cloud Platform (GCP)

Share Feedback

On this page

  * Synopsis
  * Cluster Configuration Options
  * GCP Zones
  * Integrations
  * More Information

## Synopsis

Atlas supports deploying clusters onto Google Cloud Platform (GCP). This page
provides reference material related to Atlas cluster deployments on Google
Cloud.

Depending on your cluster tier, Atlas supports the following Google Cloud
regions. While all of the following regions support `M10+` clusters, some
regions don't support Free or Shared-Tier clusters. A check mark indicates
support for Free or Shared-Tier clusters. The Atlas API uses the corresponding
Atlas Region.

Americas

Asia Pacific

Europe

Google Cloud Region

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
  
`us-central1`

|

Iowa, USA

|

`CENTRAL_US`

|

 __

|

 __

|

 __  
  
`us-east1`

|

South Carolina, USA

|

`EASTERN_US`

|

|

|  
  
`us-east4`

|

North Virginia, USA

|

`US_EAST_4`

|

|

|  
  
`northamerica-northeast1`

|

Montreal, Canada

|

`NORTH_AMERICA_NORTHEAST_1`

|

|

|  
  
`northamerica-northeast2`

|

Toronto, Canada

|

`NORTH_AMERICA_NORTHEAST_2`

|

|

|  
  
`southamerica-east1`

|

Sao Paulo, Brazil

|

`SOUTH_AMERICA_EAST_1`

|

|

|  
  
`southamerica-west1`

|

Santiago, Chile

|

`SOUTH_AMERICA_WEST_1`

|

|

|  
  
`us-west1`

|

Oregon, USA

|

`WESTERN_US`

|

|

|  
  
`us-west2`

|

Los Angeles, CA, USA

|

`US_WEST_2`

|

|

|  
  
`us-west3`

|

Salt Lake City, UT, USA

|

`US_WEST_3`

|

|

|  
  
`us-west4`

|

Las Vegas, NV, USA

|

`US_WEST_4`

|

|

|  
  
## Cluster Configuration Options

Each Atlas cluster tier comes with a default set of resources. Atlas provides
the following resource configuration options.

### Custom Storage Size

Storage size reflects the size of the server root volume. Atlas clusters
deployed onto Google Cloud use SSD persistent storage [1].

## Note

### RAM Availability

The actual amount of RAM available to each cluster tier might be slightly less
than the stated amount, due to memory that the kernel reserves.

The following cluster tiers are available:

Cluster Tiers

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

1.7 GB  
  
M20 __

|

20 GB

|

3.8 GB  
  
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
  
R40 ____

|

80 GB

|

16 GB  
  
M50 __

|

160 GB

|

32 GB  
  
R50 ____

|

160 GB

|

32 GB  
  
M60 __

|

320 GB

|

64 GB  
  
R60 ____

|

320 GB

|

64 GB  
  
M80 __

|

750 GB

|

128 GB  
  
R80 ____

|

750 GB

|

128 GB  
  
M140 __

|

1000 GB

|

192 GB  
  
M200 __

|

1500 GB

|

256 GB  
  
R200 ____

|

1500 GB

|

256 GB  
  
M250 __

|

1750 GB

|

320 GB  
  
M300 ____

|

2000 GB

|

360 GB  
  
R300 ____

|

2000 GB

|

384 GB  
  
R400 ____

|

3000 GB

|

512 GB  
  
R600 __

|

4096 GB

|

640 GB  
  
 __Can use this tier for a multi-cloud cluster.

 __Unavailable in the following regions:

  * `AUSTRALIA_SOUTHEAST_1`

  * `EUROPE_WEST_3`

  * `NORTHEASTERN_ASIA_PACIFIC`

  * `SOUTH_AMERICA_EAST_1`

  * `EUROPE_WEST_8`

  * `EUROPE_WEST_9`

  * `EUROPE_SOUTHWEST_1`

 __ Atlas limits **R** -class instances to the following regions:

#### Americas

  * `CENTRAL_US`

  * `EASTERN_US`

  * `US_EAST_4`

  * `WESTERN_US`

  * `US_WEST_3`

  * `US_WEST_4`

  * `NORTH_AMERICA_NORTHEAST_1`

  * `NORTH_AMERICA_NORTHEAST_2`

  * `SOUTH_AMERICA_EAST_1`

#### Asia Pacific

  * `ASIA_EAST_2`

  * `ASIA_NORTHEAST_2`

  * `ASIA_NORTHEAST_3`

  * `ASIA_SOUTH_1`

  * `ASIA_SOUTHEAST_2`

  * `EASTERN_ASIA_PACIFIC`

  * `NORTHEASTERN_ASIA_PACIFIC`

  * `SOUTHEASTERN_ASIA_PACIFIC`

#### Europe

  * `WESTERN_EUROPE`

  * `EUROPE_NORTH_1`

  * `EUROPE_WEST_2`

  * `EUROPE_WEST_3`

  * `EUROPE_WEST_4`

  * `EUROPE_WEST_6`

  * `EUROPE_WEST_8`

  * `EUROPE_WEST_9`

  * `EUROPE_SOUTHWEST_1`

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

Workloads typically require less than `2TB` of storage.

Atlas configures the following resources automatically and does not allow user
modification:

  * Storage Speed

  * Encrypted Storage Volumes

#### Storage Speed

Storage speed is the number of input/output operations per second (IOPS) [1]
that the system performs. This value is fixed at:

  * 30 IOPS per GB for reads

  * 30 IOPS per GB for writes, for a total of 60 IOPS per GB

For example, an `M30` cluster with 40 GB of default storage has a maximum read
speed of 1,200 IOPS and a maximum write speed of 1,200 IOPS. If you increase
the storage size to 100 GB per cluster, this increases the maximum read speed
by 3,000 IOPS and a maximum write speed by 3,000 IOPS.

#### Encrypted Storage Volumes

Google Cloud storage volumes are always encrypted.

## GCP Zones

Each Google Cloud region includes a set number of independent zones. Each zone
has power, cooling, networking, and control planes that are isolated from
other zones.

For regions that have multiple zones, such as 2Z (for two zones) or 3Z (for 3
zones), Atlas deploys clusters across these zones.

The Atlas Add New Cluster form marks regions that support 3Z clusters as
Recommended, as they provide higher availability.

For general information on Google Cloud regions and zones, see the Google
documentation on regions and zones.

The number of zones in a region has no effect on the number of MongoDB nodes
Atlas can deploy. MongoDB Atlas clusters are always made of replica sets with
a minimum of three MongoDB nodes.

### Regions with at Least Three Zones

If the selected Google Cloud region has at least three zones, Atlas clusters
are split across three zones. For example, a three node replica set cluster
would have one node deployed onto each zone.

click to enlarge

3Z clusters have higher availability compared to 2Z clusters. However, not all
regions support 3Z clusters.

[1]|  _(1, 2)_ For detailed documentation on Google storage options, see
Storage Options.  
|  
  
## Integrations

Along with global region support, the following product integrations enable
applications running on Google Cloud, such as Google Compute Engine, Google
Cloud Functions, Google Cloud Run, and Google App Engine, to use Atlas
instances easily and securely.

### Networking Services

  * Google Virtual Private Cloud (VPC): Set up network peering connections with GCP

### Security and Identity Services

  * Google Identity: Sign up and log into Atlas with Google

  * Google Cloud Key Management Service (KMS):

    * Configure Atlas disk encryption with KMS

    * Configure client-side field level encryption with KMS

### Procurement

  * GCP Marketplace: Pay for Atlas usage via GCP

## More Information

For more information on how to use Google Cloud with Atlas most effectively,
review the following best practices, guides, and case studies:

  * Case Study: Why build apps on a cloud-native database like MongoDB Atlas?

  * Google Data Stream: Streamline your real-time data pipeline with Datastream and MongoDB

← Amazon Web Services (AWS)Microsoft Azure →

