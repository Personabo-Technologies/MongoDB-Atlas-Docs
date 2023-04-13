Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Connect to a Database Deployment

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Connect to Your Database Deployment
  * Troubleshooting

## Considerations

Atlas does not guarantee that host names remain consistent with respect to
node types during topology changes.

## Example

If you have a cluster named `foo123` containing an analytics node
`foo123-shard-00-03-a1b2c.mongodb.net:27017`, Atlas does not guarantee that
specific host name will continue to refer to an analytics node after a
topology change, such as scaling a cluster to modify its number of nodes or
regions.

### Improve Connection Performance for Sharded Clusters Behind a Private
Endpoint

Atlas can generate an optimized SRV connection string for sharded clusters
using the load balancers from your private endpoint service. When you use an
optimized connection string, Atlas limits the number of connections per
`mongos` between your application and your sharded cluster. The limited
connections per `mongos` improve performance during spikes in connection
counts.

## Note

Atlas doesn't support optimized connection strings for clusters that run on
Google Cloud or Azure.

To use an optimized connection string, you must meet all of the following
criteria:

  * Configure a sharded cluster.

  * Ensure that the sharded cluster runs on AWS.

  * Ensure that the sharded cluster runs MongoDB version 5.0 or later. If your cluster currently runs an earlier version of MongoDB, upgrade your cluster's MongoDB version to version 5.0 or later to use an optimized SRV connection string.

  * Set up a private endpoint for your cluster.

  * Use either:

    * A single-region cluster or

    * A multi-region cluster with regionalized private endpoints enabled. Only the AWS regions in a multi-region cluster support an optimized SRV connection string.

Atlas doesn't support optimized connections to multi-region clusters using a
single SRV record.

  * Connect using one of the following methods:

    * Connect using a driver that meets or exceeds the minimum driver version for optimized connections.

    * Connect using Compass.

    * Connect using mongosh.

## Note

If your cluster meets the criteria for optimized SRV strings, Atlas generates
an Optimized SRV Connection string for you. If your cluster ever had legacy
connection strings, Atlas maintains those strings indefinitely and includes a
Legacy SRV Connection string when you select the Private Endpoint connection
type. Consider switching to the Optimized SRV Connection for optimal
performance and update your connection string wherever you use it.

If you create the cluster and enable private endpoints after Atlas released
this feature, Atlas displays the optimized connection string by default when
you select the Private Endpoint connection type. You can identify an optimized
connection string by the addition of `lb` to the connection string as shown in
the following example:

`mongodb+SRV://User1:P@ssword@cluster0-pl-0-lb.oq123.mongodb-dev.net/`

To disable optimized connection strings for clusters that don't have the
Legacy SRV Connection option, contact support.

#### Use Optimized Connection Strings with a Driver

To learn how to connect using a driver and an optimized connection string,
select the Private Endpoint Connection tab in the Connect Your Application
procedure.

#### Use Optimized Connection Strings with Compass

To learn how to connect using Compass and an optimized connection string,
select the Private Endpoint Connection tab in the Connect to your Database
Deployment procedure.

#### Use Optimized Connection Strings with `mongosh`

To learn how to connect using `mongosh` and an optimized connection string,
select the Private Endpoint Connection tab in the Connect to your Database
Deployment procedure.

## Prerequisites

### IP Access List

To access a database deployment, you must connect from an IP address on the
Atlas project's IP access list. If you need to add an IP address to the IP
access list, you can do so in the Connect dialog. You can also add the IP
address from the Network Access tab.

### Database User

To access a database deployment, you must create a database user with access
to the desired database(s) on your Atlas database deployment. Database users
are separate from Atlas users. Database users have access to MongoDB
databases, while Atlas users have access to the Atlas application itself.

You can create a database user to access your Atlas database deployment in the
Connect dialog. You can also add the database user from the Database
Deployment view.

### Open Ports 27015 to 27017 to Access Atlas Databases

Make sure your application can reach your MongoDB Atlas environment. To add
the inbound network access from your application environment to Atlas, do one
of the following:

  1. Add the public IP addresses to your IP access list

  2. Use VPC / VNet peering to add private IP addresses.

  3. Add private endpoints.

## Tip

### See also:

IP Access List

If your firewall blocks outbound network connections, you must also open
outbound access from your application environment to Atlas. You must configure
your firewall to allow your applications to make outbound connections to ports
27015 to 27017 to TCP traffic on Atlas hosts. This grants your applications
access to databases stored on Atlas.

## Note

By default, MongoDB Atlas clusters do not need to be able to initiate
connections to your application environments. If you wish to enable Atlas
clusters with LDAP authentication and authorization, you must allow network
access from Atlas clusters directly to your secure LDAP. You can allow access
to your LDAP by using public or private IPs as long as a public DNS hostname
points to an IP that the Atlas clusters can access.

If you are not using VPC / VNet peering and plan to connect to Atlas using
public IP addresses, see the following pages for additional information:

  * Can I specify my own VPC for my MongoDB Atlas project?

  * Do Atlas clusters' public IPs ever change?

## Connect to Your Database Deployment

Atlas CLI

Atlas UI

Use the Atlas CLI to retrieve your standard connection string. You can use the
standard connection string to connect to a database deployment via your
application, `mongosh`, or Compass.

To return the SRV connection strings for your Atlas cluster using the Atlas
CLI, run the following command:

    
    
    atlas clusters connectionStrings describe <clusterName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters connectionStrings describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

You must add your username, database name, and, in some cases, your password
to the standard connection string to successfully connect to Atlas. See the
following example to learn more.

For example, if the Atlas CLI returns the following connection string:

    
    
    mongodb+srv://mycluster.abcd1.mongodb.net  
      
  
Add your username and database name to the `mongosh` command to connect via
`mongosh`:

    
    
    mongosh "mongodb+srv://mycluster.abcd1.mongodb.net/myFirstDatabase" --apiVersion 1 --username <username>  
      
  
`mongosh` prompts you for the password for the database user.

For more information on connection strings, see Connection Strings.

To learn more about connecting via your application, see Connect via Your
Application.

To learn more about connecting via Compass, see Connect via Compass.

To learn more about connecting via VS Code, see Connect via VS Code.

## Note

To connect using `mongodump` or `mongorestore`, use the Command Line Tools
tab. The tab creates an auto-generated template for connecting to your Atlas
database deployment with your preferred tool.

## Troubleshooting

If you are experiencing issues connecting to your database deployment, see
Troubleshoot Connection Issues.

## Tip

### See also:

  * Connect via Your Application

  * Connect via Compass

  * Connect via `mongosh`

  * Connect via BI Connector for Atlas

  * Browse Data via the Atlas UI

  * Test Primary Failover

  * Manage Connections with AWS Lambda

  * Connection Limits and Cluster Tier

  * Connect via VS Code

← Cloud Providers and RegionsConnect via Your Application →

