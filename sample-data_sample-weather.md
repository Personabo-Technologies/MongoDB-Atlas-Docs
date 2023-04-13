Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sample Weather Dataset

Share Feedback

On this page

  * Collections
  * Indexes
  * Sample Document

The `sample_weatherdata` database contains detailed weather reports from
various locations. Each report contains readings such as `airTemperature`,
`wind`, and `visibility`. Each report contains a location which is stored as
GeoJSON.

To learn how to load the sample data provided by Atlas into your cluster, see
Load Sample Data.

## Collections

This database contains a single collection called `data`.

The `sample_weatherdata.data` collection contains all of the weather reports
in the dataset. Each document in the collection represents a single weather
report. The various weather observations within the document typically exist
in embedded objects.

### Indexes

The `sample_weatherdata.data` collection contains the following indexes:

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
      
      "_id": {  
        "$oid": "5553a998e4b02cf7151190c9"  
      },  
      "st": "x+51900+003200",  
      "ts": {  
        "$date": {  
          "$numberLong": "447354000000"  
        }  
      },  
      "position": {  
        "type": "Point",  
        "coordinates": [  
          {  
            "$numberDouble": "3.2"  
          },  
          {  
            "$numberDouble": "51.9"  
          }  
        ]  
      },  
      "elevation": {  
        "$numberInt": "9999"  
      },  
      "callLetters": "PLAT",  
      "qualityControlProcess": "V020",  
      "dataSource": "4",  
      "type": "FM-13",  
      "airTemperature": {  
        "value": {  
          "$numberDouble": "4.8"  
        },  
        "quality": "1"  
      },  
      "dewPoint": {  
        "value": {  
          "$numberDouble": "4.6"  
        },  
        "quality": "1"  
      },  
      "pressure": {  
        "value": {  
          "$numberDouble": "1032.6"  
        },  
        "quality": "1"  
      },  
      "wind": {  
        "direction": {  
          "angle": {  
            "$numberInt": "170"  
          },  
          "quality": "1"  
        },  
        "type": "N",  
        "speed": {  
          "rate": {  
            "$numberDouble": "0.5"  
          },  
          "quality": "1"  
        }  
      },  
      "visibility": {  
        "distance": {  
          "value": {  
            "$numberInt": "999999"  
          },  
          "quality": "9"  
        },  
        "variability": {  
          "value": "N",  
          "quality": "9"  
        }  
      },  
      "skyCondition": {  
        "ceilingHeight": {  
          "value": {  
            "$numberInt": "99999"  
          },  
          "quality": "9",  
          "determination": "9"  
        },  
        "cavok": "N"  
      },  
      "sections": [  
        "AG1",  
        "MD1",  
        "OA1",  
        "SA1"  
      ],  
      "precipitationEstimatedObservation": {  
        "discrepancy": "2",  
        "estimatedWaterDepth": {  
          "$numberInt": "999"  
        }  
      },  
      "atmosphericPressureChange": {  
        "tendency": {  
          "code": "2",  
          "quality": "1"  
        },  
        "quantity3Hours": {  
          "value": {  
            "$numberDouble": "1.2"  
          },  
          "quality": "1"  
        },  
        "quantity24Hours": {  
          "value": {  
            "$numberDouble": "99.9"  
          },  
          "quality": "9"  
        }  
      },  
      "seaSurfaceTemperature": {  
        "value": {  
          "$numberDouble": "5.5"  
        },  
        "quality": "9"  
      }  
    }  
  
← Sample Training DatasetCreate and Connect to Database Deployments →

