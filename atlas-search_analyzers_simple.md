Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Simple Analyzer

Share Feedback

The `simple` analyzer divides text into searchable terms wherever it finds a
non-letter character, such as whitespace, punctuation, or one or more digits.
It converts all terms to lower case.

## Example

The following example index definition specifies an index on the `summary`
field using the `simple` analyzer:

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "summary": {  
            "type": "string",  
            "analyzer": "lucene.simple"  
          }  
        }  
      }  
    }  
  
Consider a collection named `cases` with the following documents:

    
    
    { "_id": 1, "summary": "No action required at this time." }  
      
    { "_id": 2, "summary": "Case set aside for future action." }  
    { "_id": 3, "summary": "Frank's case is ready for planning." }  
  
The following query uses the index on the `summary` field:

    
    
    db.cases.aggregate([  
      
      {  
         $search: {  
           "text": {  
             "query": "frank",  
             "path": "summary"  
            }  
         }  
      }  
    ])  
  
The above query returns the following result:

    
    
    { "_id" : 3, "summary" : "Frank's case is ready for planning." }  
      
  
The `simple` analyzer indexes `Frank's case` as `[frank s case]`, so it
matches on the search term `frank`.

← Standard AnalyzerWhitespace Analyzer →

