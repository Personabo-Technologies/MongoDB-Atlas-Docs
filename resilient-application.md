Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Build a Resilient Application with MongoDB Atlas

Select your language

Java (Sync)

On this page

  * Install the Latest Drivers
  * Connection Strings
  * Retryable Writes and Reads
  * Write and Read Concern
  * Error Handling
  * Test Failover
  * Resilient Example Application

You can configure features of your MongoDB deployments and the driver
libraries to create a resilient application that can withstand network outages
and failover events. To write application code that takes full advantage of
the always-on capabilities of MongoDB Atlas, you should perform the following
tasks:

  * Install the latest drivers.

  * Use the connection string provided by Atlas.

  * Use retryable writes and retryable reads.

  * Use a `majority` write concern and a read concern that makes sense for your application.

  * Handle errors in your application.

## Install the Latest Drivers

First, install the latest drivers for your language from MongoDB Drivers.
Drivers connect and relay queries from your application to your database.
Using the latest drivers enables the latest MongoDB features.

Then, in your application, import the dependency:

Java (Sync)

Node.js

Python

If you are using Maven, add the following to your `pom.xml` dependencies list:

    
    
    <dependencies>  
      
        <dependency>  
            <groupId>org.mongodb</groupId>  
            <artifactId>mongodb-driver-sync</artifactId>  
            <version>4.0.1</version>  
        </dependency>  
    </dependencies>  
  
Java (Sync)

If you are using Gradle, add the following to your `build.gradle` dependencies
list:

    
    
    dependencies {  
      
      compile 'org.mongodb:mongodb-driver-sync:4.0.1'  
    }  
  
## Connection Strings

## Note

Atlas provides a pre-configured connection string. For steps to copy the pre-
configured string, see Atlas-Provided Connection Strings.

Use a connection string that specifies all the nodes in your Atlas cluster to
connect your application to your database. If your cluster performs a replica
set election and a new primary is elected, a connection string that specifies
all the nodes in your cluster discovers the new primary without application
logic.

You can specify all the nodes in your cluster using either:

  * the Standard Connection String Format, or

  * the DNS Seedlist Connection Format (recommended with Atlas).

The connection string can also specify options, notably retryWrites and
writeConcern.

Atlas can generate an optimized SRV connection string for sharded clusters
using the load balancers from your private endpoint service. When you use an
optimized connection string, Atlas limits the number of connections per
`mongos` between your application and your sharded cluster. The limited
connections per `mongos` improve performance during spikes in connection
counts.

## Note

Atlas doesn't support optimized connection strings for clusters that run on
Google Cloud or Azure.

To learn more about optimized connection strings for sharded clusters behind a
private endpoint, see Improve Connection Performance for Sharded Clusters
Behind a Private Endpoint.

### Atlas-Provided Connection Strings

If you copy your connection string from your Atlas cluster interface, the
connection string is pre-configured for your cluster, uses the DNS Seedlist
format, and includes the recommended `retryWrites` and `w` (write concern)
options for resiliency.

To copy your connection string URI from Atlas:

  1. In MongoDB Atlas, under your project, select Database from the navigation panel.

  2. Click Connect on the cluster you wish to connect your application to.

  3. Select Connect Your Application as your connection method.

  4. Select your Driver and Version.

  5. Copy the connection string or full driver example into your application code. You must provide database user credentials.

## Note

This guide uses SCRAM authentication through a connection string. If you want
to learn about using X.509 certificates to authenticate, see X.509.

Use your connection string to instantiate a MongoDB client in your
application:

Java (Sync)

Node.js

Python

    
    
    // Copy the connection string provided by Atlas  
      
    String uri = <your Atlas connection string>;  
      
    // Instantiate the MongoDB client with the URI  
    MongoClient client = MongoClients.create(uri);  
  
Java (Sync)

## Retryable Writes and Reads

## Note

Starting in MongoDB version 4.0 and with 4.2-compatible drivers, MongoDB
retries both writes and reads once by default.

### Retryable Writes

Use retryable writes to retry certain write operations a single time if they
fail. If you copied your connection string from Atlas, it includes
`"retryWrites=true"`. If you are providing your own connection string, include
`"retryWrites=true"` as a query parameter.

Retrying writes exactly once is the best strategy for handling transient
network errors and replica set elections in which the application temporarily
cannot find a healthy primary node. If the retry succeeds, the operation as a
whole succeeds and no error is returned. If the operation fails, it is likely
due to:

  * A lasting network error

  * An invalid command

When an operation fails, your application needs to handle the error itself.

### Retryable Reads

Read operations are automatically retried a single time if they fail starting
in MongoDB version 4.0 and with 4.2-compatible drivers. No additional
configuration is required to retry reads.

## Write and Read Concern

You can tune the consistency and availability of your application using write
concerns and read concerns. Stricter concerns imply that database operations
wait for stronger data consistency guarantees, whereas loosening consistency
requirements provides higher availability.

## Example

If your application handles monetary balances, consistency is extremely
important. You might use `majority` write and read concerns to ensure you
never read from stale data or data that may be rolled back.

Alternatively, if your application records temperature data from hundreds of
sensors every second, you may not be concerned if you read data that does not
include the most recent readouts. You can loosen consistency requirements and
provide faster access to that data.

### Write Concern

You can set the write concern level of your Atlas replica set through the
connection string URI. Use a `majority` write concern to ensure your data is
successfully written to your database and persisted. This is the recommended
default and sufficient for most use cases. If you copied your connection
string from Atlas, it includes `"w=majority"`.

When you use a write concern that requires acknowledgement, such as
`majority`, you may also specify a maximum time limit for writes to achieve
that level of acknowledgement:

  * The wtimeoutMS connection string parameter for all writes, or

  * The wtimeout option for a single write operation.

Whether or not you use a time limit and the value you use depend on your
application context.

## Important

If you do not specify a time limit for writes and the level of write concern
is unachievable, the write operation will hang indefinitely.

### Read Concern

You can set the read concern level of your Atlas replica set through the
connection string URI. The ideal read concern depends on your application
requirements, but the default is sufficient for most use cases. No connection
string parameter is required to use default read concerns.

Specifying a read concern can improve guarantees around the data your
application receives from Atlas.

## Note

The specific combination of write and read concern your application uses has
an effect on order-of-operation guarantees. This is called causal consistency.
For more information on causal consistency guarantees, see Causal Consistency
and Read and Write Concerns.

## Error Handling

Invalid commands, network outages, and network errors that are not handled by
retryable writes return errors. Refer to your driver's API documentation for
error details.

For example, if an application tries to insert a document that contains an
`_id` value that is already used in the database's collection, your driver
returns an error that includes:

Java (Sync)

Node.js

Python

    
    
    Unable to insert due to an error: com.mongodb.MongoWriteException:  
      
    E11000 duplicate key error collection: <db>.<collection> ...  
  
Without proper error handling, an error may block your application from
processing requests until it is restarted.

Your application should handle errors without crashing or side effects. In the
previous example of an application inserting a duplicate `_id` into a
collection, that application could handle errors as follows:

Java (Sync)

Node.js

Python

    
    
    // Declare a logger instance from java.util.logging.Logger  
      
    private static final Logger LOGGER = ...  
    ...  
    try {  
        InsertOneResult result = collection.insertOne(new Document()  
            .append("_id", 1)  
            .append("body", "I'm a goofball trying to insert a duplicate _id"));  
      
        // Everything is OK  
        LOGGER.info("Inserted document id: " + result.getInsertedId());  
      
    // Refer to the API documentation for specific exceptions to catch  
    } catch (MongoException me) {  
        // Report the error  
        LOGGER.severe("Failed due to an error: " + me);  
    }  
  
Java (Sync)

The insert operation in this example throws a "duplicate key" error the second
time it's invoked because the `_id` field must be unique. The error is caught,
the client is notified, and the app continues to run. The insert operation
fails, however, and it is up to you to decide whether to show the user a
message, retry the operation, or do something else.

You should always log errors. Common strategies for further processing errors
include:

  * Return the error to the client with an error message. This is a good strategy when you cannot resolve the error and need to inform a user that an action cannot be completed.

  * Write to a backup database. This is a good strategy when you cannot resolve the error but don't want to risk losing the request data.

  * Retry the operation beyond the single default retry. This is a good strategy when you can solve the cause of an error programmatically, then retry it.

You must select the best strategies for your application context.

## Example

In the example of a duplicate key error, you should log the error but not
retry the operation because it will never succeed. Instead, you could write to
a fallback database and review the contents of that database at a later time
to ensure that no information is lost. The user doesn't need to do anything
else and the data is recorded, so you can choose not to send an error message
to the client.

### Planning for Network Errors

Returning an error can be desirable behavior when an operation would otherwise
hang indefinitely and block your application from executing new operations.
You can use the maxTimeMS method to place a time limit on individual
operations, returning an error for your application to handle if that time
limit is exceeded.

The time limit you place on each operation depends on the context of that
operation.

## Example

If your application reads and displays simple product information from an
`inventory` collection, you can be reasonably confident that those read
operations only take a moment. An unusually long-running query is a good
indicator that there is a lasting network problem. Setting `maxTimeMS` on that
operation to 5000, or 5 seconds, means that your application receives feedback
as soon as you are confident there is a network problem.

## Test Failover

In the spirit of chaos testing, Atlas will perform replica set elections
automatically for periodic maintenance and certain configuration changes.

To check if your application is resilient to replica set elections, test the
failover process by simulating a failover event.

## Resilient Example Application

The example application brings together the following recommendations to
ensure resiliency against network outages and failover events:

  * Use the Atlas-provided connection string with retryable writes, majority write concern, and default read concern.

  * Specify an operation time limit with the maxTimeMS method. For instructions on how to set `maxTimeMS`, refer to your specific Driver Documentation.

  * Handle errors for duplicate keys and timeouts.

The application is an HTTP API that allows clients to create or list user
records. It exposes an endpoint that accepts GET and POST requests
http://localhost:3000:

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

`/users`

|

Gets a list of user names from a `users` collection.  
  
`POST`

|

`/users`

|

Requires a `name` in the request body. Adds a new user to a `users`
collection.  
  
Java (Sync)

Node.js

Python

## Note

The following server application uses NanoHTTPD and json which you need to add
to your project as dependencies before you can run it.

    
    
    1| // File: App.java  
    |  
    2|   
      
    3| import java.util.Map;  
    4| import java.util.logging.Logger;  
    5|   
      
    6| import org.bson.Document;  
    7| import org.json.JSONArray;  
    8|   
      
    9| import com.mongodb.MongoException;  
    10| import com.mongodb.client.MongoClient;  
    11| import com.mongodb.client.MongoClients;  
    12| import com.mongodb.client.MongoCollection;  
    13| import com.mongodb.client.MongoDatabase;  
    14|   
      
    15| import fi.iki.elonen.NanoHTTPD;  
    16|   
      
    17| public class App extends NanoHTTPD {  
    18|     private static final Logger LOGGER = Logger.getLogger(App.class.getName());  
    19|   
      
    20|     static int port = 3000;  
    21|     static MongoClient client = null;  
    22|   
      
    23|     public App() throws Exception {  
    24|         super(port);  
    25|   
      
    26|         // Replace the uri string with your MongoDB deployment's connection string  
    27|         String uri = "<atlas-connection-string>";  
    28|         client = MongoClients.create(uri);  
    29|   
      
    30|         start(NanoHTTPD.SOCKET_READ_TIMEOUT, false);  
    31|         LOGGER.info("\nStarted the server: http://localhost:" + port + "/ \n");  
    32|     }  
    33|   
      
    34|     public static void main(String[] args) {  
    35|         try {  
    36|             new App();  
    37|         } catch (Exception e) {  
    38|             LOGGER.severe("Couldn't start server:\n" + e);  
    39|         }  
    40|     }  
    41|   
      
    42|     @Override  
    43|     public Response serve(IHTTPSession session) {  
    44|         StringBuilder msg = new StringBuilder();  
    45|         Map<String, String> params = session.getParms();  
    46|   
      
    47|         Method reqMethod = session.getMethod();  
    48|         String uri = session.getUri();  
    49|   
      
    50|         if (Method.GET == reqMethod) {  
    51|             if (uri.equals("/")) {  
    52|                 msg.append("Welcome to my API!");  
    53|             } else if (uri.equals("/users")) {  
    54|                 msg.append(listUsers(client));  
    55|             } else {  
    56|                 msg.append("Unrecognized URI: ").append(uri);  
    57|             }  
    58|         } else if (Method.POST == reqMethod) {  
    59|             try {  
    60|                 String name = params.get("name");  
    61|                 if (name == null) {  
    62|                     throw new Exception("Unable to process POST request: 'name' parameter required");  
    63|                 } else {  
    64|                     insertUser(client, name);  
    65|                     msg.append("User successfully added!");  
    66|                 }  
    67|             } catch (Exception e) {  
    68|                 msg.append(e);  
    69|             }  
    70|         }  
    71|   
      
    72|         return newFixedLengthResponse(msg.toString());  
    73|     }  
    74|   
      
    75|     static String listUsers(MongoClient client) {  
    76|         MongoDatabase database = client.getDatabase("test");  
    77|         MongoCollection<Document> collection = database.getCollection("users");  
    78|   
      
    79|         final JSONArray jsonResults = new JSONArray();  
    80|         collection.find().forEach((result) -> jsonResults.put(result.toJson()));  
    81|   
      
    82|         return jsonResults.toString();  
    83|     }  
    84|   
      
    85|     static String insertUser(MongoClient client, String name) throws MongoException {  
    86|         MongoDatabase database = client.getDatabase("test");  
    87|         MongoCollection<Document> collection = database.getCollection("users");  
    88|   
      
    89|         collection.insertOne(new Document().append("name", name));  
    90|         return "Successfully inserted user: " + name;  
    91|     }  
    92| }  
  
Java (Sync)

← Atlas Cluster Sizing and Tier SelectionRecover a Point In Time with
Continuous Cloud Backup →

