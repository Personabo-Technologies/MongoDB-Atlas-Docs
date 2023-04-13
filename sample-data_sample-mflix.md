Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sample Mflix Dataset

Share Feedback

On this page

  * Collections
  * `sample_mflix.comments`
  * `sample_mflix.movies`
  * `sample_mflix.sessions`
  * `sample_mflix.theaters`
  * `sample_mflix.users`

The `sample_mflix` database contains data on movies and movie theaters. The
database also contains collections for certain metadata, including users and
comments on specific movies.

To learn how to load the sample data provided by Atlas into your cluster, see
Load Sample Data.

## Collections

The `sample_mflix` database contains the following collections:

Collection Name

|

Description  
  
|  
  
comments

|

Contains comments associated with specific movies.  
  
movies

|

Contains movie information, including release year, director, and reviews.  
  
sessions

|

Metadata field. Contains users' JSON Web Tokens.  
  
theaters

|

Contains locations of movie theaters.  
  
users

|

Contains user information.  
  
### `sample_mflix.comments`

This collection contains comments associated with specific movies. Each
document contains the comment text, the user who submitted it, and the movie
the comment applies to.

#### Indexes

This collection contains the following indexes:

Name

|

Index

|

Description  
  
||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.  
  
#### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "5a9427648b0beebeb69579cc"  
      },  
      "name": "Andrea Le",  
      "email": "andrea_le@fakegmail.com",  
      "movie_id": {  
        "$oid": "573a1390f29313caabcd418c"  
      },  
      "text": "Rem officiis eaque repellendus amet eos doloribus. Porro  
        dolor voluptatum voluptates neque culpa molestias. Voluptate unde  
        nulla temporibus ullam.",  
      "date": {  
        "$date": {  
          "$numberLong": "1332804016000"  
        }  
      }  
    }  
  
### `sample_mflix.movies`

This collection contains details on movies. Each document contains a single
movie, and information such as its title, release year, and cast.

#### Indexes

This collection contains the following indexes:

Name

|

Index

|

Description

|

Properties  
  
|||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.

|  
  
`cast_text_fullplot_text_genres_text_title_text`

|

`{ "_fts": "text", "_ftsx": 1 }`

|

Text index on the `cast`, `fullplot`, `genres`, and `title` fields.

|

Sparse  
  
#### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "573a1390f29313caabcd413b"  
      },  
      "title": "The Arrival of a Train",  
      "year": {  
        "$numberInt": "1896"  
      },  
      "runtime": {  
        "$numberInt": "1"  
      },  
      "released": {  
        "$date": {  
          "$numberLong": "-2335219200000"  
        }  
      },  
      "poster": "http://ia.media-imdb.com/images/M/MV5BMjEyNDk5MDYzOV5BMl5BanBnXkFtZTgwNjIxMTEwMzE@._V1_SX300.jpg",  
      "plot": "A group of people are standing in a straight line along the  
        platform of a railway station, waiting for a train, which is seen  
        coming at some distance. When the train stops at the platform, ...",  
      "fullplot": "A group of people are standing in a straight line along  
        the platform of a railway station, waiting for a train, which is  
        seen coming at some distance. When the train stops at the platform,  
        the line dissolves. The doors of the railway-cars open, and people  
        on the platform help passengers to get off.",  
      "lastupdated": "2015-08-15 00:02:53.443000000",  
      "type": "movie",  
      "directors": [  
        "Auguste Lumière",  
        "Louis Lumière"  
      ],  
      "imdb": {  
        "rating": {  
          "$numberDouble": "7.3"  
        },  
        "votes": {  
          "$numberInt": "5043"  
        },  
        "id": {  
          "$numberInt": "12"  
        }  
      },  
      "cast": [  
        "Madeleine Koehler"  
      ],  
      "countries": [  
        "France"  
      ],  
      "genres": [  
        "Documentary",  
        "Short"  
      ],  
      "tomatoes": {  
        "viewer": {  
          "rating": {  
            "$numberDouble": "3.7"  
          },  
          "numReviews": {  
            "$numberInt": "59"  
          }  
        },  
        "lastUpdated": {  
          "$date": {  
            "$numberLong": "1441993589000"  
          }  
        }  
      },  
      "num_mflix_comments": {  
        "$numberInt": "1"  
      }  
    }  
  
### `sample_mflix.sessions`

This collection contains metadata about users. Each document contains a user
and their corresponding JSON Web Token

#### Indexes

This collection contains the following indexes:

Name

|

Index

|

Description

|

Properties  
  
|||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.

|  
  
`user_id_1`

|

`{ "user_id" : 1}`

|

Ascending index on the `user_id` field.

|

Unique  
  
#### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "5a98348755593fdf68350932"  
      },  
      "user_id": "bfb9vc1zz@xhasq.5h9",  
      "jwt": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."  
    }  
  
### `sample_mflix.theaters`

This collection contains movie theater locations. Each document contains a
single movie theater and its location in both string and GeoJSON forms.

#### Indexes

Name

|

Index

|

Description

|

Properties  
  
|||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.

|  
  
`geo index`

|

`{ "location.geo": "2dsphere" }`

|

Geospatial index on the `location.geo` field.

|

Sparse  
  
#### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "59a47286cfa9a3a73e51e72c"  
      },  
      "theaterId": {  
        "$numberInt": "1000"  
      },  
      "location": {  
        "address": {  
          "street1": "340 W Market",  
          "city": "Bloomington",  
          "state": "MN",  
          "zipcode": "55425"  
        },  
        "geo": {  
          "type": "Point",  
          "coordinates": [  
            {  
              "$numberDouble": "-93.24565"  
            },  
            {  
              "$numberDouble": "44.85466"  
            }  
          ]  
        }  
      }  
    }  
  
### `sample_mflix.users`

This collection contains information on `mflix` users. Each document contains
a single user, and their name, email, and password.

#### Indexes

Name

|

Index

|

Description

|

Properties  
  
|||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.

|  
  
`email_1`

|

`{ "email: 1 }`

|

Unique, ascending index on the `email` field.

|

Unique  
  
#### Sample Document

    
    
    {  
      
      "_id": {  
        "$oid": "59b99db4cfa9a34dcd7885b6"  
      },  
      "name": "Ned Stark",  
      "email": "sean_bean@gameofthron.es",  
      "password": "$2b$12$UREFwsRUoyF0CRqGNK0LzO0HM/jLhgUCNNIJ9RJAqMUQ74crlJ1Vu"  
    }  
  
← Sample Guides DatasetSample Restaurants Dataset →

