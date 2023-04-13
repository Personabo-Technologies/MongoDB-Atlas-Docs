Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Migrate Data with Self-Managed Tools

Share Feedback

You can bring data from existing MongoDB deployments, `JSON` or `CSV` files
into Atlas using one of the following tools that you run outside of Atlas.

## Note

### Serverless Instances are in Preview

To import data using the MongoDB Tools, including `mongodump`, `mongorestore`,
`mongoexport`, and `mongoimport`, you must have MongoDB Tools version 100.5.x
or later. To move data to a serverless instance, you can also use Compass to
export and import data.

To learn more about serverless instance limitations, see Serverless Instance
Limitations.

Tool

|

Description  
  
|  
  
mongomirror

|

Migrate from a MongoDB _replica set_ into an Atlas cluster without shutting
down your existing replica set or applications. mongomirror does not import
user/role data or copy the `config` database.  
  
mongorestore

|

Seed an Atlas cluster with a `BSON` data backup dump of an existing MongoDB
deployment. mongorestore does not restore `system.profile` collection data.  
  
mongoimport

|

Load data from a `JSON` or a `CSV` file into an Atlas cluster. `mongoimport`
uses strict mode representation for certain BSON types.  
  
MongoDB Compass

|

Use a GUI to load data from a `JSON` or a `CSV` file into an Atlas cluster.  
  
You can also restore from an Atlas cluster backup data to another Atlas
cluster. For information, see Restore Your Database Deployment.

← Troubleshoot Live Migration (Pull)Migrate with `mongomirror` →

