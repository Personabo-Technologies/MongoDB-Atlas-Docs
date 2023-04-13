Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Connect to your cluster in `mongosh`.

Share Feedback

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

# Switch to the `sample_training` database.

Share Feedback

Run the following command at `mongosh` prompt:

    
    
    use sample_training  
      
  
HIDE OUTPUT

    
    
    switched to db sample_training  
      
  
3

# Run the following `$unionWith` with an Atlas Search `$search` query.

Share Feedback

The following queries search both the `companies` and `inspections`
collections for the term `mobile` in the `name` and `business_name` fields
respectively. The query uses the following stages:

  * `$search` to search for companies that include `mobile` in the name.

  * `$unionWith` to do the following:

    * Use `$search` stage in the sub-pipeline to search for inspections of companies that include `mobile` in the name.

    * Perform a union of documents from the `companies` and documents from the `inspections` collections.

  * `$set` stage to add a new field named `source` that identifies the collection of the output documents.

  * `$limit` stage to limit the output to `3` results from each collection.

  * `$project` stage to:

    * Include only the specified fields in the results.

    * Add a field named `score`.

Basic Example

Facet Example

    
    
    db.companies.aggregate([  
      
    {  
      "$search": {  
        "text": {  
          "query": "Mobile",  
          "path": "name"  
        }  
      }  
    }, {  
      "$project": {  
        "score": {  
          "$meta": "searchScore"  
        },  
        "_id": 0,  
        "number_of_employees": 1,  
        "founded_year": 1,  
        "name": 1  
      }  
    }, {  
      "$set": {  
        "source": "companies"  
      }  
    }, {  
      "$limit": 3  
    }, {  
      "$unionWith": {  
        "coll": "inspections",  
        "pipeline": [  
          {  
            "$search": {  
              "text": {  
                "query": "Mobile",  
                "path": "business_name"  
              }  
            }  
          }, {  
            "$set": {  
              "source": "inspections"  
            }  
          }, {  
            "$project": {  
              "score": {  
                "$meta": "searchScore"  
              },  
              "source": 1,  
              "_id": 0,  
              "business_name": 1,  
              "address": 1  
            }  
          },  {  
            "$limit": 3  
          }, {  
            "$sort": {  
              "score": -1  
            }  
          }  
        ]  
      }  
    }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        name: 'XLR8 Mobile',  
        number_of_employees: 21,  
        founded_year: 2006,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        name: 'Pulse Mobile',  
        number_of_employees: null,  
        founded_year: null,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        name: 'T-Mobile',  
        number_of_employees: null,  
        founded_year: null,  
        score: 2.0815043449401855,  
        source: 'companies'  
      },  
      {  
        business_name: 'T. MOBILE',  
        address: { city: 'BROOKLYN', zip: 11209, street: '86TH ST', number: 440 },  
        score: 2.900916337966919,  
        source: 'inspections'  
      },  
      {  
        business_name: 'BOOST MOBILE',  
        address: { city: 'BRONX', zip: 10458, street: 'E FORDHAM RD', number: 261 },  
        score: 2.900916337966919,  
        source: 'inspections'  
      },  
      {  
        business_name: 'SPRING MOBILE',  
        address: {  
          city: 'SOUTH RICHMOND HILL',  
          zip: 11419,  
          street: 'LIBERTY AVE',  
          number: 12207  
        },  
        score: 2.900916337966919,  
        source: 'inspections'  
      }  
    ]  
  
What is MongoDB Atlas? →

