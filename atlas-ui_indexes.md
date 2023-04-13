Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create, View, Drop, and Hide Indexes

Share Feedback

On this page

  * Required Roles
  * Considerations
  * View Indexes
  * Create an Index
  * Drop an Index
  * Hide an Index

You can use the Atlas CLI or the Atlas UI to manage indexes on your
collections.

Indexes support the efficient execution of queries in MongoDB and should be
considered for fields which your application reads often. To learn more about
creating effective indexes, see Indexing Strategies.

## Required Roles

To create, drop, or hide indexes, you must have access provided by at least
one of the following roles:

  * `Project Owner` or `Organization Owner`

  * `Project Data Access Admin`

## Considerations

By default, you can have up to three concurrent index builds. To learn more,
see Maximum Concurrent Index Builds.

## View Indexes

From the Collections tab, you can view index information for a collection. To
view index information for a collection:

1

### Select the database for the collection.

The main panel and Namespaces on the left side list the collections in the
database.

click to enlarge

2

### Select the collection on the left-hand side or in the main panel.

The main panel displays the Find, Indexes, and Aggregation views.

3

### Select the Indexes view.

The indexes table lists the indexes and associated index information for the
collection. Index information includes the index definition, the size, and the
usage frequency.

click to enlarge

## Create an Index

## Tip

When you create indexes, keep the ratio of reads to writes on the target
collection in mind. Indexes come with a performance cost, but are more than
worth the cost for frequent queries on large data sets. Before you create an
index, review the documented indexing strategies.

## Note

You can build full-text search with Atlas Search. Atlas Search offers fine-
grained text indexing. To learn more, see Review Atlas Search Index Syntax.

Atlas CLI

Atlas UI

To create a rolling index for your Atlas cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters indexes create [indexName] [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters indexes create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Drop an Index

To drop an index from a collection by using the Atlas UI:

1

### Navigate to the Indexes tab.

From the Collections tab, select the collection with the index that you want
to drop. Then, click the Indexes tab.

2

### Drop the index.

Under the Action column, click the Drop Index icon for the index that you want
to drop.

3

### Confirm action.

In the dialog box, type the name of the index and click Drop.

## Important

You can't delete or hide the `_id` index. To learn more, see Unique Indexes.

Consider hiding the index to evaluate the impact of dropping an index before
you drop it. To learn more, see Hidden Indexes.

## Note

### Atlas CLI Limitation

You can't drop a cluster's index by using the Atlas CLI.

## Hide an Index

To hide an index by using the Atlas UI:

1

### Navigate to the Indexes tab.

From the Collections tab, select the collection with the index that you want
to hide. Then, click the Indexes tab.

2

### Hide the index.

Under the Action column, click the Hide Index icon for the index that you want
to hide.

3

### Confirm action.

In the dialog box, click Confirm.

## Note

To unhide the index, click the icon again and click Confirm to confirm your
action.

← Create, View, Update, and Delete DocumentsRun Aggregation Pipelines →

