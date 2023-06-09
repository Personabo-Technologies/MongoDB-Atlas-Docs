Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Step 2: Run Atlas Search Queries

Select your language

MongoDB Shell

On this page

  * Procedure
  * Next Steps

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
examples on this page.

* * *

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

This part of the tutorial guides you through running Atlas Search queries.

## Procedure

MongoDB Shell

Compass

C#

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

### Run a simple Atlas Search query on the `movies` collection.

The following query searches for the word `baseball` in the `plot` field. It
includes a $limit stage to limit the output to 5 results and a $project stage
to exclude all fields except `title` and `plot`.

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "text": {  
            "query": "baseball",  
            "path": "plot"  
          }  
        }  
      },  
      {  
        $limit: 5  
      },  
      {  
        $project: {  
          "_id": 0,  
          "title": 1,  
          "plot": 1  
        }  
      }  
    ])  
  
MongoDB Shell

The above query returns the following results:

    
    
     {  
      
       "plot" : "A trio of guys try and make up for missed  
       opportunities in childhood by forming a three-player  
       baseball team to compete against standard children  
       baseball squads.",  
       "title" : "The Benchwarmers"  
     }  
     {  
       "plot" : "A young boy is bequeathed the ownership of a  
       professional baseball team.",  
       "title" : "Little Big League"  
     }  
     {  
       "plot" : "A trained chimpanzee plays third base for a  
       minor-league baseball team.",  
       "title" : "Ed"  
     }  
     {  
       "plot" : "The story of the life and career of the famed  
       baseball player, Lou Gehrig.",  
       "title" : "The Pride of the Yankees"  
     }  
     {  
       "plot" : "Babe Ruth becomes a baseball legend but is  
       unheroic to those who know him.",  
       "title" : "The Babe"  
     }  
  
MongoDB Shell

For more information about the $search pipeline stage, see its reference page.
For complete aggregation pipeline documentation, see the MongoDB Server
Manual.

4

### Run a complex Atlas Search query on the `movies` collection.

`$search` has several operators for constructing different types of queries.
The following query uses the compound operator to combine several operators
into a single query. It has the following search criteria:

  * The `plot` field must contain either `Hawaii` or `Alaska`.

  * The `plot` field must contain a four-digit number, such as a year.

  * The `genres` field must not contain either `Comedy` or `Romance`.

  * The `title` field must not contain `Beach` or `Snow`.

    
    
    db.movies.aggregate([  
      
      {  
        $search: {  
          "compound": {  
            "must": [ {  
              "text": {  
                "query": ["Hawaii", "Alaska"],  
                "path": "plot"  
              },  
            },  
            {  
              "regex": {  
                "query": "([0-9]{4})",  
                "path": "plot",  
                "allowAnalyzedField": true  
              }  
            } ],  
            "mustNot": [ {  
              "text": {  
                "query": ["Comedy", "Romance"],  
                "path": "genres"  
              }  
            },  
            {  
              "text": {  
                "query": ["Beach", "Snow"],  
                "path": "title"  
              }  
            } ]  
          }  
        }  
      },  
      {  
        $project: {  
          "title": 1,  
          "plot": 1,  
          "genres": 1,  
          "_id": 0  
        }  
      }  
    ])  
  
MongoDB Shell

The above query returns the following results:

    
    
     {  
      
       "plot" : "A modern aircraft carrier is thrown back in time  
       to 1941 near Hawaii, just hours before the Japanese attack  
       on Pearl Harbor.",  
       "genres" : [ "Action", "Sci-Fi" ],  
       "title" : "The Final Countdown"  
     }  
     {  
       "plot" : "Follows John McCain's 2008 presidential  
       campaign, from his selection of Alaska Governor Sarah  
       Palin as his running mate to their ultimate defeat in the  
       general election.",  
       "genres" : [ "Biography", "Drama", "History" ],  
       "title" : "Game Change"  
     }  
     {  
       "plot" : "A devastating and heartrending take on grizzly  
       bear activists Timothy Treadwell and Amie Huguenard, who  
       were killed in October of 2003 while living among  
       grizzlies in Alaska.",  
       "genres" : [ "Documentary", "Biography" ],  
       "title" : "Grizzly Man"  
     }  
     {  
       "plot" : "Truman Korovin is a lonely, sharp-witted cab  
       driver in Fairbanks, Alaska, 1980. The usual routine of  
       picking up fares and spending his nights at his favorite  
       bar, the Boatel, is disrupted ...",  
       "genres" : [ "Drama" ],  
       "title" : "Chronic Town"  
     }  
  
MongoDB Shell

## Next Steps

Now that you ran some queries, review the Atlas Search documentation to learn
more about the different operators and other queries you can run. More query
examples are available througout the Atlas Search documentation.

 **Prefer to learn by watching?**

Follow along with this video tutorial walk-through that demonstrates how to
build Atlas Search queries for a Restaurant Finder demo application, which is
also available at www.atlassearchrestaurants.com.

 _Duration: 20 Minutes_

← Step 1: Create an Atlas Search IndexAtlas Search Tutorials →

