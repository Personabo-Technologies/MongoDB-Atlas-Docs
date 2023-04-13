Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Multi Analyzer

Share Feedback

You can use the `multi` object in your index definition to specify alternate
analyzers with which to also index the field. When you index a field with
alternate analyzers in addition to the default analyzer, you can search the
collection with either the default or the alternate analyzer. This page
demonstrates how to specify alternate analyzers in your index definition using
`multi`. To learn more about searching with alternate analyzers, see Construct
a Query Path.

## Note

The `multi` path option is available only to fields of type string.

## Example

The following example index definition specifies an index on the `title` field
in the `sample_mflix.movies` collection using the `standard` analyzer. The
index definition also specifies keyword analyzer as an alternate analyzer for
the `title` field, with the name `keywordAnalyzer`. The Keyword Analyzer
analyzer indexes the entire field as a single term, so it returns results only
if the search term and the specified field match exactly.

You can create the example index using the Atlas UI Visual Editor or the JSON
Editor. After you select your preferred configuration method, select the
database and collection.

Visual Editor

JSON Editor

  1. Click Refine Your Index to configure your index.

  2. In the Field Mappings section, click Add Field to open the Add Field Mapping window.

  3. Select `title` from the Field Name dropdown.

  4. Click the Data Type dropdown and select String if it isn't already selected.

  5. Change Index Analyzer to `lucene.standard` if it isn't already selected.

  6. Click Add Multi Field to configure another analyzer on the `title` field.

  7. Enter `keywordAnalyzer` in the Multi Field Name and select `lucene.keyword` from the Index Analyzer dropdown.

  8. Click Add.

The following query uses the alternate analyzer, named `keywordAnalyzer`, to
search for exact matches on the string `The Count of Monte Cristo`.

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "The Count of Monte Cristo",  
            "path": { "value": "title", "multi": "keywordAnalyzer" }  
          }  
        }  
      },  
      {  
        $project: {  
          "title": 1,  
          "year": 1,  
          "_id": 0  
        }  
      }  
    ])  
  
The above query returns the following results:

    
    
    { "title" : "The Count of Monte Cristo", "year" : 1934 }  
      
    { "title" : "The Count of Monte Cristo", "year" : 1954 }  
    { "title" : "The Count of Monte Cristo", "year" : 1998 }  
  
By contrast, the same query using the `standard` analyzer would find all the
movies with the word `Count` or `Monte` or `Cristo` in the title.

← Language AnalyzersCustom Analyzers →

