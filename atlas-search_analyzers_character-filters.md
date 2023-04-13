Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Character Filters

Share Feedback

On this page

  * htmlStrip
  * icuNormalize
  * mapping
  * persian

Character filters require a type field, and some take additional options as
well.

    
    
    "charFilters": [  
      
      {  
        "type": "<filter-type>",  
        "<additional-option>": <value>  
      }  
    ]  
  
Atlas Search supports four types of character filters:

  * htmlStrip

  * icuNormalize

  * mapping

  * persian

The following sample index definitions and queries use the sample collection
named `minutes`. If you add the `minutes` collection to a database in your
Atlas cluster, you can create the following sample indexes and run the sample
queries against this collection.

## htmlStrip

The `htmlStrip` character filter strips out HTML constructs. It has the
following attributes:

Name

|

Type

|

Description

|

Required?

|

Default  
  
||||  
  
`type`

|

string

|

Human-readable label that identifies this character filter type. Value must be
`htmlStrip`.

|

yes

|  
  
`ignoredTags`

|

array of strings

|

List that contains the HTML tags to exclude from filtering.

|

no

|  
  
## Example

The following index definition example indexes the `text.en_US` field using a
custom analyzer named `htmlStrippingAnalyzer`. The custom analyzer specifies
the following:

  * Remove all HTML tags from the text except the `a` tag using the `htmlStrip` character filter.

  * Generate tokens based on word break rules from the Unicode Text Segmentation algorithm using the standard tokenizer.

    
    
    {  
      
      "mappings": {  
        "fields": {  
          "text": {  
            "type": "document",  
            "dynamic": true,  
            "fields": {  
              "en_US": {  
                "type": "string",  
                "analyzer": "htmlStrippingAnalyzer",  
              }  
            }  
          }  
        }  
      },  
      "analyzers": [{  
        "name": "htmlStrippingAnalyzer",  
        "charFilters": [{  
          "type": "htmlStrip",  
          "ignoredTags": ["a"]  
        }],  
        "tokenizer": {  
          "type": "standard"  
        },  
        "tokenFilters": []  
      }]  
    }  
  
The following query looks for occurrences of the string `head` in the
`text.en_US` field of the `minutes` collection.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "text": {  
    5|         "query": "head",  
    6|         "path": "text.en_US"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     "$project": {  
    12|       "_id": 1,  
    13|       "text.en_US": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 2,  
        text: { en_US: "The head of the sales department spoke first." }  
      },  
      {  
        _id: 3,  
        text: {  
          en_US: "<body>We'll head out to the conference room by noon.</body>"  
        }  
      }  
    ]  
  
Atlas Search doesn't return the document with `_id: 1` because the string
`head` is part of the HTML tag `<head>`. The document with `_id: 3` contains
HTML tags, but the string `head` is elsewhere so the document is a match. The
following table shows the tokens that Atlas Search generates for the
`text.en_US` field values in documents `_id: 1`, `_id: 2`, and `_id: 3` in the
minutes collection using the `htmlStrippingAnalyzer`.

Document ID

|

Output Tokens  
  
|  
  
`_id: 1`

|

`This`, `page`, `deals`, `with`, `department`, `meetings`  
  
`_id: 2`

|

`The`, `head`, `of`, `the`, `sales`, `department`, `spoke`, `first`  
  
`_id: 3`

|

`We'll`, `head`, `out`, `to`, `the`, `conference`, `room`, `by`, `noon`  
  
## icuNormalize

The `icuNormalize` character filter normalizes text with the ICU Normalizer.
It is based on Lucene's ICUNormalizer2CharFilter.

It has the following attribute:

Name

|

Type

|

Description

|

Required?

|

Default  
  
||||  
  
`type`

|

string

|

Human-readable label that identifies this character filter type. Value must be
`icuNormalize`.

|

yes

|  
  
## Example

The following index definition example indexes the `message` field using a
custom analyzer named `normalizingAnalyzer`. The custom analyzer specifies the
following:

  * Normalize the text in the `message` field value using the `icuNormalize` character filter.

  * tokenize the words in the field based on occurrences of whitespace between words using the whitespace tokenizer.

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "message": {  
    5|         "type": "string",  
    6|         "analyzer": "normalizingAnalyzer"  
    7|       }  
    8|     }  
    9|   },  
    10|   "analyzers": [  
    11|     {  
    12|       "name": "normalizingAnalyzer",  
    13|       "charFilters": [  
    14|         {  
    15|           "type": "icuNormalize"  
    16|         }  
    17|       ],  
    18|       "tokenizer": {  
    19|         "type": "whitespace"  
    20|       },  
    21|       "tokenFilters": []  
    22|     }  
    23|   ]  
    24| }  
  
The following query searches for occurrences of the string `no` (for number)
in the `message` field of the `minutes` collection.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "text": {  
    5|         "query": "no",  
    6|         "path": "message"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     "$project": {  
    12|       "_id": 1,  
    13|       "message": 1,  
    14|       "title": 1  
    15|     }  
    16|   }  
    17| ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 4,  
        title: 'The daily huddle',  
        message: 'write down your signature or phone №'  
      }  
    ]  
  
Atlas Search matched document with `_id: 4` to the query term `no` because it
normalized the numero symbol `№` in the field using the `icuNormalize`
character filter and created the token `no` for that typographic abbreviation
of the word "number". Atlas Search generates the following tokens for the
`message` field value in document `_id: 4` using the `normalizingAnalyzer`:

Document ID

|

Output Tokens  
  
|  
  
`_id: 4`

|

`write`, `down`, `your`, `signature`, `or`, `phone`, `no`  
  
## mapping

The `mapping` character filter applies user-specified normalization mappings
to characters. It is based on Lucene's MappingCharFilter. It has the following
attributes:

Name

|

Type

|

Description

|

Required?

|

Default  
  
||||  
  
`type`

|

string

|

Human-readable label that identifies this character filter type. Value must be
`mapping`.

|

yes

|  
  
`mappings`

|

object

|

Object that contains a comma-separated list of mappings. A mapping indicates
that one character or group of characters should be substituted for another,
in the format `<original> : <replacement>`.

|

yes

|  
  
## Example

The following index definition example indexes the `page_updated_by.phone`
field using a custom analyzer named `mappingAnalyzer`. The custom analyzer
specifies the following:

  * Remove instances of hyphen (`-`), dot (`.`), open parenthesis (`(`), close parenthesis ( `)`), and space characters in the phone field using the `mapping` character filter.

  * Tokenize the entire input as a single token using the keyword tokenizer.

    
    
    1| {  
    |  
    2|   "mappings": {  
    3|     "fields": {  
    4|       "page_updated_by": {  
    5|         "fields": {  
    6|           "phone": {  
    7|             "analyzer": "mappingAnalyzer",  
    8|             "type": "string"  
    9|           }  
    10|         },  
    11|         "type": "document"  
    12|       }  
    13|     }  
    14|   },  
    15|   "analyzers": [  
    16|     {  
    17|       "name": "mappingAnalyzer",  
    18|       "charFilters": [  
    19|         {  
    20|           "mappings": {  
    21|             "-": "",  
    22|             ".": "",  
    23|             "(": "",  
    24|             ")": "",  
    25|             " ": ""  
    26|           },  
    27|           "type": "mapping"  
    28|         }  
    29|       ],  
    30|       "tokenizer": {  
    31|         "type": "keyword"  
    32|       }  
    33|     }  
    34|   ]  
    35| }  
  
The following query searches the `page_updated_by.phone` field for the string
`1234567890`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "text": {  
    5|         "query": "1234567890",  
    6|         "path": "page_updated_by.phone"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     "$project": {  
    12|       "_id": 1,  
    13|       "page_updated_by.phone": 1,  
    14|       "page_updated_by.last_name": 1  
    15|     }  
    16|   }  
    17| ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 1,  
        page_updated_by: { last_name: 'AUERBACH', phone: '(123)-456-7890' }  
      }  
    ]  
  
The Atlas Search results contain one document where the numbers in the `phone`
string match the query string. Atlas Search matched the document to the query
string even though the query doesn't include the parentheses around the phone
area code and the hyphen between the numbers because Atlas Search removed
these characters using the `mapping` character filter and created a single
token for the field value. Specifically, Atlas Search generated the following
token for the `phone` field in document with `_id: 1`:

Document ID

|

Output Tokens  
  
|  
  
`_id: 1`

|

`1234567890`  
  
Atlas Search would also match document with `_id: 1` for searches for
`(123)-456-7890`, `123-456-7890`, `123.456.7890`, and so on because for How to
Index String Fields fields, Atlas Search also analyzes search query terms
using the index analyzer (or if specified, using the `searchAnalyzer`). The
following table shows the tokens that Atlas Search creates by removing
instances of hyphen (`-`), dot (`.`), open parenthesis (`(`), close
parenthesis ( `)`), and space characters in the query term:

Query Term

|

Output Tokens  
  
|  
  
`(123)-456-7890`

|

`1234567890`  
  
`123-456-7890`

|

`1234567890`  
  
`123.456.7890`

|

`1234567890`  
  
## Tip

### See also:

The shingle token filter for a sample index definition and query.

## persian

The `persian` character filter replaces instances of zero-width non-joiner
with the space character. This character filter is based on Lucene's
PersianCharFilter. It has the following attribute:

Name

|

Type

|

Description

|

Required?

|

Default  
  
||||  
  
`type`

|

string

|

Human-readable label that identifies this character filter type. Value must be
`persian`.

|

yes

|  
  
## Example

The following index definition example indexes the `text.fa_IR` field using a
custom analyzer named `persianCharacterIndex`. The custom analyzer specifies
the following:

  * Apply the `persian` character filter to replace non-printing characters in the field value with the space character.

  * Use the whitespace tokenizer to create tokens based on occurrences of whitespace between words.

    
    
    1| {  
    |  
    2|   "analyzer": "lucene.standard",  
    3|   "mappings": {  
    4|     "fields": {  
    5|       "text": {  
    6|         "dynamic": true,  
    7|         "fields": {  
    8|           "fa_IR": {  
    9|             "analyzer": "persianCharacterIndex",  
    10|             "type": "string"  
    11|           }  
    12|         },  
    13|         "type": "document"  
    14|       }  
    15|     }  
    16|   },  
    17|   "analyzers": [  
    18|     {  
    19|       "name": "persianCharacterIndex",  
    20|       "charFilters": [  
    21|         {  
    22|           "type": "persian"  
    23|         }  
    24|       ],  
    25|       "tokenizer": {  
    26|         "type": "whitespace"  
    27|       }  
    28|     }  
    29|   ]  
    30| }  
  
The following query searches the `text.fa_IR` field for the term `صحبت`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     "$search": {  
    4|       "text": {  
    5|         "query": "صحبت",  
    6|         "path": "text.fa_IR"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     "$project": {  
    12|       "_id": 1,  
    13|       "text.fa_IR": 1,  
    14|       "page_updated_by.last_name": 1  
    15|     }  
    16|   }  
    17| ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 2,  
        page_updated_by: { last_name: 'OHRBACH' },  
        text: { fa_IR: 'ابتدا رئیس بخش فروش صحبت کرد' }  
      }  
    ]  
  
Atlas Search returns the `_id: 2` document that contains the query term. Atlas
Search matches the query term to the document by first replacing instances of
zero-width non-joiners with the space character and then creating individual
tokens for each word in the field value based on occurrences of whitespace
between words. Specifically, Atlas Search generates the following tokens for
document with `_id: 2`:

Document ID

|

Output Tokens  
  
|  
  
`_id: 2`

|

`ابتدا`, `رئیس`, `بخش`, `فروش`, `صحبت`, `کرد`  
  
← Custom AnalyzersTokenizers →

