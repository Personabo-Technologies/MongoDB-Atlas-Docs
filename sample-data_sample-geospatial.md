Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sample Geospatial Dataset

Share Feedback

On this page

  * Collections
  * Indexes
  * Sample Document

The `sample_geospatial` database contains data specifically designed to help
familiarize you with GeoJSON data.

To learn how to load the sample data provided by Atlas into your cluster, see
Load Sample Data.

## Collections

This database contains a single collection called `shipwrecks`.

The `sample_geospatial.shipwrecks` collection contains all of the shipwreck
data in the dataset. Each document in the collection represents a shipwreck
and contains details such as where the wreck took place and the type of wreck
that occurred.

### Indexes

The `data` collection contains the following indexes:

Name

|

Index

|

Description

|

Properties  
  
|||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.

|  
  
`coordinates_2dsphere`

|

`{ "coordinates": "2dsphere" }`

|

Geospatial 2dsphere index on the `coordinates` GeoJSON format field.

|

Sparse  
  
### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "578f6fa2df35c7fbdbaed8c6"  
      },  
      "recrd": "",  
      "vesslterms": "",  
      "feature_type": "Wrecks - Submerged, dangerous",  
      "chart": "US,U1,graph,DNC H1409860",  
      "latdec": {  
        "$numberDouble": "9.3560572"  
      },  
      "londec": {  
        "$numberDouble": "-79.9074173"  
      },  
      "gp_quality": "",  
      "depth": "",  
      "sounding_type": "",  
      "history": "",  
      "quasou": "depth unknown",  
      "watlev": "always under water/submerged",  
      "coordinates": [  
        {  
          "$numberDouble": "-79.9074173"  
        },  
        {  
          "$numberDouble": "9.3560572"  
        }  
      ]  
    }  
  
← Sample Analytics DatasetSample Guides Dataset →

