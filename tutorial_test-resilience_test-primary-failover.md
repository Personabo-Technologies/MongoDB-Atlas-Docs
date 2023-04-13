Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Test Primary Failover

Share Feedback

On this page

  * Test Primary Failover Process
  * Verify the Failover
  * Troubleshoot Failover Issues

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas conducts replica set elections when it makes configuration changes, such
as patch updates, scaling events, and when failures occur. Your applications
should handle replica set elections without any downtime. To learn how to
build a resilient application, see Build a Resilient Application with MongoDB
Atlas.

You can enable retryable writes by adding retryWrites=true to your Atlas URI
connection string. To learn more, see Retryable Writes.

You can use the Atlas UI and API to test the failure of the replica set
primary in your Atlas cluster and observe how your application handles a
replica set failover.

## Test Primary Failover Process

When you submit a request to test primary failover, Atlas simulates a failover
event. During this process:

  1. Atlas shuts down the current primary.

  2. The members of the replica set hold an election to choose which of the secondaries will become the new primary.

  3. Atlas brings the original primary back to the replica set as a secondary. When the old primary rejoins the replica set, it will sync with the new primary to catch up any writes that occurred during its downtime.

The following statements describe Atlas behavior during rollovers and when
testing failover in sharded clusters:

  * If the original primary accepted write operations that had not been successfully replicated to the secondaries when the primary stepped down, the primary rolls back those write operations when it re-joins the replica set and begins synchronizing. To learn more, see Rollbacks During Replica Set Failover. Contact MongoDB Support for assistance with resolving rollbacks.

  * Only the `mongos` processes that are on the same instances as the primaries of the replica sets in the sharded cluster are restarted.

  * The primaries of the replica sets in the sharded cluster are restarted in parallel.

Atlas CLI

Atlas Administration API

Atlas UI

To start a failover test for the specified cluster in your project using the
Atlas CLI, run the following command:

    
    
    atlas clusters failover <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters failover.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Verify the Failover

To verify that the failover is successful:

  1. Log in to the Atlas UI and click Database.

  2. Click the name of the cluster for which you performed the failover test.

  3. Observe the following changes in the list of nodes in the Overview tab:

    * The original `PRIMARY` node is now a `SECONDARY` node.

    * A former `SECONDARY` node is now the `PRIMARY` node.

## Troubleshoot Failover Issues

If your application doesn't handle the failover gracefully, ensure the
following:

  * You are using the connections-dns-seedlist.

  * You are using the latest version of the driver.

  * You have implemented appropriate retry logic in your application.

← Test ResilienceSimulate Regional Outage →

