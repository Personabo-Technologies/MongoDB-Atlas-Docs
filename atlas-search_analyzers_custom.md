Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Custom Analyzers

Share Feedback

On this page

  * Overview
  * Syntax
  * Attributes
  * Usage
  * Example Collection

## Overview

An Atlas Search analyzer prepares a set of documents to be indexed by
performing a series of operations to transform, filter, and group sequences of
characters. You can define a custom analyzer to suit your specific indexing
needs.

## Syntax

A custom analyzer has the following syntax:

    
    
    "analyzers": [  
      
      {  
        "name": "<name>",  
        "charFilters": [ <list-of-character-filters> ],  
        "tokenizer": {  
          "type": "<tokenizer-type>"  
        },  
        "tokenFilters": [ <list-of-token-filters> ]  
      }  
    ]  
  
## Attributes

A custom analyzer has the following attributes:

Attribute

|

Type

|

Description

|

Required?  
  
|||  
  
`name`

|

string

|

Name of the custom analyzer. Names must be unique within an index, and may not
start with any of the following strings:

  * `lucene.`

  * `builtin.`

  * `mongodb.`

|

yes  
  
`charFilters`

|

list of objects

|

Array containing zero or more character filters. See Usage for more
information.

|

no  
  
`tokenizer`

|

object

|

Tokenizer to use to create tokens. See Usage for more information.

|

yes  
  
`tokenFilters`

|

list of objects

|

Array containing zero or more token filters. See Usage for more information.

|

no  
  
## Usage

To use a custom analyzer when indexing a collection, include the following in
your index definition `analyzers` field:

  1.  _Optional_. Specify one or more character filters. Character filters examine text one character at a time and perform filtering operations.

  2.  _Required_. Specify the tokenizer. An analyzer uses a tokenizer to split chunks of text into groups, or tokens, for indexing purposes. For example, the whitespace tokenizer splits text fields into individual words based on where whitespace occurs.

  3.  _Optional_. Specify one or more token filters. After the tokenization step, the resulting tokens can pass through one or more token filters. A token filter performs operations such as:

    * Stemming, which reduces related words, such as "talking", "talked", and "talks" to their root word "talk".

    * Redaction, the removal of sensitive information from public documents.

## Note

The text passes through character filters first, then a tokenizer, and then
the token filters.

## Example Collection

The Character Filters, Tokenizers, and Token Filters pages contain sample
index definitions and query examples for character filters, tokenizers, and
token filters. These examples use a sample `minutes` collection with the
following documents:

    
    
    {  
      
      "_id": 1,  
      "page_updated_by": {  
        "last_name": "AUERBACH",  
        "first_name": "Siân",  
        "email": "auerbach@example.com",  
        "phone": "(123)-456-7890"  
      },  
      "title": "The team's weekly meeting",  
      "message": "try to siGn-In",  
      "text": {  
        "en_US": "<head> This page deals with department meetings. </head>"  
      }  
    }  
      
    
    {  
      
      "_id": 2,  
      "page_updated_by": {  
        "last_name": "OHRBACH",  
        "first_name": "Noël",  
        "email": "ohrbach@example.com",  
        "phone": "(123) 456 0987"  
      },  
      "title": "The check-in with sales team",  
      "message": "do not forget to SIGN-IN",  
      "text" : {  
        "en_US": "The head of the sales department spoke first.",  
        "fa_IR": "ابتدا رئیس بخش فروش صحبت کرد"  
      }  
    }  
      
    
    {  
      
      "_id": 3,  
      "page_updated_by": {  
        "last_name": "LEWINSKY",  
        "first_name": "Brièle",  
        "email": "lewinsky@example.com",  
        "phone": "(123).456.9870"  
      },  
      "title": "The regular board meeting",  
      "message": "try to sign-in",  
      "text" : {  
        "en_US": "<body>We'll head out to the conference room by noon.</body>"  
      }  
    }  
      
    
    {  
      
      "_id": 4,  
      "page_updated_by": {  
        "last_name": "LEVINSKI",  
        "first_name": "François",  
        "email": "levinski@example.com",  
        "phone": "123-456-8907"  
      },  
      "title": "The daily huddle on StandUpApp2",  
      "message": "write down your signature or phone №",  
      "text" : {  
        "en_US": "<body>This page has been updated with the items on the agenda.</body>" ,  
        "es_MX": "La página ha sido actualizada con los puntos de la agenda.",  
        "pl_PL": "Strona została zaktualizowana o punkty porządku obrad."  
      }  
  
← Multi AnalyzerCharacter Filters →

