Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Atlas Data Federation Query Limits

Share Feedback

On this page

  * Overview
  * What Happens When Atlas Data Federation Reaches the Data Limit?
  * What Happens When You Enable Query Termination?
  * Procedures
  * Add Query Limits
  * View Query Limits
  * Edit Query Limits
  * Delete Query Limits

## Overview

You can limit the amount of data that Atlas Data Federation processes for your
federated database instances to control costs. To limit the amount of
processed data, you can configure query limits per federated database instance
and for all federated database instances in your project. The query limits
that you configure only apply to data processing costs and don't apply to
other Atlas Data Federation costs such as data retrieval and transfer.

You can configure one limit _per query_ , _per day_ , _per week_ , and _per
month_ per project and per federated database instance. Atlas Data Federation
considers each limit of each type independent of other configured limits. If
you configure the same type of limit for the project and for a federated
database instance in the project, Atlas Data Federation enforces the more
restrictive limit of the two.

By default, Atlas Data Federation sets a 100 TB limit on the amount of
processed data per month for all new federated database instances.

### What Happens When Atlas Data Federation Reaches the Data Limit?

When the amount of processed data reaches the configured limit amount, Atlas
Data Federation stops processing data for the query that has reached the limit
if the limit type is _per query_. For limits of other types, Atlas Data
Federation doesn't execute any new queries until the limit resets based on the
configured limit type. That is, Atlas Data Federation doesn't execute any new
queries until:

  * The next calendar day beginning at `00:00` UTC for limit type of _per day_.

  * The next calendar week beginning on Monday at `00:00` UTC for limit type of _per week_.

  * The next calendar month beginning on the first day (1st) of the month at `00:00` UTC for limit type of _per month_.

If you configure the same type of limit for both the project and federated
database instances in the project, but with different limit amounts for the
project and the federated database instances in the project, the following
apply:

  * If Atlas Data Federation reaches the project limit amount before reaching the limit amount for any federated database instance in the project, Atlas Data Federation allows all running queries against all federated database instances in the project to complete.

  * If Atlas Data Federation doesn't reach the limit amount for the project, but reaches the limit amount set for any federated database instance in the project, Atlas Data Federation allows all running queries against that federated database instance to complete, but doesn't execute any new queries against that federated database instance. Atlas Data Federation continues to execute queries against other federated database instances in the project until it reaches the limit amount set for the project. When Atlas Data Federation reaches the project limit amount, Atlas Data Federation allows all running queries against all federated database instances in the project to complete, but doesn't execute any new queries against any federated database instances in the project.

Atlas Data Federation displays a warning in the Atlas UI when Atlas Data
Federation reaches the data processing limit. Additionally, you can configure
Atlas Data Federation to terminate queries that exceed the limit ASAP when
Atlas Data Federation reaches the limit instead of allowing running queries to
complete.

### What Happens When You Enable Query Termination?

If you configure Atlas Data Federation to terminate queries that exceed the
limit, Atlas Data Federation attempts to terminate the queries when Atlas Data
Federation reaches the applicable limit. While Atlas Data Federation attempts
to terminate the query, Atlas Data Federation might exceed the limit
marginally. Atlas Data Federation doesn't return any results and returns only
an error. However, you will see data processing charges for the amount of data
that Atlas Data Federation processed before it reached the limit.

If you configure the same type of limit for both the project and federated
database instances in the project, but with different limit amounts and query
termination settings, Atlas Data Federation will terminate the query only when
the amount of data that Atlas Data Federation processes reaches the limit
amount that you associated with query termination.

## Example

Suppose a 100 GB _per week_ project limit with termination enabled and a 60 GB
_per week_ federated database instance limit with termination disabled.

  * When one or more queries against the federated database instance reach the 60 GB limit, Atlas Data Federation terminates all running queries against the federated database instance and doesn't execute any new queries. Atlas Data Federation continues to execute all running and new queries against other federated database instances in the project until Atlas Data Federation reaches the project limit of 100 GB.

  * When one or more queries reach the 100 GB limit for the project, Atlas Data Federation doesn't execute any new queries and terminates all queries against all federated database instances in the project.

## Procedures

### Add Query Limits

You can configure limits on the amount of data processed for your queries from
the Atlas UI and API.

UI

API

1

#### Navigate to your federated database instances page.

  1. Log in to MongoDB Atlas.

  2. Select the Data Federation option on the left-hand navigation.

2

#### Click Manage Query Limits to configure limits per federated database
instance or for all federated database instances in the project.

You can configure limits for the project and per federated database instance.
Project level query limits apply to all federated database instances in the
project, which prevents new queries against any federated database instance
when the amount of processed data reaches the limit. Query limits on a
federated database instance apply to only that federated database instance,
and Atlas Data Federation won't execute any new queries against that federated
database instance when the amount of processed data reaches the limit. You can
also, optionally, enable termination of queries when Atlas Data Federation
reaches the configured limit.

3

#### Click Add Query Limit to configure the limit.

You can configure the following fields in the Add Query Limit window:

Field Name

|

Description  
  
|  
  
Limit For

|

Specify whether the limit is for a project or federated database instance.
Click the dropdown and select the project or federated database instance to
apply the limit to. After you add the limit, you can't modify this setting.  
  
Limit Type

|

Specify the limit duration. Click the dropdown to choose one of the following:

  * Per query \- Indicates that the limit is per individual query.

  * Per day \- Indicates that the limit is per calendar day beginning at `00:00` UTC.

  * Per week \- Indicates that the limit is per calendar week beginning on Monday at `00:00` UTC.

  * Per month \- Indicates that the limit is per calendar month beginning on the first day (1st) of the month at `00:00` UTC.

After you add the limit, you can't modify this setting.  
  
Limit Amount

|

Specify the amount of data in `MB`, `GB`, or `TB` to limit to.  
  
Terminate Queries

|

Toggle to enable query termination. You can't enable query termination for
**Per query** limit type because, by default, Atlas Data Federation terminates
the query when it reaches the limit for this limit type.  
  
4

#### Click Add Query Limit for the changes to take effect.

For limits of type Per query, the changes take effect immediately and Atlas
Data Federation enforces the limit for all new queries only. For limits of
other types, the following apply:

  * Per day \- The changes take effect at the start of Monday in the current week in UTC time.

  * Per week \- The changes take effect at the start of Monday in the current week in UTC time.

  * Per month \- The changes take effect on the first day, the beginning of the the monthly billing period, for the project in UTC time.

### View Query Limits

You can view the project and federated database instance limits on queries
from the Atlas UI and API. You can also view the amount of data that Atlas
Data Federation processed per instance per day.

UI

API

1

#### Navigate to your federated database instances page.

  1. Log in to MongoDB Atlas.

  2. Select the Data Federation option on the left-hand navigation.

2

#### Click Manage Query Limits to view the limits per federated database
instance and for all federated database instances in the project.

The Data Federation Query Limits page displays the following:

Column Name

|

Column Description  
  
|  
  
Limit for

|

Specifies the name of the project if the limit is for the project or the name
of the federated database instance if the limit is for a federated database
instance.  
  
Data Processed / Limit

|

Indicates the total amount of data processed by the queries. You can hover
your mouse over the processed data to view the following:

  * For a federated database instance, the limit start date and time

  * For a project:

    * If there aren't any federated database instance limits of the same type in the project, only the limit start date and time

    * If there are any federated database instance limits of any limit type:

      * Limit start date and time

      * Amount of processed data for the limit type

  
  
Limit Type

|

Indicates the type of limit. Value can be:

  * Per query

  * Per day

  * Per week

  * Per month

  
  
Terminate Queries

|

Indicates whether the flag to terminate running queries when Atlas Data
Federation reaches the limit is enabled.  
  
Actions

|

Displays the actions you can take on the limit. You can do the following:

  * Edit a query limit

  * Delete a query limit

  
  
### Edit Query Limits

You can edit the project and per federated database instance limits from the
Atlas UI and API.

UI

API

1

#### Navigate to your federated database instances page.

  1. Log in to MongoDB Atlas.

  2. Select the Data Federation option on the left-hand navigation.

2

#### Click Manage Query Limits to view the limits per federated database
instance and for all federated database instances in the project.

The Data Federation Query Limits page displays the actions you can take on the
corresponding limit in the Actions column.

3

#### Click __to open the Edit Query Limit window.

4

#### Make changes as needed to the following.

You can modify any of the following settings:

Field Name

|

Description  
  
|  
  
Limit Amount

|

Specify the amount of data in `MB`, `GB`, or `TB` to limit to. The following
apply if the new limit amount is more restrictive than any other limit of the
same type at another level:

  * If Atlas Data Federation hasn't yet reached the new limit amount, Atlas Data Federation starts executing new queries and restarts any terminated queries. To learn more, see What Happens When Atlas Data Federation Reaches the Data Limit?.

  * If Atlas Data Federation has already reached the new limit amount, Atlas Data Federation doesn't execute any new queries, but allows all running queries to complete if query termination is disabled. If you enabled query termination, Atlas Data Federation terminates all running queries. To learn more, see What Happens When You Enable Query Termination?.

  
  
Terminate Queries

|

Toggle to enable query termination. You can't enable query termination for
**Per query** limit type because for this limit type, Atlas Data Federation
will attempt to terminate each query as soon as it reaches the limit by
default. If you enable query termination for any other type, Atlas Data
Federation terminates the running queries that have reached the limit. If you
disable termination, Atlas Data Federation won't restart any terminated
queries and won't terminate any new or running query when Atlas Data
Federation reaches the limit amount. Instead, your running queries will be
able to finish and scan additional data.

To learn more, see What Happens When You Enable Query Termination?.  
  
5

#### Click Save Changes for the changes to take effect.

### Delete Query Limits

You can delete a project or per federated database instance limit from the
Atlas UI and API.

UI

API

1

#### Navigate to your federated database instances page.

  1. Log in to MongoDB Atlas.

  2. Select the Data Federation option on the left-hand navigation.

2

#### Click Manage Query Limits to view the limits per federated database
instance and for all federated database instances in the project.

The Data Federation Query Limits page displays the actions you can take on the
corresponding limit in the Actions column.

3

#### Click __to open the Delete Query Limit confirmation window.

4

#### Click Delete to confirm and delete the query limit.

When you delete a query limit, the changes take effect immediately. Atlas Data
Federation doesn't enforce limits on any running or new queries.

← Query a Federated Database InstanceQuery with SQL →

