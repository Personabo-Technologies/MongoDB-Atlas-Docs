Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Connect to your cluster in MongoDB Compass.

Share Feedback

Open MongoDB Compass and connect to your cluster. For detailed instructions on
connecting, see Connect via Compass.

2

# Use the `schools` collection in the `local_school_district` database.

Share Feedback

On the Database screen, click the `local_school_district` database, and then
click the `schools` collection.

3

# Run the following Atlas Search queries against the `schools` collection.

Share Feedback

The following queries search the documents inside the `teachers` array. The
queries use the following pipeline stages:

  * `$search` to search the collection.

  * `$project` to include the `_id` field and all the fields in the `teachers` array of documents, and add a field named `score` in the results.

Basic Search

Nested Array Search

The following query searches at the `teachers` path for teachers with the
first name `John` and specifies a preference for teachers with the last name
`Smith`.

Pipeline Stage

|

Query  
  
|  
  
`$search`

|

    
    
    | {  
      
      "embeddedDocument": {  
        "path": "teachers",  
        "operator": {  
          "compound": {  
            "must": [{  
              "text": {  
                "path": "teachers.first",  
                "query": "John"  
              }  
            }],  
            "should":[{  
              "text": {  
                "path": "teachers.last",  
                "query": "Smith"  
              }  
            }]  
          }  
        }  
      }  
    }  
  
`$project`

|

    
    
    | {  
      
      "_id": 1,  
      "teachers": 1,  
      "score": { $meta: "searchScore" }  
    }  
  
If you enabled Auto Preview, MongoDB Compass displays the following documents
next to the `$project` pipeline stage:  
      
    
    1| [  
    |  
    2|   {  
    3|     _id: 1,  
    4|     teachers: [  
    5|       {  
    6|         firstName: 'Jane',  
    7|         lastName: 'Earwhacker',  
    8|         classes: [  
    9|           { subject: 'art', grade: '9th' },  
    10|           { subject: 'science', grade: '12th' }  
    11|         ]  
    12|       },  
    13|       {  
    14|         firstName: 'John',  
    15|         lastName: 'Smith',  
    16|         classes: [  
    17|           { subject: 'math', grade: '12th' },  
    18|           { subject: 'art', grade: '10th' }  
    19|         ]  
    20|       }  
    21|     ],  
    22|     score: 0.7830756902694702  
    23|   },  
    24|   {  
    25|     _id: 2,  
    26|     teachers: [  
    27|       {  
    28|         firstName: 'Jane',  
    29|         lastName: 'Smith',  
    30|         classes: [  
    31|           { subject: 'science', grade: '9th' },  
    32|           { subject: 'math', grade: '12th' }  
    33|         ]  
    34|       },  
    35|       {  
    36|         firstName: 'John',  
    37|         lastName: 'Redman',  
    38|         classes: [ { subject: 'art', grade: '12th' } ]  
    39|       }  
    40|     ],  
    41|     score: 0.468008816242218  
    42|   }  
    43| ]  
  
The two documents in the results contain teachers with the first name `John`.
The document with `_id: 1` ranks higher because it contains a teacher with the
first name `John` who also has the last name `Smith`.

What is MongoDB Atlas? →

