Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create, View, and Drop Databases

Share Feedback

On this page

  * Required Roles
  * Create a Database
  * View Databases
  * Drop a Database

You can use the Atlas UI to manage the databases in your database deployments.

## Required Roles

The following table describes the roles required to perform various actions to
a database in the Atlas UI:

Action

|

Required Role(s)  
  
|  
  
Create Databases

|

One of the following roles:

  * `Project Owner` or `Organization Owner`

  * `Project Data Access Admin`

  * `Project Data Access Read/Write`

  
  
View Databases

|

At least the `Project Data Access Read Only` role.  
  
Drop Databases

|

One of the following roles:

  * `Project Owner`

  * `Project Data Access Admin`

  
  
## Create a Database

To create a database through the Atlas UI:

1

### Navigate to the Collections tab.

2

### Click Create Database.

3

### Enter the Database Name and the Collection Name.

Enter the Database Name and the Collection Name to create the database and its
first collection.

## Important

Don't include sensitive information in your database and collection names.

For more information on MongoDB database names and collection names, see
Naming Restrictions.

4

### Optional. Specify a capped collection.

Select whether the collection is a capped collection. If you select to create
a capped collection, specify the maximum size in bytes.

5

### Optional. Specify a time series collection.

Select whether the collection is a time series collection. If you select to
create a time series collection, specify the time field and granularity. You
can optionally specify the meta field and the time for old data in the
collection to expire.

6

### Click Create.

Upon successful creation, the database and the collection appears in the Atlas
UI.

## View Databases

From the Collections tab, you can view the databases and collections in the
deployment. Atlas UI shows the databases in the left pane:

click to enlarge

### Visualize Database Data

From the Collections tab, you can launch MongoDB Charts to visualize data in
your databases and collections.

To visualize data in MongoDB Charts from the Atlas UI, click Visualize Your
Data when viewing a specific database or collection. Charts loads the data
source and you can start building a chart in the Charts view. For detailed
steps, see Build Charts.

## Drop a Database

To drop a database, including all its collections, through the Atlas UI:

1

### Drop the database.

Either select or hover of the database to drop and click on its trash can
icon.

2

### Confirm action.

Confirm by typing the name of the database, and click Drop.

← Interact with Your DataCreate, View, Drop, and Shard Collections →

