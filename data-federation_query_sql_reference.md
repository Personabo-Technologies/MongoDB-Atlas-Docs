Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# SQL Reference

Share Feedback

On this page

  * FLATTEN
  * Syntax
  * Flatten Example
  * UNWIND
  * Syntax
  * Unwind Example
  * Unwind and Flatten Example
  * Limitations

## Note

### Preview

The support for SQL queries is available as a Preview feature. This feature
and the corresponding documentation may change at any time during the Preview
phase.

The Atlas SQL interface is a SQL-92 compatible dialect (read-only) with some
limitations. This reference covers specific capabilities of the dialect that
are included to make it easier for you to interact with document structures.

## FLATTEN

`FLATTEN` flattens semi-structured data (name-value pairs in JSON) into
separate columns. Field names become column names that hold all of the values
for that field in rows.

### Syntax

The syntax for flattening nested documents is a `FLATTEN` function that can be
used in the `FROM` clause in conjunction with a data source and options.

    
    
    SELECT * FROM FLATTEN(<data source> WITH DEPTH => <integer>, SEPARATOR => <string>)  
      
  
Variable

|

Necessity

|

Description  
  
||  
  
<data source>

|

Required

|

Data source to flatten.  
  
`DEPTH`

|

Optional

|

Positive integer indicating how many levels of subdocuments to flatten.
Defaults to flattening every level of subdocuments.  
  
`SEPARATOR`

|

Optional

|

String to use as the delimiter when concatenating field names. Defaults to
`_`.  
  
### Flatten Example

In an example scenario, a `customerInfo` collection contains documents that
are structured as follows:

    
    
    {  
      
      id: 1,  
      location: "New York",  
      customer: {  
        age: 50,  
        email: "customer@email.com",  
        satisfaction: 5  
      }  
    }  
  
If you run the query `SELECT * FROM customerInfo`, Atlas SQL returns documents
with the following top-level fields:

|  
  
|  
  
`id`

|

1  
  
`location`

|

"New York"  
  
`customer`

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }  
  
If you run the query `SELECT * FROM FLATTEN(customerInfo)`, Atlas SQL returns
documents with the following top-level fields:

|  
  
|  
  
`id`

|

1  
  
`location`

|

"New York"  
  
`customer_age`

|

50  
  
`customer_email`

|

"customer@email.com"  
  
`customer_satisfaction`

|

5  
  
When you use `FLATTEN`, each flattened field from the original document
becomes a top-level field in the result set. Nested fields are concatenated
with their parent field names and separated by the default delimiter, `_`.

## UNWIND

`UNWIND` deconstructs an array field from the input data source to output one
row for each item in that array. To learn more about unwinding, see the
$unwind aggregation stage documentation.

### Syntax

The syntax for unwinding array fields is an `UNWIND` function that can be used
in the `FROM` clause in conjunction with a data source and options.

    
    
    SELECT * FROM UNWIND(<data source> WITH PATH => <array_path>, INDEX => <identifier>, OUTER => <bool>)  
      
  
Variable

|

Necessity

|

Description  
  
||  
  
<data source>

|

Required

|

Source of the array field to unwind.  
  
`PATH`

|

Required

|

Path to the field in the data source to unwind.  
  
`INDEX`

|

Optional

|

Name to assign the index column. If omitted, Atlas SQL does not create an
index field.  
  
`OUTER`

|

Optional

|

Flag that indicates whether documents with null, missing, or empty array
values are preserved. If `true`, documents with null, missing, or empty array
values are preserved. Defaults to `false`.  
  
### Unwind Example

In an example scenario, a `customerInfo` collection contains documents that
are structured as follows:

    
    
    {  
      
      id: 1,  
      location: "New York",  
      customer: {  
        age: 50,  
        email: "customer@email.com",  
        satisfaction: 5  
      },  
      visits: [  
        {  
          year: 2020,  
          score: 10  
        },  
        {  
          year: 2021,  
          score: 8  
        },  
        {  
          year: 2022  
          score: 7  
        }  
      ]  
    }  
  
If you run the query `SELECT * FROM customerInfo`, Atlas SQL returns documents
with the following top-level fields:

|  
  
|  
  
`id`

|

1  
  
`location`

|

"New York"  
  
`customer`

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }  
  
`visits`

|

[ { year: 2020, score: 10 }, { year: 2021, score: 8 }, { year: 2022, score: 7
} ]  
  
If you run the query `SELECT * FROM UNWIND(customerInfo WITH PATH => visits,
INDEX => idx)`, Atlas SQL returns documents with the following top-level
fields:

|

|

|  
  
|||  
  
`id`

|

1

|

1

|

1  
  
`location`

|

"New York"

|

"New York"

|

"New York"  
  
`customer`

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }  
  
`idx`

|

0

|

1

|

2  
  
`visits`

|

{ year: 2020, score: 10 }

|

{ year: 2021, score: 8 }

|

{ year: 2022, score: 7 }  
  
When you use `UNWIND` with `PATH => visits`, each `visits` object becomes a
table row.

### Unwind and Flatten Example

The following example combines the `FLATTEN` and `UNWIND` functions.

In an example scenario, a `customerInfo` collection contains documents that
are structured as follows:

    
    
    {  
      
      id: 1,  
      location: "New York",  
      customer: {  
        age: 50,  
        email: "customer@email.com",  
        satisfaction: 5  
      },  
      visits: [  
        {  
          year: 2020,  
          score: 10  
        },  
        {  
          year: 2021,  
          score: 8  
        },  
        {  
          year: 2022  
          score: 7  
        }  
      ]  
    }  
  
If you run the query `SELECT * FROM customerInfo`, Atlas SQL returns documents
with the following top-level fields:

|  
  
|  
  
`id`

|

1  
  
`location`

|

"New York"  
  
`satisfaction`

|

5  
  
`customer`

|

{ age: 50, email: "customer@email.com", satisfaction: 5 }  
  
`visits`

|

[ { year: 2020, score: 10 }, { year: 2021, score: 8 }, { year: 2022, score: 7
} ]  
  
If you run the query `Select * from FLATTEN(UNWIND(customerInfo WITH PATH =>
visits, INDEX => idx))`, Atlas SQL returns documents with the following top-
level fields:

|

|

|  
  
|||  
  
`id`

|

1

|

1

|

1  
  
`location`

|

"New York"

|

"New York"

|

"New York"  
  
`satisfaction`

|

5

|

5

|

5  
  
`customer_age`

|

50

|

50

|

50  
  
`customer_email`

|

"customer@email.com"

|

"customer@email.com"

|

"customer@email.com"  
  
`idx`

|

0

|

1

|

2  
  
`visits_year`

|

2020

|

2021

|

2022  
  
`visits_score`

|

10

|

8

|

7  
  
When you use both the `FLATTEN` and `UNWIND` functions, Atlas SQL flattens the
`customer` nested document, and unwinds and flattens the `visits` array.

## Limitations

Atlas SQL is not fully SQL-92 compatible due to the following limitations:

  * The `UNION` function is not supported. However, `UNION ALL` is supported.

  * The `date` data type is not supported. Use `timestamp` instead.

  * Interval and date interval arithmetic are not supported.

← `sqlGetSchema`Release Notes →

