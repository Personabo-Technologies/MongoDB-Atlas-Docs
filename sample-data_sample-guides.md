Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sample Guides Dataset

Share Feedback

On this page

  * Collections
  * Indexes
  * Sample Document

The `sample_guides` database contains data used in our guided tutorials.

To learn how to load the sample data provided by Atlas into your cluster, see
Load Sample Data.

## Collections

This database contains a single collection called `planets`.

The `sample_guides.planets` collection contains documents that represent a
planet in our Solar System.

Each document includes the following information about the planet:

  * Its order from the sun

  * Whether it has rings

  * The composition of its atmosphere

  * Its surface temperature

### Indexes

The `sample_guides.planets` collection contains the following indexes:

Name

|

Index

|

Description  
  
||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.  
  
### Sample Document

    
    
    {  
      
      _id: new ObjectId("6220f6b78a733c51b416c80e"),  
      name: 'Uranus',  
      orderFromSun: 7,  
      hasRings: true,  
      mainAtmosphere: [ 'H2', 'He', 'CH4' ],  
      surfaceTemperatureC: { min: null, max: null, mean: -197.2 }  
    }  
  
← Sample Geospatial DatasetSample Mflix Dataset →

