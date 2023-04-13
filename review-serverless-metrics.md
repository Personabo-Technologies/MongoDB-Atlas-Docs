Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Serverless Metrics

Share Feedback

On this page

  * Chart Controls
  * Chart Display
  * Chart Selection

To view the metrics for a specific Atlas serverless instance from the Database
view of a project, click the View Monitoring button for that serverless
instance. Alternatively, click on the name of the serverless instance to open
the overview, then click Monitoring and the Metrics tab.

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
  
Filter by time range

|

Modifies the start and end date-time range of metrics displayed for each
chart. Modifying the start and end date sets the value of Zoom to `custom` and
overrides the previously selected zoom level.  
  
Add Chart

|

Select one or more charts to display or hide.  
  
Group Opcounters metrics

|

Directs Atlas to group the individual components of the Opcounters chart.  
  
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
  
View a chart in list or tile format.

|

Click the list and tile toggle to switch between the list and tile view.  
  
## Chart Selection

Atlas displays the available metrics to chart for the selected serverless
instance under the Toggle Charts header.

## Note

Currently, serverless instance metrics don't support any third-party services
(for example, Datadog).

Connections

    

Number that indicates the total active connections to the database deployment.

Monitor connections to determine whether the current connection limits are
sufficient. If necessary, upgrade the cluster tier.

Data Size

    

Number the indicates the amount of storage space in bytes that your stored
data uses.

Monitor storage space to determine whether to use disk auto-scaling or
manually increase the disk size. You can also monitor this metric to verify
backup billing.

Execution Time

    

Metrics that indicate the average time in seconds to execute operations.

Monitor execution time for an increase in read operations to optimize queries
and indexes.

Network

    

Metrics that indicate network performance.

Monitor network metrics to track network performance.

Opcounters

    

Metrics that indicate the operations per second run on a MongoDB process since
the process last started.

Monitor MongoDB operations to validate performance issues related to high
workloads. Confirm the type of operations responsible for the load.

Read/Write Units

    

Metrics that indicate the total read processing units (RPUs) and the total
write processing units (WPUs).

Monitor read and write units to help optimize queries and indexes.

← Review Project OverviewReview Replica Set Clusters →

