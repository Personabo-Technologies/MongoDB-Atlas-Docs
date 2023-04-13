Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Namespace Metadata Catalog for Wildcard Collections

Share Feedback

The Atlas Data Federation namespace catalog contains namespace metadata (such
as databases, collections, and partitions) for each wildcard (`*`) collection
in each federated database instance store in the federated database instance
storage configuration. For commands and queries on wildcard collections, Data
Federation returns the data from the catalog or returns an error if the
federated database instance store doesn't exist.

When objects that are included in a wildcard collection specification are
modified in your S3 bucket, the catalog must be updated for you to see the
changes when you run `list` commands against wildcard collections. By default,
the catalog is refreshed every hour for all active federated database
instances. In addition, the namespace metadata catalog is refreshed in the
background when you:

  * Update the storage configuration.

  * Run the `show collections` command.

  * Query a collection.

  * Run the `updateCatalog` command.

You can determine when the catalog was last updated by using the `catalogInfo`
command and can manually update the catalog by using the `updateCatalog`
command. You must have the atlasAdmin role to update the catalog.

← `dropStore``catalogInfo` →

