Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Remove Unnecessary Indexes

Share Feedback

On this page

  * Overview
  * Example
  * Identify & Drop Unnecessary Indexes
  * Learn More

## Overview

Indexes support the efficient execution of queries in MongoDB. However, each
index you create has a negative performance impact on writes and requires some
disk space.

Creating unnecessary indexes leads to a bloated collection and slow writes.
Consider each query your application performs and whether it justifies an
index. Remove indexes that are unused, either because the field is not used to
query the database or because the index is redundant.

You should identify and drop unnecessary indexes. Use the Atlas UI to manage
indexes in Atlas.

## Example

Consider a game that awards `coins` to players. When a player reaches 20
`coins`, that player earns 1 `star` and their `coins` are reset to 0. The game
has a `players` collection with documents such as the following:

    
    
    // players collection  
      
    {  
      "_id": "ObjectId(123)",  
      "first_name": "John",  
      "last_name": "Doe",  
      "coins": 11,  
      "stars": 2  
    }  
  
The `players` collection has an index for every field:

  * `_id` is indexed by default.

  * `{ last_name: 1 }`

  * `{ last_name: 1, first_name: 1 }`

  * `{ coins: -1 }`

  * `{ stars: -1 }`

### `last_name` Index

In this example, when the game queries the database for player information, it
finds a single record using a player's full name. The compound index `{
last_name: 1, first_name: 1 }` covers this case, so the game should drop the
index `{ last_name: 1 }` because it is redundant.

### `coins` Index

In this example, the `coins` field is never used to search the database. The
game should drop the index `{ coins: -1 }` because it is unused.

### `stars` Index

In this example, at the end of a game, the players' names are displayed on a
leaderboard in descending order by number of stars. The game should maintain
the index `{ stars: -1 }`, even if it is used infrequently, to avoid scanning
every document in the `players` collection.

Now, the game uses the following indexes:

  * `_id` is indexed by default.

  * `{ last_name: 1, first_name: 1 }`

  * `{ stars: -1 }`

After dropping unnecessary indexes, the `players` collection has more free
space and can perform faster writes. The most frequent reads do not experience
a drop in performance because the indexes supporting those reads still exist
in the collection.

## Identify & Drop Unnecessary Indexes

To identify unnecessary indexes in Atlas, View Indexes with the Atlas UI.

Under the Indexes tab in Data Explorer, you can view Size, Usage, and other
information for each of your indexes. If an index is unused or covered by
another index, you should drop it.

To drop an index in Atlas, Drop an Index with the Atlas UI.

## Learn More

  * To learn more about indexes, see Indexes.

  * To learn more about indexing for your use case, see Indexing Strategies.

  * MongoDB also offers a free MongoDB University Course on improving database performance, including optimizing indexes: M201: MongoDB Performance.

← Avoid Unbounded ArraysReduce the Size of Large Documents →

