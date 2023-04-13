Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Language Analyzers

Share Feedback

On this page

  * Examples
  * Built-In Language Analyzer Example
  * Custom Language Analyzer Example

Use language-specific analyzers to create indexes tailored to a particular
language. Each language analyzer has built-in stop words and word divisions
based on that language's usage patterns.

Atlas Search offers the following language analyzers:

|

|

|  
  
|||  
  
`lucene.arabic`

|

`lucene.armenian`

|

`lucene.basque`

|

`lucene.bengali`  
  
`lucene.brazilian`

|

`lucene.bulgarian`

|

`lucene.catalan`

|

`lucene.chinese`  
  
`lucene.cjk` 1

|

`lucene.czech`

|

`lucene.danish`

|

`lucene.dutch`  
  
`lucene.english`

|

`lucene.finnish`

|

`lucene.french`

|

`lucene.galician`  
  
`lucene.german`

|

`lucene.greek`

|

`lucene.hindi`

|

`lucene.hungarian`  
  
`lucene.indonesian`

|

`lucene.irish`

|

`lucene.italian`

|

`lucene.japanese`  
  
`lucene.korean`

|

`lucene.kuromoji` 2

|

`lucene.latvian`

|

`lucene.lithuanian`  
  
`lucene.morfologik` 3

|

`lucene.nori` 4

|

`lucene.norwegian`

|

`lucene.persian`  
  
`lucene.polish`

|

`lucene.portuguese`

|

`lucene.romanian`

|

`lucene.russian`  
  
`lucene.smartcn` 5

|

`lucene.sorani`

|

`lucene.spanish`

|

`lucene.swedish`  
  
`lucene.thai`

|

`lucene.turkish`

|

`lucene.ukrainian`

|  
  
1 `cjk` is a generic Chinese, Japanese, and Korean analyzer

2 `kuromoji` is a Japanese analyzer

3 `morfologik` is a Polish analyzer

4 `nori` is a Korean analyzer

5 `smartcn` is a Chinese analyzer

## Examples

Consider a collection named `cars` with the following documents:

    
    
    {  
      
      "_id": 1,  
      "subject": {  
        "en": "It is better to equip our cars to understand the causes of the accident.",  
        "fr": "Mieux équiper nos voitures pour comprendre les causes d'un accident.",  
        "he": "עדיף לצייד את המכוניות שלנו כדי להבין את הגורמים לתאונה."  
      }  
    }  
      
    
    {  
      
      "_id": 2,  
      "subject": {  
        "en": "The best time to do this is immediately after you've filled up with fuel",  
        "fr": "Le meilleur moment pour le faire c'est immédiatement après que vous aurez fait le plein de carburant.",  
        "he": "הזמן הטוב ביותר לעשות זאת הוא מיד לאחר שמילאת דלק."  
      }  
    }  
  
### Built-In Language Analyzer Example

The following example index definition specifies an index on the `subject.fr`
field using the `french` analyzer:

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "subject": {  
            "fields": {  
              "fr": {  
                "analyzer": "lucene.french",  
                "type": "string"  
              }  
            },  
            "type": "document"  
          }  
        }  
      }  
    }  
  
The following query searches for the string `pour` in the `subject.fr` field:

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "pour",  
            "path": "subject.fr"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "subject.fr": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

The previous query returns no results when using the `french` analyzer,
because `pour` is a built-in stop word. Using the `standard` analyzer, the
same query would return both documents.

The following query searches for the string `carburant` in the `subject.fr`
field:

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "carburant",  
            "path": "subject.fr"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "subject.fr": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    { subject: { fr: "Le meilleur moment pour le faire c'est immédiatement après que vous aurez fait le plein de carburant." } }  
      
  
Atlas Search returns a document with `_id: 1` in the results because the query
matched a token that the `lucene.french` analyzer created for the document.
The `lucene.french` analyzer creates the following tokens for the `subject.fr`
field in document with `_id: 1`:

|

|  
  
||  
  
`meileu`

|

`moment`

|

`fair`  
  
`est`

|

`imediat`

|

`aprè`  
  
`fait`

|

`plein`

|

`carburant`  
  
### Custom Language Analyzer Example

You can also create indexes for unsupported languages by creating a custom
analyzer with the icuFolding and stopword token filters.

The following example index definition specifies an index on the `subject.he`
field using a custom analyzer called `myHebrewAnalyzer` to analyze and create
tokens for Hebrew text:

    
    
    {  
      
      "analyzer": "lucene.standard",  
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "subject": {  
            "fields": {  
              "he": {  
                "analyzer": "myHebrewAnalyzer",  
                "type": "string"  
              }  
            },  
            "type": "document"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "myHebrewAnalyzer",  
          "tokenFilters": [  
            {  
              "type": "icuFolding"  
            },  
            {  
              "tokens": [  
                "אן",  
                "שלנו",  
                "זה",  
                "אל"  
              ],  
              "type": "stopword"  
            }  
          ],  
          "tokenizer": {  
            "type": "standard"  
          }  
        }  
      ]  
    }  
  
The following query searches for the string `המכוניות` in the `subject.he`
field:

    
    
    db.cars.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "המכוניות",  
            "path": "subject.he"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 0,  
          "subject.he": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    { subject: { he: 'עדיף לצייד את המכוניות שלנו כדי להבין את הגורמים לתאונה.' } }  
      
  
Atlas Search returns a document with `_id: 1` in the results because the query
matched a token that the `myHebrewAnalyzer` analyzer created for document. The
`myHebrewAnalyzer` analyzer creates the following tokens for the `subject.he`
field in document with `_id: 1`:

|

|  
  
||  
  
`עדיף`

|

`לצייד`

|

`את`  
  
`המכוניות`

|

`כדי`

|

`להבין`  
  
`את`

|

`הגורמים`

|

`לתאונה`  
  
← Keyword AnalyzerMulti Analyzer →

