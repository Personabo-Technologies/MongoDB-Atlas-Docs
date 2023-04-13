Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Changelog

Share Feedback

On this page

  * 2023 Releases
  * 2022 Releases
  * 2021 Releases
  * 2020 Releases
  * 2019 Releases
  * 2018 Releases

## 2023 Releases

### 15 February 2023 Release

  * Supports simulating an outage for Atlas for regions that contain a majority of database nodes, and reconfiguring a cluster from an unhealthy to a healthy state in the event of such an outage.

  * Supports connecting to your database behind private endpoints with an optimized SRV connection string for sharded clusters.

  * Adds a streamlined experience for users deploying their first Atlas database using templates for best practices.

  * Adds EU region support for the PagerDuty integration.

### 25 January 2023 Release

Supports converting shared clusters (`M0`, `M2`, `M5`) to serverless
instances.

## 2022 Releases

## Important

On 17 March 2022, MongoDB Atlas moved to Let's Encrypt as the new Certificate
Authority for TLS certificates for `cloud.mongodb.com`. For more information,
see FAQ: Security.

### 14 December 2022 Release

  * Adds the ability to configure some Atlas project limits using the Projects Administration API resource.

  * Adds the ability to push live migrations of replica sets using private endpoints.

  * Introduces Atlas Goto.

### 16 November 2022 Release

  * Adds the ability to simulate a regional outage for Atlas.

### 26 October 2022 Release

  * Introduces Termination Protection for database deployments.

  * Adds a project setting that lets you configure some M40+ clusters with greater maximum storage than the standard limit.

  * Adds the Set Oplog Size UI configuration setting. This setting allows you to set the minimum retention window for Oplog entries. You can see the Set Oplog Size configuration setting in the UI only if you previously configured it for your cluster. For all new clusters, set the Minimum Oplog Window instead.

### 05 October 2022 Release

  * Adds three more Google Cloud Platform (GCP) regions:

    * `europe-west8` (Milan, Italy)

    * `europe-west9` (Paris, France)

    * `europe-southwest1` (Madrid, Spain)

  * Adds the ability to automatically copy backup snapshots to other regions.

  * Improves the memory utilization calculation used to auto-scale clusters.

### 14 September 2022 Release

  * Introduces the Local NVMe SSD storage option in the Atlas UI for some dedicated clusters that run on Azure. Locally attached ephemeral NVMe SSDs offer the highest level of speed and performance. To learn more, see NVMe Storage.

  * Adds the `enableSharding` privilege to custom database roles.

  * Adds the ability to set the maximum lifetime of multi-document transactions per cluster.

### 24 August 2022 Release

  * Supports Azure Private Link for serverless instances. To learn more, see Set Up a Private Endpoint for a Serverless Instance.

  * Enhancements to the Atlas billing experience for tax invoices.

### 3 August 2022 Release

  * Introduces analytics node tiers.

  * Adds support for VPC peering for Prometheus monitoring integration.

  * Adds support for VPC peering for Live Migrate (Push).

  * Disallows Atlas clusters on MongoDB 5.0+ from configuring a default read concern of `available`.

### 19 July 2022 Release

  * Introduces the General Availability of MongoDB 6.0.

### 01 June 2022 Release

  * Introduces the General Availability of Atlas serverless instances, which includes the following changes:

    * Supports AWS PrivateLink connections

    * Adds continuous backup

    * Reduces RPU and WPU pricing

  * Supports using GitHub credentials to sign in to MongoDB Cloud.

  * Adds support for MongoDB 6.0 Release Candidate. Atlas will upgrade the cluster to the stable release version when it is generally available.

To learn more about the changes in MongoDB 6.0, see the Release Notes.

### 11 May 2022 Release

  * Adds additional privileges to custom database roles.

  * Adds the `OPLOG_REPLICATION_LAG_TIME` host measurement series to the Measurements Administration API resource.

  * Updates PagerDuty integration to use the PagerDuty Events API v2.

### 20 April 2022 Release

  * Supports new AWS region: `ap-southeast-3` (Jakarta, Indonesia).

  * Supports new Google Cloud region: `southamerica-west1` (Santiago, Chile).

  * Supports new Azure regions:

    * `australiacentral` (Canberra, Australia)

    * `australiacentral2` (Canberra, Australia)

    * `francesouth` (Marseille, France)

    * `norwaywest` (Stavanger, Norway)

    * `swedencentral` (Gävle, Sweden)

    * `swedensouth` (Staffanstrop, Sweden)

    * `southafricawest` (Cape Town, South Africa)

    * `brazilsoutheast` (Rio de Janeiro, Brazil)

    * `westus3` (Arizona, USA)

  * Introduces deploying Low-CPU Atlas clusters into additional Google Cloud regions:

    * `europe-west3` (Frankfurt, Germany)

    * `europe-west6` (Zurich, Switzerland)

    * `northamerica-northeast1` (Montreal, Canada)

    * `northamerica-northeast2` (Toronto, Canada)

    * `asia-east2` (Hong Kong, China)

    * `asia-northeast2` (Osaka, Japan)

    * `asia-northeast3` (Seoul, South Korea)

    * `asia-southeast2` (Jakarta, Indonesia)

    * `europe-north1` (Finland)

    * `asia-south1` (Mumbai, India)

    * `southamerica-east1` (São Paulo, Brazil)

    * `us-west3` (Salt Lake City, UT, USA)

    * `us-west4` (Las Vegas, NV, USA)

  * Spreads newly deployed clusters in the following Azure regions across three availability availability zones:

    * `brazilsouth` (São Paulo, Brazil)

    * `eastasia` (Hong Kong, China)

    * `norwayeast` (Oslo, Norway)

    * `centralindia` (Pune, India)

    * `koreacentral` (Seoul, South Korea)

  * Spreads newly deployed clusters in the following AWS regions across three availability zones:

    * `ca-central-1` (Montreal, QC, Canada)

    * `ap-south-1` (Mumbai, India)

    * `ap-northeast-2` (Seoul, South Korea)

    * `sa-east-1` (São Paulo, Brazil)

    * `ap-northeast-1` (Tokyo, Japan)

  * Supports online archive data expiration. This feature is in preview.

  * Fixes existing behavior where Metrics Chart only shows the duration for which data is available.

### 31 March 2022 Release

  * Adds support for upgrading shared tiers through the Atlas Administration API.

  * Adds support for managing project settings through the Atlas Administration API.

### 9 March 2022 Release

  * Introduces a metrics integration with Prometheus.

  * Introduces a new `Project Search Index Editor` role to manage Atlas Search indexes using the Atlas UI or Administration API.

  * Introduces the ability to configure Federated Authentication with the Atlas Administration API.

  * Introduces the M140 and M250 cluster tiers in all GCP regions.

### 16 February 2022 Release

  * Upgrades free (`M0`) and shared (`M2` and `M5`) clusters to MongoDB 5.0.

  * Defaults new clusters to MongoDB 5.0.

### 26 January 2022 Release

  * Adds support for the Toronto, Canada (`NORTH_AMERICA_NORTHEAST_2`) Google Cloud region.

  * Introduces an alerts integration with Microsoft Teams.

  * Increases the memory for new `M30` to `M200` for Google Cloud clusters.

### 19 January 2022 Release

  * Adds support for MongoDB 5.2.

### 05 January 2022 Release

  * Improves the credits table in the Cloud Billing console.

  * Changes how the MongoDB Agent rotates `mongosqld` logs to copy and truncate.

## 2021 Releases

### 15 December 2021 Release

  * Adds the ability to link an AWS Billing Account to your MongoDB Atlas account.

### 2 December 2021 Release

  * Adds the ability to assign a built-in role, multiple custom roles, and multiple specific privileges to a single database user.

  * Introduces a new specific privilege, killOpSession.

  * Adds the ability to revoke temporary infrastructure access to MongoDB Support.

  * Changes the default recipients for billing alerts if you don't provide a billing email address.

### 17 November 2021 Release

  * Adds support for Google Private Service with Atlas Private Endpoints via the console.

  * Introduces the ability to export backup snapshots to their own Amazon S3 buckets on-demand via the API.

  * Adds support for time-series collections for Atlas Online Archive.

### 11 November 2021 Release

  * Adds support for MongoDB 5.1.

### 27 October 2021 Release

  * Supports the use of Security Key and Biometrics as a multi-factor authentication option.

  * Supports zstd as a compression standard for clusters on MongoDB 4.2 and later.

### 18 October 2021 Release

  * Supports `M0` free clusters and `M2/M5` shared clusters in the following regions:

    * AWS Tokyo (`ap-northeast-1`)

    * AWS Stockholm (`eu-north-1`)

    * AWS Bahrain (`me-south-1`)

    * Google Cloud Jakarta (`asia-southeast2`)

    * Google Cloud Seoul (`asia-northeast3`)

  * Supports increased throughput for 4 TB volumes on Azure. The following Atlas clusters deployed to Azure now offer 16,000 IOPS (up from 7,500) and 500 MB/second throughput (up from 250 MB/second):

    * New clusters with 4 TB storage volumes.

    * Existing clusters that you scale up to 4 TB storage volumes.

### 06 October 2021 Release

  * Supports Google Private Service with Atlas Private Endpoints via the API.

  * Supports the following GCP regions:

    * `asia-south2` (Delhi, India)

    * `australia-southeast2` (Melbourne, Australia)

    * `europe-central2` (Warsaw, Poland)

  * Adds support for cluster tier auto-scaling to low-CPU class clusters.

  * Enables cluster tier auto-scaling by default for all new Atlas clusters created via the web interface.

  * Supports using Live Migration from Ops Manager or Cloud Manager for MongoDB deployments running MongoDB 5.0.

  * Introduces metrics alerts for Atlas serverless instances.

  * For Cross-Organization Billing customers, Atlas now allocates subscription charges across all linked organizations in proportion to spend.

### 15 September 2021 Release

  * Supports Osaka, Japan (ap-northeast-3) AWS region.

  * Introduces serverless instances into additional GCP regions:

    * Iowa (CENTRAL_US)

    * Belgium (WESTERN_EUROPE)

  * Introduces serverless instances into additional AWS regions:

    * Oregon (US_WEST_2)

    * Mumbai (AP_SOUTH_1)

    * Sydney (AP_SOUTHEAST_2)

  * Adds 10 second granularity cluster metrics for all dedicated clusters in projects with at least one `M40+` cluster.

  * Adds support for time series collections in Data Explorer and Query Profiler.

  * Introduces the ability to create new time series collections and build secondary indexes from the UI.

  * Introduces the ability to visualize slow queries in times series collections.

  * Introduces the ability to deploy `M0` free clusters using the create endpoint.

### 25 August 2021 Release

  * Introduces serverless instances into the following Azure regions:

    * Virginia (US_EAST_2)

    * Netherlands (EUROPE_WEST)

  * Adds metrics that report maximum observed values, in 60-second intervals, for all hardware metrics.

  * Adds the ability to specify Sort, Project, and Collation query options when you query your data using the Atlas UI.

  * Adds the ability for a user with the `Project Cluster Manager` role to test failover.

### 03 August 2021 Release

  * Increases the maximum number of provisioned IOPS for clusters `M140` and up on AWS to 64,000 IOPS.

  * Introduces embedded data visualizations on the Billing Overview page and within each invoice.

  * Lowers data transfer rates within the following AWS regions:

    * Tokyo

    * Sydney

    * Bahrain

    * São Paulo

  * Spreads newly deployed clusters in the South Central US Azure region across three availability zones.

  * Introduces the ability to set an Atlas user account to be granted the `Project Owner` role on a specified project via the API.

  * Removes IP Whitelist resources. The IP Access List resource replaces the whitelist resource. We encourage you to update your applications to use this new resource.

  * Removes the API Key Whitelist endpoints. The API Key Access List endpoints replace the whitelist endpoints. We encourage you to update your applications to use these new endpoints.

  * Introduces email verification for all new Atlas user registrations.

### 13 July 2021 Release

  * Introduces the general availability of MongoDB 5.0, which includes support for:

    * Time Series collections,

    * Live Re-Sharding,

    * the Versioned API,

    * Client Side Field Level Encryption via AWS KMS, Google Cloud KMS and Azure Key Vault,

    * and more.

  * Introduces serverless instances as a new database deployment option in Atlas, available in preview.

  * Introduces the general availability of the new MongoDB Shell.

  * Updates the Atlas Uptime SLA to apply to `M10+` clusters.

  * Introduces MongoDB Atlas for Government, approved as FedRAMP Ready for Agency Authorization in AWS GovCloud (US) and AWS US East/West regions.

  * Introduces the ability to deploy and Manage MongoDB Atlas from AWS CloudFormation using the newly generally available AWS CloudFormation Public Registry.

  * Introduces new hardware-level metrics for Disk Queue Depth.

### 23 June 2021 Release

  * Removes Personal API keys. Personal API Keys reached End of Life (EOL) on March 1, 2021. Communications sent beginning 2 years before this date notified users. We encourage you to use Programmatic API Keys.

### 11 May 2021 Release

  * Introduces a search tester UI to run queries and see results for Atlas Search.

  * Introduces Atlas Global Clusters support for using a unique compound index as a shard key and using a compound shard with a hashed second field.

  * Introduces the ability for Data Federation to target cluster analytics nodes for federated queries.

### 21 April 2021 Release

  * Adds more IOPS and more consistent throughput to standard storage for Atlas clusters on AWS at no extra cost.

  * Introduces trial version of the MongoDB Atlas Kubernetes Operator.

  * Adds an easy MongoDB CLI quickstart command to get started with Atlas.

### 30 March 2021 Release

  * Supports using Realm in multi-cloud clusters.

### 09 March 2021 Release

  * Introduces a new Data Federation onboarding experience.

  * Adds API support for multi-cloud clusters.

  * Incorporates database and collection name drop-down menus in the Atlas Search index builder.

  * Supports recommendations to remove redundant indexes in Monitor and Improve Slow Queries.

  * Adds alert options for Disk IOPS and Disk Latency on Atlas.

  * Disables the ability to deploy new MongoDB 3.6 clusters.

  * Adds the ability to proactively change a cluster's TLS certificate root CA in order to test readiness ahead of the Let's Encrypt planned root CA change from IdenTrust to ISRG. All Atlas clusters' certificates will be migrated to the ISRG root CA between May and September of this year.

### 17 February 2021 Release

  * Introduces additional Asia Pacific Live Migrations regions in Singapore, Mumbai, and Tokyo.

  * Makes the M400 NVMe cluster tier available in all major AWS regions.

  * Enhances Maintenance Windows:

    * Can auto-defer maintenance by one week.

    * Displays the current and target maintenance database version when maintenance includes a version upgrade.

  * Spreads newly deployed clusters in the following Azure regions across three availability zones:

    * Germany West Central

    * South Africa North

    * Australia East

  * Supports cluster tier auto-scaling for multi-cloud clusters.

  * Improves Data Explorer load times.

### 26 January 2021 Release

  * Introduces private network access for multi-cloud clusters.

  * Atlas free clusters ( **M0** ) and shared clusters ( **M2** / **M5** ) upgraded to MongoDB 4.4.

  * Defaults new clusters to MongoDB 4.4.

  * Introduces custom archiving rules for Atlas Online Archive.

  * Introduces the ability to use an AWS IAM role to authorize Atlas to access:

    * AWS KMS encryption keys for customer key management, or

    * S3 buckets for federated database instances.

  * Introduces the ability to peer to Atlas VPCs on Google Cloud with a smaller CIDR block. When you create the network peering container using the Atlas API, you can specify a CIDR block between `/21` and `/24`, inclusive, insead of the default, `/18`.

  * Adds the ability to specify an AWS ARN with a compound path when you create an AWS IAM-authenticated database user.

### 06 January 2021 Release

  * Changes the cluster-level navigation UI so that Atlas Search is now a top level tab.

  * Introduces a visual editor for creating an Atlas Search index.

  * Allows users of the BI Connector for Atlas to download BI Connector logs.

## 2020 Releases

### 15 December 2020 Release

  * Introduces an optional connection string for Atlas Online Archive that enables querying of archived data only (instead of the union of cluster and archive data).

  * Enables Multi-Cloud Clusters to be used with the following:

    * Global Clusters

    * Bring Your Own Key Management Service (KMS) for Encryption at Rest

    * Low-CPU cluster tiers

  * Introduces improvements to the Billing Invoice Summary table including a summary of usage by top line product categories.

  * Introduces Voice and SMS Factors as options for use with Okta MFA.

### 30 November 2020 Release

  * Supports Customer Federation Role Mappings for users of Identity Federation with SAML.

  * Supports passwordless X.509 authentication for database users on `M0`, `M2`, and `M5` clusters.

  * Releases Atlas Online Archive to general availability.

### 23 November 2020 Release

  * Offers self-serve customers the option to sign up for Atlas Pro support.

  * Introduces Low-CPU clusters into additional Google Cloud regions: `us-east1` (South Carolina), `us-east4` (Virginia), and `australia-southeast1` (Sydney).

  * Introduces availability zones for new clusters in the Azure Canada Central region.

  * Introduces a new project setting for advanced multi-region private endpoint use.

    * The project setting requires that all clusters in a project be sharded clusters. When enabled, customers are able to configure multiple private endpoints in multiple regions and connect via regionalized connection strings.

    * When this setting is disabled (the default), only a single private endpoint can be created per region for a multi-region project. (For a single region project, multiple private endpoints have always been supported.)

  * Updates terminology for API Access List management. Introduces API Access List for Programmatic API Keys and deprecates API whitelist.

### 3 November 2020 Release

  * Introduces multi-cloud clusters and the ability to move clusters between cloud providers.

  * Online Archive now supports using a nested field for the archiving date and for the customer-chosen query fields.

  * Introduces the ability to use the Okta Verify mobile app for multi-factor authentication.

### 13 October 2020 Release

  * Supports Azure Private Link with Atlas Private Endpoints.

  * Improved filtering for the Activity Feed.

  * Optimizes slow query logging by automatically adjusting the slowMS threshold based on the workload to capture more slow queries.

  * Introduces a feedback button for Index Suggestions in the Performance Advisor.

### 22 September 2020 Release

  * Supports the following AWS regions:

    * `af-south-1` (Cape Town, South Africa)

    * `eu-south-1` (Milan, Italy)

  * Supports the following Google Cloud regions:

    * `asia-southeast2` (Jakarta, Indonesia)

    * `uswest3` (Las Vegas, NV, USA)

    * `uswest4` (Salt Lake City, UT, USA)

  * Supports the following Azure regions:

    * `westcentralus` (Wyoming, USA)

    * `germanynorth` (Berlin, Germany)

  * Updates terminology for Atlas cluster firewall management. Introduces IP Access List and deprecates "IP Whitelist".

  * Introduces new host-level monitoring metrics for total memory, total memory free and total swap used.

### 01 September 2020 Release

  * Reduces cluster pricing and introduces new storage options for Atlas on Azure:

    * M10 clusters include 8 GB of storage

    * M20 clusters include 16 GB of storage

    * M40 clusters include 64 GB of storage

  * Allows you to scope database users to one or more specific clusters and Data Lakes in an Atlas project.

#### Atlas Data Lake

Introduces easier authorization management for S3 access:

  * Provides a centralized UI to authorize and view AWS IAM roles and associated Data Lakes under the Atlas Project Integrations.

  * Allows you to re-use an existing AWS IAM role when granting access to a new Atlas Data Lake.

### 12 August 2020 Release

  * Enhances Performance Advisor and Query Profiler with higher volume log ingestion.

  * Improves user experience with the Real Time Performance Panel, including one-minute history views.

  * Introduces predefined `getLastErrorModes` to enable multi-region write concern.

### 30 July 2020 Release

  * Introduces general availability of MongoDB 4.4.

### 21 July 2020 Release

  * Cloud Backups on Azure now use incremental snapshots.

  * Introduces Low-CPU Cluster Tiers on Azure.

### 24 June 2020 Release

  * Introduces alerts for Performance Advisor recommendations.

### 02 June 2020 Release

  * Renames "Cloud Provider Snapshots" to "Cloud Backup".

  * Renames "Cloud Provider Snapshots with Point in Time Restore" to "Continuous Cloud Backup".

  * Introduces Low-CPU Cluster Tiers on Google Cloud in select regions.

### 12 May 2020 Release

  * Introduces Cross-Org Billing for customers on annual subscriptions.

  * Changes default for new Atlas cluster deployments to TLS 1.2 from TLS 1.1.

  * Adds Atlas Search support for geospatial search queries and autocomplete features.

### 22 April 2020 Release

  * Redesigns the MongoDB Cloud navigation.

  * Introduces schema suggestions in Performance Advisor and Data Explorer.

  * Reduces the price of NVMe storage for AWS clusters.

  * Supports the following advanced federation options for customers who use SAML-based single sign-on:

    * Restrict organization membership

    * Restrict access by domain

    * Bypass single sign-on

  * Removes legacy Legacy Backup as an option for new Google Cloud\- and Azure-backed clusters. New Google Cloud\- and Azure-backed clusters use Cloud Backups for backup.

### 31 March 2020 Release

  * Supports multiple connection strings to the same cluster:

    * Supports deploying a multi-region Atlas cluster on Azure and connecting to it using VNet peering.

    * Supports using Realm to connect to an Atlas cluster that uses VPC peering on Google Cloud or VNet peering on Azure.

    * Supports using MongoDB Charts to connect to an Atlas cluster that uses VPC peering on Google Cloud or VNet peering on Azure.

    * Supports using Live Migration to migrate to an Atlas cluster where VPC peering on GCP or VNet peering on Azure is enabled.

    * Supports connecting from public IP using a special connection string to an Atlas cluster on Google Cloud or Azure that is using peering.

    * Supports connecting to an Atlas cluster over an AWS VPC peering connection where you use a custom DNS provider (and AWS's built in split horizon DNS cannot be used) and a special connection string for private IP.

  * Supports M0 free clusters and M2/M5 shared clusters in the Google Cloud Mumbai region.

### 19 March 2020 Release

  * `M10` and `M20` cluster tiers now support Atlas Search. All cluster tiers running MongoDB version 4.2 and higher can use Atlas Search.

### 10 March 2020 Release

  * Supports the Google Cloud Seoul region.

  * Supports the following Azure regions:

    * Azure Norway East

    * Azure Switzerland West: This non-standard Azure region should be used as a secondary disaster recovery region for Switzerland North.

    * Azure UAE Central: This non-standard Azure region should be used secondary disaster recovery region for UAE North.

  * Supports Continuous Cloud Backups for Google Cloud and Azure backups.

  * Defaults new clusters to MongoDB 4.2.

  * Displays a review change modal to users after making edits to a cluster.

### 18 February 2020 Release

  * Supports "Click-to-Create" Index Suggestions in Performance Advisor.

  * Supports MongoDB 4.2 on AWS using Cloud Backups with Continuous Cloud Backup restores.

  * Transitions customers with Legacy Backups automatically to Cloud Backups when upgrading from 4.0 to 4.2.

  * Increases maximum storage to memory ratio:

Cluster Tiers

|

Old Max Storage Ratio

|

New Max Storage Ratio  
  
||  
  
M10 - M40

|

50:1

|

60:1  
  
M50+ cluster tiers

|

100:1

|

120:1  
  
  * Increases number of connections to M10 and M20 tiers.

Cluster Tiers

|

Old Connections

|

New Connections  
  
||  
  
M10

|

750

|

1,500  
  
M20

|

1,500

|

3,000  
  
  * Starts port numbers from 1024 instead of 1 on Atlas Private Endpoints on AWS cluster nodes.

 **Starting week of 24 February:**

  * Scales cluster to next cluster tier (from M30 to M40 for example) to continue storage scaling when the cluster:

    * Has enabled storage auto-scaling, and

    * Approaches the cluster tier’s maximum storage level

### 04 February 2020 Release

  * Supports using Google authentication for MongoDB Cloud user login.

  * Introduces account.mongodb.com: a unified login experience for MongoDB Cloud, Support, JIRA, and Feedback.

### 28 January 2020 Release

  * Removes Legacy Backup as a backup option for new AWS-backed clusters. Newly deployed AWS-backed clusters use Cloud Backups for backup.

  * Provides customers with project-level maintenance windows enabled with ability to receive the 72-hour alert notification in their configured alerts destination.

### 07 January 2020 Release

  * Modifies behavior so that clusters enter a terminal state after customers revoke MongoDB Atlas encryption keys that they manage with AWS KMS, Google Cloud KMS, or Azure Key Vault.

  * Provides ability to manage AWS PrivateLink via API.

## 2019 Releases

### 10 December 2019 Release

  * Supports `M0` free clusters and `M2/M5` shared clusters in the Google Cloud Japan (Tokyo) and Azure Canada Central (Toronto) regions.

  * Introduces Atlas Triggers integration with Amazon EventBridge.

  * Introduces Identity Federation with SAML.

  * Supports higher maximum connection limits for new cluster deployments on select cluster tiers:

    * `M10` lifted from 350 to 1,500

    * `M20` lifted from 700 to 3,000

    * `M30` lifted from 2,000 to 3,000

    * `M40` lifted from 4,000 to 6,000

### 18 November 2019 Release

  * Supports Private Endpoints with AWS PrivateLink.

  * Supports "Passwordless" X.509 authentication for database users. You can Configure Database Users to use Atlas-managed X.509 authentication, or you can Set up Self-Managed X.509.

  * Enhancements to index recommendations in Performance Advisor.

  * Enables always-on database-level authentication access auditing for dedicated clusters.

  * Enables API management for third party service integrations like DataDog and Slack.

  * Enables API management for AWS security group IDs on the Atlas project IP access list when using VPC peering.

  * Introduces the `humanReadable` field to webhook alert notifications. This field contains a human-readable description of the alert.

  * Includes new guides for configuring Atlas to authenticate and authorize users from third-party LDAP providers:

    * Configure User Authentication and Authorization with Okta LDAP Interface

    * Configure User Authentication and Authorization with OneLogin VLDAP

  * Billing invoices now show usage by project in the Summary by Project section.

### 23 October 2019 Release

  * Supports the following Azure regions:

    * Germany West Central

    * Switzerland North

  * Supports `M0` free clusters and `M2`/`M5` shared clusters in the Google Cloud Brazil (São Paulo) region.

  * Supports `M0` free clusters in the AWS Syndey region.

  * Enables faster restores from Cloud Backup backups.

### 01 October 2019 Release

  * Introduces compute auto-scaling in public beta.

  * Enhances Integrations interface for third party services.

  * Introduces EU destinations for DataDog and Opsgenie integrations.

  * Supports the official Terraform MongoDB Atlas Provider.

  * Supports the MongoDB Atlas Open Service Broker for Kubernetes.

  * Introduces Continuous Cloud Backup (PITR) available for clusters using AWS Cloud Backups.

  * Increases throughput for M2 & M5 cluster tiers.

### 10 September 2019 Release

  * Introduces the Query Profiler for `M10+` clusters.

  * Newly deployed MongoDB Atlas clusters in the following Azure regions will be spread across availability zones:

    * Central US

    * East US

    * East US 2

    * West US 2

    * France Central

    * North Europe

    * UK South

    * West Europe

    * Japan East

    * Southeast Asia

Pre-existing clusters, and clusters in all other Azure other regions will
continue to be deployed in _Availability Sets_.

  * Internal Realm/Charts-created database users and IP access list entries no longer show in the Atlas console.

  * MongoDB Cloud billing authenticates credit cards for customers in the European Economic Area in compliance with the second Payment Services Directive (PSD2). To learn more about Strong Customer Authentication, see Strong Customer Authentication (SCA) Changes.

### 20 August 2019 Release

  * Supports the AWS Bahrain region.

  * Changes the preferred region in a multi-region cluster without requiring a rolling resync.

  * Adds key-value pair labels to cluster resources in the Public API.

### 30 July 2019 Release

  * Supports the Azure United Arab Emirates North region.

  * Introduces `M80` general class cluster tier on AWS offering next-gen infrastructure. This replaces the more expensive `M100`.

  * Removes `M100` cluster tier on AWS as an option for new cluster deployments.

  * Disables the ability to create new Personal API Keys. These keys are deprecated. Use Programmatic API Keys to access the Cloud Manager API.

### 09 July 2019 Release

  * Enables free daily backups for M2 and M5 clusters.

  * Unifies the login experience: accounts for MongoDB Cloud, Support, and JIRA use the same credentials.

  * Adds new project-level role `Project Cluster Manager`. This role allows operators to scale clusters but not allow those operators to:

    * Terminate clusters,

    * Change the security configuration changes, or

    * Access data.

  * Allows deploy single-shard sharded clusters in Atlas.

### 18 June 2019 Release

  * Supports MongoDB 4.2.

  * Supports `$searchBeta`.

    * Includes Memory, CPU, and Disk Usage monitoring. For more information, see Performance Considerations.

    * Includes alerts for Memory.

    * Requires MongoDB 4.2.

  * Introduces Atlas Data Federation on-demand query service.

  * Supports Cloud Backups for 4.2 replica sets.

  * Supports Encryption at Rest for snapshots.

  * Added Aggregation Pipeline Builder to the Atlas UI.

### 29 May 2019 Release

  * Support for Google Cloud Osaka region.

  * Support to search for organization or project names that are one character long.

### 07 May 2019 Release

  * Cloud Backups are now available for Google Cloud-backed clusters.

  * Atlas clusters can now use Google Cloud KMS for encryption at rest.

  * Atlas clusters now have a new MongoDB configuration option that allows agents to continue connecting even if you have exceeded the maximum number of connections. For example, this means that Atlas continues to gather monitoring data after reaching the maximum number of connections. This change affects all new Atlas clusters. Existing Atlas clusters are affected the next time you request a configuration change to a cluster.

  * Atlas projects may now use either the Legacy Backup or the Cloud Backups backup method. An Atlas project supports multiple backup types among clusters within that project. You must terminate the existing backup method before switching between backup methods for an Atlas cluster.

  * Enhanced left-hand navigation.

### 16 April 2019 Release

  * Supports Microsoft Azure VNet peering.

  * Can load sample data into an Atlas cluster.

  * Supports the Microsoft Azure South Africa North region.

  * Supports the Google Cloud Platform Zurich region.

  * Offers self-serve customers option to sign up for a support package.

### 26 March 2019 Release

  * Atlas clusters can re-use public IP addresses when replaced in the same region.

  * Can configure backup schedule and retention for Snapshots Backup.

  * AWS EC2 Capacity for all cluster tiers in all regions and availability zones is visible via the Atlas Admin UI.

### 05 March 2019 Release

  * UX improvements to the cluster Connect modal.

  * Most server replacements get initial data from a disk snapshot of the primary instead of an initial sync.

  * Support for new shared cluster regions:

    * AWS

      * `eu-central-1` (`M2/M5`)

      * `eu-west-1` (`M0`)

      * `us-west-2` (`M0`)

    * Azure

      * `northeurope` (`M0`)

      * `westus` (`M0/M2/M5`)

  * Cloud Backups for Geo-sharded clusters.

### 13 February 2019 Release

  * Supports Google Cloud Peering.

  * Introduces Analytics Nodes. These are similar to read-only nodes but this special node type makes use of replica set tags to let you target workloads to specific secondaries.

  * Support for AWS Stockholm region. With this region comes a new largest cluster, `M700`.

  * Atlas on Azure 2.0.

    * `M10`, `M80`, and `M200` clusters are now supported in all regions. The `M90` tier is going to be removed shortly.

    * Pricing reductions in most regions.

    * All Azure clusters have been migrated to latest generation hardware.

### 23 January 2019 Release

  * Optimizes safe cluster upgrades after failure (no user-facing components, internal Atlas planner optimizations).

  * Allows creation of API Keys that are scoped to an organization and are not tied to a human.

  * Credit cards will be authorized for a small amount ($1.00) to reduce the risk of failed charges.

  * Users can now remove themselves from a project.

### 01 January 2019 Release

  * Optimizes automated rollout to ensure that rollouts happen within 1 U.S. East business day for non-maintenance-window projects.

  * Provides more visibility to maintenance timing in the administration user interface.

  * Supports On-Demand Cloud Backups.

## 2018 Releases

### 04 December 2018 Release

  * Allow users to set when they would prefer to start Atlas maintenance.

  * Support NVMe storage.

  * Create and manage custom roles for database users.

  * Can peer across regions.

  * Improved speed of backup restores for Legacy Backup.

### 13 November 2018 Release

  * Improved the Cluster Connect experience.

  * Support for sharded clusters for Snapshot Backup in both AWS and Azure.

  * Support for new GCP regions:

    * Finland

    * Los Angeles

    * Hong Kong

### 24 October 2018 Release

  * Improved experience for connecting to cluster.

  * Can now set advanced configuration options when deploying the Business Intelligence Connector.

  * Can restrict MongoDB employee access to their Atlas servers.

  * Can use Snapshot Backups for sharded clusters AWS and Azure as private beta.

  * Can now create rolling indexes via Data Explorer.

### 04 October 2018 Release

  * Ability for Project Owners to disable the use of Data Explorer for their Project.

### 11 September 2018 Release

  * Encrypted Storage Engine available with Azure KeyVault integration

  * Data Explorer Available for Atlas shared clusters (M0/M2/M5)

  * Public API: Ability to perform point in time automated restores

  * Send project alert notifications to organization members by role

← Release NotesData Federation Changelog →

