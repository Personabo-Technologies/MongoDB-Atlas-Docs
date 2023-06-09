Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Keyword Analyzer

Share Feedback

The `keyword` analyzer accepts a string or array of strings as a parameter and
indexes them as single terms. Only exact matches on the field are returned.

## Important

Atlas Search won't index string fields that exceed 32766 characters using the
`keyword` analyzer.

## Example

The following example index definition specifies an index on the `summary`
field using the `keyword` analyzer:

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "summary": {  
            "type": "string",  
            "analyzer": "lucene.keyword"  
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
             "query": "No action required at this time.",  
             "path": "summary"  
            }  
         }  
      }  
    ])  
  
The above query returns the following result:

    
    
    { "_id" : 1, "summary" : "No action required at this time." }  
      
  
The following query returns no results:

    
    
    db.cases.aggregate([  
      
      {  
         $search: {  
           "text": {  
             "query": "action",  
             "path": "summary"  
            }  
         }  
      }  
    ])  
  
Two documents in the collection contain the string `action`, but the `keyword`
analyzer matches only documents in which the search term matches the entire
contents of the field exactly.

← Whitespace AnalyzerLanguage Analyzers →

