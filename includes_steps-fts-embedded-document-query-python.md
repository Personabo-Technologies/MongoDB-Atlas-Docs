Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Create files named `basic-embedded-documents-query.py` and `nested-embedded-
documents-query.py`.

Share Feedback

2

# Copy and paste the code example into the respective file.

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

    
    
    import pymongo  
      
      
    # connect to your Atlas cluster  
    client = pymongo.MongoClient('<connection-string>')  
      
    # define pipeline  
    pipeline = [  
        {  
            '$search': {  
                'embeddedDocument': {  
                    'path': 'teachers',  
                    'operator': {  
                        'compound': {  
                            'must': [  
                                {  
                                    'text': {  
                                        'path': 'teachers.first',  
                                        'query': 'John'  
                                    }  
                                }  
                            ],  
                            'should': [  
                                {  
                                    'text': {  
                                        'path': 'teachers.last',  
                                        'query': 'Smith'  
                                    }  
                                }  
                            ]  
                        }  
                    }  
                }  
            }  
        }, {  
            '$project': {  
                '_id': 1,  
                'teachers': 1,  
                'score': {  
                    '$meta': 'searchScore'  
                }  
            }  
        }  
    ]  
      
    # run pipeline  
    result = client['local_school_district']['schools'].aggregate(pipeline)  
      
    # print results  
    for i in result:  
        print(i)  
  
Before you run the sample, replace `<connection-string>` with your Atlas
connection string. Ensure that your connection string includes your database
user's credentials. To learn more, see Connect via Your Application.

3

# Run the following command to query your collection:

Share Feedback

Basic Search

Nested Array Search

    
    
    python basic-embedded-documents-query.py  
      
  
HIDE OUTPUT

    
    
    1| {  
    |  
    2|     '_id': 1,   
    3|     'teachers': [  
    4|         {'first': 'Jane', 'last': 'Earwhacker', 'classes': [{'subject': 'art', 'grade': '9th'}, {'subject': 'science', 'grade': '12th'}]},   
    5|         {'first': 'John', 'last': 'Smith', 'classes': [{'subject': 'math', 'grade': '12th'}, {'subject': 'art', 'grade': '10th'}]}  
    6|     ],   
    7|     'score': 0.7830756902694702  
    8| }  
    9| {  
    10|     '_id': 2,   
    11|     'teachers': [  
    12|         {'first': 'Jane', 'last': 'Smith', 'classes': [{'subject': 'science', 'grade': '9th'}, {'subject': 'math', 'grade': '12th'}]},   
    13|         {'first': 'John', 'last': 'Redman', 'classes': [{'subject': 'art', 'grade': '12th'}]}  
    14|     ],   
    15|     'score': 0.468008816242218  
    16| }  
  
The two documents in the results contain teachers with the first name `John`.
The document with `_id: 1` ranks higher because it contains a teacher with the
first name `John` who also has the last name `Smith`.

What is MongoDB Atlas? →

