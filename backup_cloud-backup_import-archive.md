Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Import Archive from S3

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

You can restore data archived to S3 buckets using `mongoimport`. This page has
a sample procedure to import archived data using the AWS CLI and the MongoDB
`mongoimport` utility.

## Prerequisites

Before you begin, you must:

  * Install the AWS CLI

  * Configure the AWS CLI

  * Install the mongoimport tool

## Procedure

1

### Copy the data in the S3 bucket to a folder using the AWS CLI and extract
the data.

    
    
    aws s3 cp s3://<bucketName>/<prefix> <downloadFolder> --recursive  
      
    gunzip -r <downloadFolder>  
  
where:

|  
  
|  
  
`<bucketName>`

|

Name of the AWS S3 bucket.  
  
`<prefix>`

|

Path to archived data in the bucket. The path has the following format:

    
    
    | /exported_snapshots/<orgName>/<projectName>/<clusterName>/<initiationDateOfSnapshot>/<timestamp>/  
      
  
`<downloadFolder>`

|

Path to the local folder where you want to copy the archived data.  
  
For example, run a command similar to the following:

## Example

    
    
    aws s3 cp s3://export-test-bucket/exported_snapshots/myOrg/myProj/export-me-sharded-cluster/2021-04-24T0013/1619224539 mybucket --recursive  
      
    gunzip -r mybucket  
  
2

### Copy and store the following script in a file named `massimport.sh`.

    
    
    #!/bin/bash  
      
    regex='/(.+)/(.+)/.+'  
    dir=${1%/}  
    find $dir -type f -not -path '*/\.*' -not -path '*metadata\.json' | while read line ; do  
      [[ $line =~ $regex ]]  
      db_name=${BASH_REMATCH[1]}  
      col_name=${BASH_REMATCH[2]}  
      mongoimport --uri "$2" --mode=upsert -d $db_name -c $col_name --file $line --type json  
    done  
  
Here:

  * `--mode=upsert` enables `mongoimport` to handle duplicate documents from an archive.

  * `--uri` specifies the connection string for the Atlas cluster.

3

### Run the `massimport.sh` utility to import the archived data into your
collection using `mongoimport`.

    
    
    sh massimport.sh <downloadFolder> "mongodb+srv://<connectionString>"  
      
  
where:

|  
  
|  
  
`<downloadFolder>`

|

Path to the local folder where you copied the archived data.  
  
`<connectionString>`

|

Connection string for the Atlas cluster.  
  
For example, run a command similar to the following:

## Example

    
    
    sh massimport.sh mybucket/ "mongodb+srv://<myConnString>"  
      
  
← Restore from a Snapshot Using Encryption at RestArchive Data →

