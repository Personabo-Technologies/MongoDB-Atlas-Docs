Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Atlas Search Metrics

Share Feedback

On this page

  * Chart Controls
  * Chart Display
  * Chart Selection

## Note

### Availability

  * Atlas provides Atlas Search metrics for database deployments with at least one active Atlas Search index. To set up an Atlas Search index, see What is MongoDB Atlas Search?.

  * `M0` (Free Tier) clusters don't support these metrics.

To view Atlas Search metrics for a database deployment:

  1. Click the View Monitoring button for that database deployment.

  2. Select one or more of the search charts.

Alternatively:

  1. Click on the name of the database deployment to open the database deployment overview.

  2. Click the Metrics tab.

  3. Select one or more of the search charts.

To view Atlas Search metrics for a specific process:

  1. Click the link for the process.

  2. Click the Search Metrics tab.

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

The following Atlas Search metrics are available to evaluate and optimize your
Atlas Search indexes:

Chart

|

Data  
  
|  
  
Search Disk Space Used

|

Total bytes of disk space that search indexes occupy.  
  
Search Fields Indexed

|

Total number of unique fields present in the Atlas Search index.  
  
Search Index Size

|

Total size of all indexes on disk in bytes.  
  
Search JVM Heap Memory

|

Amount of memory that the JVM heap is currently using.  
  
Search Max Number of Lucene Docs

|

Upper bound on the number of Lucene docs used to store Atlas Search indexes in
this replica set or shard.  
  
Search Max Replication Lag

|

Approximate number of milliseconds that Atlas Search is behind in replicating
changes from the oplog of `mongod`.  
  
Search Normalized Process CPU

|

CPU usage of search processes on the node scaled to a range of 0-100% by
dividing by the number of CPU cores.  
  
Search Opcounters

|

Total number of Atlas Search operations.  
  
Search Process CPU

|

Percentage of time that the CPU spent servicing search processes. For servers
with more than 1 CPU core, this value can exceed 100%.  
  
Search Process Memory

|

Total bytes of memory that search processes occupy.  
  
Search Query Status

|

Total number of Atlas Search queries with each status.  
  
## Note

### Monitoring Data Storage Granularity

Atlas stores metrics data at increasing granularity levels. For more
information, see Monitoring Data Storage Granularity.

## Chart Controls

Atlas provides the following controls for the metrics charts. Adjusting any of
these options affects all charts displayed under the selected view:

Control

|

Function  
  
|  
  
Granularity

|

Modifies the granularity of metrics displayed for each chart. Select a
granularity, usually between 1 minute and 1 day (24 hours). Select `Auto` to
automatically adjust the granularity based on the selected Zoom or Current
Display date controls. `Auto` granularity selects the highest fidelity
granularity available for the time range.

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
  
Add Chart

|

Select one or more charts to display or hide. Adding charts using this
dropdown is identical to adding charts from the Toggle Charts section of the
Metrics view.  
  
Select Database

|

Only visible for the DB Stats view. Selects the database for which to display
metrics.  
  
Display Opcounters on Separate Charts

|

Directs Atlas to split the Opcounters chart into its individual components.
You can then choose to chart one or more of those components.  
  
Display Timeline Annotations

|

Directs Atlas to display or hide chart annotations. Chart annotations consist
of colored vertical lines that indicate server events, such as a server
restart or a transition in member state.  
  
## Chart Display

When viewing charts, you can do the following:

Task

|

Action  
  
|  
  
View a detailed description of a chart.

|

Hover your mouse over the chart to display the context menu.

Click __next to the chart name to open the Chart Info modal. This modal
includes a breakdown of the chart's data series, the annotations available for
that chart, and the operations the chart supports.  
  
Expand a chart.

|

Hover your mouse over the chart to display the context menu.

Click the two-way arrow at the top right of the chart.  
  
Zoom in on a period of time.

|

Click and drag the mouse pointer over a portion of the chart.

To reset to the originally selected range (zoom out), double-click the chart.

## Note

When you zoom in on one period of time, the Current Display date range in the
chart control section automatically updates to reflect the selected period.  
  
View statistics at a particular time.

|

Hover the mouse pointer over a point on the chart.  
  
Move a chart.

|

Click and hold the grabber in the upper left corner of the chart, and drag the
chart to the new position.  
  
Share a URL to the chart.

|

Hover your mouse over the chart to display the context menu.

Click the curved arrow on the chart. Select Chart Permalink to retrieve a URL
to the chart. Select Email Chart to email the chart.

The recipient of the chart URL must have a Atlas user account with access to
the project and cluster.  
  
## Chart Selection

Atlas displays the available metrics to chart for the selected database
deployment under the Toggle Charts header.

Charts marked with the `+` symbol are inactive, while charts marked with the
`-` symbol are active. Click on any chart to toggle the chart state.

← Fix Atlas Search IssuesAtlas Search M0 (Free Cluster), M2, and M5
Limitations →

