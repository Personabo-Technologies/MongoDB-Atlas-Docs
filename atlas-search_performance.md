Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Tune Atlas Search Performance

Share Feedback

Atlas Search runs a new process, called `mongot`, alongside the `mongod`
process on each host in your Atlas cluster. `mongot` maintains all Atlas
Search indexes on collections in your Atlas databases. The amount of CPU,
memory, and disk resources `mongot` consumes depends on several factors,
including our index configuration and the complexity of your queries. Atlas
Search alerts measure the amount of CPU and memory used by Atlas Search
processes.

The following pages contain recommendations that you can apply when
configuring your Atlas Search index and defining your Atlas Search queries to
improve performance:

  * Atlas Search Index Performance

  * Atlas Search Query Performance

To fix and monitor Atlas Search issues, see the following pages:

  * Manage Atlas Search Alerts

  * Review Atlas Search Metrics

## Important

### Upgrading to NVMe Storage

Upgrading an Atlas cluster to use NVMe triggers an initial sync on that
cluster. Atlas Search is unavailable until both the `mongod` and `mongot`
finish their initial syncs.

← Troubleshoot Atlas Search ErrorsAtlas Search Index Performance →

