Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Explain Timing Breakdown

Share Feedback

On this page

  * Timing Breakdown
  * Areas of Query

The `explain` response for executionStats and allPlansExecution verbosity
modes includes a `stats` field that contains information on how much time a
query spends in various stages of query execution.

## Timing Breakdown

The timing breakdown describes execution statistics pertinent to an area of
query execution. The following fields show the timing breakdown:

Field

|

Type

|

Description  
  
||  
  
`nanosElapsed`

|

Long

|

Approximate wall-clock time elapsed performing tasks in this area including
the amount of time the children of the query spent in this area. The value is
approximate number of nanoseconds elapsed while performing tasks in this area.  
  
`invocationCounts`

|

Map<String, Long>

|

Number of invocations of tasks included in this area. The value is a map of
task names to their invocation count.  
  
## Areas of Query

Statistics are available for the following areas of query:

Option

|

Description  
  
|  
  
`context`

|

Statistics related to the execution of the Lucene query. There are two tasks
whose invocation counts are enumerated in this area:

|

|  
  
|  
  
`createScorer`

|

Scorer iterates over documents and generates a score for each document.
Invocations of `createScorer` create the object responsible for scoring. Note
that time associated with this task is not time spent actually scoring
documents. Count includes the number of `scorerSupplier` invocations.  
  
`createWeight`

|

Weight stores state associated with a query and `IndexSearcher`. Count
includes the number of `createWeight` invocations.  
  
The time spent in this area is related to the structure of the query, and is
not based on the number of results that are iterated through and scored.

For example:

    
    
    "context" : {  
      
      "nanosElapsed" : NumberLong(4934751),  
      "invocationCounts" : {  
        "createWeight" : NumberLong(1),  
        "createScorer" : NumberLong(10)  
      }  
    }  
  
`match`

|

Statistics related to iterating over and matching result documents. This
statistic shows the time it takes to determine which document is the next
match. Time spent matching results can vary significantly depending on the
nature of the query. There are two tasks whose invocation counts are
enumerated in this area:

|

|  
  
|  
  
`nextDoc`

|

Requests to advance to the next document of the result set. This involves
identifying and moving past skips, or other tasks necessary to find the next
match. Count includes the number of `nextDoc` and `advance` invocations.  
  
`refineRoughMatch`

|

Performs a more thorough match. Some queries execute in a two-phase process
where a document is first "roughly" matched, and is checked with a second,
more thorough phase only after satisfying the first rough match. The
`refineRoughMatch` task is the second phase of the two-phase process. Count
includes the number of `refineRoughMatch` invocations.  
  
For example:

    
    
    "match" : {  
      
      "nanosElapsed" : NumberLong(4901597),  
      "invocationCounts" : {  
        "nextDoc" : NumberLong(541),  
        "refineRoughMatch" : NumberLong(0)  
      }  
    }  
  
`score`

|

Statistics related to scoring documents in the result set. There are two tasks
whose invocation counts are enumerated in this area:

|

|  
  
|  
  
`score`

|

Scores each document in the result set. Count includes the number of `score`
invocations.  
  
`setMinCompetitiveScore`

|

Ignores documents whose score is less than the given value. Indicates that a
query may have been able to reduce the number of scoring operations performed
by ignoring documents with scores below some uncompetitive threshold. Count
includes the number of `setMinCompetitiveScore` invocations.  
  
For example:

    
    
    "score" : {  
      
      "nanosElapsed" : NumberLong(3931312),  
      "invocationCounts" : {  
        "score" : NumberLong(536),  
        "setMinCompetitiveScore" : NumberLong(0)  
      }  
    }  
  
← Lucene Query Structured SummaryReturn Stored Source Fields →

