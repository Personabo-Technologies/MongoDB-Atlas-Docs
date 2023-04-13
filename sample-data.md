Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Load Sample Data

Share Feedback

On this page

  * Load Sample Data
  * Available Sample Datasets
  * Sample Data Namespaces
  * Tutorials Using Sample Data
  * MongoDB University Courses that Use Sample Data

 _Estimated completion time: 5 minutes_

Atlas provides sample data you can load into your Atlas database deployments.
You can use this data to quickly get started experimenting with data in
MongoDB and using tools such as the Atlas UI and MongoDB Charts.

For a list of datasets in the sample and a description of each, see Available
Sample Datasets. Each dataset page contains information on the databases,
collections, and indexes in the dataset.

## Load Sample Data

### Prerequisites

To utilize the sample data provided by Atlas, you must create an Atlas
database deployment to load data into. To learn more, see Create a Database
Deployment.

### Procedure

You can load sample data into your Atlas database deployment in several ways.
You can load sample data from the Atlas UI Database Deployments view, or use
the Atlas CLI.

Select the appropriate tab based on how you would like to load sample data:

Atlas CLI

Atlas UI

To load sample data into your Atlas cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters loadSampleData <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters loadSampleData.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

If you run `atlas setup` with the default selections, you don't need to run
`atlas loadSampleData`.

## Available Sample Datasets

The following table shows the sample datasets available for Atlas database
deployments. Click a sample dataset to learn more about it.

For instructions on loading this sample data into your Atlas database
deployment, see Load Sample Data.

Dataset Name

|

Description  
  
|  
  
Sample AirBnB Listings Dataset

|

Contains details on AirBnB listings.  
  
Sample Analytics Dataset

|

Contains training data for a mock financial services application.  
  
Sample Geospatial Dataset

|

Contains shipwreck data.  
  
Sample Guides Dataset

|

Contains planet data.  
  
Sample Mflix Dataset

|

Contains movie data.  
  
Sample Restaurants Dataset

|

Contains restaurant data.  
  
Sample Supply Store Dataset

|

Contains data from a mock office supply store.  
  
Sample Training Dataset

|

Contains MongoDB training services dataset.  
  
Sample Weather Dataset

|

Contains detailed weather reports.  
  
## Sample Data Namespaces

When you load the sample data, Atlas creates the following namespaces on your
database deployment:

## Warning

If any of these namespaces already exist on your database deployment when you
attempt to load the sample data, the operation will fail and no sample data
will be loaded into your database deployment.

Database

|

Collection  
  
|  
  
`sample_airbnb`

|

`listingsAndReviews`  
  
`sample_analytics`

|

`accounts`  
  
`sample_analytics`

|

`customers`  
  
`sample_analytics`

|

`transactions`  
  
`sample_geospatial`

|

`shipwrecks`  
  
`sample_guides`

|

`planets`  
  
`sample_mflix`

|

`comments`  
  
`sample_mflix`

|

`movies`  
  
`sample_mflix`

|

`theaters`  
  
`sample_mflix`

|

`users`  
  
`sample_supplies`

|

`sales`  
  
`sample_training`

|

`companies`  
  
`sample_training`

|

`grades`  
  
`sample_training`

|

`inspections`  
  
`sample_training`

|

`posts`  
  
`sample_training`

|

`routes`  
  
`sample_training`

|

`trips`  
  
`sample_training`

|

`zips`  
  
`sample_weatherdata`

|

`data`  
  
## Tutorials Using Sample Data

### Atlas Tutorials

The Get Started with Atlas tutorial walks through setting up an Atlas cluster
and populating that cluster with sample data.

### Atlas Search Tutorials

Get Started with Atlas Search

    Create an Atlas Search index using data from the sample_mflix sample database and run queries against the movies collection in the sample database.
Atlas Search Tutorials

    Set up and query an Atlas Search index. The Atlas Search Tutorials section contains many tutorials to take you through the steps of using Atlas Search. You can learn about everything from How to Use Autocomplete with Atlas Search, to How to Run Atlas Search Queries with a Date Range Filter, or How to Run Multilingual Atlas Search Queries, and more. Many of these tutorials use the sample_mflix sample database.

### MongoDB Charts Tutorials

The following MongoDB Charts tutorials guide you through visualizing sample
data provided by Atlas:

Visualizing Order Data

    Visualize the Sample Supply Store Dataset, which contains sales order data from a mock office supply company.
Visualizing Movie Details

    Visualize the Sample Mflix Dataset, which contains data on movies and movie theaters.

## Tip

To visualize data in MongoDB Charts from the Atlas UI, click Visualize Your
Data when viewing a specific database or collection. Charts loads the data
source and you can start building a chart in the Charts view. For detailed
steps, see Build Charts.

## MongoDB University Courses that Use Sample Data

The following MongoDB University courses and trainings utilize the sample data
provided by Atlas.

M001: MongoDB Basics

    MongoDB Basics is designed for learners brand new to MongoDB.
M121: The MongoDB Aggregation Framework

    Learn how to use MongoDB Aggregation Framework in your application development practices.
M220J: MongoDB for Java Developers

    Learn how to use MongoDB as the database for a Java application.
M220JS: MongoDB for Javascript Developers

    Learn how to use MongoDB as the database for a Node.js application.
M220P: MongoDB for Python Developers

    Learn how to use MongoDB as the database for a Python application.
All In-Person Training

    Get quickly ramped on MongoDB with comprehensive private training programs for developers and operations teams.

← Insert and View a DocumentSample AirBnB Listings Dataset →

