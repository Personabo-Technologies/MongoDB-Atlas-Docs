Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Replica Set Clusters

Share Feedback

On this page

  * View Replica Set Metrics
  * Chart Controls
  * Chart Display
  * Chart Selection

A replica set in MongoDB is a group of `mongod` processes that maintain the
same data set.

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

## View Replica Set Metrics

Atlas CLI

Atlas UI

To return the metrics for a database on a replica set's specified host using
the Atlas CLI, run the following command:

    
    
    atlas metrics databases describe <hostname:port> <databaseName> [options]  
      
  
To list available databases for the replica set's specified host using the
Atlas CLI, run the following command:

    
    
    atlas metrics databases list <hostname:port> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas metrics databases describe and atlas
metrics databases list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

The Metrics view in the Atlas UI has three distinct sections:

## Note

### Monitoring Data Storage Granularity

Atlas stores metrics data at increasing granularity levels. For more
information, see Monitoring Data Storage Granularity.

## Chart Controls

Atlas provides the following controls for the Metric view. Adjusting any of
these options affects all charts displayed under the Metrics view:

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
  
Toggle Members

|

Limit charts to the selected replica set members. The `P` icon represents the
primary replica set member, while the `S` icon represents a secondary member.

## Note

When a secondary member needs to replicate data to catch up with the primary
node, it enters the recovering state.

  * The light yellow `R` icon represents a member that is recovering.

  * The dark yellow `R` icon represents a member that has fallen too far behind the primary's oplog and is now stuck in the recovering state. When this happens, you must resync the member.

For information on all member states, see Replica Set Member States.  
  
Add Chart

|

Select one or more charts to display or hide. Adding charts using this
dropdown is identical to adding charts from the Toggle Charts section of the
Metrics view.  
  
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

Atlas displays the available metrics to chart for the selected cluster under
the Toggle Charts header. Metrics are grouped into two sections:

MongoDB Metrics

    

Metrics associated with the MongoDB process. For metrics related to database
performance, such as DB Storage, Atlas presents the sum total across all
databases in the cluster.

## Note

Atlas retrieves database metrics every 20 minutes by default but adjusts
frequency when necessary to reduce the impact on database performance.

If you enable Display Opcounters on Separate Charts, Atlas replaces the
Opcounters option with the individual components of that chart.

Hardware Metrics

    

Metrics associated with the host machines supporting the cluster.

Charts marked with the `+` symbol are inactive, while charts marked with the
`-` symbol are active. Click on any chart to toggle the chart state.

← Review Serverless MetricsReview Sharded Clusters →

