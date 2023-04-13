Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Lucene Query Structured Summary

Share Feedback

The explain response of a search command contains information about the query
executed with that command. The response includes structured details of what
Lucene queries Atlas Search executed to satisfy a `$search` query.

This page contains:

  * Some of the Lucene queries that Atlas Search operators create

  * Lucene query options that are included in the structured summary

  * Lucene query structured summary example for each Lucene query type

## Note

### About the Examples

The examples in this section are based on queries run against the sample
datasets with the `queryPlanner` verbosity mode. In the example response, the:

  * `mongotQuery` field shows the Atlas Search operator and the query that was run.

  * `explain.type` field shows the Lucene Query that the operator created.

For complete examples, see Examples.

`BooleanQuery`

    

Options

Example

For Lucene `BooleanQuery`, the structured summary includes details on the
following options:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`must`

|

<Explain Response>

|

Optional

|

Clauses which must match.  
  
`mustNot`

|

<Explain Response>

|

Optional

|

Clauses which must not match.  
  
`should`

|

<Explain Response>

|

Optional

|

Clauses which should match.  
  
`filter`

|

<Explain Response>

|

Optional

|

Clauses which must all match.  
  
`minimumShouldMatch`

|

Integer

|

Optional

|

The minimum number of `should` clauses which must match.  
  
`ConstantScoreQuery`

    

Options

Example

For constant score queries, the structured summary includes details on the
following options:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`query`

|

Explain Response

|

Required

|

Child of the `ConstantScoreQuery`.  
  
`FunctionScoreQuery`

    

Options

Example

For Lucene `FunctionScoreQuery` queries, the structured summary includes
details on the following options:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`scoreFunction`

|

string

|

Required

|

Scoring expression used in the query.  
  
`query`

|

Explain Response

|

Required

|

The query.  
  
`LatLonPointDistanceQuery`

    

Options

Example

For Lucene `LatLonPointDistanceQuery` queries, the response contains an
Explain Timing Breakdown only.

`LatLonShapeQuery`

    

Options

Example

For Lucene `LatLonShapeQuery` queries, the response contains an Explain Timing
Breakdown only.

`LongDistanceFeatureQuery`

    

Options

Example

For Lucene `LongDistanceFeatureQuery`, the response contains an Explain Timing
Breakdown only.

`MultiTermQueryConstantScoreWrapper`

    

Options

Example

For Lucene `MultiTermQueryConstantScoreWrapper` queries, the structured
summary includes details on the following arguments:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`queries`

|

List<Explain Response>

|

Required

|

List of queries.  
  
`PhraseQuery`

    

Options

Example

For Lucene `PhraseQuery` queries, the structured summary includes details on
the following arguments:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`path`

|

string

|

Required

|

Indexed field to search.  
  
`query`

|

string

|

Required

|

String or strings to search for.  
  
`slop`

|

int

|

Required

|

Allowable distance between words in the `query` phrase.  
  
`PointRangeQuery`

    

Options

Example

For Lucene `PointRangeQuery` queries, the structured summary includes details
on the following arguments:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`path`

|

string

|

Required

|

Indexed field to search.  
  
`representation`

|

string

|

Optional

|

Numeric representation. Queries over date-typed data do not include
representation.  
  
`gte`

|

number

|

Optional

|

Lower bound of the query.  
  
`lte`

|

number

|

Optional

|

Upper bound of the query.  
  
`TermQuery`

    

Options

Example

For term queries, the structured summary includes details on the following
arguments:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`path`

|

string

|

Required

|

Indexed field to search.  
  
`value`

|

string

|

Required

|

String to search for.  
  
`Default`

    

Options

Example

Lucene queries that are not explicitly defined by another Lucene query are
serialized using the default query. The structured summary includes details on
the following option:

Field

|

Type

|

Necessity

|

Description  
  
|||  
  
`queryType`

|

string

|

Required.

|

Type of Lucene query.

