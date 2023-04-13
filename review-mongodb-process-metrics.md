Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review MongoDB Processes

Share Feedback

On this page

  * Chart Controls
  * Chart Display
  * Chart Selection

Monitor database deployment metrics to identify performance issues and
determine whether your current database deployment meets your requirements.
For more information on the metrics available to monitor your database
deployments, see Review Available Metrics.

Atlas CLI

Atlas UI

To return the details for the MongoDB process you specify using the Atlas CLI,
run the following command:

    
    
    atlas processes describe <hostname:port> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas processes describe.

To list MongoDB processes for your project using the Atlas CLI, run the
following command:

    
    
    atlas processes list [options]  
      
  
To list MongoDB processes for the host you specify using the Atlas CLI, run
the following command:

    
    
    atlas metrics processes <hostname:port> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas processes list and atlas metrics
processes.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Chart Controls

Atlas provides the following controls for the Status, Hardware, and DB Stats
views. Adjusting any of these options affects all charts displayed under the
selected view:

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

Atlas displays the available metrics to chart for the selected cluster under
the Toggle Charts header.

Charts marked with the `+` symbol are inactive, while charts marked with the
`-` symbol are active. Click on any chart to toggle the chart state.

← Review Sharded ClustersReview Real-Time Metrics →

