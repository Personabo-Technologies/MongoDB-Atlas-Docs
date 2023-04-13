Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Atlas Search String Queries Against Date and Numeric Fields

Select your language

MongoDB Shell

On this page

  * Create a Materialized View on the Collection
  * Create Atlas Search Indexes on Fields in the Materialized View
  * Perform Text Search on Converted Fields

This tutorial describes how to run Atlas Search queries against `string`,
`date`, and `number` fields in the `sample_airbnb.listingsAndReviews`
collection. You will create a materialized view that stores the numeric and
date field values as strings. You will then create an Atlas Search index on
the materialized view and run queries against these string fields using the
queryString and autocomplete operators. This tutorial takes you through the
following steps:

  1. Create a materialized view on the `sample_airbnb.listingsAndReviews` collection `name`, `property_type`, `last_scraped`, and `accomodates` fields.

  2. Set up dynamic and static Atlas Search indexes on the materialized view.

  3. Run Atlas Search queries against the fields in the materialized view using the queryString and autocomplete operators to search for properties.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create a Materialized View on the Collection

In this section, you will create a materialized view named `airbnb-mat-view`
for `name`, `property_type`, `last_scraped`, `accomodates`, and
`maximum_nights` fields in the `airbnb_listingsAndReviews` collection. The
materialized view allows you to take the numeric and date fields in the source
collection and store them as string fields in the materialized view.

1

### Log in to Atlas and connect to your cluster using `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Verify and switch to the `sample_airbnb` database.

  1. Run the following command to verify that the database exists in your cluster:
    
        show dbs  
      
  
HIDE OUTPUT

    
        sample_airbnb       55.3 MB  
      
    sample_analytics    9.59 MB  
    sample_geospatial   1.43 MB  
    sample_guides         41 kB  
    sample_mflix        51.1 MB  
    sample_restaurants  6.95 MB  
    sample_supplies     1.21 MB  
    sample_training     55.5 MB  
    sample_weatherdata  2.89 MB  
    admin                348 kB  
    local                2.1 GB  
  
  2. Run the following command to switch to the `sample_airbnb` database.
    
        use sample_airbnb  
      
  
HIDE OUTPUT

    
        switched to db sample_airbnb  
      
  

3

### Create a materialized view named `airbnb_mat_view`.

To create a materialized view, run the following query. The query specifies
the following aggregation pipeline stages:

  * `$project`: In this stage, the query does the following:

    * Converts the `last_scraped` date object to a string in the format `YYYY-MM-DD` using `$dateToString`.

    * Includes `name` and `property_type` string fields.

    * Converts `accomodates` number field to a string using `$toString`.

    * Converts `maximum_nights` number field to a string using `$toString`.

  * `$merge`: In this stage, the query writes the output fields from the `$project` stage to a materialized view named `airbnb_mat_view`.
    
        db.listingsAndReviews.aggregate( [  
      
      {  
        $project: {  
          lastScrapedDate: { $dateToString: { format: "%Y-%m-%d", date: "$last_scraped" } },  
          propertyName: "$name",  
          propertyType: "$property_type",  
          accommodatesNumber: { $toString: "$accommodates" },  
          maximumNumberOfNights: { $toString: "$maximum_nights" }  
        }  
      },  
      { $merge: { into: "airbnb_mat_view", whenMatched: "replace" } }  
    ] )  
  

4

### Verify that the materialized view was successfully created.

To verify, run the following command:

    
    
    db.airbnb_mat_view.findOne()  
      
  
HIDE OUTPUT

    
    
    {  
      
      _id: '10006546',  
      lastScrapedDate: '2019-02-16',  
      propertyName: 'Ribeira Charming Duplex',  
      propertyType: 'House',  
      accommodatesNumber: '8',  
      maximumNumberOfNights: '30'  
    }  
  
## Create Atlas Search Indexes on Fields in the Materialized View

In this section, you will create Atlas Search indexes on the
`lastScrapedDate`, `name`, `propertyType`, `accommodatesNumber`, and
`maximumNumberOfNights` fields for running queries against these fields.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_airbnb` database, and select the `airbnb_mat_view` collection.

5

### Define an index on the fields in the materialized view.

You can create one of the following indexes:

  * Index that uses dynamic mappings for running queries using the queryString operator. You can't run queries using the autocomplete operator if your index definition uses only dynamic mappings.

  * Index that uses static mappings for running queries using autocomplete operator. You can't run queries using the queryString operator against fields indexed as type `autocomplete`.

Dynamic Mappings

Static Mappings

You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Create Search Index.

6

### Click Create Search Index.

## Note

The You're All Set! modal window appears to let you know your index is
building.

7

### Close the You're All Set! modal window and wait for the index build to
complete.

## Perform Text Search on Converted Fields

You can run queries against the numeric and date fields that were converted to
strings. This tutorial uses queryString and autocomplete operators to search
for properties. The query uses the following pipeline stages:

  * `$search` stage to search the collection

  * `$limit` stage to limit the output to `5` results

  * `$project` stage to exclude `_id`

In this section, you will connect to your Atlas cluster and run the sample
queries using the operator against the fields in the `airbnb_mat_view`
collection.

## Note

You can't run near or range queries against the date and number fields that
were converted to strings in your materialized view.

* * *

➤ Use the **Select your language** drop-down menu on this page to set the
language of the examples in this section.

* * *

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster using `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_airbnb` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_airbnb  
      
  
MongoDB Shell

HIDE OUTPUT

    
    
    switched to db sample_airbnb  
      
  
3

### Run the following Atlas Search queries using the operator for which you
created the index.

If you created an index that uses dynamic mappings, you can query the
`airbnb_mat_view` collection using the queryString operator. If you created an
index that uses static mappings, you can query the `airbnb_mat_view`
collection using the autocomplete operator.

queryString Operator

autocomplete Operator

AND Query

OR Query

The following query searches for properties where the property type is
`Apartment` or `Condominium`, accommodates `2` people, and was listed in
`2019`.

    
    
    db.airbnb_mat_view.aggregate([  
      
      {  
        "$search": {  
          "queryString": {  
            "defaultPath": "propertyType",  
            "query": "propertyType: (Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019"  
          }  
        }  
      },  
      { $limit: 5 },  
      {  
        $project: {  
          "_id": 0  
        }  
      }  
    ])  
  
MongoDB Shell

HIDE OUTPUT

    
    
    1|   [  
    |  
    2|     {  
    3|       lastScrapedDate: '2019-03-06',  
    4|       propertyName: 'LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!',  
    5|       propertyType: 'Condominium',  
    6|       accommodatesNumber: '4'  
    7|     },  
    8|     {  
    9|       lastScrapedDate: '2019-03-06',  
    10|       propertyName: 'Makaha Valley Paradise with OceanView',  
    11|       propertyType: 'Condominium',  
    12|       accommodatesNumber: '4'  
    13|     },  
    14|     {  
    15|       lastScrapedDate: '2019-03-06',  
    16|       propertyName: 'March 2019 availability! Oceanview on Sugar Beach!',  
    17|       propertyType: 'Condominium',  
    18|       accommodatesNumber: '4'  
    19|     },  
    20|     {  
    21|       lastScrapedDate: '2019-03-06',  
    22|       propertyName: 'Tropical Jungle Oasis',  
    23|       propertyType: 'Condominium',  
    24|       accommodatesNumber: '4'  
    25|     },  
    26|     {  
    27|       lastScrapedDate: '2019-02-11',  
    28|       propertyName: 'Hospede-se com acesso fácil.',  
    29|       propertyType: 'Condominium',  
    30|       accommodatesNumber: '4'  
    31|     }  
    32|   ]  
    33|     
  
← How to Sort Your Atlas Search Results for Your Perfomance NeedsHow to Run
Atlas Search Queries Across Collections →

