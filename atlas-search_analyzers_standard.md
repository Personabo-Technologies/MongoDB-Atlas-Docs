Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Standard Analyzer

Share Feedback

The `standard` analyzer is the default for all Atlas Search indexes and
queries. It divides text into terms based on word boundaries, which makes it
language-neutral for most use cases. It converts all terms to lower case and
removes punctuation. It provides grammar-based tokenization that recognizes
email addresses, acronyms, Chinese-Japanese-Korean characters, alphanumerics,
and more.

## Example

The following example index definition specifies an index on the `summary`
field using the `standard` analyzer:

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "summary": {  
            "type": "string",  
            "analyzer": "lucene.standard"  
          }  
        }  
      }  
    }  
  
Consider a collection named `cases` with the following documents:

    
    
    { "_id": 1, "summary": "No action required at this time." }  
      
    { "_id": 2, "summary": "Case set aside for future action." }  
    { "_id": 3, "summary": "Ready for planning." }  
  
The following query uses the index on the `summary` field:

    
    
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
  
The above query returns the following results:

    
    
    { "_id" : 1, "summary" : "No action required at this time." }  
      
    { "_id" : 2, "summary" : "Case set aside for future action." }  
  
← Process Data with AnalyzersSimple Analyzer →

