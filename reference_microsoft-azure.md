Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Microsoft Azure

Share Feedback

On this page

  * Synopsis
  * Cluster Configuration Options
  * Azure Availability Zones
  * Azure Fault Domains
  * Integrations
  * More Information

## Synopsis

Atlas supports deploying clusters and serverless instances onto Microsoft
Azure. This section applies to Atlas database deployments on Azure.

Depending on your cluster tier, Atlas supports the following Azure regions. A
check mark indicates support for free clusters, shared clusters, serverless
instances, or Availability Zones. The Atlas Region is the corresponding region
name used by Atlas processes.

While all of the following regions support `M10+` clusters, some regions don't
support free clusters, shared clusters, or serverless instances.

## Important

We recommend that you use the regions marked by an asterisk ( __) in the
following table as a secondary disaster recovery (DR) region only in amulti-
region cluster because these regions cost higher than the other regions in the
table.

Also, these regions might not be available in your Azure environments without
approval from Azure support. If you want to leverage private networking
options, such as VNet peering or private endpoints, with a cluster deployed in
one or more of these regions, you must allow your Azure subscription to create
resources in these regions. To learn more, contact Azure support.

Americas

Europe

Asia Pacific

Africa

Middle East

Azure Region

|

Location

|

Atlas Region

|

`M0` Support

|

`M2/M5` Support

|

`M10+` Support

|

Serverless Instances

|

Availability Zones  
  
|||||||  
  
`centralus`

|

Iowa, USA

|

`US_CENTRAL`

|

|

|

 __

|

|

 __  
  
`eastus`

|

Virginia (East US)

|

`US_EAST`

|

|

|

 __

|

 __

|

 __  
  
`eastus2`

|

Virginia, USA

|

`US_EAST_2`

|

 __

|

 __

|

 __

|

|

 __  
  
`northcentralus`

|

Illinois, USA

|

`US_NORTH_CENTRAL`

|

|

|

 __

|

|  
  
`westus`

|

California, USA

|

`US_WEST`

|

 __

|

 __

|

 __

|

|  
  
`westus2`

|

Washington, USA

|

`US_WEST_2`

|

|

|

 __

|

|

 __  
  
`westus3`

|

Arizona, USA

|

`US_WEST_3`

|

|

|

 __

|

|

 __  
  
`westcentralus`

|

Wyoming, USA

|

`US_WEST_CENTRAL`

|

|

|

 __

|

|  
  
`southcentralus`

|

Texas, USA

|

`US_SOUTH_CENTRAL`

|

|

|

 __

|

|

 __  
  
`brazilsouth`

|

Sao Paulo, Brazil

|

`BRAZIL_SOUTH`

|

|

|

 __

|

|

 __  
  
`brazilsoutheast` __

|

Rio de Janeiro, Brazil

|

`BRAZIL_SOUTHEAST`

|

|

|

 __

|

|  
  
`canadaeast`

|

Quebec City, QC, Canada

|

`CANADA_EAST`

|

|

|

 __

|

|  
  
`canadacentral`

|

Toronto, ON, Canada

|

`CANADA_CENTRAL`

|

 __

|

 __

|

 __

|

|

 __  
  
## Cluster Configuration Options

Each Atlas cluster tier comes with a default set of resources. Atlas provides
the following resource configuration options:

Custom Storage Size

    

The size of the server root volume. Atlas clusters deployed onto Azure use
premium SSDs. [1]

## Note

### RAM Availability

The actual amount of RAM available to each cluster tier might be slightly less
than the stated amount, due to memory that the kernel reserves.

## Note

As of October 18, 2021, the following Atlas clusters deployed to Azure offer
16,000 IOPS (up from 7,500) and 500 MB/second throughput (up from 250
MB/second):

  * New clusters with 4 TB storage volumes.

  * Existing clusters that you scale up to 4 TB storage volumes.

The following clusters tiers are available:

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

8 GB

|

2 GB  
  
M20 __

|

16 GB

|

4 GB  
  
M30 __

|

32 GB

|

8 GB  
  
M40 __

|

64 GB

|

16 GB  
  
R40 __

|

128 GB

|

16 GB  
  
M50 __

|

128 GB

|

32 GB  
  
R50 __

|

128 GB

|

32 GB  
  
M60 __

|

128 GB

|

64 GB  
  
M60_NVME

|

1600 GB

|

64 GB  
  
R60 __

|

128 GB

|

64 GB  
  
M80 __

|

256 GB

|

128 GB  
  
R80 __

|

256 GB

|

128 GB  
  
M80_NVME

|

1600 GB

|

128 GB  
  
M200 __

|

256 GB

|

256 GB  
  
R200 __

|

256 GB

|

256 GB  
  
M200_NVME

|

3100 GB

|

256 GB  
  
R300 ____

|

512 GB

|

384 GB  
  
M300_NVME

|

3600 GB

|

384 GB  
  
R400 __

|

512 GB

|

432 GB  
  
M400_NVME

|

4000 GB

|

512 GB  
  
M600_NVME

|

4000 GB

|

640 GB  
  
 __Can use this tier for a multi-cloud cluster.

 __Not available in the following regions:

  *  **germanywestcentral**

  *  **switzerlandnorth**

  *  **switzerlandwest**

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

NVMe clusters don't support multi-cloud cluster configurations.

Atlas configures the following resources automatically and does not allow user
modification:

Storage Speed

    The input/output operations per second (IOPS) [1] the system can perform. This value is fixed based on the specified custom storage size.
Encrypted Storage Volumes

    Azure storage volumes are always encrypted.

## Azure Availability Zones

Azure maintains multiple data centers within each region. Azure groups the
data centers into availability zones, which are separate locations within the
region. Maintaining data centers in different physical locations helps Azure
tolerate local failures.

Azure availability zones aren't available in all regions. To learn which Azure
regions maintain availability zones, see the Azure Region table. In regions
where availability zones aren't yet available, Azure uses fault domains to
help ensure failure tolerance.

Atlas uses Azure availability zones automatically when you deploy a dedicated
cluster to a region that supports them. Atlas splits the cluster's nodes
across availability zones. For example, a three-node replica set cluster would
have one node deployed onto each zone. A local failure in the Azure data
center hosting one node doesn't impact the operation of data centers hosting
the other nodes.

## Note

Regions with availability zones provide higher uptime for dedicated clusters
deployed after September 12, 2019. Clusters deployed before September 13, 2019
to regions that now offer availability zones aren't split across availability
zones automatically. To learn more about availability zones, see Azure's
documentation.

## Azure Fault Domains

Each Azure region includes a set number of fault domains for failure
tolerance. Fault domains consist of a group of virtual machines that share a
common power source and network switch. If you deploy your cluster to a region
that doesn't support availability zones, Atlas spreads the nodes across the
fault domains instead.

Atlas uses availability sets to deploy clusters across fault domains. For
regions that have at least three fault domains (3FD), Atlas deploys clusters
across three fault domains. For regions that only have two fault domains
(2FD), Atlas deploys clusters across two fault domains.

The Atlas Add New Cluster form marks regions that support 3FD clusters as
Recommended, as they provide higher availability.

The number of fault domains in a region has no effect on the number of MongoDB
nodes Atlas can deploy. MongoDB Atlas clusters are always made of replica sets
with a minimum of three MongoDB nodes.

For general information on Azure fault domains and availability sets, see
Availability Sets Overview

### Regions with at Least Three Fault Domains

If the selected Azure region has at least three fault domains, Atlas clusters
are split across three fault domains. For example, a three node replica set
cluster would have one node deployed onto each zone.

click to enlarge

3FD clusters have higher availability compared to 2FD clusters. However, not
all regions support 3FD clusters.

### Regions with Only Two Fault Domains

If the selected Azure region has two fault domains, Atlas clusters are split
across the two fault domains. For example, a three node replica set cluster
would have two nodes deployed to one zone and the remaining node deployed to
the other zone.

click to enlarge

2FD clusters have a higher chance of loss of availability in the event of the
loss of an zone than 3FD clusters. However, where latency or location are a
priority, a region that supports 2FD clusters may be preferred.

[1]|  _(1, 2)_ For detailed documentation on Azure storage options, see High-
performance Premium Storage and managed disks for VMs  
|  
  
## Integrations

Along with global region support, the following product integrations enable
applications running on Azure, such as Azure Virtual Machines, Azure
Functions, and Azure Container Instances, to use Atlas instances easily and
securely.

### Networking Services

  * Azure Virtual Network: Set up network peering connections with Azure

  * Azure Private Link: Set up private endpoints with Azure

  * Azure Key Vault:

    * Configure Atlas disk encryption with Key Vault

    * Configure client-side field level encryption with Key Vault

### Security and Identity Services

  * Azure Active Directory (AD): Configure federated authentication to the MongoDB UI

  * Azure Active Directory Domain Services: Configure database user authentication and authorization

### Integrations with other Azure Services

  * Azure Databricks: Read and write to Atlas using Databricks and Apache Spark

  * Azure Data Factory: Copy data from or to MongoDB Atlas using Azure Data Factory or Synapse Analytics

## More Information

For more information on how to use Azure with Atlas most effectively, review
the following best practices, guides, and case studies:

  * Power BI Desktop: Connect to Atlas from Power BI Desktop

  * Visual Studio (VS) Code: Work with MongoDB from VS Code

← Google Cloud Platform (GCP)Limitations →

