Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Token Filters

Share Feedback

On this page

  * asciiFolding
  * daitchMokotoffSoundex
  * edgeGram
  * englishPossessive
  * flattenGraph
  * icuFolding
  * icuNormalizer
  * kStemming
  * length
  * lowercase
  * nGram
  * porterStemming
  * regex
  * reverse
  * shingle
  * snowballStemming
  * spanishPluralStemming
  * stempel
  * stopword
  * trim
  * wordDelimiterGraph

Token Filters always require a type field, and some take additional options as
well.

    
    
    "tokenFilters": [  
      
      {  
        "type": "<token-filter-type>",  
        "<additional-option>": <value>  
      }  
    ]  
  
Atlas Search supports the following token filters.

## asciiFolding

The `asciiFolding` token filter converts alphabetic, numeric, and symbolic
unicode characters that are not in the Basic Latin Unicode block to their
ASCII equivalents, if available. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`asciiFolding`.

|

yes

|  
  
`originalTokens`

|

string

|

String that specifies whether to include or omit the original tokens in the
output of the token filter. Value can be one of the following:

  * `include` \- include the original tokens with the converted tokens in the output of the token filter. We recommend this value if you want to support queries on both the original tokens as well as the converted forms.

  * `omit` \- omit the original tokens and include only the converted tokens in the output of the token filter. Use this value if you want to query only on the converted forms of the original tokens.

|

no

|

`omit`  
  
## Example

The following index definition example uses a custom analyzer named
`asciiConverter`. It uses the standard tokenizer with the `asciiFolding` token
filter to index the fields in the example collection and convert the field
values to their ASCII equivalent.

    
    
    {  
      
      "analyzer": "asciiConverter",  
      "searchAnalyzer": "asciiConverter",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "asciiConverter",  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "asciiFolding"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `first_name` field for names using their
ASCII equivalent.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "Sian",  
            "path": "page_updated_by.first_name"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "page_updated_by.last_name": 1,  
          "page_updated_by.first_name": 1  
        }  
      }  
    ])  
  
Atlas Search returns the following results:

    
    
    [  
      
      {  
         _id: 1,  
         page_updated_by: { last_name: 'AUERBACH', first_name: 'Siân'}  
      }  
    ]  
  
## daitchMokotoffSoundex

The `daitchMokotoffSoundex` token filter creates tokens for words that sound
the same based on the Daitch-Mokotoff Soundex phonetic algorithm. This filter
can generate multiple encodings for each input, where each encoded token is a
6 digit number.

## Note

Don't use the `daitchMokotoffSoundex` token filter in:

  * Synonym or autocomplete mapping definitions.

  * Operators where `fuzzy` is enabled. Atlas Search supports the `fuzzy` option for the following operators:

    * autocomplete

    * text

It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`daitchMokotoffSoundex`.

|

yes

|  
  
`originalTokens`

|

string

|

String that specifies whether to include or omit the original tokens in the
output of the token filter. Value can be one of the following:

  * `include` \- include the original tokens with the encoded tokens in the output of the token filter. We recommend this value if you want queries on both the original tokens as well as the encoded forms.

  * `omit` \- omit the original tokens and include only the encoded tokens in the output of the token filter. Use this value if you want to only query on the encoded forms of the original tokens.

|

no

|

`include`  
  
## Example

The following index definition example uses a custom analyzer named
`dmsAnalyzer`. It uses the standard tokenizer with the `daitchMokotoffSoundex`
token filter to index and query for words that sound the same as their encoded
forms.

    
    
    {  
      
      "analyzer": "dmsAnalyzer",  
      "searchAnalyzer": "dmsAnalyzer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "dmsAnalyzer",  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "daitchMokotoffSoundex",  
              "originalTokens": "include"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches for terms that sound similar to `AUERBACH` in the
`page_updated_by.last_name` field of the `minutes` collection.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "AUERBACH",  
            "path": "page_updated_by.last_name"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "page_updated_by.last_name": 1  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    { "_id" : 1, "page_updated_by" : { "last_name" : "AUERBACH" } }  
      
    { "_id" : 2, "page_updated_by" : { "last_name" : "OHRBACH" } }  
  
Atlas Search returns documents with `_id: 1` and `_id: 2` because the terms in
both documents are phonetically similar, and are coded using the same six
digit `097500`.

## edgeGram

The `edgeGram` token filter tokenizes input from the left side, or "edge", of
a text input into n-grams of configured sizes. You can't use the edgeGram
token filter in synonym or autocomplete mapping definitions. It has the
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

Human-readable label that identifies this token filter type. Value must be
`edgeGram`.

|

yes

|  
  
`minGram`

|

integer

|

Number that specifies the minimum length of generated n-grams. Value must be
less than or equal to `maxGram`.

|

yes

|  
  
`maxGram`

|

integer

|

Number that specifies the maximum length of generated n-grams. Value must be
greater than or equal to `minGram`.

|

yes

|  
  
`termNotInBounds`

|

string

|

String that specifies whether to index tokens shorter than `minGram` or longer
than `maxGram`. Accepted values are:

  * `include`

  * `omit`

If `include` is specified, tokens shorter than `minGram` or longer than
`maxGram` are indexed as-is. If `omit` is specified, those tokens are not
indexed.

|

no

|

`omit`  
  
## Example

The following index definition example uses a custom analyzer named
`englishAutocomplete`. It performs the following operations:

  * Tokenizes with the standard tokenizer.

  * Token filtering with the following filters:

    * `icuFolding`

    * `shingle`

    * `edgeGram`

    
    
    {  
      
      "analyzer": "englishAutocomplete",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "englishAutocomplete",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "icuFolding"  
            },  
            {  
              "type": "shingle",  
              "minShingleSize": 2,  
              "maxShingleSize": 3  
            },  
            {  
              "type": "edgeGram",  
              "minGram": 1,  
              "maxGram": 10  
            }  
          ]  
        }  
      ]  
    }  
  
## Tip

### See also:

The shingle token filter for a sample index definition and query.

## englishPossessive

The `englishPossessive` token filter removes possessives (trailing `'s`) from
words. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`englishPossessive`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`englishPossessiveStemmer` on the minutes collection. After it applies the
standard tokenizer to create tokens based on word break rules, it applies the
englishPossessive token filter to remove possessives (trailing `'s`) from the
tokens.

    
    
    {  
      
      "analyzer": "englishPossessiveStemmer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "englishPossessiveStemmer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "englishPossessive"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `title` field in the minutes collection for
the term `team`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "team",  
            "path": "title"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "title": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 1,  
        title: "The team's weekly meeting"  
      },  
      {  
        _id: 2,  
        title: 'The check-in with sales team'  
      }  
    ]  
  
Atlas Search returns results that contain the term `team` in the `title`
field. Atlas Search returns the document with `_id: 1` because Atlas Search
transforms `team's` in the `title` field to the token `team` during analysis.

## flattenGraph

The `flattenGraph` token filter transforms a token filter graph into a flat
form suitable for indexing. If you use the wordDelimiterGraph token filter,
use this filter after the wordDelimiterGraph token filter. It has the
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

Human-readable label that identifies this token filter type. Value must be
`flattenGraph`.

|

yes

|  
  
## Example

The following index definition uses a custom analyzer called
`wordDelimiterGraphFlatten`. After it applies the whitespace tokenizer to
create tokens based on occurrences of whitespace between words, it applies the
wordDelimiterGraph token filter to split tokens based on sub-words, generate
tokens for the original words, and also protect the word `SIGN_IN` from
delimination. It applies the flattenGraph token filter after the
wordDelimiterGraph token filter.

    
    
    {  
      
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "message": {  
            "type": "string",  
            "analyzer": "wordDelimiterGraphFlatten"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "name": "wordDelimiterGraphFlatten",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "type": "wordDelimiterGraph",  
              "delimiterOptions" : {  
                "generateWordParts" : true,  
                "preserveOriginal" : true  
              },  
              "protectedWords": {  
                "words": [  
                  "SIGN_IN"  
                ],  
                "ignoreCase": false  
              }  
            },  
            {  
              "type": "flattenGraph"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `message` field in the minutes collection for
the term `sign`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "sign",  
            "path": "message"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "message": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 3,  
        message: 'try to sign-in'  
      }  
    ]  
  
Atlas Search returns the document with `_id: 3` in the results for the query
term `sign` even though the document contains the hyphenated term `sign-in` in
the `title`. The wordDelimiterGraph token filter creates a token filter graph
and the flattenGraph token filter transforms the token filter graph into a
flat form suitable for indexing.

## icuFolding

The `icuFolding` token filter applies character folding from Unicode Technical
Report #30. It has the following attribute:

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

Human-readable label that identifies this token filter type. Value must be
`icuFolding`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`diacriticFolder`. It uses the keyword tokenizer with the `icuFolding` token
filter to apply foldings from UTR#30 Character Foldings. Foldings include
accent removal, case folding, canonical duplicates folding, and many others
detailed in the report.

    
    
    {  
      
      "analyzer": "diacriticFolder",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "diacriticFolder",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "keyword"  
          },  
          "tokenFilters": [  
            {  
              "type": "icuFolding"  
            }  
          ]  
        }  
      ]  
    }  
  
## icuNormalizer

The `icuNormalizer` token filter normalizes tokens using a standard Unicode
Normalization Mode. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`icuNormalizer`.

|

yes

|  
  
`normalizationForm`

|

string

|

Normalization form to apply. Accepted values are:

  * `nfd` (Canonical Decomposition)

  * `nfc` (Canonical Decomposition, followed by Canonical Composition)

  * `nfkd` (Compatibility Decomposition)

  * `nfkc` (Compatibility Decomposition, followed by Canonical Composition)

To learn more about the supported normalization forms, see Section 1.2:
Normalization Forms, UTR#15.

|

no

|

`nfc`  
  
## Example

The following index definition example uses a custom analyzer named
`normalizer`. It uses the whitespace tokenizer, then normalizes tokens by
Canonical Decomposition, followed by Canonical Composition.

    
    
    {  
      
      "analyzer": "normalizer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "normalizer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "type": "icuNormalizer",  
              "normalizationForm": "nfc"  
            }  
          ]  
        }  
      ]  
    }  
  
## kStemming

The `kStemming` token filter combines algorithmic stemming with a built-in
dictionary for the english language to stem words. It expects lowercase text
and doesn't modify uppercase text. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`kStemming`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`kStemmer`. After it applies the standard tokenizer and the lowercase token
filter, it applies the kStemming token filter.

    
    
    {  
      
      "analyzer": "kStemmer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "kStemmer",  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "type": "kStemming"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `text.en_US` field in the minutes collection
for the term `Meeting`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "Meeting",  
            "path": "text.en_US"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "text.en_US": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 1,  
        text: {  
          en_US: '<head> This page deals with department meetings. </head>'  
        }  
      }  
    ]  
  
Atlas Search returns the document with `_id: 1` because the lowercase token
filter normalizes token text to lowercase. The kStemming token filter lets
Atlas Search match the plural `meetings` in the `text.en_US` field of the
document to the singular query term.

## length

The `length` token filter removes tokens that are too short or too long. It
has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`length`.

|

yes

|  
  
`min`

|

integer

|

Number that specifies the minimum length of a token. Value must be less than
or equal to `max`.

|

no

|

0  
  
`max`

|

integer

|

Number that specifies the maximum length of a token. Value must be greater
than or equal to `min`.

|

no

|

255  
  
## Example

The following index definition example uses a custom analyzer named
`longOnly`. It uses the `length` token filter to index only tokens that are at
least 20 UTF-16 code units long after tokenizing with the standard tokenizer.

    
    
    {  
      
      "analyzer": "longOnly",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "longOnly",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "length",  
              "min": 20  
            }  
          ]  
        }  
      ]  
    }  
  
## lowercase

The `lowercase` token filter normalizes token text to lowercase. It has the
following attribute:

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

Human-readable label that identifies this token filter type. Value must be
`lowercase`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`lowercaser`. It uses the standard tokenizer with the `lowercase` token filter
to lowercase all tokens.

    
    
    {  
      
      "analyzer": "lowercaser",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "lowercaser",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            }  
          ]  
        }  
      ]  
    }  
  
## Tip

### See also:

The regex token filter for a sample index definition and query.

## nGram

The `nGram` token filter tokenizes input into n-grams of configured sizes. You
can't use the nGram token filter in synonym or autocomplete mapping
definitions. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`nGram`.

|

yes

|  
  
`minGram`

|

integer

|

Number that specifies the minimum length of generated n-grams. Value must be
less than or equal to `maxGram`.

|

yes

|  
  
`maxGram`

|

integer

|

Number that specifies the maximum length of generated n-grams. Value must be
greater than or equal to `minGram`.

|

yes

|  
  
`termNotInBounds`

|

string

|

String that specifies whether to index tokens shorter than `minGram` or longer
than `maxGram`. Accepted values are:

  * `include`

  * `omit`

If `include` is specified, tokens shorter than `minGram` or longer than
`maxGram` are indexed as-is. If `omit` is specified, those tokens are not
indexed.

|

no

|

`omit`  
  
## Example

The following index definition example uses a custom analyzer named
`persianAutocomplete`. It functions as an autocomplete analyzer for Persian
and other languages that use the zero-width non-joiner character. It performs
the following operations:

  * Normalizes zero-width non-joiner characters with the persian character filter.

  * Tokenizes by whitespace with the whitespace tokenizer.

  * Applies a series of token filters:

    * `icuNormalizer`

    * `shingle`

    * `nGram`

    
    
    {  
      
      "analyzer": "persianAutocomplete",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "persianAutocomplete",  
          "charFilters": [  
            {  
              "type": "persian"  
            }  
          ],  
          "tokenizer": {  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "type": "icuNormalizer",  
              "normalizationForm": "nfc"  
            },  
            {  
              "type": "shingle",  
              "minShingleSize": 2,  
              "maxShingleSize": 3  
            },  
            {  
              "type": "nGram",  
              "minGram": 1,  
              "maxGram": 10  
            }  
          ]  
        }  
      ]  
    }  
  
## porterStemming

The `porterStemming` token filter uses the porter stemming algorithm to remove
the common morphological and inflectional suffixes from words in English. It
expects lowercase text and doesn't work as expected for uppercase text. It has
the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`porterStemming`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`porterStemmer`. After it applies the standard tokenizer and the lowercase
token filter, it applies the porterStemming token filter.

    
    
     {  
      
       "analyzer": "porterStemmer",  
       "mappings": {  
         "dynamic": true  
       },  
       "analyzers": [  
        {  
          "name": "porterStemmer",  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "type": "porterStemming"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `title` field in the minutes collection for
the term `Meet`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "Meet",  
            "path": "title"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "title": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 1,  
        title: "The team's weekly meeting"  
      },  
      {  
        _id: 3,  
        title: 'The regular board meeting'  
      }  
    ]  
  
Atlas Search returns the documents with `_id: 1` and `_id: 2` because the
lowercase token filter normalizes token text to lowercase. The porterStemming
token filter lets Atlas Search match `meeting` in the `title` field of the
documents to the `meet` token.

## regex

The `regex` token filter applies a regular expression to each token, replacing
matches with a specified string. It has the following attributes:

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

Human-readable label that identifies this token filter. Value must be `regex`.

|

yes

|  
  
`pattern`

|

string

|

Regular expression pattern to apply to each token.

|

yes

|  
  
`replacement`

|

string

|

Replacement string to substitute wherever a matching pattern occurs.

|

yes

|  
  
`matches`

|

string

|

Acceptable values are:

  * `all`

  * `first`

If `matches` is set to `all`, replace all matching patterns. Otherwise,
replace only the first matching pattern.

|

yes

|  
  
## Example

The following index definition uses a custom analyzer named `emailRedact` for
indexing the `page_updated_by.email` field in the `minutes` collection. It
uses the standard tokenizer. It first applies the lowercase token filter to
turn uppercase characters in the field to lowercase and then finds strings
that look like email addresses and replaces them with the word `redacted`.

    
    
    {  
      
      "analyzer": "lucene.standard",  
      "mappings": {  
        "dynamic": false,  
        "fields": {  
          "page_updated_by": {  
            "type": "document",  
            "fields": {  
              "email": {  
                "type": "string",  
                "analyzer": "emailRedact"  
              }  
            }  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "charFilters": [],  
          "name": "emailRedact",  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "matches": "all",  
              "pattern": "^([a-z0-9_\\.-]+)@([\\da-z\\.-]+)\\.([a-z\\.]{2,5})$",  
              "replacement": "redacted",  
              "type": "regex"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches for the term `example` in the
`page_updated_by.email` field of the `minutes` collection.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "example",  
            "path": "page_updated_by.email"  
          }  
        }  
      }  
    ])  
  
Atlas Search doesn't return any results for the query because the
`page_updated_by.email` field doesn't contain any instances of the word
`example` that aren't in an email address. Atlas Search replaces strings that
match the regular expression provided in the custom analyzer with the word
`redacted`.

## reverse

The `reverse` token filter reverses each string token. It has the following
attribute:

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

Human-readable label that identifies this token filter. Value must be
`reverse`.

|

yes

|  
  
## Example

The following index definition example for the minutes collection uses a
custom analyzer named `keywordReverse`. It performs the following operations:

  * Uses dynamic mapping

  * Tokenizes with the keyword tokenizer

  * Applies the `reverse` token filter to tokens

    
    
    {  
      
      "analyzer": "lucene.keyword",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "keywordReverse",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "keyword"  
          },  
          "tokenFilters": [  
            {  
              "type": "reverse"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `page_updated_by.email` field in the
`minutes` collection using the wildcard operator to match any characters
preceding the characters `@example.com` in reverse order. The `reverse` token
filter can speed up leading wildcard queries.

    
    
    db.minutes.aggregate([  
      
      {  
        "$search": {  
          "index": "default",  
          "wildcard": {  
            "query": "*@example.com",  
            "path": "page_updated_by.email",  
            "allowAnalyzedField": true  
          }  
        }  
      },  
      {  
        "$project": {  
          "_id": 1,  
          "page_updated_by.email": 1,  
        }  
      }  
    ])  
  
For the preceding query, Atlas Search applies the custom analyzer to the
wildcard query to transform the query as follows:

    
    
    moc.elpmaxe@*  
      
  
Atlas Search then runs the query against the indexed tokens, which are also
reversed. The query returns the following documents:

    
    
    [  
      
      { _id: 1, page_updated_by: { email: 'auerbach@example.com' } },  
      { _id: 2, page_updated_by: { email: 'ohrback@example.com' } },  
      { _id: 3, page_updated_by: { email: 'lewinsky@example.com' } },  
      { _id: 4, page_updated_by: { email: 'levinski@example.com' } }  
    ]  
  
## shingle

The `shingle` token filter constructs shingles (token n-grams) from a series
of tokens. You can't use the `shingle` token filter in synonym or autocomplete
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

Human-readable label that identifies this token filter type. Value must be
`shingle`.

|

yes

|  
  
`minShingleSize`

|

integer

|

Minimum number of tokens per shingle. Must be less than or equal to
`maxShingleSize`.

|

yes

|  
  
`maxShingleSize`

|

integer

|

Maximum number of tokens per shingle. Must be greater than or equal to
`minShingleSize`.

|

yes

|  
  
## Example

The following index definition example uses two custom analyzers,
`emailAutocompleteIndex` and `emailAutocompleteSearch`, to implement
autocomplete-like functionality. Atlas Search uses the
`emailAutocompleteIndex` analyzer during index creation to:

  * Replace `@` characters in a field with `AT`

  * Create tokens with the whitespace tokenizer

  * Shingle tokens

  * Create edgeGram of those shingled tokens

Atlas Search uses the `emailAutocompleteSearch` analyzer during a search to:

  * Replace `@` characters in a field with `AT`

  * Create tokens with the whitespace tokenizer tokenizer

    
    
     {  
      
      "analyzer": "lucene.keyword",  
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "page_updated_by": {  
            "type": "document",  
            "fields": {  
              "email": {  
                "type": "string",  
                "analyzer": "emailAutocompleteIndex",  
                "searchAnalyzer": "emailAutocompleteSearch",  
              }  
            }  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "name": "emailAutocompleteIndex",  
          "charFilters": [  
            {  
              "mappings": {  
                "@": "AT"  
              },  
              "type": "mapping"  
            }  
          ],  
          "tokenizer": {  
            "maxTokenLength": 15,  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "maxShingleSize": 3,  
              "minShingleSize": 2,  
              "type": "shingle"  
            },  
            {  
              "maxGram": 15,  
              "minGram": 2,  
              "type": "edgeGram"  
            }  
          ]  
        },  
        {  
          "name": "emailAutocompleteSearch",  
          "charFilters": [  
            {  
              "mappings": {  
                "@": "AT"  
              },  
              "type": "mapping"  
            }  
          ],  
          "tokenizer": {  
            "maxTokenLength": 15,  
            "type": "whitespace"  
          }  
        }  
      ]  
    }  
  
The following query searches for an email address in the
`page_updated_by.email` field of the `minutes` collection:

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "auerbach@ex",  
             "path": "page_updated_by.email"  
          }  
        }  
      }  
    ])  
  
The query returns the following results:

    
    
    {  
      
      "_id" : 1,  
      "page_updated_by" : {  
        "last_name" : "AUERBACH",  
        "first_name" : "Siân",  
        "email" : "auerbach@example.com",  
        "phone" : "123-456-7890"  
      },  
      "title": "The team's weekly meeting",  
      "message": "try to siGn-In",  
      "text": {  
        "en_US": "<head> This page deals with department meetings. </head>"  
      }  
    }  
  
## snowballStemming

The `snowballStemming` token filters Stems tokens using a Snowball-generated
stemmer. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`snowballStemming`.

|

yes

|  
  
`stemmerName`

|

string

|

The following values are valid:

  * `arabic`

  * `armenian`

  * `basque`

  * `catalan`

  * `danish`

  * `dutch`

  * `english`

  * `estonian`

  * `finnish`

  * `french`

  * `german`

  * `german2` (Alternative German language stemmer. Handles the umlaut by expanding ü to ue in most contexts.)

  * `hungarian`

  * `irish`

  * `italian`

  * `kp` (Kraaij-Pohlmann stemmer, an alternative stemmer for Dutch.)

  * `lithuanian`

  * `lovins` (The first-ever published "Lovins JB" stemming algorithm.)

  * `norwegian`

  * `porter` (The original Porter English stemming algorithm.)

  * `portuguese`

  * `romanian`

  * `russian`

  * `spanish`

  * `swedish`

  * `turkish`

|

yes

|  
  
## Example

The following example index definition uses a custom analyzer named
`frenchStemmer`. It uses the `lowercase` token filter and the standard
tokenizer, followed by the `french` variant of the `snowballStemming` token
filter.

    
    
    {  
      
      "analyzer": "frenchStemmer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "frenchStemmer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "type": "snowballStemming",  
              "stemmerName": "french"  
            }  
          ]  
        }  
      ]  
    }  
  
## spanishPluralStemming

The `spanishPluralStemming` token filter stems spanish plural words. It
expects lowercase text. It has the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`spanishPluralStemming`.

|

yes

|  
  
## Example

The following index definition specifies that Atlas Search dynamically index
all fields in the `minutes` collection with the `standard` analyzer. The index
definition example specifies a custom analyzer named `spanishPluralStemmer`
for the `text.es_MX` field. The custom analyzer specifies that Atlas Search
convert spanish terms to lowercase and tokenize plural spanish words into
their singular form.

    
    
    {  
      
      "analyzer": "spanishPluralStemmer",  
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "text.es_MX": {  
            "analyzer": "spanishPluralStemmer",  
            "searchAnalyzer": "spanishPluralStemmer",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "name": "spanishPluralStemmer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "type": "spanishPluralStemming"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `text.es_MX` field in the minutes collection
for the spanish term `punto`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "punto",  
            "path": "text.es_MX"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "text.es_MX": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 4,  
        text : {  
          es_MX: 'La página ha sido actualizada con los puntos de la agenda.',  
        }  
      }  
    ]  
  
Atlas Search returns the document with `_id: 4` because the `text.es_MX` field
in the document contains the plural term `puntos`. Atlas Search matches this
document for the query term `punto` because Atlas Search analyzes `puntos` as
`punto` by stemming the plural (`s`) from the term.

## stempel

The `stempel` token filter uses Lucene's default Polish stemmer table to stem
words in the Polish language. It expects lowercase text. It has the following
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

Human-readable label that identifies this token filter type. Value must be
`stempel`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`stempelStemmer`. After it applies the standard tokenizer and the lowercase
token filter, it applies the stempel token filter to the `text.pl_PL` field.

    
    
    {  
      
      "analyzer": "stempelStemmer",  
      "mappings": {  
        "dynamic": true,  
        "fields": {  
          "text.pl_PL": {  
            "analyzer": "stempelStemmer",  
            "searchAnalyzer": "stempelStemmer",  
            "type": "string"  
          }  
        }  
      },  
      "analyzers": [  
        {  
          "name": "stempelStemmer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "standard"  
          },  
          "tokenFilters": [  
            {  
              "type": "lowercase"  
            },  
            {  
              "type": "stempel"  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `text.pl_PL` field in the minutes collection
for the Polish term `punkt`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "punkt",  
            "path": "text.pl_PL"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "text.pl_PL": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 4,  
        text: {  
          pl_PL: 'Strona została zaktualizowana o punkty porządku obrad.'  
        }  
      }  
    ]  
  
Atlas Search returns the document with `_id: 4` because the `text.pl_PL` field
in the document contains the plural term `punkty`. Atlas Search matches this
document for the query term `punkt` because Atlas Search analyzes `punkty` as
`punkt` by stemming the plural (`y`) from the term.

## stopword

The `stopword` token filter removes tokens that correspond to the specified
stop words. This token filter doesn't analyze the specified stop words. It has
the following attributes:

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

Human-readable label that identifies this token filter type. Value must be
`stopword`.

|

yes

|  
  
`tokens`

|

array of strings

|

List that contains the stop words that correspond to the tokens to remove.
Value must be one or more stop words.

|

yes

|  
  
`ignoreCase`

|

boolean

|

Flag that indicates whether to ignore the case of stop words when filtering
the tokens to remove. The value can be one of the following:

  * `true` \- ignore case and remove all tokens that match the specified stop words

  * `false` \- be case-sensitive and remove only tokens that exactly match the specified case

If omitted, defaults to `true`.

|

no

|

true  
  
## Example

The following index definition example uses a custom analyzer named It uses
the `stopword` token filter after the whitespace tokenizer to remove the
tokens that match the defined stop words `is`, `the`, and `at`. The token
filter is case-insensitive and will remove all tokens that match the specified
stop words.

    
    
    {  
      
      "analyzer": "tokenTrimmer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "stopwordRemover",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "type": "stopword",  
              "tokens": ["is", "the", "at"]  
            }  
          ]  
        }  
      ]  
    }  
  
## trim

The `trim` token filter trims leading and trailing whitespace from tokens. It
has the following attribute:

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

Human-readable label that identifies this token filter type. Value must be
`trim`.

|

yes

|  
  
## Example

The following index definition example uses a custom analyzer named
`tokenTrimmer`. It uses the `trim` token filter after the keyword tokenizer to
remove leading and trailing whitespace in the tokens created by the keyword
tokenizer.

    
    
    {  
      
      "analyzer": "tokenTrimmer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "tokenTrimmer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "keyword"  
          },  
          "tokenFilters": [  
            {  
              "type": "trim"  
            }  
          ]  
        }  
      ]  
    }  
  
## wordDelimiterGraph

The `wordDelimiterGraph` token filter splits tokens into sub-tokens based on
configured rules. We recommend that you don't use this token filter with the
standard tokenizer because this tokenizer removes many of the intra-word
delimiters that this token filter uses to determine boundaries. It has the
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

Human-readable label that identifies this token filter type. Value must be
`wordDelimiterGraph`.

|

yes

|  
  
`delimiterOptions`

|

object

|

Object that contains the rules that determine how to split words into sub-
words.

|

no

|

{}  
  
`delimterOptions`

`.generateWordParts`

|

boolean

|

Flag that indicates whether to split tokens based on sub-words. For examples,
if `true`, this option splits `PowerShot` into `Power` and `Shot`.

|

no

|

true  
  
`delimterOptions`

`.generateNumberParts`

|

boolean

|

Flag that indicates whether to split tokens based on sub-numbers. For
examples, if `true`, this option splits `100-2` into `100` and `2`.

|

no

|

true  
  
`delimterOptions`

`.concatenateWords`

|

boolean

|

Flag that indicates whether to concatenate runs of sub-words. For examples, if
`true`, this option concatenates `wi-fi` into `wifi`. [1]

|

no

|

false  
  
`delimterOptions`

`.concatenateNumbers`

|

boolean

|

Flag that indicates whether to concatenate runs of sub-numbers. For examples,
if `true`, this option concatenates `100-2` into `1002`. [1]

|

no

|

false  
  
`delimterOptions`

`.concatenateAll`

|

boolean

|

Flag that indicates whether to concatenate all runs. For examples, if `true`,
this option concatenates `wi-fi-100-2` into `wifi1002`. [1]

|

no

|

false  
  
`delimterOptions`

`.preserveOriginal`

|

boolean

|

Flag that indicates whether to generate tokens of the original words. [1]

|

no

|

true  
  
`delimterOptions`

`.splitOnCaseChange`

|

boolean

|

Flag that indicates whether to split tokens based on letter-case transitions.
For examples, if `true`, this option splits `camelCase` into `camel` and
`Case`.

|

no

|

true  
  
`delimterOptions`

`.splitOnNumerics`

|

boolean

|

Flag that indicates whether to split tokens based on letter-number
transitions. For examples, if `true`, this option splits `g2g` into `g`, `2`,
and `g`.

|

no

|

true  
  
`delimterOptions`

`.stemEnglishPossessive`

|

boolean

|

Flag that indicates whether to remove trailing possessives from each sub-word.
For examples, if `true`, this option changes `who's` into `who``.

|

no

|

true  
  
`delimterOptions`

`.ignoreKeywords`

|

boolean

|

Flag that indicates whether to skip tokens with the `keyword` attribute set to
`true`.

|

no

|

false  
  
`protectedWords`

|

object

|

Object that contains options for protected words.

|

no

|

{}  
  
`protectedWords`

`.words`

|

array

|

List that contains the tokens to protect from delimination. If you specify
`protectedWords`, you must specify this option.

|

conditional

|  
  
`protectedWords`

`.ignoreCase`

|

boolean

|

Flag that indicates whether to ignore case sensisitivity for protected words.

|

no

|

`true`  
  
[1]|  _(1, 2, 3, 4)_ If `true`, apply the flattenGraph token filter after this
option to make the token stream suitable for indexing.  
|  
  
## Example

The following index definition example:

  * Uses a custom analyzer named `wordDelimiterGraphAnalyzer`.

  * Doesn't try and split `is`, `the`, and `at`. The exclusion is case sensitive. For example `Is` and `tHe` are not excluded.

  * Splits tokens on case changes and removes tokens that contain only alphabetical letters from the English alphabet.

After it applies the whitespace tokenizer, it applies the wordDelimiterGraph
token filter.

    
    
    {  
      
      "analyzer": "wordDelimiterGraphAnalyzer",  
      "mappings": {  
        "dynamic": true  
      },  
      "analyzers": [  
        {  
          "name": "wordDelimiterGraphAnalyzer",  
          "charFilters": [],  
          "tokenizer": {  
            "type": "whitespace"  
          },  
          "tokenFilters": [  
            {  
              "type": "wordDelimiterGraph",  
              "protectedWords": {  
                "words": ["is", "the", "at"],  
                "ignoreCase": false  
              },  
              "delimiterOptions" : {  
                "generateWordParts" : false,  
                "splitOnCaseChange" : true  
              }  
            }  
          ]  
        }  
      ]  
    }  
  
The following query searches the `title` field in the minutes collection for
the term `App2`.

    
    
    db.minutes.aggregate([  
      
      {  
        $search: {  
          "index": "default",  
          "text": {  
            "query": "App2",  
            "path": "title"  
          }  
        }  
      },  
      {  
        $project: {  
          "_id": 1,  
          "title": 1  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
    [  
      
      {  
        _id: 4,  
        title: 'The daily huddle on StandUpApp2'  
      }  
    ]  
  
Atlas Search returns the document with `_id: 4` because the `title` field in
the document contains `App2`. Atlas Search splits tokens on case changes and
removes tokens that contain only alphabetical letters. A search for letters
from the english alphabet won't return any results.

← TokenizersDefine Field Mappings →

