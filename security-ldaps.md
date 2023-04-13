Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up User Authentication and Authorization with LDAP

Share Feedback

On this page

  * Prerequisites
  * Recommendation
  * Considerations
  * Procedures
  * Tutorials for Third-Party LDAP Providers

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas provides the ability to manage user authentication and authorization
from all MongoDB clients using your own Lightweight Directory Access Protocol
(LDAP) server over TLS. A single LDAPS (LDAP over TLS) configuration applies
to all clusters in a project.

If you enable user authorization with LDAP, you can create LDAP groups on the
`admin` database by mapping LDAP groups to MongoDB roles on your Atlas
databases. To use LDAP groups effectively, create additional projects within
Atlas to control access to specific deployments in your organization, such as
creating separate Atlas projects for development and production environments.
You can then map an LDAP group to a role in the Atlas project to provide
access to the desired deployment.

## Note

When you enable user authorization and an LDAP user doesn't belong to any LDAP
group, Atlas doesn't assign any database roles to the user. When you enable
user authentication and you disable user authorization, Atlas assigns MongoDB
database roles to the LDAP user.

If you have multiple departments with their own billing needs, alert settings,
and project members, consider creating a new set of projects or a new
organization for each department or business unit.

## Note

An explanation of LDAP is out of scope for the MongoDB documentation. Please
review RFC 4515 and RFC 4516 or refer to your preferred LDAP documentation.

## Prerequisites

You must meet the following prerequisites to manage user authentication and
authorization using LDAP in Atlas:

  * Atlas cluster using MongoDB 4.0 or later.

  * LDAP server using TLS that your Atlas clusters can access over the network using either VPC or VNet peering connection or the cluster nodes' public IP addresses.

  * LDAP group memberships embedded as an attribute for each user in the LDAP entry for user authorization only.

## Recommendation

For your LDAPS service to access Atlas clusters, MongoDB recommends one of two
configurations:

Using a VPC or VNet:

  1. Run your LDAP server in a VPC or VNet.

  2. Establish a peering connection to your Atlas project.

  3. Use a public FQDN that resolves to the private IP address of your LDAP server.

Using your data center:

  1. Run your LDAP server with a public FQDN that resolves to a public IP address.

  2. Configure the LDAP server to allow inbound access from the Atlas cluster nodes' public IP addresses.

## Considerations

### Conflicts between LDAP Authorization and X.509 Users

If you enable LDAP authorization, you can't connect to your database
deployments with users that authenticate with an Atlas-managed X.509
certificate.

After you enable LDAP authorization, you _can_ connect to your database
deployments with users that authenticate with an self-managed X.509
certificate. However, the user's Common Name in their X.509 certificate must
match the Distinguished Name of a user who is authorized to access your
database with LDAP.

### Usernames

Atlas uses the full Distinguished Name (DN) of users in your LDAP server as
the Atlas username. For example, an example LDAP user named `ralph` has the
following username in Atlas:

`cn=ralph,cn=Users,dc=aws-atlas-ldap-01,dc=myteam,dc=com`

### Connection String

If the administrator enables user authentication or both user authentication
and authorization with LDAP, database users must override the following
parameters in the connection string for their clients.

  * `authSource` must be `$external`

  * `authenticationMechanism` must be `PLAIN`

## Example

The following connection string for `mongosh` authenticates an LDAP user named
`rob`:

    
    
    mongosh "mongodb+srv://cluster0-tijis.mongodb.net/test?authSource=%24external" \  
      
      --authenticationMechanism PLAIN \  
      --username cn=rob,cn=Users,dc=ldaps-01,dc=myteam,dc=com  
  
To copy the connection string:

  1. Click Database in the top-left corner of Atlas.

  2. Click Connect on the Database Deployments page.

  3. Edit the string with your `User DN` and password.

## Note

If your passwords, database names, or connection strings contain reserved URI
characters, you must escape the characters. For example, if your password is
`@bc123`, you must escape the `@` character when specifying the password in
the connection string, such as `%40bc123`. To learn more, see Special
Characters in Connection String Password.

### Rolling Restart on Configuration Change

If you change your LDAP configuration, Atlas performs a rolling restart of
your cluster. This restart allows Atlas to use the correct settings to
authenticate users.

### Using Public IP Addresses

You can use public IP addresses that refer to other internal or private IP
addresses using Network Address Translation to allow Atlas traffic to your
LDAP server. If you do this, be aware that certain activities trigger a change
in the Atlas cluster's public IP addresses.

If you allowed LDAP server access based on public IP addresses, changes to the
Atlas cluster's public IP address prevent LDAP access. To restore LDAP access,
add the new Atlas cluster public IP addresses to the LDAP access list.

### Limitations

You cannot use both LDAP and SCRAM authentication for the same database user.

## Procedures

### Configure Authentication with LDAP

Atlas CLI

Atlas UI

## Note

You can use the same Atlas CLI command to configure LDAP authentication and
LDAP authorization.

To save one LDAP configuration for the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas security ldap save [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas security ldap save.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Configure Authorization

Atlas CLI

Atlas UI

## Note

You can use the same Atlas CLI command to configure LDAP authentication and
LDAP authorization.

To save one LDAP configuration for the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas security ldap save [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas security ldap save.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View LDAP Configuration

Atlas CLI

Atlas UI

To return the details for one LDAP configuration using the Atlas CLI, run the
following command:

    
    
    atlas security ldap get [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas security ldap get.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Disable LDAP Configuration

Atlas CLI

Atlas UI

## Note

You can use the same Atlas CLI command to disable LDAP authentication settings
and LDAP authorization settings.

To delete one LDAP configuration using the Atlas CLI, run the following
command:

    
    
    atlas security ldap delete [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas security ldap delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Tutorials for Third-Party LDAP Providers

Use the following tutorials to configure Atlas to authenticate and authorize
users from third-party LDAP providers:

  * Configure User Authentication and Authorization with Azure AD Domain Services

  * Configure User Authentication and Authorization with Okta LDAP Interface

  * Configure User Authentication and Authorization with OneLogin VLDAP

← Set Up Passwordless Authentication with AWS IAMConfigure User Authentication
and Authorization with Azure AD Domain Services →

