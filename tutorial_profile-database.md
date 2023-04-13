Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Monitor Query Performance

Share Feedback

On this page

  * Considerations
  * Enable and Disable Profiling
  * Access the Query Profiler

 _Only available on M10+ clusters and serverless instances_

The Query Profiler diagnoses and monitors performance issues. This monitoring
can expose slow-running queries and their key performance statistics in the
Atlas UI. You can explore a sample of historical queries for up to the last 24
hours without additional cost or performance overhead.

Atlas collects and displays statistics from any of your `mongod` instances.
The Query Profiler identifies slow queries based on log data from your
`mongod` instances. Atlas displays this data in the Profiler section of an
instance.

## Note

The Query Profiler differs from the Database Profiler. The Query Profiler
identifies specific inefficient queries based on entries from your `mongod`
logs. The Database Profiler returns detailed information about commands
executed on the `mongod` based on the specified profiling level. Changing the
profiling level doesn't impact the slow queries displayed in the Query
Profiler.

The Profiler displays one aspect, such as Operation Execution Time or Server
Execution Time (serverless instances), that could reveal slow database
operations over a set time frame. It displays this data in both a chart and a
table that each can filter on aspect and time frame.

Atlas manages the threshold for slow operations for each `mongod` host based
on average operation execution time on that host.

## Note

To opt out of the Atlas-managed slow operation threshold and use a fixed slow
query threshold of 100 milliseconds instead, use the Atlas Administration API.
See Disable Managed Slow Operation Threshold. For `M0`, `M2`, `M5` clusters
and serverless instances, Atlas disables the Atlas-managed slow query
operation threshold by default and you can't enable it.

## Considerations

## Important

### Please read the following considerations before you enable profiling.

### Security

Profile data may include sensitive information including the content of
database queries. Ensure that exposing this data to Atlas is consistent with
your information security practices.

### Data Analysis Limitations

The Query Profiler displays up to the first of the following limits:

  * the most recent 10,000 operations, or

  * the most recent 10MB of logs.

### Data Display Limitations

Atlas displays no more than 10,000 data points in the Profiler charts.

Log data is processed in batches. Data can be delayed up to five minutes from
realtime.

#### Log Quantity

If a cluster experiences an activity spike and generates an extremely large
quantity of log messages, Atlas may stop collecting and storing new logs for a
period of time.

## Note

Log analysis rate limits apply only to the Performance Advisor UI, the Query
Profiler UI, and the Access Tracking UI. Downloadable log files are always
complete.

## Enable and Disable Profiling

## Important

### Required Privileges

To enable or disable Performance Advisor and Profiler for a project, you must
have the `Project Owner` role for the project or the `Organization Owner` role
on its parent organization.

Atlas enables Profiling by default.

To disable profiling:

  1. Click Project Settings in the left navigation.

  2. Toggle Performance Advisor and Profiler to Off.

## Access the Query Profiler

To access the Query Profiler:

  * For a cluster, click View Monitoring for that instance in the project panel then click Profiler.

## Note

When you access the Query Profiler at the cluster level, the Query Profiler
displays the data from the log on the primary node. You must select each
specific secondary node to view any long-running queries on those nodes.

  * For a serverless instance, click the Monitoring tab.

### Profiling Chart

Above the chart, select the metric and time period you want to see.

  1. Select the metric from the Display menu. Atlas accepts:

    * Default: Operation Execution Time or Server Execution Time (serverless instances)

    * Keys Examined

    * Docs Returned

    * Examined:Returned Ratio

    * Num Yields

    * Response Length

  2. Select the time period from the View Last menu. Atlas accepts:

    * 24 hr (default)

    * 12 hr

    * 6 hr

    * 1 hr

    * 15 min

To view a full query and its execution statistics, click on the point
representing it on the chart.

### Profiling Table

Above the table, select the namespace, operation type, and metric you wish to
profile:

  1. Click All Namespaces to change which combination of databases and collections to profile.

  2. Click All Operations to change which operations you want to profile.

  3. Click Operation Execution Time or Server Execution Time (serverless instances) to change which metric you want to profile. Atlas accepts:

    * Default: Operation Execution Time or Server Execution Time (serverless instances)

    * Keys Examined

    * Docs Returned

    * Examined:Returned Ratio

    * Num Yields

    * Response Length

← Enable or Disable Performance Advisor for a ProjectMonitor Real-Time
Performance →

