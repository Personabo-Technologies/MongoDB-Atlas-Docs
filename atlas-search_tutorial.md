Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Started with Atlas Search

Share Feedback

On this page

  * Prerequisites
  * Roles
  * Next Steps

This tutorial takes you through the steps of setting up and querying an Atlas
Search index. You will use a collection with movie data from the Atlas sample
data set.

## Note

### Feature Unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Prerequisites

To complete this tutorial you will need:

  * An Atlas cluster with MongoDB version 4.2 or higher.

  * The sample datasets loaded into your Atlas cluster.

  * One of the following applications to run queries on your Atlas cluster:

    * `mongosh`

    * Compass

    * C#

    * Go

    * Java

    * MongoDB Node Driver

    * Pymongo

    * Atlas CLI

  * Choose static or dynamic index mapping.

## Roles

The following table shows the modes of access each role supports.

Role

|

Action

|

Atlas UI

|

Atlas API

|

Atlas Search API

|

Atlas CLI  
  
|||||  
  
`Project Data Access Read Only` or higher role

|

To view Atlas Search analyzers and indexes.

|

✓

|

✓

|

|  
  
`Project Data Access Admin` or higher role

|

To create and manage Atlas Search analyzers and indexes, and assign the role
to your API Key.

|

✓

|

✓

|

✓

|

✓  
  
`Project Owner` role

|

To create and assign project access to API Keys.

|

|

|

✓

|

✓  
  
`Organization Owner` role

|

To create access list entries for your API Key and send the request from a
client that appears in the access list for your API Key.

|

|

|

✓

|

✓  
  
`Project Search Index Editor`

|

To create, view, edit, and delete Atlas Search indexes using the Atlas UI or
API.

|

✓

|

✓

|

✓

|  
  
## Next Steps

Choose one of the following ways to create your Atlas Search index:

  * Atlas UI

  * Atlas Search API

  * Atlas CLI

## Note

To learn more about Atlas Search, you can take Unit 9 of the Intro To MongoDB
Course on MongoDB University. The 1.5 hour unit includes an overview of Atlas
Search and lessons on how to create Atlas Search indexes, use `$search` with
compound operators, and group results using facet.

← Use Atlas Search for Full-Text Search QueriesStep 1: Create an Atlas Search
Index →

