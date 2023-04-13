Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Process Data with Analyzers

Share Feedback

You can control how Atlas Search turns a `string` field's contents into
searchable terms using _analyzers_. Analyzers are policies that combine a
tokenizer, which extracts tokens from text, with filters that you define.
Atlas Search applies your filters to the tokens to create indexable terms that
correct for differences in punctuation, capitalization, filler words, and
more.

To control how Atlas Search creates search terms, use an Atlas Search analyzer
in the index definition. You may specify an analyzer when creating an index,
executing a query, or both.

Atlas Search provides the following built-in analyzers:

Analyzer

|

Description  
  
|  
  
Standard

|

Uses the default analyzer for all Atlas Search indexes and queries.  
  
Simple

|

Divides text into searchable terms wherever it finds a non-letter character.  
  
Whitespace

|

Divides text into searchable terms wherever it finds a whitespace character.  
  
Language

|

Provides a set of language-specific text analyzers.  
  
Keyword

|

Indexes text fields as single terms.  
  
You can also create your own custom analyzer. You can specify alternate
analyzers using multi analyzer.

If you don't specify an analyzer, MongoDB uses the default standard analyzer.

To learn more about analyzers, see Analyzing Analyzers to Build The Right
Search Index For Your App in the MongoDB Developer Center.

← Create an Atlas Search IndexStandard Analyzer →

