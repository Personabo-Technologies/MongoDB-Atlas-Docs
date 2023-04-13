Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Sharded Clusters

Share Feedback

On this page

  * Chart Controls
  * Chart Display
  * Data Sources

A sharded cluster is the set of nodes comprising a sharded MongoDB deployment.
To view the metrics for a specific Atlas cluster in a project, click the View
Monitoring button for that cluster. Alternatively, click on the name of the
cluster to open the cluster overview, then click the Metrics tab.

The Metrics tab for sharded clusters provides a side-by-side comparision of
shards in one view. The Display drop-down contains many available metrics.

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

The Metrics view has three distinct sections:

## Note

### Monitoring Data Storage Granularity

Atlas stores metrics data at increasing granularity levels. For more
information, see Monitoring Data Storage Granularity.

## Chart Controls

Atlas provides the following controls for the Metric view:

Control

|

Function  
  
|  
  
Granularity

|

Modifies the granularity of metrics displayed for each chart. Select a
granularity, usually between 1 minute and 1 day (24 hours). Select `Auto` to
automatically adjust the granularity based on the selected Zoom or Current
Display date controls.

`Auto` granularity selects the highest fidelity granularity available within
the selected time range and sharded cluster metric rendering limits.

## Note

### Sharded Cluster Metric Rendering Limits

In the Sharded Cluster metrics view, Atlas renders a maximum of:

  * 100,000 total data points and

  * 3,000 data points for a single series.

As a result, when rendering metrics for large deployments over a long period
of time, Atlas may display metrics at a lower granularity than expected. To
learn more about the granularity at which Atlas stores metric data, see
Monitoring Data Storage Granularity.

## Note

Atlas supports a 10 second granularity only on `M40` and larger clusters. To
learn more, see Premium Monitoring Granularity.  
  
Zoom

|

Modifies the date range of metrics displayed for each chart. Select a zoom
range between 1 hour and 5 years. Adjusting the Zoom automatically adjusts the
Current Display date range.  
  
Current Display

|

Modifies the start and end date-time range of metrics displayed for each
chart. Modifying the start and end date sets the value of Zoom to `custom` and
overrides the previously selected zoom level.  
  
Display

|

Selects which metric to chart. You can display no more than one chart at a
time.  
  
Display Data

|

Directs Atlas to display data based on the selected option

  * `Individually` \- displays the selected metrics for each shard as an individual line.

  * `Sum` \- displays the sum of the selected metrics across all shards in the cluster.

  * `Averaged` \- displays the average of the selected metrics across all shards in the cluster.

  
  
View

|

Selects which sharded cluster components to display

  * `SHARDS` \- displays metrics for each shard in the sharded cluster.

  * `MONGOS` \- displays metrics for each `mongos` in the sharded cluster.

  * `CONFIGS` \- displays metrics for the config server in the sharded cluster config server replica set.

  
  
## Chart Display

When viewing charts, you can do the following:

Task

|

Action  
  
|  
  
Zoom in on a period of time.

|

Click and drag the mouse pointer over a portion of the chart. To reset to the
originally selected range (zoom out), double-click the chart.

## Note

When you zoom in on one period of time, the Current Display date range in the
chart control section automatically updates to reflect the selected period.  
  
View statistics at a particular time.

|

Hover the mouse pointer over a point on the chart.  
  
## Data Sources

Atlas displays each data source that contributes to the metric chart in a
table below the chart. The table consists of the following:

Column

|

Description  
  
|  
  
Shard Name

|

When View is set to `SHARDS`, displays the name of each shard in the sharded
cluster.

When View is set to `MONGOS` or `CONFIGS`, displays the name of each `mongos`
or config server `mongod` process in the cluster.

Click on a listed component to open the Metrics view for that component.  
  
Alerts

|

Indicates if there are any open alerts for the listed shard or process. Click
on the alert icon to open the Alerts view for that shard or process. For more
information on responding to open alerts, see Resolve Alerts.  
  
Data Size

|

Only visible if View is set to `SHARDS`.

Indicates the logical size of all documents and indexes on the shard.  
  
Show

|

Only visible if View is set to `SHARDS`

Indicates which replica set members to show on the selected chart. Select
`Primaries`, `Secondaries` or `All`.  
  
Read, Write, and Queued

|

Metric data related to the displayed chart. Hover over the corresponding
column for a pop up with detailed information on the metrics shown.  
  
← Review Replica Set ClustersReview MongoDB Processes →

