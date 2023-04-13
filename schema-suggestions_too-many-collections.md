Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Reduce Number of Collections

Share Feedback

On this page

  * Overview
  * Example
  * How to Check for Unnecessary Collections
  * Learn More

## Overview

Collections are groupings of MongoDB documents, similar to an RDBMS table. A
collection exists within a single database.

Even if a collection does not contain any documents, it still comes with a
resource cost in the form of an undroppable default _id index. Although this
index does not take up much space on its own (especially for small
collections) if you have thousands of collections these indexes can add up in
resources and strain your database allocation.

If your deployment contains unnecessary or an increasing number of
collections, you should consider restructuring your data to reduce the number
of collections and ultimately reduce the resource requirements of your
application.

## Example

Consider a `temperatures` database that stores collections of temperature
readings obtained from a sensor. The sensor takes readings every half hour
from 10 AM to 10 PM. Each day's readings are stored in a separate collection,
named by the reading date:

    
    
    // temperatures.march-09-2020  
      
      
    {  
      "_id": 1,  
      "timestamp": "2020-03-09T010:00:00Z",  
      "temperature": 29  
    }  
    {  
      "_id": 2,  
      "timestamp": "2020-03-09T010:30:00Z",  
      "temperature": 30  
    }  
    ...  
    {  
      "_id": 25,  
      "timestamp": "2020-03-09T022:00:00Z",  
      "temperature": 26  
    }  
      
    
    // temperatures.march-10-2020  
      
      
    {  
      "_id": 1,  
      "timestamp": "2020-03-10T010:00:00Z",  
      "temperature": 30  
    }  
    {  
      "_id": 2,  
      "timestamp": "2020-03-10T010:30:00Z",  
      "temperature": 32  
    }  
    ...  
    {  
      "_id": 25,  
      "timestamp": "2020-03-10T022:00:00Z",  
      "temperature": 28  
    }  
  
With each passing day, the number of collections in the database increments.
Since the number of collections is unbounded, there is an ever-growing need
from the database to maintain these collections and their corresponding
indexes. If the database eventually reaches a point where it is managing
thousands of collections and indexes, it may result in performance
degradation.

Additionally, this approach does not easily facilitate queries across multiple
days. To query data from multiple days to obtain temperature trends over
longer periods of time, you would need to perform a `$lookup` operation, which
is not as performant as querying data in the same collection.

### Updated Schema

Instead, a better approach to structure this data is to store all temperature
readings in a single collection, and have each day's readings in a single
document. Consider this updated schema, where all temperatures are in a single
collection: `temperatures.readings`:

    
    
    // temperatures.readings  
      
      
    {  
      "_id": ISODate("2020-03-09"),  
      "readings": [  
        {  
          "timestamp": "2020-03-09T010:00:00Z",  
          "temperature": 29  
        },  
        {  
          "timestamp": "2020-03-09T010:30:00Z",  
          "temperature": 30  
        },  
        ...  
        {  
          "timestamp": "2020-03-09T022:00:00Z",  
          "temperature": 26  
        }  
      ]  
    }  
    {  
      "_id": ISODate("2020-03-10"),  
      "readings": [  
        {  
          "timestamp": "2020-03-10T010:00:00Z",  
          "temperature": 30  
        },  
        {  
          "timestamp": "2020-03-10T010:30:00Z",  
          "temperature": 32  
        },  
        ...  
        {  
          "timestamp": "2020-03-10T022:00:00Z",  
          "temperature": 28  
        }  
      ]  
    }  
  
This updated schema requires much fewer resources than the original schema.
Now, rather than requiring an index for every single day that temperatures are
read, the default `_id` index on this collection helps facilitate queries by
date.

## Tip

### See also:

Use Buckets for Time-Series Data

## How to Check for Unnecessary Collections

### MongoDB Shell

To check the number of collections in your database, you can run the following
command from `mongosh`:

    
    
    db.getCollectionNames().length  
      
  
The db.stats() method also returns the number of collections in your database,
along with useful database statistics such as the total size of your data and
indexes.

### MongoDB Atlas

#### Atlas UI

If the Data Explorer is enabled, the Atlas UI provides a high-level overview
of collections in your databases. The Atlas UI shows the total size of a
collection, including the size of a collection's indexes. If the majority of a
collection's size is comprised of indexes, you can consider consolidating that
collection's data into another collection and dropping the original
collection. Refer to the `$merge` documentation for an approach to merging
data from one collection into another.

Additionally, if the Atlas UI reveals that you have empty collections, you can
drop those collections directly from the Atlas UI.

#### Real-Time Performance Panel

The Atlas Real-Time Performance Panel shows which collections receive the most
activity. You can use this tool to ensure that before you drop a collection,
it is not being actively used by your application.

## Learn More

  * To learn more about Data Modeling in MongoDB and the flexible schema model, see Data Modeling Introduction.

  * To learn more about databases and collections, see Databases and Collections.

  * To learn more about embedding related data in a single document, see Embedded Data Models

### MongoDB.live 2020 Presentations

To learn how to incorporate the flexible data model into your schema, see the
following presentations from **MongoDB.live 2020** :

  * Learn about entity relationships in MongoDB and examples of their implementations with Data Modeling with MongoDB.

  * Learn advanced data modeling design patterns you can incorporate into your schema with Advanced Schema Design Patterns.

← Reduce the Size of Large DocumentsUse Atlas Search for Full-Text Search
Queries →

