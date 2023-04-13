Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `$sql`

Share Feedback

On this page

  * Syntax
  * Fields
  * Output
  * Example

## Note

### Beta

The support for SQL format queries is available as a Beta feature. The feature
and the corresponding documentation may change at any time during the Beta
stage.

`$sql` processes an SQL query of the data in a collection. The `$sql` stage:

  * Must be the first stage in the pipeline.

  * Supports `SELECT` and `UNION` statements only.

Use this stage for read-only queries.

## Syntax

    
    
    {  
      
      $sql: {  
        statement: "<SQL-statement>",  
        format: "jdbc",  
        formatVersion: <version-number>,  
        dialect: "mongosql"  
      }  
    }  
  
## Fields

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`dialect`

|

string

|

SQL dialect used by the statement. Value must be `mongosql`.

|

Required  
  
`format`

|

string

|

Structure of the output documents. Value must be `jdbc`.

|

Required  
  
`formatVersion`

|

int

|

Version of the requested output format. Atlas Data Federation supports the
following versions for the jdbc output format:

  * `1`

  * `2` (latest)

If omitted, defaults to the latest version of the requested output format.

|

Optional  
  
`statement`

|

string

|

SQL query or command to run.

|

Required  
  
## Output

If the SQL statement is not a query or a command that returns a result set,
the `$sql` stage does not return any documents.

The output differs based on the format and format version used in the query.

formatVersion 1

formatVersion 2

The `value` field value differs based on whether or not the result set is
empty.

Normal Result set

Empty Result set

If the SQL statement is a query, the `$sql` stage returns one document per row
in the SQL result set. Each document includes a single array field named
`values` that contains documents representing the columns in the result set
and their values. For example:

    
    
    {  
      
      "values": [  
        {  
          "database": "<databaseName>",  
          "table": "<tableName>",  
          "tableAlias": "<tableAlias>",  
          "column": "<columnName>",  
          "columnAlias": "<columnAlias>",  
          "bsonType": "<bsonType>",  
          "value": "<columnValue>"  
        },  
        ...  
      ]  
    }  
  
Field

|

Type

|

Description  
  
||  
  
`emptyResultSet`

|

boolean

|

Flag that indicates if the result set of the query is empty. Value is `true`
if the result set of the query is empty. Atlas Data Federation returns this
field only if the result set of the query is empty.  
  
`values`

|

array of documents

|

Column metadata including column values.  
  
`values[n].database`

|

string

|

Name of the database. For queries against `DUAL`, the field has a `null`
value.  
  
`values[n].table`

|

string

|

Name of the table. For computed columns, the field has a `null` value.  
  
`values[n].tableAlias`

|

string

|

Alias for the table. If the query provides no alias, value is the same as the
table name. For computed columns, the field has a `null` value.  
  
`values[n].column`

|

string

|

Name of the column. For computed columns, the field has a `null` value.  
  
`values[n].columnAlias`

|

string

|

Alias for the column. If the query provides no alias, value is the same as the
column name. For computed columns, the field contains the column name.  
  
`values[n].bsonType`

|

string

|

Type of value. To learn more, see BSON Types.  
  
`values[n].value`

|

BSON data type

|

Column value. Value is `null` if the result set of the query is empty.  
  
## Example

The following example shows the `$sql` syntax for querying a `sampleDB.egData`
collection:

    
    
    {  
      
      $sql: {  
        statement: "select * from egData limit 2",  
        format: "jdbc",  
        formatVersion: 1,  
        dialect: "mongosql",  
      }  
    }  
  
← Retrieve Federated Database Instance Query HistoryData Federation
Limitations →

