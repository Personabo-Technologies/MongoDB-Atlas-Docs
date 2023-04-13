Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Step 1: Create an Atlas Search Index

Share Feedback

On this page

  * Atlas UI
  * Atlas Search API
  * Atlas CLI
  * Next Steps

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Atlas Search index is a data structure that categorizes data in an easily
searchable format. It is a mapping between terms and the documents that
contain those terms. Atlas Search indexes enable faster retrieval of documents
using certain identifiers. You must configure an Atlas Search index to query
data in your Atlas cluster using Atlas Search.

You can create an Atlas Search index on a single field or on multiple fields.
We recommend that you index the fields that you regularly use to sort or
filter your data in order to quickly retrieve the documents that contain the
relevant data at query-time.

You can create an Atlas Search index using the Atlas UI, Atlas Search API, or
Atlas CLI.

This tutorial uses the `sample_mflix.movies` collection from the sample
datasets.

## Atlas UI

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

### Specify an index definition.

You can create an Atlas Search index that uses dynamic mappings or static
mappings. To learn more about dynamic and static mappings, see Static and
Dynamic Mappings.

The following index definition dynamically indexes the fields of supported
types in the `movies` collection. You can use the Visual Editor or the JSON
Editor in the Atlas user interface to create the index.

#### Visual Editor

  1. Click Next.

  2. Review the `"default"` index definition for the `movies` collection.

#### JSON Editor

  1. Click Next.

  2. Review the index definition.

Your index definition should look similar to the following:

    
        {  
      
      "mappings": {  
        "dynamic": true  
      }  
    }  
  
The above index definition dynamically indexes the fields of supported types
in each document in the `movies` collection.

  3. Click Next.

6

### Click Save Changes.

7

### Click Create Search Index.

8

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

9

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Atlas Search API

1

### Copy and paste the sample cURL request in your preferred text editor.

The following index definition dynamically indexes the fields of supported
types in the `movies` collection.

    
    
    1| PUBLIC_KEY=MY_PUBLIC_KEY # replace replace with your public key  
    |  
    2| PRIVATE_KEY=MY_PRIVATE_KEY # replace with your private key  
    3| GROUP_ID=YOUR_GROUP_ID # replace with your project ID  
    4| CLUSTER_NAME=YOUR_CLUSTER_NAME # replace with your cluster's name  
    5|   
      
    6| curl --user "$PUBLIC_KEY:$PRIVATE_KEY" --digest \  
    7|      --header "Content-Type: application/json" \  
    8|      --include \  
    9|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/$GROUP_ID/clusters/$CLUSTER_NAME/fts/indexes?pretty=true" \  
    10|      --data '{  
    11|          "collectionName": "movies",  
    12|          "database": "sample_mflix",  
    13|          "mappings": {  
    14|              "dynamic": true  
    15|          },  
    16|          "name": "default"  
    17|        }'  
  
2

### Replace the variables in your sample cURL request.

The sample cURL requests use these variables. Replace these variables with
your desired values before running the cURL command to create an Atlas Search
index.

Name

|

Type

|

Description  
  
||  
  
PUBLIC_KEY

|

string

|

Your public API Key for your API credentials.  
  
PRIVATE_KEY

|

string

|

Your private API Key for your API credentials.  
  
GROUP_ID

|

string

|

Unique 24-hexadecimal character string that identifies the project that
contains the cluster that contains the collection for which you want to create
an Atlas Search index.  
  
CLUSTER_NAME

|

string

|

Human-readable label that identifies the cluster that contains the collection
for which you want to create an Atlas Search index.

Use the API to get the **CLUSTER_NAME**. For each cluster, Atlas returns the
**CLUSTER_NAME** in the **name** field.  
  
3

### Run the modified cURL request to create the Atlas Search index.

    
    
    1| {  
    |  
    2|   "collectionName" : "movies",  
    3|   "database" : "sample_mflix",  
    4|   "indexID" : "60bfd25f59fc81594354eed3",  
    5|   "mappings" : {  
    6|     "dynamic" : true  
    7|   },  
    8|   "name" : "default",  
    9|   "status" : "IN_PROGRESS"  
    10| }  
  
## Atlas CLI

1

### Create and save the JSON index definition in a file.

Copy the following sample index definition, then paste the JSON index example
into a new file, and save the file:

The following index definition dynamically indexes the fields of supported
types in the `movies` collection.

    
    
    1| {  
    |  
    2|   "name": "INDEX_NAME",  
    3|   "clusterName": "CLUSTER_NAME",  
    4|   "collectionName": "movies",  
    5|   "database": "sample_mflix",  
    6|   "mappings": {  
    7|     "dynamic": true  
    8|   }  
    9| }  
  
2

### Copy and modify the sample Atlas CLI request.

Paste the following sample Atlas CLI request into your favorite text editor
and replace the variables.

    
    
    atlas clusters search index create \  
      
        --clusterName CLUSTER_NAME \  
        --file FILE_PATH \  
        --projectId PROJECT_ID  
        --profile PROFILE_NAME  
  
The sample Atlas CLI requests use these variables. Replace these variables
with your desired values before running the command to create an Atlas Search
index.

Name

|

Type

|

Description  
  
||  
  
PROJECT_ID

|

string

|

Unique 24-hexadecimal character string that identifies the project that
contains the cluster. The cluster contains the collection for which you want
to create an Atlas Search index.  
  
CLUSTER_NAME

|

string

|

Unique 24-hexadecimal character string that identifies the cluster. The
cluster contains the collection for which you want to create an Atlas Search
index.  
  
FILE_PATH

|

string

|

Path to the JSON index file that you created and saved in the previous steps,
including the `.json` file extension.  
  
PROFILE_NAME

|

string

|

 **Optional**. Name of the profile that sets the public and private keys for
the project. See Save Connection Settings for more information. If you remove
the `--profile` flag, the Atlas CLI uses the default profile.  
  
3

### Run the modified Atlas CLI request in your terminal to create the Atlas
Search index.

Run the request. You receive this response when Atlas Search begins creating
the index:

    
    
    {  
      
      "collectionName": "movies",  
      "database": "sample_mflix",  
      "indexID": <index-id>,  
      "mappings": {  
        "dynamic": true  
      },  
      "name": <index-name>,  
      "status": "IN_PROGRESS"  
    }  
  
## Next Steps

Now that you have created the index, proceed to Step 2: Run Atlas Search
Queries.

