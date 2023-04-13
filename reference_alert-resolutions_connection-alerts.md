Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Fix Connection Issues

Share Feedback

On this page

  * Alert Conditions
  * Common Triggers
  * Fix the Immediate Problem
  * Implement a Long-Term Solution
  * Monitor Your Progress

Connection alerts typically occur when the maximum number of allowable
connections to a MongoDB process has been exceeded. Once the limit is
exceeded, no new connections can be opened until the number of open
connections drops down below the limit.

## Alert Conditions

You can configure the following alert conditions in the project-level alert
settings page to trigger alerts.

`Connections` occurs if the number of active connections to the host meets the
specified average.

`Connections % of configured limit` occurs if the number of open connections
to the host exceeds the specified percentage.

## Common Triggers

Exceeding the connection limit for an Atlas cluster may occur for a number of
reasons. Different Atlas tiers have different connection limits; clusters of
size `M0/M2/M5`, for example, are limited to 500 connections, and clusters of
size `M10` are limited to 1500 connections. Larger cluster tiers have higher
connection limits. Different database access applications have different ways
of implementing connection pooling, which affects how many open connections
your application maintains at any given time.

## Fix the Immediate Problem

### M0/M2/M5 Clusters

To resolve a connection alert condition, restart the application which is
currently making connections to your Atlas cluster. Restarting the application
terminates all existing connections opened by the application and allows the
Atlas cluster to resume normal operations.

### M10+ Clusters

Atlas clusters of size `M10` and greater can utilize the Test Primary Failover
option. The Test Primary Failover procedure steps down the current primary
node and triggers an election, which drops all connections to the primary
node.

## Note

If your application connects exclusively to a secondary node, you may need to
perform the Test Failover procedure several times to make sure the applicable
secondary node rotates its position within the replica set and drops its
connections.

Test Failover is usually the preferable solution, but another possible
solution is to restart the application currently making connections to your
Atlas cluster. Restarting the application terminates all existing connections
and allows the Atlas cluster to resume normal operations.

## Implement a Long-Term Solution

Connection alerts are generally a symptom of a larger problem. Employing one
of the strategies outlined above will fix the immediate problem, but a
permanent solution usually requires either:

  * Examining your database applications for flawed connection code. Situations in which connections are opened but never closed can allow old connections to pile up and eventually exceed the connection limit. Additionally, you may need to implement some form of connection pooling.

  * Upgrading to a larger Atlas cluster tier which allows a greater number of connections, if your user base is too large for your current cluster tier.

## Monitor Your Progress

View the Connections chart to monitor the total number of connections to the
cluster.

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.

To learn more, see View Cluster Metrics.

← Fix Atlas Search IssuesFix IOPS Issues →

