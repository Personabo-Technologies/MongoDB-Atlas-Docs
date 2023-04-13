Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Database Triggers

Share Feedback

On this page

  * Database Triggers
  * Scheduled Triggers
  * Atlas Functions Provide Server-side Logic
  * Create a Trigger
  * Restart a Suspended Trigger
  * Find the Suspended Trigger
  * Restart the Trigger
  * External Dependencies
  * Configure a Trigger

Atlas **Triggers** allow you to execute server-side logic in response to
database events or according to a schedule. Atlas provides two kinds of
Triggers: **Database** and **Scheduled** triggers.

click to enlarge

## Database Triggers

Database Triggers allow you to execute server-side logic whenever a document
is added, updated, or removed in a linked Atlas cluster. Unlike SQL data
triggers, which run on the database server, triggers run on a serverless
compute layer that scales independently of the database server. Triggers
automatically call Atlas Functions and can forward events to external handlers
through AWS EventBridge.

Use database triggers to implement event-driven data interactions. For
example, you can automatically update information in one document when a
related document changes or send a request to an external service whenever a
new document is inserted.

Database triggers use MongoDB change streams to watch for real-time changes in
a collection. A change stream is a series of database events that each
describe an operation on a document in the collection. Your app opens a single
change stream for each collection with at least one enabled trigger. If
multiple triggers are enabled for a collection they all share the same change
stream.

You control which operations cause a trigger to fire as well as what happens
when it does. For example, you can run a function whenever a specific field of
a document is updated. The function can access the entire change event, so you
always know what changed. You can also pass the change event to AWS
EventBridge to handle the event outside of Atlas.

Triggers support $match expressions to filter change events and $project
expressions to limit the data included in each event.

## Important

### Change Stream Limitations

There are limits on the total number of change streams you can open on a
cluster, depending on the cluster's size. See change stream limitations for
more information.

You cannot define a database trigger on a serverless instance or federated
database instance because they do not support change streams.

## Note

MongoDB Atlas performs a `replace` command rather than an `update` command
when executing an update via the Atlas UI. Database triggers will only
recognize this update via the Atlas UI if you have marked the replace database
event for the trigger.

## Scheduled Triggers

Scheduled triggers allow you to execute server-side logic on a regular
schedule that you define using CRON expressions. Use scheduled triggers to do
work that happens on a periodic basis, such as updating a document every
minute, generating a nightly report, or sending an automated weekly email
newsletter.

## Atlas Functions Provide Server-side Logic

Triggers execute a function that you specify. Each trigger is associated with
exactly one Function.

When you create a trigger, you will see a function editor where you can write
the JavaScript code to be executed by the trigger. This function exists in a
shared App Services app called Triggers, which Atlas creates automatically for
you.

To find this app, click App Services in the navigation and select the Triggers
app.

## Note

Triggers created between 09 June 2020 and 01 June 2022 use the name
Triggers_RealmApp. Triggers created prior to 09 June 2020 use the name
Triggers_StitchApp.

## Create a Trigger

To create a new database or scheduled trigger:

  1. Click the Data Services tab in the top navigation of your screen if you haven't already navigated to Atlas.

  1. Click Triggers in the left-hand navigation.

  2. On the Overview tab of the Triggers page, click Add Trigger to open the trigger configuration page.

  3. Enter configuration values for the trigger and click Save at the bottom of the page.

## Restart a Suspended Trigger

Triggers may enter a suspended state in response to an event that prevents the
trigger's change stream from continuing, such as a network disruption. When a
trigger is suspended, it does not receive change events and will not fire.

## Note

In the event of a failed trigger, Atlas App Services sends an email
notification to the project owner, alerting them of the issue.

To restart a suspended trigger:

1

### Find the Suspended Trigger

On the Database Triggers tab of the Triggers page, find the trigger that you
want to resume in the list of triggers. Suspended triggers are marked with a
Status of Suspended.

click to enlarge

2

### Restart the Trigger

Click Restart in the trigger's Actions column.

You can choose to restart the trigger with a change stream resume token or
open a new change stream. Indicate whether or not to use a resume token and
then click Resume Database Trigger.

## Note

### Resume Tokens

If you use a resume token, Atlas attempts to resume the trigger's underlying
change stream at the event immediately following the last change event it
processed. If successful, the trigger processes any events that occurred while
it was suspended.

If you do not use a resume token, the trigger begins listening for new events
but will not fire for any events that occurred while it was suspended.

click to enlarge

## External Dependencies

An external dependency is an external library that includes logic you'd rather
not implement yourself, such as string parsing, convenience functions for
array manipulations, and data structure or algorithm implementations.

You can upload external dependencies from the npm repository to App Services
and then import those libraries into your functions using standard JavaScript
module syntax. To use external dependencies in the functions run by your
triggers, see External Dependencies.

## Configure a Trigger

To configure a Database trigger, see Database Trigger Configuration.

To configure a Scheduled trigger, see Scheduled Trigger Configuration.

← Run Aggregation PipelinesTrigger Configuration Parameters →

