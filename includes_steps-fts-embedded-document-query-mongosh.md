Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Connect to your cluster using `mongosh`.

Share Feedback

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

# Use the `local_school` database.

Share Feedback

Run the following command at `mongosh` prompt:

    
    
    use local_school_district  
      
  
HIDE OUTPUT

    
    
    switched to db local_school_district  
      
  
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

    
    
    1| db.schools.aggregate({  
    |  
    2|   "$search": {  
    3|     "embeddedDocument": {  
    4|       "path": "teachers",  
    5|       "operator": {  
    6|         "compound": {  
    7|           "must": [{  
    8|             "text": {  
    9|               "path": "teachers.first",  
    10|               "query": "John"  
    11|             }  
    12|           }],  
    13|           "should":[{  
    14|             "text": {  
    15|               "path": "teachers.last",  
    16|               "query": "Smith"  
    17|             }  
    18|           }]  
    19|         }  
    20|       }  
    21|     }  
    22|   }  
    23| },  
    24| {  
    25|   "$project": {  
    26|     "_id": 1,  
    27|     "teachers": 1,  
    28|     "score": { $meta: "searchScore" }  
    29|   }  
    30| })  
  
HIDE OUTPUT

    
    
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

