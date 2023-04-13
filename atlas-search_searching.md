Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create and Run Atlas Search Queries

Share Feedback

You can construct Atlas Search queries using the $search aggregation pipeline
stage. Atlas Search provides operators that you can use to perform specific
types of searches on your collection. When you run a `$search` query, Atlas
Search performs a full-text search of the indexed fields for data that matches
your query.

  * Enter the term to search in the collection.

  * View your Atlas Search query syntax, which you can then run in your MongoDB Shell, `mongosh`, or export to a programming language.

You must create Atlas Search indexes on the collection for all fields that you
want to search.

Atlas Search provides options that allow you to modify the score of returned
documents and to display the search terms in their original context.

You can run queries from `mongosh`, from your application using a driver, or
from the Atlas user interface.

Use the explain method to return detailed information about your queries.

## Note

If you are experiencing issues with your Atlas Search `$search` queries, see
Troubleshoot Atlas Search Errors.

← Delete an Atlas Search IndexChoose an Aggregation Pipeline Stage →

