Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Schema Management

Share Feedback

## Note

### Preview

The support for SQL queries is available as a Preview feature. This feature
and the corresponding documentation may change at any time during the Preview
phase.

Atlas SQL schemas are JSON schemas that describe data as it exists in MongoDB,
including its polymorphism, sparseness, and nested, structured data. Atlas
Data Federation can automatically generate a schema by sampling data from
documents in your collection or view.

Atlas Data Federation automatically generates a schema for a collection or
view in the storage configuration when you:

  * Create the collection or view in the storage configuration.

  * Rename a collection or view that does not already have a schema. If you rename a collection or view that already has a schema, the schema is also renamed. Atlas Data Federation does not generate a new schema for a renamed collection or view if it already exists.

  * Set the storage configuration.

In addition, for wildcard (`*`) collections, Atlas Data Federation generates a
schema when it discovers the collections in the namespace catalog for the
wildcard (`*`) collections.

You can manually generate schemas for all collections and views using the
`sqlGenerateSchema` command, set or update the schema for your collections or
views using the `sqlSetSchema` command, and view the stored schema using the
`sqlGetSchema` command.

You can manually delete a schema for a collection or view by running the
`sqlSetSchema` command with an empty schema document. Data Federation
automatically removes the schema for a collection or view when you:

  * Drop the collection or view from the storage configuration.

  * Modify the storage configuration to remove the collection or view from the storage configuration.

  * Drop the database that contains the collection or view from the storage configuration.

In addition, for a wildcard (`*`) collection, Atlas Data Federation deletes
the schema when it discovers that the collection has been removed from the
namespace catalog.

← Connect from the MongoDB ShellSQL Schema Format →

