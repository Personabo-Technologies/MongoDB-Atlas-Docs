Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run an Atlas Search Compound Geo JSON Query

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index
  * Run a Combined Geo, Number, and Text Fields Query

This tutorial describes how to create an index on the `listingsAndReviews`
collection in the `sample_airbnb` database and run a query that returns
documents with the `name`, `address`, and `property_type` for each property
within the specified polygon defined using `coordinates`.

This tutorial takes you through the following steps:

  1. Set up an Atlas Search index on the `address` field in the `sample_airbnb.listingsAndReviews` collection.

  2. Run a query that returns 10 documents with the `name`, `address`, and `property_type` of each property within the specified geographic `coordinates`. Atlas Search results reflect a preference for properties of type `condominium`, and each document in the result is assigned a relevance `score`, returned in order from highest to lowest.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index

In this section, you will create an Atlas Search index on the `address` field
in the `sample_airbnb.listingsAndReviews` collection.

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

  2. In the Database and Collection section, find the `sample_airbnb` database, and select the `listingsAndReviews` collection.

5

### Define an index on the `address` field.

You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index. The following index definition specifies that Atlas
Search must index:

  * All of the fields in the collection automatically.

  * The `address.location` field of a `document` as type `geo`.

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. In the Field Mappings section, click Add Field.

  4. Select address.location from the Field Name dropdown.

  5. Click the Data Type dropdown and select Geo.

  6. Click Add.

  7. Click Save Changes.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Run a Combined Geo, Number, and Text Fields Query

* * *

➤ Use the **Select your language** drop-down menu on this page to set the
language of the examples in this section.

* * *

In this section, you will run a query that returns 10 documents with the
`name`, `address`, and `property_type` for each property within the specified
geographic `coordinates`. A field specifying each documents `score` is also
returned, and results are ordered with a preference for properties of type
`condominium`.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_airbnb` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_airbnb  
      
  
MongoDB Shell

3

### Run the combined Atlas Search query in the `mongosh`.

The following Atlas Search query:

  * Uses a compound `$search` stage to:

    * Specify that `address.location` results `must` be within a `Polygon` defined by a set of `coordinates`.

    * Give preference to results for properties of type `condominium`.

  * Uses a `$project` stage to:

    * Exclude all fields except `name`, `address` and `property_type`.

    * Add a relevance `score` to each returned document.

The query is as follows:

    
    
    db.listingsAndReviews.aggregate([  
      
    {  
      "$search": {  
        "compound": {  
          "must": [{  
            "geoWithin": {  
              "geometry": {  
                "type": "Polygon",  
                "coordinates": [[[ -161.323242, 22.512557 ],  
                              [ -152.446289, 22.065278 ],  
                              [ -156.09375, 17.811456 ],  
                              [ -161.323242, 22.512557 ]]]  
              },  
              "path": "address.location"  
            }  
          }],  
          "should": [{  
            "text": {  
              "path": "property_type",  
              "query": "Condominium"  
            }  
          }]  
        }  
      }  
    },  
    {  
      "$limit": 10  
    },  
    {  
      $project: {  
        "_id": 0,  
        "name": 1,  
        "address": 1,  
        "property_type": 1,  
        score: { $meta: "searchScore" }  
      }  
    }  
    ])  
  
The preceding query returns the following results:

    
    
    [  
      
      {  
        name: 'Ocean View Waikiki Marina w/prkg',  
        property_type: 'Condominium',  
        address: {  
          street: 'Honolulu, HI, United States',  
          suburb: 'Oʻahu',  
          government_area: 'Primary Urban Center',  
          market: 'Oahu',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -157.83919, 21.28634 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!',  
        property_type: 'Condominium',  
        address: {  
          street: 'Lahaina, HI, United States',  
          suburb: 'Maui',  
          government_area: 'Lahaina',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.68012, 20.96996 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'Makaha Valley Paradise with OceanView',  
        property_type: 'Condominium',  
        address: {  
          street: 'Waianae, HI, United States',  
          suburb: 'Leeward Side',  
          government_area: 'Waianae',  
          market: 'Oahu',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -158.20291, 21.4818 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'March 2019 availability! Oceanview on Sugar Beach!',  
        property_type: 'Condominium',  
        address: {  
          street: 'Kihei, HI, United States',  
          suburb: 'Maui',  
          government_area: 'Kihei-Makena',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.46881, 20.78621 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'Tropical Jungle Oasis',  
        property_type: 'Condominium',  
        address: {  
          street: 'Hilo, HI, United States',  
          suburb: 'Island of Hawaiʻi',  
          government_area: 'South Hilo',  
          market: 'The Big Island',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -155.09259, 19.73108 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: '2 Bdrm/2 Bath  Family Suite Ocean View',  
        property_type: 'Condominium',  
        address: {  
          street: 'Honolulu, HI, United States',  
          suburb: 'Waikiki',  
          government_area: 'Primary Urban Center',  
          market: 'Oahu',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -157.82696, 21.27971 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: '302 Kanai A Nalu Ocean front/view',  
        property_type: 'Condominium',  
        address: {  
          street: 'Wailuku, HI, United States',  
          suburb: 'Maui',  
          government_area: 'Kihei-Makena',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.5039, 20.79664 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'Sugar Beach Resort 1BR Ground Floor Condo !',  
        property_type: 'Condominium',  
        address: {  
          street: 'Kihei, HI, United States',  
          suburb: 'Maui',  
          government_area: 'Kihei-Makena',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.46697, 20.78484 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: '2 BR Oceanview - Great Location!',  
        property_type: 'Condominium',  
        address: {  
          street: 'Kihei, HI, United States',  
          suburb: 'Kihei/Wailea',  
          government_area: 'Kihei-Makena',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.44917, 20.73013 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      },  
      {  
        name: 'PALMS AT WAILEA #905-2BR-REMODELED-LARGE LANAI-AC',  
        property_type: 'Condominium',  
        address: {  
          street: 'Kihei, HI, United States',  
          suburb: 'Maui',  
          government_area: 'Kihei-Makena',  
          market: 'Maui',  
          country: 'United States',  
          country_code: 'US',  
          location: {  
            type: 'Point',  
            coordinates: [ -156.4409, 20.69735 ],  
            is_location_exact: true  
          }  
        },  
        score: 2.238388776779175  
      }  
    ]  
  
← How to Run Atlas Search Queries with a Date Range FilterHow to Use Facets
with Atlas Search →

