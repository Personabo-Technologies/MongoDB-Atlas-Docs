Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data Transfer

Share Feedback

On this page

  * Sources of Data Transfer Costs
  * Live Migrate Your Data to Atlas
  * How to Reduce Data Transfer Costs

## Sources of Data Transfer Costs

Atlas data transfer costs depend on the cloud service provider hosting your
database deployment. Atlas tabulates data transfer costs daily.

### Clusters

Multi-region clusters might have higher data transfer costs depending on the
number and location of additional regions, as well as the number of clusters
deployed to each region.

## Note

### Exceptions to Data Transfer Cost

Atlas doesn't charge for data transfer for incoming or outgoing data on `M0`,
`M2`, or `M5` cluster tiers.

### Serverless Instances

Serverless instances incur costs for data transfer to and from the virtual
machine responsible for backing up and restoring data.

AWS

Azure

GCP

Atlas charges for data transfer between the Atlas node and another node. Data
transfer charges increase, from lowest to highest, when you transfer data
between your Atlas node and another node:

  * In the same AWS region.

  * In a different AWS region.

  * Outside of any AWS region, excluding incoming transfers to the Atlas node.

### Cloud Backup Snapshot Export

Atlas charges `$.125` per GB of data exported to the AWS S3 bucket, in
addition to the data transfer cost incurred from AWS itself. Atlas compresses
the data before exporting. To estimate the amount of data being exported, add
up the dataSize of each database in your cluster. This total should correspond
to the uncompressed size of your export, which would be the maximum cost
incurred from Atlas for the data export operation.

To learn more about cloud backup snapshot export, see Export Cloud Backup
Snapshot.

## Live Migrate Your Data to Atlas

MongoDB hosts and operates the free Atlas Live Migration Service to help users
migrate existing MongoDB databases to MongoDB Atlas. MongoDB doesn't charge
for any incoming data transfers to an Atlas database deployment. Learn more
about migrating to Atlas.

## How to Reduce Data Transfer Costs

The vast majority of Atlas customers spend less than 10% of their budget on
data transfer. If you are spending significantly more, some of these
optimizations may reduce your data transfer costs:

  * Check all applications and processes that access your data for inefficiencies. Ensure that queries do not:

    * Re-read data that already exists on the client.

    * Re-write existing data to your database deployment.

  * Ensure that queries originate from the same cloud region and provider as your database deployment whenever possible.

When cross-region queries are necessary:

    * Ensure read queries use the preference "nearest."

    * Source write queries from your Highest Priority Region whenever possible. For more information on region priorities, see Electable Nodes for High Availability.

  * Use the Aggregation Framework to preprocess your data before you transfer it. For example, you can project document fields using the `$project` aggregation stage to reduce the size of a document before you transfer it.

  * Ensure that your client driver uses wire protocol compression to communicate with MongoDB. Atlas always compresses intra-cluster communication. To learn how to configure your driver, refer to your Driver's Documentation.

## Note

Queries from on-premises environments into Atlas, across cloud providers, or
between continents on the same cloud provider incur the greatest data transfer
costs.

← Data Federation CostsOnline Archive Costs →

