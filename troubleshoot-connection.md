Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Troubleshoot Connection Issues

Select your language

Go

On this page

  * Database deployment Connect button is disabled
  * Connecting IP address not in IP Access List
  * Authentication to the database deployment failed
  * Too many open connections to your database deployment
  * Degraded performance in sharded clusters during spikes in connection counts
  * Attempting to connect from behind a firewall
  * Database Deployment Availability
  * MongoDB Compass Troubleshooting
  * Connection String Issues

This page outlines common connection issues and possible resolutions.

To learn more about connecting to an Atlas cluster, see the Get Started with
Atlas tutorial.

## Note

If you are an enterprise customer looking for support, file a ticket. For
community support, visit Community Support Resouces.

## Note

Serverless instances don't support connecting via certain drivers or driver
versions at this time. To learn more, see Serverless Instance Limitations.

## Database deployment Connect button is disabled

Your database deployment's Connect button may be disabled if your database
deployment is in the provisioning state. Your database deployment needs to
provision when it is first deployed. Clusters also must provision when you
scaled them up or down. The provisoning process can take up to 10 minutes,
after which the Connect button will become enabled.

## Connecting IP address not in IP Access List

Before connecting to your Atlas database deployment, check that you added your
host's IP address to the IP access list for your database deployment's
project. Atlas allows client connections only from IP addresses and CIDR
address ranges in the IP access list.

## Authentication to the database deployment failed

To connect to Atlas, you must authenticate with a MongoDB database user. To
create a database user for your database deployment, see Configure Database
Users.

### Possible solutions

If you have created a user and are having trouble authenticating, try the
following:

  * Check that you are using the correct username and password for your database user, and that you are connecting to the correct database deployment.

  * Check that you are specifying the correct `authSource` database in your connection string.

  * If you have a special character in your password, see Special characters in connection string password.

## Too many open connections to your database deployment

Atlas sets limits for concurrent incoming connections to a database
deployment. For clusters, this is based on the cluster tier. If you try to
connect when you are at this limit, MongoDB displays an error stating
`connection refused because too many open connections`.

For a detailed comparision of cluster tiers and their maximum concurrent
connections, see Connection Limits and Cluster Tier.

### Possible solutions

  * Close any open connections to your database deployment not currently in use.

  * Scale your cluster to a higher tier to support more concurrent connections.

  * Restart your application.

  * To prevent this issue in the future, consider using the `maxPoolSize` connection string option to limit the number of connections in the connection pool.

To learn how to fix this issue, see Fix Connection Issues.

## Degraded performance in sharded clusters during spikes in connection counts

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

## Attempting to connect from behind a firewall

### Connecting to the Atlas UI

Atlas uses a CDN to serve content quickly. If your organization uses a
firewall, add the following Atlas CDN host to the firewall's allow list to
prevent issues accessing the Atlas UI: `https://assets.mongodb-cdn.com/`.

### Connecting to a Database Deployment

Atlas database deployments operate on port `27017`. You must be able to reach
this port to connect to your database deployments. Additionally, ensure that
the appropriate ports are open for the following:

  * For sharded clusters, grant access to port 27016.

  * For BI Connector, grant access to port 27015.

You can check your ability to reach a port using the third-party Outgoing port
tester.

## Example

To check your ability to reach port 27017, visit http://portquiz.net:27017.

If you can't access these ports, check your system firewall settings and
ensure that they are not blocking access to these ports.

## Database Deployment Availability

If you are using a `mongodb+srv://` connection string and your driver or shell
can't find the DNS host of the Atlas database deployment, the database
deployment might be paused or deleted. Check that the database deployment
exists. If this is a paused cluster, you can resume the cluster if necessary.

## Note

Atlas automatically pauses idle `M0` clusters after 60 days with no
connections.

## MongoDB Compass Troubleshooting

If you use MongoDB Compass to connect to your cluster and experience issues,
see:

  * Connection Refused using SRV Connection String in this section.

  * Compass Connection Errors in the MongoDB Compass documentation.

If you use a self-managed X.509 certificate or an auto-generated X.509
certificate managed by Atlas to authenticate to the MongoDB database, when you
connect to MongoDB Compass, you must:

  1. In MongoDB Compass, choose Fill in connection fields individually.

  2. In the Authentication dropdown, select `X.509`.

  3. Select More Options.

  4. In the SSL dropdown, select Server and Client Validation.

  5. Add the same path to the downloaded Atlas-managed certificate, or the self-managed certificate (depending on which you use) to each of these fields: Certificate Authority, Client Certificate, and Client Private Key.

To learn more, see Connect to MongoDB in the MongoDB Compass documentation.

## Connection String Issues

### Incorrect Connection String Format

The connection string format you use to connect to Atlas depends on several
factors, including:

  * Your `mongosh` version. To learn more, see Connect via `mongosh`.

  * Your driver version. To learn more, see Connect via Your Application.

Verify your connection string in a test environment before putting it into
production.

### Special Characters in Connection String Password

If your password includes special characters, and you are using your password
in a connection string URI, encode the special characters.

## Note

The following characters must be converted using percent encoding if included
in a username or password:

    
    
    : / ? # [ ] @  
      
  
For example, if your password in plain-text is `p@ssw0rd'9'!`, you need to
encode your password as:

    
    
    p%40ssw0rd%279%27%21  
      
  
* * *

➤ Use the **Select your language** drop-down menu to set the language of the
encoding example in this section.

* * *

Go

Java (Sync)

Node.js

Python

    
    
    1| package main  
    |  
    2|   
      
    3| import (  
    4| 	"context"  
    5| 	"fmt"  
    6| 	"net/url"  
    7|   
      
    8| 	"go.mongodb.org/mongo-driver/bson"  
    9| 	"go.mongodb.org/mongo-driver/mongo"  
    10| 	"go.mongodb.org/mongo-driver/mongo/options"  
    11| )  
    12|   
      
    13| func main() {  
    14| 	username := "<username>"  
    15| 	password := "<password>"  
    16| 	cluster := "<clusterName>"  
    17| 	authSource  := "<authSource>"  
    18| 	authMechanism := "<authMechanism>"  
    19|   
      
    20| 	uri := "mongodb+srv://" + url.QueryEscape(username) + ":" +   
    21| 		url.QueryEscape(password) + "@" + cluster +   
    22| 		"/?authSource=" + authSource +  
    23| 		"&authMechanism=" + authMechanism  
    24|   
      
    25| 	client, err := mongo.Connect(context.TODO(), options.Client().ApplyURI(uri))  
    26| 	if err != nil {  
    27| 		panic(err)  
    28| 	}  
    29| 	defer client.Disconnect(context.TODO())  
    30|   
      
    31| 	collection := client.Database("<dbName>").Collection("<collName>")  
    32|   
      
    33| 	cursor, err := collection.Find(context.TODO(), bson.D{})  
    34| 	if err != nil {  
    35| 		panic(err)  
    36| 	}  
    37|   
      
    38| 	var results []bson.D  
    39| 	if err = cursor.All(context.TODO(), &results); err != nil {  
    40| 		panic(err)  
    41| 	}  
    42| 	for _, result := range results {  
    43| 		fmt.Println(result)  
    44| 	}  
    45| }  
  
Go

## Important

Do not encode special characters in your password if you are using your
password outside of a connection string URI (for example, pasting it into
`mongosh`).

### Connection String Incompatible with Driver Version

If you see this error message, your driver is likely out of date. For
instructions on updating your driver, refer to your specific Driver
Documentation.

### Internet Service Provider DNS Blocks Connection String

When you use the DNS seed list connection string format to connect to Atlas,
you might see the following error:

    
    
    DNSHostNotFound: Failed to look up service “<MongoDB service name>”  
      
  
This error may occur when using the default DNS server that your ISP provides.
That DNS server might not support SRV lookups that the DNS seed list
connection string format uses.

To resolve the issue, you can try changing your DNS configuration to use a
public DNS server.

## Example

You can configure your network settings to use Google Public DNS instead of
your ISP's DNS servers.

After you update your network settings to use a public DNS server, connect to
the database deployment.

### Connection String Error with DB Tools on Ubuntu 18.04

If running Ubuntu 18.04 and using the DNS seed list connection string format
(`mongodb+srv://`) to connect to Atlas from one of the MongoDB Database Tools
(`mongodump`, `mongorestore`, etc), you might see the following error:

    
    
    lookup nta8e.mongodb.net on 123.45.67.8:27017: cannot unmarshal DNS message  
      
  
If so, use one of the following connection options instead:

  * use the `--uri` option with a non-SRV connection string (`mongodb://`).

  * use the `--host` option to specify the host to connect.

### Connection Refused using SRV Connection String

When using the DNS seed list connection string format (`mongodb+srv://`) with
a driver or Compass, you may receive in the following error:

    
    
    Error: querySrv ECONNREFUSED _mongodb._tcp.<SRV Record>  
      
  
To remedy this issue, use the Standard Connection String format with Compass
or that driver. With Compass, don't set the **SRV Record** value, set the
**Hostname** and **Port** values instead.

← Manage Connections with AWS LambdaConfigure Security Features for Database
Deployments →

