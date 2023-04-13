Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Insert and View a Document

Share Feedback

On this page

  * Insert and View Data
  * Next Steps

## Insert and View Data

 _Estimated completion time: 5 minutes_

The steps in this tutorial show you how to insert data into your cluster using
one of the supported MongoDB Drivers. MongoDB drivers allow you to interact
with your databases programmatically using a supported programming language.

Select the appropriate tab based on the programming language you use:

PyMongo Driver

Node.js Driver

MongoDB Shell

Atlas Console

### Insert Data into your Atlas Cluster with the PyMongo Driver

 _Estimated completion time: 5 minutes_

In the previous section you used the PyMongo driver to connect to your Atlas
cluster. In this section, you'll create a new collection, add data to it, and
read the new data.

1

#### Create a new database on your cluster.

We have already established our client connection and stored it in a variable
called `client`. Run the following command in your Python shell to create a
database on your cluster:

    
    
    db = client.gettingStarted  
      
  
This command creates a new database on your cluster called `gettingStarted`.
The variable `db` points to your new database.

2

#### Create a collection for your database.

Run the following command in your Python shell to create a new collection for
your database:

    
    
    people = db.people  
      
  
This command creates a new collection in your `gettingStarted` database called
`people`. The variable `people` points to your new collection.

3

#### Create a new document to insert into your collection.

In your Python shell, run the following command to create a document which
will be inserted into your collection:

    
    
    import datetime  
      
    personDocument = {  
      "name": { "first": "Alan", "last": "Turing" },  
      "birth": datetime.datetime(1912, 6, 23),  
      "death": datetime.datetime(1954, 6, 7),  
      "contribs": [ "Turing machine", "Turing test", "Turingery" ],  
      "views": 1250000  
    }  
  
The document is stored in a variable called `personDocument`.

## Note

This command does not insert the document into your collection. This command
only specifies the document. We will insert the document in the next step.

4

#### Insert the document into your collection.

In your Python shell, run the following command to insert the document you
created in the previous step into your collection:

    
    
    people.insert_one(personDocument)  
      
  
Remember that the `people` variable refers to our `people` collection we
specified in a previous step of this section, and `personDocument` contains
the document we want to insert.

If your insert was successful, PyMongo displays a message similar to the
following:

    
    
    <pymongo.results.InsertOneResult object at 0x10950e5f0>  
      
  
### View Your Cluster Data

Now that you have successfully inserted a document into your Atlas cluster
using the PyMongo driver, you can try reading that data with the PyMongo
`find_one()` method.

The following command returns one document from the `people` collection that
has a `name.last` value of `Turing`:

    
    
    people.find_one({ "name.last": "Turing" })  
      
  
This command returns the following output. This example has been broken into
multiple lines for readability.

    
    
    {  
      
      '_id': ObjectId('5ecd43aa2600f51da704b35f'),  
       'name': {  
          'first': 'Alan',  
          'last': 'Turing'  
      },  
      'birth': datetime.datetime(1912, 6, 23, 0, 0),  
      'death': datetime.datetime(1954, 6, 7, 0, 0),  
      'contribs': [  
          'Turing machine',  
          'Turing test',  
          'Turingery'  
      ],  
      'views': 1250000  
    }  
  
## Note

You may see a different value for ObjectId, because it is a system-generated
value.

## Tip

### See also:

To learn more about querying data with PyMongo, see the PyMongo documentation.

### Summary

Congratulations! You've used the PyMongo driver to interact with data in your
Atlas cluster.

## Next Steps

If you continue to grow your cluster, consider scaling your cluster to support
more users and operations.

