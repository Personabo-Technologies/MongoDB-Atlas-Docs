Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Whitespace Analyzer

Share Feedback

The `whitespace` analyzer divides text into searchable terms wherever it finds
a whitespace character. It leaves all terms in their original case.

## Example

The following example index definition specifies an index on the `summary`
field using the `whitespace` analyzer:

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "summary": {  
            "type": "string",  
            "analyzer": "lucene.whitespace"  
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
             "query":  "Frank's",  
             "path": "summary"  
            }  
         }  
      }  
    ])  
  
The above query returns the following result:

    
    
    { "_id" : 3, "summary" : "Frank's case is ready for planning." }  
      
  
The index is case-sensitive.

    
    
    db.cases.aggregate([  
      
      {  
         $search: {  
           "text": {  
             "query": "Case",  
             "path": "summary"  
            }  
         }  
      }  
    ])  
  
The above query returns the following result:

    
    
    { "_id" : 2, "summary" : "Case set aside for future action." }  
      
  
The document with `_id: 3` is not included, because it has the lower-case
string `case` and the search term is `Case`.

← Simple AnalyzerKeyword Analyzer →

