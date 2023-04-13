Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Atlas Search Queries Using Materialized Views

Share Feedback

On this page

  * Create the `purchaseOrders` Collection
  * Create the `updateMonthlySales` Function
  * Create the `updateMonthlyPurchaseOrders` Function
  * Create Scheduled Triggers
  * Create an Atlas Search Index on the Materialized View
  * Run a Query on the Materialized View

This tutorial describes how to create an index and run queries against the
`sample_supplies.sales` collection from the sample dataset and a new
`sample_supplies.purchaseOrders` collection using a combination of the
following features:

  * on-demand materialized views

  * Atlas App Services scheduled triggers

An on-demand materialized view is a collection that you create and update
using a `$merge` aggregation pipeline stage. You can create an Atlas Search
index on the materialized view and then run queries on the materialized view
using the `$search` aggregation pipeline stage.

This tutorial takes you through the following steps:

  1. Create a collection named `purchaseOrders` in the `sample_supplies` database.

  2. Create an App Services function named `updateMonthlySales` in the App Services UI to initialize the `monthlyPhoneTransactions` materialized view using data from the sample `sample_supplies.sales` collection on your Atlas cluster.

  3. Create an App Services function named `updateMonthlyPurchaseOrders` in the App Services UI to update the `monthlyPhoneTransactions` materialized view using data from the `sample_supplies.purchaseOrders` collection that you created on your Atlas cluster.

  4. Schedule the following functions to update the `monthlyPhoneTransactions` materialized view on a periodic basis using App Services scheduled triggers:

    1. `updateMonthlySales`

    2. `updateMonthlyPurchaseOrders`

  5. Create an Atlas Search index on the `monthlyPhoneTransactions` materialized view.

  6. Run a query on the `monthlyPhoneTransactions` materialized view.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the `purchaseOrders` Collection

1

### Connect to the `sample_supplies` database.

  1. Open `mongosh` in a terminal window and connect to your cluster. For detailed instructions on connecting, see Connect via `mongosh`.

  2. Use the `sample_supplies` database:
    
        use sample_supplies  
      
  

2

### Add a new collection.

Add the `purchaseOrders` collection with new phone purchase order data from
January of 2018.

    
    
    db.purchaseOrders.insertMany( [  
      
      {  
        saleDate: ISODate("2018-01-23T21:06:49.506Z"),  
        items: [  
          {  
            name: 'printer paper',  
            tags: [ 'office', 'stationary' ],  
            price: Decimal128("40.01"),  
            quantity: 2  
          },  
          {  
            name: 'notepad',  
            tags: [ 'office', 'writing', 'school' ],  
            price: Decimal128("35.29"),  
            quantity: 2  
          },  
          {  
            name: 'pens',  
            tags: [ 'writing', 'office', 'school', 'stationary' ],  
            price: Decimal128("56.12"),  
            quantity: 5  
          },  
          {  
            name: 'backpack',  
            tags: [ 'school', 'travel', 'kids' ],  
            price: Decimal128("77.71"),  
            quantity: 2  
          },  
          {  
            name: 'notepad',  
            tags: [ 'office', 'writing', 'school' ],  
            price: Decimal128("18.47"),  
            quantity: 2  
          },  
          {  
            name: 'envelopes',  
            tags: [ 'stationary', 'office', 'general' ],  
            price: Decimal128("19.95"),  
            quantity: 8  
          },  
          {  
            name: 'envelopes',  
            tags: [ 'stationary', 'office', 'general' ],  
            price: Decimal128("8.08"),  
            quantity: 3  
          },  
          {  
            name: 'binder',  
            tags: [ 'school', 'general', 'organization' ],  
            price: Decimal128("14.16"),  
            quantity: 3  
          }  
        ],  
        storeLocation: 'Denver',  
        customer: {  
          gender: 'M',  
          age: 42,  
          email: 'cauho@witwuta.sv',  
          satisfaction: 4  
        },  
        couponUsed: true,  
        purchaseMethod: 'Phone'  
      },  
      {  
        saleDate: ISODate("2018-01-25T10:01:02.918Z"),  
        items: [  
          {  
            name: 'envelopes',  
            tags: [ 'stationary', 'office', 'general' ],  
            price: Decimal128("8.05"),  
            quantity: 10  
          },  
          {  
            name: 'binder',  
            tags: [ 'school', 'general', 'organization' ],  
            price: Decimal128("28.31"),  
            quantity: 9  
          },  
          {  
            name: 'notepad',  
            tags: [ 'office', 'writing', 'school' ],  
            price: Decimal128("20.95"),  
            quantity: 3  
          },  
          {  
            name: 'laptop',  
            tags: [ 'electronics', 'school', 'office' ],  
            price: Decimal128("866.5"),  
            quantity: 4  
          },  
          {  
            name: 'notepad',  
            tags: [ 'office', 'writing', 'school' ],  
            price: Decimal128("33.09"),  
            quantity: 4  
          },  
          {  
            name: 'printer paper',  
            tags: [ 'office', 'stationary' ],  
            price: Decimal128("37.55"),  
            quantity: 1  
          },  
          {  
            name: 'backpack',  
            tags: [ 'school', 'travel', 'kids' ],  
            price: Decimal128("83.28"),  
            quantity: 2  
          },  
          {  
            name: 'pens',  
            tags: [ 'writing', 'office', 'school', 'stationary' ],  
            price: Decimal128("42.9"),  
            quantity: 4  
          },  
          {  
            name: 'envelopes',  
            tags: [ 'stationary', 'office', 'general' ],  
            price: Decimal128("16.68"),  
            quantity: 2  
          }  
        ],  
        storeLocation: 'Seattle',  
        customer: { gender: 'M', age: 50, email: 'keecade@hem.uy', satisfaction: 5 },  
        couponUsed: false,  
        purchaseMethod: 'Phone'  
      },  
    ] )  
  
3

### Query the new collection.

Query the `purchaseOrders` collection to confirm the new purchase order
entries.

    
    
    db.purchaseOrders.find().sort( {saleDate: -1} )  
      
  
VIEW OUTPUT

The two query results reflect that the purchase order data ends in January of
2018.

## Create the `updateMonthlySales` Function

Create the updateMonthlySales function in the App Services UI.

### How the `updateMonthlySales` Function Works

The `updateMonthlySales` function defines a `monthlyPhoneTransactions`
materialized view that contains cumulative monthly sales information. The
function updates monthly sales information for sales conducted over the phone.

The following example defines the function:

    
    
    exports = function(){  
      
      
       var pipeline = [  
         { $match: {purchaseMethod: "Phone"} },  
         { $unwind: {path: "$items"}},  
         { $group: {  
          _id: { $dateToString:  
          { format: "%Y-%m", date: "$saleDate" } },  
          sales_quantity: { $sum: "$items.quantity"},  
          sales_price: { $sum: "$items.price"}  
         }},  
         { $set: { sales_price: { $toDouble: "$sales_price"}}},  
         { $merge: { into: "monthlyPhoneTransactions", whenMatched: "replace" } }  
       ]  
      
       var monthlyPhoneTransactions = context.services.get("mongodb-atlas").db("sample_supplies").collection("sales");  
      
       return monthlyPhoneTransactions.aggregate(pipeline);  
    };  
  
The function uses the following aggregation pipeline stages to update
`monthlyPhoneTransactions`:

  * The `$match` stage filters the data to process only those sales that were completed over the `Phone`.

  * The `$group` stage groups the sales information by the year-month. This stage outputs documents that have the form:
    
        { "_id" : "<YYYY-mm>", "sales_quantity" : <num>, "sales_amount" : <NumberDecimal> }  
      
  
  * The `$set` stage changes the data type of the `sales_price` field to `double`. Atlas Search `$search` operators don't support the `Decimal128` data type. Changing the `sales_price` field's data type allows you to query this field using Atlas Search indexes.

  * The `$merge` stage writes the output to the `monthlyPhoneTransactions` collection.

Based on the `_id` field, (the default for unsharded output collections), the
stage checks if the document in the aggregation results matches an existing
document in the collection:

    * When Atlas Search finds a match (that is, a document with the same year-month already exists in the collection), Atlas Search replaces the existing document with the document from the aggregation results as specified in the stage.

    * When Atlas Search doesn't find a match, Atlas Search inserts the document from the aggregation results into the collection as specified in the stage. This is the default behavior when there is no match for the field.

### Procedure

1

#### Create a new app.

To define a new server-side function from the UI, you must first create an App
Services App:

  1. If you have not already done so, click the App Services tab.

  2. Create the app:

    * If you are creating your first App Services App in the project, you will be shown an option to start without a template (Build your own App). Select the Build your own App option.

    * If you have already created at least one App Services App in the project, click Create a New App.

  3. In the Name field, enter `Sales-App` as the name of the function.

  4. Under the Link your Database field, select the Use an existing MongoDB Atlas Data Source option.

  5. From the dropdown, select the Atlas cluster you created in the Prerequisites.

  6. Click Create App Service.

2

#### Create a new function.

To define a new server-side function from the UI:

  1. Click Functions in the left navigation menu.

  2. Click Create New Function.

  3. Enter `updateMonthlySales` as the name of the function.

  4. Under Authentication, select System.

3

#### Input the `updateMonthlySales` function code.

  1. Click the Function Editor tab.

  2. Add the javascript code to the `exports` function. At minimum, the code must assign a function to the global variable `exports`:
    
        exports = function(){  
      
      
    var pipeline = [  
      { $match: {purchaseMethod: "Phone"} },  
      { $unwind: {path: "$items"}},  
      { $group: {  
        _id: { $dateToString:{ format: "%Y-%m", date: "$saleDate" } },  
        sales_quantity: { $sum: "$items.quantity"},  
        sales_price: { $sum: "$items.price"}  
        }  
      },  
      { $set: { sales_price: { $toDouble: "$sales_price"}}},  
      { $merge: { into: "monthlyPhoneTransactions", whenMatched: "replace" } }  
    ]  
      
    var monthlyPhoneTransactions = context.services.get("mongodb-atlas").db("sample_supplies").collection("sales");  
      
    return monthlyPhoneTransactions.aggregate(pipeline);  
    };  
  
  3. Click the Run button in the lower right-hand corner of the Function Editor to create the `monthlyPhoneTransactions` materialized view.

The Result tab at the bottom of the Function Editor should indicate success
without any errors.

  4. Click Save Draft.

4

#### Test the function.

  1. Open `mongosh` in a terminal window and connect to your cluster. For detailed instructions on connecting, see Connect via `mongosh`.

  2. Use the `sample_supplies` database:
    
        use sample_supplies  
      
  
  3. Query the `sales` collection. Note that the last sale in `sales` occurs in December of 2017:
    
        db.sales.find().sort( {saleDate: -1} )  
      
  
  4. Confirm that the materialized view has been created in your `sample_supplies` database:
    
        show collections  
      
  
VIEW OUTPUT

The command lists your collections, including the newly created
`monthlyPhoneTransactions` materialized view.

  5. Query the `monthlyPhoneTransactions` materialized view:
    
        db.monthlyPhoneTransactions.find().sort( { _id: -1} )  
      
  
VIEW OUTPUT

The `monthlyPhoneTransactions` materialized view shows the newly added data.
The top result reflects that the most recent transaction took place in
December 2017.

## Create the `updateMonthlyPurchaseOrders` Function

Create the updateMonthlyPurchaseOrders function in the App Services UI.

### How the `updateMonthlyPurchaseOrders` Function Works

The `updateMonthlyPurchaseOrders` function adds cumulative monthly purchase
order information to the `monthlyPhoneTransactions` materialized view. The
function updates the monthly purchase order information for purchase orders
conducted over the phone.

The following example defines the function:

    
    
    exports = function(){  
      
      
       var pipeline = [  
         { $match: {purchaseMethod: "Phone"} },  
         { $unwind: {path: "$items"}},  
         { $group: {  
          _id: { $dateToString:  
          { format: "%Y-%m", date: "$saleDate" } },  
          sales_quantity: { $sum: "$items.quantity"},  
          sales_price: { $sum: "$items.price"}  
         }},  
         { $set: { sales_price: { $toDouble: "$sales_price"}}},  
         { $merge: { into: "monthlyPhoneTransactions", whenMatched: "replace" } }  
       ]  
      
       var monthlyPhoneTransactions = context.services.get("mongodb-atlas").db("sample_supplies").collection("purchaseOrders");  
      
       return monthlyPhoneTransactions.aggregate(pipeline);  
    };  
  
The `updateMonthlyPurchaseOrders` function uses the same aggregation pipeline
stages to update `monthlyPhoneTransactions` as the updateMonthlySales
function.

### Procedure

1

#### Create a New Function for the `purchaseOrders` collection.

To define a new server-side function from the UI:

  1. Return to your App Services App.

  2. Click Functions in the left navigation menu.

  3. Click Create New Function.

  4. Enter `updateMonthlyPurchaseOrders` as the name of the function.

  5. Under Authentication, select System.

2

#### Input the `updateMonthlyPurchaseOrders` Function Code

  1. Click the Function Editor tab.

  2. Add the javascript code to the `exports` function. At minimum, the code must assign a function to the global variable `exports`:
    
        exports = function(){  
      
      
    var pipeline = [  
      { $match: {purchaseMethod: "Phone"} },  
      { $unwind: {path: "$items"}},  
      { $group: {  
        _id: { $dateToString:{ format: "%Y-%m", date: "$saleDate" } },  
        sales_quantity: { $sum: "$items.quantity"},  
        sales_price: { $sum: "$items.price"}  
        }  
      },  
      { $set: { sales_price: { $toDouble: "$sales_price"}}},  
      { $merge: { into: "monthlyPhoneTransactions", whenMatched: "replace" } }  
    ]  
      
    var monthlyPhoneTransactions = context.services.get("mongodb-atlas").db("sample_supplies").collection("purchaseOrders");  
      
    return monthlyPhoneTransactions.aggregate(pipeline);  
    };  
  
  3. Click the Run button in the lower right-hand corner of the Function Editor to update the `monthlyPhoneTransactions` materialized view.

The Result tab at the bottom of the Function Editor should indicate success
without any errors.

The `updateMonthlyPurchaseOrders` function refreshes the
`monthlyPhoneTransactions` materialized view with the January 2018 purchase
order data.

  4. Click Save Draft.

3

#### Confirm the update.

  1. Return to the `mongosh` and query the `monthlyPhoneTransactions` collection to confirm the update:
    
        db.monthlyPhoneTransactions.find().sort( { _id: -1} )  
      
  
VIEW OUTPUT

The `monthlyPhoneTransactions` materialized view shows the newly added data.
The top result reflects that the most recent transaction took place in January
2018.

## Create Scheduled Triggers

Schedule the App Services functions created in the previous step to run once a
day to keep the materialized view up-to-date.

1

### Click Triggers.

2

### Click Add a Trigger to open the Trigger configuration page.

3

### Enter configuration values for the Trigger.

UI Field Name

|

Configuration  
  
|  
  
Trigger Type

|

Select Scheduled.  
  
Name

|

Specify `updateMonthlySales`.  
  
Schedule Type

|

  1. Select Basic.

  2. For Repeat once by, select `Day of the Month` and set the value to your preferred date.

## Note

Alternatively, for testing purposes, set Repeat once by dropdown to a more
frequent occurrence, such as Minute or Hour

  
  
Select An Event Type

|

Select Function.  
  
Function

|

Select `updateMonthlySales`.  
  
4

### Click Save.

5

### Click Triggers.

6

### Click Add a Trigger to add another trigger.

7

### Enter configuration values for the new Trigger.

UI Field Name

|

Configuration  
  
|  
  
Trigger Type

|

Select Scheduled.  
  
Name

|

Specify `updateMonthlyPurchaseOrders`.  
  
Schedule Type

|

  1. Select Basic.

  2. For Repeat once by, select `Day of the Month` and set the value to your preferred date.

## Note

Alternatively, for testing purposes, set Repeat once by dropdown to a more
frequent occurrence, such as Minute or Hour

  
  
Select An Event Type

|

Select Function.  
  
Function

|

Select `updateMonthlyPurchaseOrders`.  
  
8

### Click Save.

9

### Review and deploy the `Sales-App` application draft.

## Create an Atlas Search Index on the Materialized View

Create an Atlas Search index on the `monthlyPhoneTransactions` collection.

1

### Navigate to the Atlas Cluster Overview page.

Click Database in the top-left corner of Atlas to navigate to the Database
Deployments page for your project.

2

### Click the cluster name to view cluster details.

3

### Click the Search tab.

4

### Click Create Search Index

5

### Select Visual Editor, then click Next.

6

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `monthlyPhoneTransactions`.

  2. In the Database and Collection section, find the `sample_supplies` database, and select the `monthlyPhoneTransactions` collection.

  3. Click Next.

7

### Review the default Atlas Search index configuration settings.

8

### Click Create Search Index.

9

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

10

### Check the status.

The newly created index appears on the Search tab. While the index is
building, the Status field reads Build in Progress. When the index is finished
building, the Status field reads Active.

## Note

Larger collections take longer to index. You will receive an email
notification when your index is finished building.

## Run a Query on the Materialized View

Run a query against the newly updated and indexed `monthlyPhoneTransactions`
collection.

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_supplies` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_supplies  
      
  
3

### Run a simple Atlas Search query on the
`sample_supplies.monthlyPhoneTransactions` collection.

The following query counts the number of months in monthlyPhoneTransactions
with total sales greater than or equal to `10000` dollars:

    
    
    db.monthlyPhoneTransactions.aggregate([  
      
      {  
          $search: {  
              "index": "monthlySalesIndex",  
              "range": {  
                  "gt": 10000,  
                  "path": ["sales_price"]  
              }  
          }  
      },  
      {  
        $count: 'months_w_over_10000'  
      },  
    ])  
  
The above query returns `4`, indicating that only 4 months out of all the
months in the `monthlyPhoneTransactions` materialized view had total sales
greater than or equal to 10000 dollars. This result reflects data from both
the `sample_supplies.sales` and `sample_supplies.purchaseOrders` collections.

For complete aggregation pipeline documentation, see the MongoDB Server
Manual.

← How to Run Atlas Search Queries Across CollectionsHow to Run `$lookup` with
an Atlas Search `$search` Query →

