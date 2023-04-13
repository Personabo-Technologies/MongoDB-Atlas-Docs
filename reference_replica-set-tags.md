Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Query using Replica Set Tags

Share Feedback

On this page

  * Replica Set Tag Descriptions
  * Use Cases and Examples
  * Built-In Custom Write Concerns

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas clusters are configured with pre-defined replica set tags for different
member types in the cluster. You can utilize these pre-defined replica set
tags to direct queries from specific applications to desired node types and
regions. These tags sets allow you to customize read preferences for a replica
set, thus improving cluster performance and reliability.

To use replica set tags in your connection string and direct queries to
desired nodes, set the tag in your the readPreferenceTags connection string
option. For examples, see Use Cases and Examples. This connection string
option is unavailable for the mongo shell. See cursor.readPref() and
Mongo.setReadPref() instead.

## Replica Set Tag Descriptions

The following table describes the pre-defined replica set tags Atlas
implements.

Tag Name

|

Description

|

Example  
  
||  
  
Provider

|

Cloud provider on which the node is provisioned.

Possible values are:

  * `AWS`

  * `GCP`

  * `AZURE`

|

`{"provider" : "AWS"}`  
  
Region

|

Cloud region in which the node resides.

For a complete list of possible `region` values for each cloud provider, refer
to the cloud provider's reference page:

  * AWS

  * GCP

  * Azure

|

`{"region" : "US_EAST_2"}`  
  
Node Type

|

Node type.

Possible values are:

  * `ELECTABLE`

  * `READ_ONLY`

  * `ANALYTICS`

For more information, see Node Types.

|

`{"nodeType" : "ANALYTICS"}`  
  
Workload Type

|

Tag to distribute your workload evenly among your non-analytics (electable or
read-only) nodes.

Possible values are:

  * `OPERATIONAL`

|

`{"workloadType" : "OPERATIONAL"}`  
  
### Node Types

The following table describes the possible `nodeType` values in your replica
set tags.

Node Type

|

Description  
  
|  
  
`ELECTABLE`

|

Read from nodes eligible to be elected primary. `ELECTABLE` nodes correspond
to Electable nodes for high availability in the cluster creation UI.  
  
`READ_ONLY`

|

Read from read-only nodes. `READ_ONLY` nodes correspond to Read-only nodes for
optimal local reads in the cluster creation UI.  
  
`ANALYTICS`

|

Read from read-only analytics nodes. `ANALYTICS` nodes correspond to Analytics
nodes for workload isolation in the cluster creation UI.  
  
To learn how to configure electable, read-only, and analytics nodes for your
cluster, see Configure High Availability and Workload Isolation.

## Tip

### See also:

For details on how these replica set tags correspond to BI Connector for Atlas
read preferences, refer to the BI Connector cluster options section of the
Create a Cluster Page.

## Use Cases and Examples

Consider the following scenarios where utilizing pre-defined replica set tags
would be beneficial, and see the corresponding sample connection strings.

## Note

Each of the following example connection strings employ the
`readConcernLevel=local` connection string option. Specifying a read concern
of local ensures that secondary reads on sharded clusters do not return
orphaned documents. You do not need to specify this option when connecting to
non-sharded replica sets.

### Use Analytics Nodes to Isolate Workloads

If an application performs complex or long-running operations, such as ETL or
reporting, you may want to isolate the application's queries from the rest of
your operational workload by connecting exclusively to analytics nodes.

Consider the following connection string:

    
    
    mongodb+srv://<USERNAME>:<PASSWORD>@foo-q8x1v.mycluster.com/test?readPreference=secondary&readPreferenceTags=nodeType:ANALYTICS&readConcernLevel=local  
      
  
The connection string options appear in the following order:

  * `readPreference=secondary`

  * `readPreferenceTags=nodeType:ANALYTICS`

  * `readConcernLevel=local`

The readPreference option of `secondary` and readPreferenceTag option of `{
nodeType : ANALYTICS }` limit the application connections to analytic nodes.

#### Isolate Normal Application Secondary Reads from Analytics Nodes

You may want to isolate regular application reads from the workload on
analytics nodes.

Consider the following connection string:

    
    
    mongodb+srv://<USERNAME>:<PASSWORD>@foo-q8x1v.mycluster.com/test?readPreference=secondary&readPreferenceTags=workloadType:OPERATIONAL&readConcernLevel=local  
      
  
The connection string options appear in the following order:

  * `readPreference=secondary`

  * `readPreferenceTags=workloadType:OPERATIONAL`

  * `readConcernLevel=local`

The specified options prevent your application from reading from analytics
nodes. The application must read from `operational`, or non-analytics, nodes.

### Target Local Reads for Geographically-Distributed Applications

You can utilize Atlas replica set tags to target local reads to specific
regions for globally distributed applications. Prior to the introduction of
these tags, local reads for globally distributed applications relied on
correctly calculating the nearest read preference. With Atlas replica set
tags, specifying appropriate geographic tags in combination with a read
preference mode of `nearest` provides more consistent behavior.

The following connection string prioritizes connections to the AWS `US_EAST_1`
region, followed by the `US_EAST_2` region:

    
    
    mongodb+srv://<USERNAME>:<PASSWORD>@foo-q8x1v.mycluster.com/test?readPreference=nearest&readPreferenceTags=provider:AWS,region:US_EAST_1&readPreferenceTags=provider:AWS,region:US_EAST_2&readPreferenceTags=&readConcernLevel=local  
      
  
The connection string options appear in the following order:

  * `readPreference=nearest`

  * `readPreferenceTags=provider:AWS,region:US_EAST_1`

  * `readPreferenceTags=provider:AWS,region:US_EAST_2`

  * `readPreferenceTags=`

  * `readConcernLevel=local`

Atlas considers each read preference tag in the order you specify them. After
Atlas matches a node to a tag, it finds all eligible nodes that match that
tag. Atlas then ignores any following `readPreferenceTags`.

In this example, the application first tries to connect to a node in AWS
region `US_EAST_1`. If there no nodes in that region are available, the
application tries to connect to a node in AWS region `US_EAST_2`.

The final (empty) `readPreferenceTags=` provides a fallback option. With an
empty `readPreferenceTags=` option, the application can connect to any
available node regardless of provider or region.

These options help ensure that the application connects to the closest
geographic region for reduced latency and improved performance.

## Tip

### See also:

For additional information and use cases for various read preferences, refer
to the Read Preference page in the MongoDB Manual.

## Built-In Custom Write Concerns

Atlas provides built-in custom write concerns for multi-region clusters. Write
concern describes the level of acknowledgment requested from MongoDB for write
operations to a cluster.

Atlas's built-in custom write concerns can help improve data consistency by
ensuring your operations are propagated to a set number of regions to succeed.

To use a custom write concern, specify the write concern in the write concern
document of your operation.

Atlas provides the following custom write concerns for multi-region clusters:

Write Concern

|

Tags

|

Description  
  
||  
  
`twoRegions`

|

`{ region: 2 }`

|

Write operations must be acknowledged by at least two regions in your cluster.  
  
`threeRegions`

|

`{ region: 3 }`

|

Write operations must be acknowledged by at least three regions in your
cluster.  
  
`twoProviders`

|

`{ provider: 2 }`

|

Write operations must be acknowledged by at least two regions in your cluster
with distinct cloud providers.  
  
## Example

Consider a multi-region cluster across three regions: **us-east-1** , **us-
east-2** , and **us-west-1**. You want to have write operations propagate to
all three regions in your cluster before Atlas accepts them.

The following operation inserts a document and requires that the operation be
propagated to all three regions due to the `{ w: "threeRegions" }` write
concern object:

    
    
    db.employees.insertOne(  
      
      { name: "Bob Smith", company: "MongoDB" },  
      { writeConcern: { w: "threeRegions" } }  
    )  
  
← Configure High Availability and Workload IsolationManage Serverless
Instances →

