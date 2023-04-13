Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Cluster Sizing and Tier Selection

Share Feedback

On this page

  * Cluster Auto-Scaling
  * Memory
  * Network Traffic

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Choosing the correct Atlas cluster tier and configuration is an important step
in setting up a successful production MongoDB deployment. You can always
modify a cluster at a later time, but getting started with the right
configuration is possible with a few calculations based on your data set size
and network requirements.

You can also configure your cluster to automatically scale its cluster tier,
storage capacity, or both in response to cluster usage, thereby reducing the
manual maintenance required for your cluster. To learn more, see Cluster Auto-
Scaling.

## Note

### Recommend M30 or Larger Clusters for Production Use

M30 and higher clusters are recommended for production environments. You can
use M10 and M20 clusters as production environments for low-traffic
applications, but these tiers are recommended for development environments.

## Cluster Auto-Scaling

Cluster tiers `M10` and greater support Cluster Auto-Scaling. Cluster tier
Auto-scaling is enabled by default when you create new clusters in the user
interface. It is disabled by defaut if you create new clusters in the API.
With auto-scaling enabled, Atlas automatically scales your cluster tier,
storage capacity, or both in response to cluster usage. Auto-scaling allows
your cluster to adapt to your current workload and reduce the need to make
manual optimizations.

  * Cluster storage scaling automatically increases your cluster storage capacity when 90% of disk capacity is used. This setting is enabled by default to help ensure that your cluster can always support sudden influxes of data. To opt out of cluster storage scaling, un-check the Storage Scaling checkbox in the Auto-scale section.

  * Cluster tier scaling automatically scales your cluster tier up or down in response to various cluster metrics. To opt out of cluster tier auto-scaling, un-check the Cluster Tier Scaling checkbox in the Auto-scale section.

To control how Atlas should auto-scale your cluster, you set:

    * The maximum cluster tier to which your cluster can automatically scale up. By default, this setting is set to the next cluster tier compared to your current cluster tier.

    * The minimum cluster tier to which your cluster can scale down. By default, this setting is set to the current cluster tier.

## Memory

Memory refers to the total physical RAM available on each data bearing node of
your Atlas cluster. For example, an `M30` standard replica set is configured
with 8 GB RAM on each of the 3 data bearing nodes.

Atlas uses the WiredTiger storage engine.

  * By default, for M40 or larger clusters, WiredTiger dedicates 50% of physical RAM for the WiredTiger cache. The other 50% is reserved for in-memory operations such as sorts and calculations, the underlying operating system and other system services.

  * By default, for M30 or smaller clusters, WiredTiger dedicates 25% of physical RAM for the WiredTiger cache.

To learn more about memory use, see WiredTiger and Memory Use.

MongoDB uses the WiredTiger cache to hold most recently used data and indexes.
The working set is the sum of all the indexes plus the set of documents that
are accessed frequently. If your working set fits in RAM, then MongoDB can
serve queries from memory, which provides the fastest query response times.

To estimate the size of the working set, you can either perform a calculation
using the information obtained from `db.stats()` for the total index space and
assume a percentage of your data space will be accessed frequently, or you can
estimate your memory requirements based on educated assumptions.

### Example: The Atlas Sample Data Sets

Using the Atlas sample data sets, we will calculate the memory requirements to
run all these databases in a single Atlas cluster. The following JavaScript
program returns database information for your cluster:

    
    
    var totalIndexSize = 0;  
      
    var totalDataSize = 0;  
    var reservedDBs = ["admin","config","local"];  
      
    // Switch to admin database and get list of databases.  
    db = db.getSiblingDB("admin");  
    dbs = db.runCommand({ "listDatabases": 1 }).databases;  
      
    // Iterate through each database and get its stats.  
    dbs.forEach(function(database) {  
       if (reservedDBs.includes(database.name))  
           return;  
      
       db = db.getSiblingDB(database.name);  
           print("Obtaining stats for " + database.name);  
       var stats = db.stats();  
      
           totalIndexSize += (stats.indexSize / (1024*1024*1024)) ;  
           totalDataSize += (stats.dataSize / (1024*1024*1024)) ;  
    });  
      
    print ("Total data size in GB: " + totalDataSize.toFixed(2));  
    print ("Total index size in GB: " + totalIndexSize.toFixed(2));  
  
This program returns the following results:

    
    
    Obtaining stats for sample_airbnb  
      
    Obtaining stats for sample_geospatial  
    Obtaining stats for sample_mflix  
    Obtaining stats for sample_supplies  
    Obtaining stats for sample_training  
    Obtaining stats for sample_weatherdata  
    Total data size in GB: 0.32  
    Total index size in GB: 0.02  
  
To run these databases completely in memory, you would need a minimum of 0.68
GB of physical RAM, as WiredTiger uses 50% of the physical RAM and we need at
least 0.34 GB to fit the working set in memory.

A realistic production cluster would have a much higher data and index size
and it may not be practical, or not a business or performance requirement, to
run the complete data set and indexes in memory. Let’s look at another
scenario.

### Example: Mobile App

A popular mobile game has 512 GB of data and 32 GB of indexes. The game’s
internal system data occupies 16 GB, and the rest is player profile data. A
player's profile is required to be in memory while the player is active in the
game. About 25% of all players are active at any point in time. The system
data is used constantly and it must fit completely in RAM for optimal game
performance. All indexes must also fit in RAM for the fastest query response
time. The memory sizing is as follows:

Data

|

RAM Requirements

|

RAM for WiredTiger Cache  
  
||  
  
System: 16 GB

|

100% in RAM

|

16 GB  
  
Index: 32 GB

|

100% in RAM

|

32 GB  
  
Player Profiles: 496 GB

|

25% in RAM

|

124 GB  
  
Given these requirements, you can expect an average working set to require 172
GB of RAM.

WiredTiger dedicates 50% of physical RAM to the WiredTiger cache, so the
minimum total physical RAM required to accommodate your working set is twice
the working set.

In this example, you need at least 344 GB of physical RAM to accommodate the
WiredTiger cache and a 172 GB working set. The following table lists suitable
Atlas cluster tiers:

Service Provider

|

Possible Cluster Tiers

|

Notes  
  
||  
  
AWS

|

  * `M300` 384 GB RAM

  * `M400` 488 GB RAM

  * `M700` 768 GB RAM

|

`M300` has sufficient RAM, and there is room to scale vertically to higher
cluster tiers.  
  
GCP

|

  * `M300` 360 GB RAM

|

`M300` has sufficient RAM, but there are no higher tiers available if vertical
scaling is required.  
  
Azure

|

  * `M300` 384 GB RAM

  * `M400` 432 GB RAM

|

`M300` has sufficient RAM, and there is room to scale vertically to a higher
cluster tier.  
  
## Note

If you select a cluster tier without sufficient RAM, such as an Azure `M200`
with 256 GB RAM, sharding is required.

## Network Traffic

All network traffic between cluster nodes and between clients consuming data
from your Atlas cluster impact network bandwidth. For purposes of cluster
sizing, consider the maximum traffic that any node on your cluster will bear
and use this as the basis for selecting an adequate Atlas cluster tier.

Downstream data transfer rates from your cluster to client applications can be
calculated as the sum of the total documents returned over a period of time.
If you are reading only from the primary node, this is the only calculation
you need to do. If your applications read from secondary nodes as well, you
can divide this number by the number of nodes that can serve read operations.

You can find the average document size for a database with the `db.stats()`
method. Multiply the average document size (`avgObjSize`) by the number of
documents served per second to estimate your bandwidth requirements.

## Example

10 KB average document size

100,000 documents per second served

10 KB * 100,000 = 1 GB per second

Atlas instances provide faster bandwidth speeds at the higher tiers. Instances
which are backed by AWS provide up to 10 gigabits per second at the `M30`
level, while the `M200` level provides up to 25 gigabits per second.

### Connections

An Atlas cluster can support a number of client connections which is
determined by its cluster tier. `M30` clusters support up to 2000 simultaneous
connections, while `M200` clusters support up to 128,000 simultaneous
connections.

← Production NotesBuild a Resilient Application with MongoDB Atlas →

