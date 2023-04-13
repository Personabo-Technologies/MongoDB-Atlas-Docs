Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Run Queries Against Your Federated Database Instance

Share Feedback

On this page

  * Prerequisites
  * Queries
  * Summary

 _Estimated completion time: 5 minutes_

You can run operations using the MongoDB Query Language (MQL) which includes
most, but not all standard server commands. To learn which MQL operations are
supported, see the MQL Support documentation.

## Note

The Atlas Data Federation sample datasets are read-only.

## Prerequisites

To complete this part of the tutorial, you will need to have completed:

  *  **Part 1:** Deploy a Federated Database Instance

  *  **Part 2:** Configure Connection for Your Federated Database Instance

  *  **Part 3:** Connect to Your Federated Database Instance

  *  **Part 4:** Verify Your Database and Collections

You must be connected to your federated database instance with the MongoDB
Shell before running the following queries.

## Queries

Before running the queries, switch to `Database0` database:

    
    
    use FederatedDatabaseInstance0  
      
  
The following queries use the paths that you added to your federated database
instance during deployment. If you added all the paths to the sample datasets,
you can run all the queries in the following tabs. If you only added some
paths, click and run the queries in the appropriate tabs for the sample
dataset paths that you added.

AirBnb

Analytics

Mflix

Find the number of AirBnB offerings with `3` bedrooms and a high review score:

    
    
    db.Collection0.aggregate([{$match: {"bedrooms" : 3, "review_scores.review_scores_rating": {$gt: 79}} },{ $count: "numProperties"}])  
      
  
Find properties with `3` bedrooms and sort the returned documents by customer
review rating. Limit the number of documents returned to `5`:

    
    
    db.Collection0.find({"bedrooms" : 3} ).sort({review_scores_rating: -1}).limit(5)  
      
  
## Summary

Congratulations! You just set up a federated database instance, created a
database and collections from data stored in an S3 bucket, and queried the
data using MQL commands.

For more information on federated database instances, see Atlas Data
Federation.

## Note

When you dynamically generate collections from filenames, the number of
collections is not accurately reported in the Data Federation view.

