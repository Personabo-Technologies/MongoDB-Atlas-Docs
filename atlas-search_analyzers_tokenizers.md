Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Tokenizers

Share Feedback

On this page

  * edgeGram
  * keyword
  * nGram
  * regexCaptureGroup
  * regexSplit
  * standard
  * uaxUrlEmail
  * whitespace

A custom analyzer's tokenizer determines how Atlas Search splits up text into
discrete chunks for indexing. Tokenizers require a type field, and some take
additional options as well.

    
    
    "tokenizer": {  
      
      "type": "<tokenizer-type>",  
      "<additional-option>": "<value>"  
    }  
  
Atlas Search supports the following tokenizer options:

  * edgeGram

  * keyword

  * nGram

  * regexCaptureGroup

  * regexSplit

  * standard

  * uaxUrlEmail

  * whitespace

## edgeGram

The `edgeGram` tokenizer tokenizes input from the left side, or "edge", of a
text input into n-grams of given sizes. You can't use a custom analyzer with
edgeGram tokenizer in the `analyzer` field for synonym or autocomplete field
mapping definitions. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`edgeGram`.

|

yes

|  
  
`minGram`

|

integer

|

Number of characters to include in the shortest token created.

|

yes

|  
  
`maxGram`

|

integer

|

Number of characters to include in the longest token created.

|

yes

|  
  
## Example

The following index definition indexes the `message` field in the `minutes`
collection using a custom analyzer named `edgegramExample`. It uses the
`edgeGram` tokenizer to create tokens (searchable terms) between `2` and `7`
characters long starting from the first character on the left side of words in
the `message` field.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "message": {  
            "analyzer": "edgegramExample",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "edgegramExample",  
          "tokenFilters": [],  
          "tokenizer": {  
            "maxGram": 7,  
            "minGram": 2,  
            "type": "edgeGram"  
          }  
        }  
      ]  
    }  
  
The following query searches the `message` field in the `minutes` collection
for text that begin with `tr`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "tr",  
    6|         "path": "message"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "message": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
    { _id: 1, message: 'try to siGn-In' },  
      
    { _id: 3, message: 'try to sign-in' }  
  
Atlas Search returns documents with `_id: 1` and `_id: 3` in the results
because Atlas Search created a token with the value `tr` using the `edgeGram`
tokenizer for the documents, which matches the search term. If you index the
`message` field using the `standard` tokenizer, Atlas Search would not return
any results for the search term `tr`.

The following table shows the tokens that the `edgeGram` tokenizer and by
comparison, the `standard` tokenizer, create for the documents in the results:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`try`, `to`, `sign`, `in`  
  
`edgeGram`

|

`tr`, `try`, `try{SPACE}`, `try t`, `try to`, `try to{SPACE}`  
  
## keyword

The `keyword` tokenizer tokenizes the entire input as a single token. Atlas
Search doesn't index string fields that exceed 32766 characters using the
`keyword` tokenizer. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`keyword`.

|

yes

|  
  
## Example

The following index definition indexes the `message` field in the `minutes`
collection using a custom analyzer named `keywordExample`. It uses the
`keyword` tokenizer to create a token (searchable terms) on the entire field
as a single term.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "message": {  
            "analyzer": "keywordExample",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "keywordExample",  
          "tokenFilters": [],  
          "tokenizer": {  
            "type": "keyword"  
          }  
        }  
      ]  
    }  
  
The following query searches the `message` field in the `minutes` collection
for the phrase `try to sign-in`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "try to sign-in",  
    6|         "path": "message"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "message": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
     { _id: 3, message: 'try to sign-in' }  
      
  
Atlas Search returns the document with `_id: 3` in the results because Atlas
Search created a token with the value `try to sign-in` using the `keyword`
tokenizer for the documents, which matches the search term. If you index the
`message` field using the `standard` tokenizer, Atlas Search returns documents
with `_id: 1`, `_id: 2` and `_id: 3` for the search term `try to sign-in`
because each document contains some of the tokens the `standard` tokenizer
creates.

The following table shows the tokens that the `keyword` tokenizer and by
comparison, the `standard` tokenizer, create for the document with `_id: 3`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`try`, `to`, `sign`, `in`  
  
`keyword`

|

`try to sign-in`  
  
## nGram

The `nGram` tokenizer tokenizes into text chunks, or "n-grams", of given
sizes. You can't use a custom analyzer with nGram tokenizer in the `analyzer`
field for synonym or autocomplete field mapping definitions. It has the
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

Human-readable label that identifies this tokenizer type. Value must be
`nGram`.

|

yes

|  
  
`minGram`

|

integer

|

Number of characters to include in the shortest token created.

|

yes

|  
  
`maxGram`

|

integer

|

Number of characters to include in the longest token created.

|

yes

|  
  
## Example

The following index definition indexes the `title` field in the `minutes`
collection using a custom analyzer named `ngramExample`. It uses the `nGram`
tokenizer to create tokens (searchable terms) between `4` and `6` characters
long in the `title` field.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "title": {  
            "analyzer": "ngramExample",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "ngramExample",  
          "tokenFilters": [],  
          "tokenizer": {  
            "maxGram": 6,  
            "minGram": 4,  
            "type": "nGram"  
          }  
        }  
      ]  
    }  
  
The following query searches the `title` field in the `minutes` collection for
the term `week`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "week",  
    6|         "path": "title"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "title": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
     { _id: 1, title: "The team's weekly meeting" }  
      
  
Atlas Search returns the document with `_id: 1` in the results because Atlas
Search created a token with the value `week` using the `nGram` tokenizer for
the documents, which matches the search term. If you index the `title` field
using the `standard` or `edgeGram` tokenizer, Atlas Search would not return
any results for the search term `week`.

The following table shows the tokens that the `nGram` tokenizer and by
comparison, the `standard` and `edgeGram` tokenizer create for the document
with `_id: 1`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`The`, `team's`, `weekly`, `meeting`  
  
`edgeGram`

|

`The{SPACE}`, `The t`, `The te`  
  
`nGram`

|

`The{SPACE}`, `The t`, `The te`, `he t`, ... , `week`, `weekl`, `weekly`,
`eekl`, ..., `eetin`, `eeting`, `etin`, `eting`, `ting`  
  
## regexCaptureGroup

The `regexCaptureGroup` tokenizer matches a regular expression pattern to
extract tokens. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`regexCaptureGroup`.

|

yes

|  
  
`pattern`

|

string

|

Regular expression to match against.

|

yes

|  
  
`group`

|

integer

|

Index of the character group within the matching expression to extract into
tokens. Use `0` to extract all character groups.

|

yes

|  
  
## Example

The following index definition indexes the `page_updated_by.phone` field in
the `minutes` collection using a custom analyzer named `phoneNumberExtractor`.
It uses the following:

  * `mappings` character filter to remove parenthesis around the first three digits and replace all spaces and periods with dashes

  * `regexCaptureGroup` tokenizer to create a single token from the first US-formatted phone number present in the text input

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "page_updated_by": {  
            "fields": {  
              "phone": {  
                "analyzer": "phoneNumberExtractor",  
                "type": "string"  
              }  
            },  
            "type": "document"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [  
            {  
              "mappings": {  
                " ": "-",  
                "(": "",  
                ")": "",  
                ".": "-"  
              },  
              "type": "mapping"  
            }  
          ],  
          "name": "phoneNumberExtractor",  
          "tokenFilters": [],  
          "tokenizer": {  
            "group": 0,  
            "pattern": "^\\b\\d{3}[-]?\\d{3}[-]?\\d{4}\\b$",  
            "type": "regexCaptureGroup"  
          }  
        }  
      ]  
    }  
  
The following query searches the `page_updated_by.phone` field in the
`minutes` collection for the phone number `123-456-9870`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "123-456-9870",  
    6|         "path": "page_updated_by.phone"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "page_updated_by.phone": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
     { _id: 3, page_updated_by: { phone: '(123).456.9870' }  
      
  
Atlas Search returns the document with `_id: 3` in the results because Atlas
Search created a token with the value `123-456-7890` using the
`regexCaptureGroup` tokenizer for the documents, which matches the search
term. If you index the `page_updated_by.phone` field using the `standard`
tokenizer, Atlas Search returns all of the documents for the search term
`123-456-7890`.

The following table shows the tokens that the `regexCaptureGroup` tokenizer
and by comparison, the `standard` tokenizer, create for the document with
`_id: 3`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`123`, `456.9870`  
  
`regexCaptureGroup`

|

`123-456-9870`  
  
## regexSplit

The `regexSplit` tokenizer splits tokens with a regular-expression based
delimiter. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`regexSplit`.

|

yes

|  
  
`pattern`

|

string

|

Regular expression to match against.

|

yes

|  
  
## Example

The following index definition indexes the `page_updated_by.phone` field in
the `minutes` collection using a custom analyzer named `dashDotSpaceSplitter`.
It uses the `regexSplit` tokenizer to create tokens (searchable terms) from
one or more hyphens, periods and spaces on the `page_updated_by.phone` field.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "page_updated_by": {  
            "fields": {  
              "phone": {  
                "analyzer": "dashDotSpaceSplitter",  
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
          "name": "dashDotSpaceSplitter",  
          "tokenFilters": [],  
          "tokenizer": {  
            "pattern": "[-. ]+",  
            "type": "regexSplit"  
          }  
        }  
      ]  
    }  
  
The following query searches the `page_updated_by.phone` field in the
`minutes` collection for the digits `9870`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "9870",  
    6|         "path": "page_updated_by.phone"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "page_updated_by.phone": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
     { _id: 3, page_updated_by: { phone: '(123).456.9870' }  
      
  
Atlas Search returns the document with `_id: 3` in the results because Atlas
Search created a token with the value `9870` using the `regexSplit` tokenizer
for the documents, which matches the search term. If you index the
`page_updated_by.phone` field using the `standard` tokenizer, Atlas Search
would not return any results for the search term `9870`.

The following table shows the tokens that the `regexCaptureGroup` tokenizer
and by comparison, the `standard` tokenizer, create for the document with
`_id: 3`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`123`, `456.9870`  
  
`regexSplit`

|

`(123)`, `456`, `9870`  
  
## standard

The `standard` tokenizer tokenizes based on word break rules from the Unicode
Text Segmentation algorithm. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`standard`.

|

yes

|  
  
`maxTokenLength`

|

integer

|

Maximum length for a single token. Tokens greater than this length are split
at `maxTokenLength` into multiple tokens.

|

no

|

255  
  
## Example

The following index definition indexes the `message` field in the `minutes`
collection using a custom analyzer named `standardExample`. It uses the
`standard` tokenizer and the stopword token filter.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "message": {  
            "analyzer": "standardExample",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "standardExample",  
          "tokenFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          }  
        }  
      ]  
    }  
  
The following query searches the `message` field in the `minutes` collection
for the term `signature`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "signature",  
    6|         "path": "message"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "message": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
    { _id: 4, message: 'write down your signature or phone №' }  
      
  
Atlas Search returns the document with `_id: 4` because Atlas Search created a
token with the value `signature` using the `standard` tokenizer for the
documents, which matches the search term. If you index the `message` field
using the `keyword` tokenizer, Atlas Search would not return any results for
the search term `signature`.

The following table shows the tokens that the `standard` tokenizer and by
comparison, the `keyword` analyzer, create for the document with `_id: 4`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`write`, `down`, `your`, `signature`, `or`, `phone`  
  
`keyword`

|

`write down your signature or phone №`  
  
## uaxUrlEmail

The `uaxUrlEmail` tokenizer tokenizes URLs and email addresses. Although
`uaxUrlEmail` tokenizer tokenizes based on word break rules from the Unicode
Text Segmentation algorithm, we recommend using `uaxUrlEmail` tokenizer only
when the indexed field value includes URLs and email addresses. For fields
that don't include URLs or email addresses, use the standard tokenizer to
create tokens based on word break rules. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`uaxUrlEmail`.

|

yes

|  
  
`maxTokenLength`

|

int

|

Maximum number of characters in one token.

|

no

|

`255`  
  
## Example

Basic Example

Advanced Example

The following index definition indexes the `page_updated_by.email` field in
the `minutes` collection using a custom analyzer named
`basicEmailAddressAnalyzer`. It uses the `uaxUrlEmail` tokenizer to create
tokens (searchable terms) from URLs and email addresses in the
`page_updated_by.email` field.

    
    
     {  
      
       "mappings": {  
         "fields": {  
           "page_updated_by": {  
             "fields": {  
               "email": {  
                 "analyzer": "basicEmailAddressAnalyzer",  
                 "type": "string"  
               }  
             },  
             "type": "document"  
           }  
         }  
       },  
       "analyzers": [  
         {  
           "name": "basicEmailAddressAnalyzer",  
           "tokenizer": {  
             "type": "uaxUrlEmail"  
           }  
         }  
       ]  
     }  
  
The following query searches the `page_updated_by.email` field in the
`minutes` collection for the email `lewinsky@example.com`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "lewinsky@example.com",  
            "path": "page_updated_by.email"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "page_updated_by.email": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    { _id: 3, page_updated_by: { email: 'lewinsky@example.com' } }  
      
  
Atlas Search returns the document with `_id: 3` in the results because Atlas
Search created a token with the value `lewinsky@example.com` using the
`uaxUrlEmail` tokenizer for the documents, which matches the search term. If
you index the `page_updated_by.email` field using the `standard` tokenizer,
Atlas Search returns all the documents for the search term
`lewinsky@example.com`.

The following table shows the tokens that the `uaxUrlEmail` tokenizer and by
comparison, the `standard` tokenizer, create for the document with `_id: 3`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`lewinsky`, `example.com`  
  
`uaxUrlEmail`

|

`lewinsky@example.com`  
  
## whitespace

The `whitespace` tokenizer tokenizes based on occurrences of whitespace
between words. It has the following attributes:

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

Human-readable label that identifies this tokenizer type. Value must be
`whitespace`.

|

yes

|  
  
`maxTokenLength`

|

integer

|

Maximum length for a single token. Tokens greater than this length are split
at `maxTokenLength` into multiple tokens.

|

no

|

255  
  
## Example

The following index definition indexes the `message` field in the `minutes`
collection using a custom analyzer named `whitespaceExample`. It uses the
`whitespace` tokenizer to create tokens (searchable terms) from any
whitespaces in the `message` field.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "message": {  
            "analyzer": "whitespaceExample",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "whitespaceExample",  
          "tokenFilters": [],  
          "tokenizer": {  
            "type": "whitespace"  
          }  
        }  
      ]  
    }  
  
The following query searches the `message` field in the `minutes` collection
for the term `SIGN-IN`.

    
    
    1| db.minutes.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "query": "SIGN-IN",  
    6|         "path": "message"  
    7|       }  
    8|     }  
    9|   },  
    10|   {  
    11|     $project: {  
    12|       "_id": 1,  
    13|       "message": 1  
    14|     }  
    15|   }  
    16| ])  
  
HIDE OUTPUT

    
    
    { _id: 2, message: 'do not forget to SIGN-IN' }  
      
  
Atlas Search returns the document with `_id: 2` in the results because Atlas
Search created a token with the value `SIGN-IN` using the `whitespace`
tokenizer for the documents, which matches the search term. If you index the
`message` field using the `standard` tokenizer, Atlas Search returns documents
with `_id: 1`, `_id: 2` and `_id: 3` for the search term `SIGN-IN`.

The following table shows the tokens that the `whitespace` tokenizer and by
comparison, the `standard` tokenizer, create for the document with `_id: 2`:

Tokenizer

|

Token Outputs  
  
|  
  
`standard`

|

`do`, `not`, `forget`, `to`, `sign`, `in`  
  
`whitespace`

|

`do`, `not`, `forget`, `to`, `SIGN-IN`  
  
← Character FiltersToken Filters →

