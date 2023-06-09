Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Trigger Configuration Parameters

Share Feedback

On this page

  * Database Trigger Configuration
  * Database Change Events
  * Scheduled Trigger Configuration

## Database Trigger Configuration

Database triggers have the following configuration parameters:

Field

|

Description  
  
|  
  
Trigger Type

|

The type of the trigger. Set to Database to make a Database trigger.  
  
Name

|

The name of the trigger.  
  
Enabled

|

Default: Enabled. A toggle that indicates whether or not the trigger is
enabled. If enabled, the trigger will listen for events and execute its
associated function when events cause it to fire.  
  
Event Ordering

|

Default: Enabled. Indicates whether event ordering is enabled for this
trigger.

If event ordering is enabled, multiple executions of this trigger will occur
sequentially based on the timestamps of the change events. If event ordering
is disabled, multiple executions of this trigger will occur independently.

## Tip

Consider disabling event ordering if the trigger fires in response to periodic
bursts of events.

For example, suppose you have a daily batch job that inserts data to a
collection and a database trigger that fires on inserts to that collection.
Whenever the batch job runs, there will be a large number of trigger events to
handle.

Ordered triggers wait to execute a function for a particular event until the
functions of previous events have finished executing. As a consequence,
ordered triggers are effectively rate-limited by the run time of each
sequential trigger function. This may cause a significant delay between the
database event and the trigger firing if a sufficiently large number of
trigger executions are queued.

Unordered triggers execute functions in parallel if possible, which can be
significantly faster (depending on your use case) but does not guarantee that
multiple executions of a trigger function occur in event order.  
  
Linked Data Sources

|

The names of one or more MongoDB Atlas clusters that the trigger function can
access after an event causes it to fire. A trigger can interact with
collections in a cluster if the cluster is listed in this field.  
  
Select Linked Cluster

|

The name of the MongoDB Atlas cluster that the trigger applies to. The trigger
listens for events in a collection within this cluster.  
  
Database Name

|

The MongoDB database that contains the watched collection.  
  
Collection Name

|

The name of the collection that the trigger watches for change events.  
  
Operation Type

|

One or more database operation types that cause the trigger to fire.  
  
Full Document

|

Default: Disabled. If enabled, indicates that `UPDATE` change events should
include the most current majority-committed version of the modified document
in the `fullDocument` field.

## Note

This option only affects `UPDATE` change events. `INSERT` and `REPLACE` events
always include the `fullDocument` field. `DELETE` events never include the
`fullDocument` field. For more information, see the change events reference
page.

## Warning

Update operations executed from MongoDB Compass or the MongoDB Atlas UI fully
replace the previous document. As a result, update operations from these
clients will generate `REPLACE` change events rather than `UPDATE` events.  
  
Full Document Before Change

|

 **(Beta)** If enabled, change events include a _document preimage_ , a copy
of the modified document from immediately _before_ MongoDB applied the change.
You can access the document preimage from the `fullDocumentBeforeChange` field
of `UPDATE`, `REPLACE`, and `DELETE` events.

## Important

### Collection-Level Preimage Settings

To include document preimages in change events, MongoDB stores the preimage
for each change as part of the change's entry in the oplog. Depending on your
use case, this additional preimage data may have negative performance
implications and cause operations to fall off the oplog faster than they
otherwise would.

MongoDB stores preimages for entire collections. Once preimages are enabled
for any trigger on a given collection, you can enable preimages for other
triggers on the same collection without additional overhead.

Once enabled, a collection's oplog entries continue to include preimage data
even if no triggers actively use them. To stop including preimages in the
oplog, you must explicitly disable preimages for the collection.

To learn more, see Collection-level Preimages in the App Services
documentation.  
  
Function

|

an Atlas function, written in JavaScript, that the trigger executes whenever
it fires. The trigger passes the database event object that caused it to fire
as the only argument to this function.

This function exists in a shared App Services app called Triggers, which Atlas
automatically creates for you.

## Note

Triggers created between 09 June 2020 and 01 June 2022 use the name
Triggers_RealmApp. Triggers created prior to 09 June 2020 use the name
Triggers_StitchApp.

## Tip

### See also:

Functions Provide Server-side Logic

## Note

### AWS EventBridge

You can configure a trigger to send an event to AWS EventBridge rather than
call a function.

## Tip

### See also:

Send Trigger Events to AWS EventBridge.  
  
Match Expression

|

Default: `{}` i.e. "Match All". A `$match` expression document that is
prepended to the beginning of the trigger's underlying change stream
aggregation pipeline. All change event objects for the trigger are evaluated
against this match expression and the trigger will not fire unless the
expression evaluates to `true` for a given change event. This is useful when
you want to filter change events using data other than their operation type.

## Example

The following Match Expression document prevents the trigger from firing
unless the document's `status` field was updated to have a value of
`"blocked"`:

    
    
    | {  
      
      "updateDescription.updatedFields": {  
        "status": "blocked"  
      }  
    }  
  
### Database Change Events

Database change events represent individual changes in a specific collection
of a MongoDB cluster.

Every database event has the same operation type and structure as the change
event object that was emitted by the underlying change stream. Change events
have the following operation types:

Operation Type

|

Represents  
  
|  
  
`INSERT`

|

A new document that was added to the collection.  
  
`UPDATE`

|

A change to an existing document in the collection.  
  
`REPLACE`

|

A new document that replaced a document in the collection.  
  
`DELETE`

|

A document that was deleted from the collection.  
  
Database change event objects have the following general form:

    
    
    {  
      
       _id : <ObjectId>,  
       "operationType": <string>,  
       "fullDocument": <document>,  
       "ns": {  
          "db" : <string>,  
          "coll" : <string>  
       },  
       "documentKey": {  
         "_id": <ObjectId>  
       },  
       "updateDescription": <document>,  
       "clusterTime": <Timestamp>  
    }  
  
## Tip

### See also:

change events for detailed descriptions of these fields.

## Scheduled Trigger Configuration

Scheduled triggers have the following configuration parameters:

Field

|

Description  
  
|  
  
Trigger Type

|

The type of the trigger. Set to Scheduled to make a Scheduled trigger.  
  
Name

|

The name of the trigger.  
  
Enabled

|

Default: Enabled. A toggle that indicates whether or not the trigger is
enabled. If enabled, the trigger will execute its associated function on
schedule.  
  
Schedule Type

|

Default: Basic. The schedule on which to run the trigger.

In Basic mode, drop-downs control the trigger frequency. You can set the
trigger to repeat by minutes, by hours, on a specific day of the week, or on a
specific day of the month. The Next Events box shows a preview of when the
trigger will run according to the dropdown settings.

In Advanced mode, a CRON expression determines when to fire the trigger. The
Next Events box shows a preview of when the trigger will run according to the
CRON expression.  
  
Enabled Clusters

|

The names of one or more MongoDB Atlas clusters that the trigger function can
access after an event causes it to fire. A trigger can interact with
collections in a cluster if the cluster is listed in this field.  
  
Function

|

an Atlas function, written in JavaScript, that the trigger executes whenever
it fires. This function exists in a shared App Services app called Triggers,
which Atlas automatically creates for you.

## Note

Triggers created between 09 June 2020 and 01 June 2022 use the name
Triggers_RealmApp. Triggers created prior to 09 June 2020 use the name
Triggers_StitchApp.

## Tip

### See also:

Functions Provide Server-side Logic.  
  
← Configure Database TriggersSend Trigger Events to AWS EventBridge →

