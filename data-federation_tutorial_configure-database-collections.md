Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Verify Your Database and Collections

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Next Steps

 _Estimated completion time: 2 minutes_

When you first connect to your federated database instance, Atlas maps sample
data stored in the S3 buckets to a set of databases and collections. This part
of the tutorial walks you through verifying your databases and collections.

## Prerequisites

To complete this part of the tutorial, you will need to have completed:

  *  **Part 1:** Deploy a Federated Database Instance

  *  **Part 2:** Configure Connection for Your Federated Database Instance

  *  **Part 3:** Connect to Your Federated Database Instance

## Procedure

1

### Run the following command in your MongoDB Shell to display the mapped
database.

    
    
    show dbs  
      
  
The MongoDB Shell outputs the following:

    
    
    FederatedDatabaseInstance0  
      
  
2

### Switch to the `FederatedDatabaseInstance0` database.

    
    
    use FederatedDatabaseInstance0  
      
  
3

### Run the following command to display the mapped collections.

    
    
    show collections  
      
  
The MongoDB Shell outputs the following:

    
    
    Collection0  
      
  
## Next Steps

Now that you mapped your data store to virtual databases and virtual
collections, we're ready to run some queries. Proceed to Run Queries Against
Your federated database instance.

