Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect via BI Connector for Atlas

Share Feedback

On this page

  * Multi-Cloud Cluster Considerations

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can enable the BI Connector for Atlas when you create or scale an `M10` or
larger cluster.

## Note

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.

To connect to the BI Connector for Atlas:

  1. Click the Connect button for your cluster.

  2. Click Connect Your Business Intelligence Tool and use the provided connection information to connect with your BI tool.

For more information on connecting to the BI Connector for Atlas, see
Connection Tutorials.

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.

## Multi-Cloud Cluster Considerations

If you have a multi-cloud cluster, your BI Connector connection string may
include the cloud provider type (`.gcp` or `.azure`). In the event of a
failover in which nodes on one cloud provider fail and requests are routed to
nodes in another cloud provider, your BI Connector connection string may
change.

To mitigate this hazard, add analytics nodes to clusters deployed only in one
cloud provider and set the BI Connector read preference to Analytics. This
ensures that your connection string remains constant.

### Connection Tutorials

Use the displayed information to connect from various clients using the BI
Connector for Atlas:

  * Create a System DSN

  * Connect from Excel

  * Connect from Tableau Desktop

  * Connect from Qlik Sense

  * Connect from MySQL Workbench

  * Connect from Power BI Desktop (Windows)

### Additional Reference

For more information on the MongoDB Connector for Business Intelligence, see
MongoDB Connector for BI Manual.

← Connect via `mongosh`Create a System DSN →

