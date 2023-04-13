Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Reduce the Size of Large Documents

Share Feedback

On this page

  * Overview
  * Example
  * Learn More

## Overview

Storing large documents in your database can lead to excessive RAM and
bandwidth usage. MongoDB keeps frequently accessed data, referred to as the
working set, in RAM. When the working set grows beyond the RAM allotment,
performance is degraded as data must be retrieved from disk instead.

If your most frequent queries are for documents that contain much more
information than you need for that query, consider restructuring your schema
with smaller documents using references to additional collections. By breaking
up your data into more collections and using smaller documents for frequently
accessed data, you reduce the overall size of the working set and improve
performance.

## Note

Your hardware configuration can affect the size of documents that your system
can support. The BSON Document Size limit is 16 megabytes.

## Example

Consider a movie catalog website that displays a list of the 50 most recently
released movie titles and their poster images on the home page. From the home
page, a user can click on a movie to see additional details.

The website stores information about movies in a `movies` collection. Each
movie document contains all of the information available for that movie:

    
    
    // movies collection  
      
      
    {  
        "_id": 123,  
        "title": "2001: A Space Odyssey",  
        "poster": <url>,  
        "director": "Stanley Kubrick",  
        "release_year": 1968,  
        "box_office_usd": 146000000,  
        "countries_released": [  
            "United States",  
            ...  
        ],  
        "cast": [  
            "Keir Dullea",  
            ...  
        ],  
        "crew": [  
             "Ray Lovejoy",  
             ...  
        ],  
        ...  
      
    }  
  
## Note

Whenever possible, you should host images outside of your MongoDB deployment
and reference them with URLs. If you store images in your database, you are
much more likely to reach the document size limit.

In this example, the most frequent query the website performs is to find the
50 most recent movies' `title` and `poster`. Instead of querying for all movie
information, consider breaking up the `movie` collection into two separate
collections, `movies` and `movie_metadata`. The collections are linked with
the `_id` of `movie` documents:

    
    
    // movies collection  
      
      
    {  
        "_id": 123,  
        "title": "2001: A Space Odyssey",  
        "poster": <url>  
    }  
      
    
    // movie_metadata collection  
      
      
    {  
        "_id": <object_id>,  
        "movie_id": 123, // reference to a movies document  
        "director": "Stanley Kubrick",  
        "release_year": 1968,  
        "box_office_usd": 146000000,  
        "countries_released": [  
            "United States",  
            ...  
        ],  
        "cast": [  
            "Keir Dullea",  
            ...  
        ],  
        "crew": [  
             "Ray Lovejoy",  
             ...  
        ],  
        ...  
      
    }  
  
This way, when the website queries for the 50 most recent movies and their
posters, it only loads information that it needs. If a user clicks on a movie,
the site performs another query to find the `movie_metadata` document
associated with that movie. This new schema is more performant than the
original because the most frequent query returns much smaller documents.

Consider your use case, especially the operations you most frequently perform,
and design a schema that efficiently uses your working set.

## Learn More

  * To learn more about Data Modeling in MongoDB and the flexible schema model, see Data Modeling Introduction.

  * To learn more about using references to model your schema, see Model One-to-Many Relationships with Document References.

  * MongoDB also offers a free MongoDB University Course on Data Modeling: M320: Data Modeling.

### Design Patterns

To read about strategies for keeping documents in your working set at a
manageable size, see the following patterns:

  * Use The Extended Reference Pattern to duplicate a frequently-read portion of data from large documents to smaller ones.

  * Use The Subset Pattern to reduce the size of documents with large array fields.

  * Use The Outlier Pattern to handle a few large documents in an otherwise standard collection.

### MongoDB.live 2020 Presentations

To learn how to incorporate the flexible data model into your schema, see the
following presentations from **MongoDB.live 2020** :

  * Learn about entity relationships in MongoDB and examples of their implementations with Data Modeling with MongoDB.

  * Learn advanced data modeling design patterns you can incorporate into your schema with Advanced Schema Design Patterns.

← Remove Unnecessary IndexesReduce Number of Collections →

