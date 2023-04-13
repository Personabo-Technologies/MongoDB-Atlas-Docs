Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Storage

Share Feedback

On this page

  * What happens when I reach my Atlas storage limit?
  * Without using Provisioned IOPS on MongoDB Atlas on AWS, what kind of IOPS should I expect?

## What happens when I reach my Atlas storage limit?

The result of reaching your Atlas storage limit depends on the Atlas cluster
you are using.

  * For shared clusters (`M0`, `M2`, `M5`), the maximum storage is a hard limit and cannot be exceeded. You can add additional storage by upgrading to a dedicated cluster (`M10+`). For details on how Atlas calculates storage limits for shared clusters, see this section of the FAQ.

  * By default, `M10+` clusters auto-expand storage based on disk usage thresholds. To modify this setting to a fixed storage limit, refer to the Modify a Cluster page.

If you attempt to write to a shared cluster that does not have space for the
desired write operation, Atlas displays an error message similar to the
following:

    
    
    WriteResult({  
      
      "writeError": {  
        "code": 8000,  
        "errmsg": "you are over your space quota, using 513 MB of 512 MB"  
      }  
    })  
  
## Tip

### See also:

To learn about the differences between shared and dedicated clusters, see
Atlas M0 free cluster, M2, and M5 Limitations.

## Tip

You can configure alerts which trigger once your allocated storage reaches a
specified threshold. Atlas calculates allocated storage using metrics returned
by the `dbStats` command.

Atlas retrieves database metrics every 20 minutes by default but adjusts
frequency when necessary to reduce the impact on database performance.

To learn more about storage alerts, see DB Storage alert conditions.

### How does Atlas calculate storage limits for shared clusters (M0, M2, M5)

Atlas calculates the storage limit for shared clusters based on data usage, as
opposed to the `storageSize` metric used by non-shared clusters (which
includes compression). Atlas determines data usage by summing a cluster's
`dataSize` and `indexSize`. You can issue the db.stats() method to view the
values of these fields.

## Without using Provisioned IOPS on MongoDB Atlas on AWS, what kind of IOPS
should I expect?

Atlas provides an estimate of how many 16K IOPS you can expect, calculated as
the lesser of 3 IOPS per provisioned GB, or the cluster node's maximum IOPS
capacity.

However, non-provisioned IOPS on AWS can burst above this estimate or drop
below it. As a result, customers who are interested in consistent IOPS
throughput should consider leveraging Provisioned IOPS.

← FAQ: SecurityFAQ: Support →

