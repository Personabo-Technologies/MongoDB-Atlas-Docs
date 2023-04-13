Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Use Synonyms with Atlas Search

Select your language

MongoDB Shell

On this page

  * Load the Sample Synonyms Source Collection
  * Create the Atlas Search Index With Synonym Mapping Definition
  * Search the Collection

This tutorial describes how to add a collection that configures words as
synonyms, create an index that defines synonym mappings on the
`sample_mflix.movies` collection, and run Atlas Search queries against the
`title` field using words that are configured as synonyms.

The tutorial takes you through the following steps:

  1. Load one or more sample synonyms source collections in the `sample_mflix` database.

  2. Create an Atlas Search index with one or more synonym mappings for the `sample_mflix.movies` collection.

  3. Run Atlas Search queries against the `title` field in the `sample_mflix.movies` collection for words configured as synonyms in the synonyms source collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Note

To create multiple synonym mappings and run the advanced sample query in this
tutorial, you will need an `M10` or higher cluster.

## Load the Sample Synonyms Source Collection

Each document in the synonyms source collection describe how one or more words
map to one or more synonyms of those words. To learn more about the fields and
word mapping types in the synonyms source collection documents, see Format of
Synonyms Source Collection Documents.

To begin, you create the synonyms source collection and then add the
collection to the database where you intend to use the synonyms source
collection. In this section, you create one or two sample synonyms source
collections in the `sample_mflix` database, and then use the synonyms source
collections with an index of the `movies` collection in the same database.

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Click your cluster's Browse Collections button.

3

### Create one or more sample synonyms collections in the `sample_mflix`
database.

If you are running a free or shared tier cluster, follow the steps in the
_Transportation Synonyms_ tab to create the collection for a single synonym
mapping definition in your index. If you have a `M10` or higher cluster and
wish to create multiple synonym mappings in your index, follow the steps in
both the tabs to create both the _Transportation Synonyms_ and _Attire
Synonyms_ collections.

Transportation Synonyms

Attire Synonyms

  1. Expand the `sample_mflix` database and click the __icon to open the Create Collection modal.

  2. Type `transportation_synonyms` in the Collection name field.

  3. Click Create to create the collection in the `sample_mflix` database.

4

### Load the sample data into the synonyms collection.

Follow the steps in the tabs to load data into the respective collection.

Transportation Synonyms

Attire Synonyms

  1. Select the `transport_synonyms` collection if it's not selected.

  2. Click Insert Document for each of the sample documents to add to the collection.

  3. Click the JSON view ({}) to replace the default document.

  4. Copy and paste the following sample documents, one at a time, and click Insert to add the documents, one at a time, to the collection.
    
        {  
      
      "mappingType": "equivalent",  
      "synonyms": ["car", "vehicle", "automobile"]  
    }  
  
MongoDB Shell

    
        {  
      
      "mappingType": "explicit",  
      "input": ["boat"],  
      "synonyms": ["boat", "vessel", "sail"]  
    }  
  
MongoDB Shell

## Create the Atlas Search Index With Synonym Mapping Definition

The synonym mapping in a collection's index specifies the synonyms source
collection and the analyzer to use with the collection.

In this section, you create an Atlas Search index that defines one or many
synonym mappings for the `sample_mflix.movies` collection. The mapping
definition in the index references the synonyms source collection that you
created in the `sample_mflix` database.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

### Modify the default index definition.

To run the simple example query only, use the index definition in the **Single
Synonym Mapping** tab below. If you have an `M10` or higher cluster and if you
loaded both the example synonyms source collections, you can run both the
simple and advanced example queries using the index definition that specifies
multiple synonym mappings in the **Multiple Synonym Mappings** tab below.

Single Synonym Mapping

Multiple Synonym Mappings

The following index definition specifies:

  * The language analyzer `lucene.english` as the default analyzer for both indexing and querying the `title` field.

  * The name `transportSynonyms` as the name for this synonym mapping.

  * The `transport_synonyms` collection as the source synonyms collection to look for synonyms for queries using `transportSynonyms` mapping. `transportSynonyms` can be used in text queries over any field indexed with the `lucene.english` analyzer (including the `title` field, in this example).

Visual Editor

JSON Editor

  1. Click Next.

  2. Click Refine Your Index.

  3. Click Add Field in the Field Mappings section.

  4. Configure the following fields in the Add Field Mapping window and click Add after:

UI Field Name

|

Configuration  
  
|  
  
Field Name

|

Enter `title`.  
  
Enable Dynamic Mapping

|

Toggle to Off.  
  
Data Type Configuration

|

    1. Click Add Data Type.

    2. Select String.

    3. For Index Analyzer and Search Analyzer, click the dropdown to select lucene.english from the lucene.language analyzers dropdown.  
  
For all other fields not listed above, accept the default.

  5. Click Add Synonym Mapping in the Synonym Mappings section.

  6. Configure the following fields in the Add Synonym Mapping window and click Add after:

UI Field Name

|

Configuration  
  
|  
  
Synonym Mapping Name

|

Enter `transportSynonyms`.  
  
Synonym Source Collection

|

Select `transport_synonyms`.  
  
Analyzer

|

Select `lucene.english`.  
  
  7. Click Save Changes.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Search the Collection

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
examples in this section.

* * *

Synonyms can be used only in queries that use the text operator. In this
section, you connect to your Atlas cluster and then run the sample queries
using the `text` operator against the `title` field in the
`sample_mflix.movies` collection. The sample queries use words that are
configured as synonyms of different mapping types in the synonyms source
collection. The source collection is referenced in the synonyms mapping that
the queries use.

MongoDB Shell

Compass

Go

Java (Sync)

Node.js

Python

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

### Run the following example queries on the `movies` collection.

If you created an index with a single synonym mapping definition, run the
query in the Simple Example tab below. If you defined multiple synonym
mappings in your index, you can run the queries in both the tabs below.

These queries use the following pipeline stages:

  * `$search` stage to search the collection.

  * `$limit` stage to limit the output to `10` results.

  * `$project` stage to:

    * Exclude all fields except the `title` field.

    * Add a field named `score`.

Simple Example

Advanced Example

Atlas Search query results vary based on the type of word mapping defined in
the synonyms source collection.

equivalent Mapping Type

explicit Mapping Type

The query searches the `title` field for the word `automobile` and uses the
synonym mapping definition named `transportSynonyms` to search for words
configured as synonyms of the query word `automobile` in the synonyms source
collection named `transport_synonyms`.

    
    
    1| db.movies.aggregate([  
    |  
    2|   {  
    3|     $search: {  
    4|       "text": {  
    5|         "path": "title",  
    6|         "query": "automobile",  
    7|         "synonyms": "transportSynonyms"  
    8|       }  
    9|     }  
    10|   },  
    11|   {  
    12|     $limit: 10  
    13|   },  
    14|   {  
    15|     $project: {  
    16|       "_id": 0,  
    17|       "title": 1,  
    18|       "score": { $meta: "searchScore" }  
    19|     }  
    20|   }  
    21| ])  
  
MongoDB Shell

This query returns the following results:

    
    
    1| { "title" : "Cars", "score" : 4.197734832763672 }  
    |  
    2| { "title" : "Planes, Trains & Automobiles", "score" : 3.8511905670166016 }  
    3| { "title" : "Car Wash", "score" : 3.39473032951355 }  
    4| { "title" : "Used Cars", "score" : 3.39473032951355 }  
    5| { "title" : "Blue Car", "score" : 3.39473032951355 }  
    6| { "title" : "Cars 2", "score" : 3.39473032951355 }  
    7| { "title" : "Stealing Cars", "score" : 3.39473032951355 }  
    8| { "title" : "Cop Car", "score" : 3.39473032951355 }  
    9| { "title" : "The Cars That Eat People", "score" : 2.8496146202087402 }  
    10| { "title" : "Khrustalyov, My Car!", "score" : 2.8496146202087402 }  
  
MongoDB Shell

The Atlas Search results contain movies with `car` and `automobile` in the
`title` field although the query term is `automobile` because we configured
`automobile` to be a synonym of `car`, `vehicle`, and `automobile` in the
synonyms source collection named `sample_synonyms`, which is specified in the
index for the collection. Atlas Search returns the same results for a search
of the words `car` and `vehicle`. To test this, replace the value of the
`query` field in the query above with either `car` or `vehicle` and run the
query in your `mongosh`.

← How to Run Partial Match Atlas Search QueriesHow to Run Multilingual Atlas
Search Queries →

