Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Security Features for Database Deployments

Share Feedback

On this page

  * Preconfigured Security Features
  * Encryption in Transit
  * Virtual Private Cloud
  * Encryption at Rest
  * Required Security Features
  * Network and Firewall Requirements
  * IP Access List
  * User Authentication or Authorization
  * Optional Security Features
  * Network Peering Connection
  * Private Endpoints
  * Unified AWS Access
  * Database Deployment Authentication and Authorization
  * Encryption at Rest using your Key Management
  * Client-Side Field Level Encryption
  * Database Auditing
  * Access Tracking
  * Multi-Factor Authentication for Atlas UI Access
  * Allow Access to or from the Atlas Control Plane
  * Allow Access to Data Federation
  * OCSP Certificate Revocation Check

You can use Atlas securely out of the box. Atlas comes preconfigured with
secure default settings. You can fine-tune the security features for your
database deployments to meet your unique security needs and preferences.
Review the following security features and considerations for database
deployments.

## Important

As a security best practice, don't include sensitive information in namespaces
and field names. Atlas doesn't obfuscate this information.

## Preconfigured Security Features

The following security features are part of the Atlas product:

### Encryption in Transit

Atlas requires TLS/SSL to encrypt the connections to your databases.

To configure SSL or TLS OCSP certificate revocation checking, see OCSP
Certificate Revocation Check.

### Virtual Private Cloud

All Atlas projects with one or more M10+ dedicated clusters receive their own
dedicated VPC (or VNet if you use Azure). Atlas deploys all dedicated clusters
inside this VPC or VNet.

### Encryption at Rest

By default, Atlas encrypts all data stored on your Atlas database deployments.
Atlas also supports Encryption at Rest using your Key Management.

## Required Security Features

You _must_ configure the following security features:

### Network and Firewall Requirements

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

### IP Access List

Atlas only allows client connections to the database deployment from entries
in the project's IP access list. To connect, you must add an entry to the IP
access list. To set up the IP access list for the project, see Configure IP
Access List Entries.

For Atlas clusters deployed on Google Cloud Platform (GCP) or Microsoft Azure,
add the IP addresses of your Google Cloud or Azure services to Atlas project
IP access list to grant those services access to the cluster.

### User Authentication or Authorization

Atlas requires clients to authenticate to connect to the database. You must
create database users to access the database. To set up database users to your
database deployments, see Configure Database Users. Atlas offers many security
features for database deployment authentication and authorization.

To access database deployments in a project, users must belong to that
project. Users can belong to multiple projects.

## Tip

### See also:

Configure Access to the Atlas UI.

## Optional Security Features

You _may_ configure the following security features:

### Network Peering Connection

Atlas supports peering connections with other AWS, Azure, or Google Cloud
network peering connections. To learn more, see Set Up a Network Peering
Connection.

## Important

If this is the first `M10+` dedicated paid cluster for the selected region or
regions _and_ you plan on creating one or more VPC peering connections, please
review the documentation on VPC peering connections before continuing.

### Private Endpoints

Atlas supports private endpoints on:

  * AWS using the AWS PrivateLink feature

  * Azure using the Azure Private Link feature

  * Google Cloud using the Private Service Connect feature

To use private endpoints, see Set Up a Private Endpoint.

### Unified AWS Access

Some Atlas features, including Data Federation and Encryption at Rest using
Customer Key Management, use AWS IAM roles for authentication.

To set up an AWS IAM role for Atlas to use, see Set Up Unified AWS Access.

### Database Deployment Authentication and Authorization

Atlas offers the following security features for database deployment
authentication and authorization.

#### Database User Authentication or Authorization

Atlas requires clients to authenticate to access database deployments. You
must create database users to access the database. To set up database users
for your database deployments, see Configure Database Users.

#### Custom Roles for Database Authorization

Atlas supports creating custom roles for database authorization in cases where
the built-in Atlas roles don't grant your desired set of privileges.

#### Passwordless Authentication with AWS IAM

You can set up passwordless authentication for your AWS IAM users in the
following ways:

  * Configure AWS IAM roles to make username or password fields optional. To learn more, see Set Up Passwordless Authentication with AWS IAM Roles.

  * Use temporary credentials obtained with the AssumeRoleWithSAML API operation. To learn more, see Set Up Passwordless Authentication Using SAML.

#### User Authentication or Authorization with LDAP

Atlas supports performing user authentication and authorization with LDAP. To
use LDAP, see Set Up User Authentication and Authorization with LDAP.

#### User Authentication with X.509

X.509 client certificates provide database users access to the database
deployments in your project. Options for X.509 authentication include Atlas-
managed X.509 authentication and self-managed X.509 authentication. To learn
more about self-managed X.509 authentication, see Set Up Self-Managed X.509
Authentication.

#### Restrict MongoDB Support Access to Atlas Backend Infrastructure

Organization owners can restrict MongoDB Production Support Employees from
accessing Atlas backend infrastructure for any Atlas database deployment in
their organization. Organization owners may grant a 24 hour bypass to the
access restriction at the Atlas database deployment level.

## Important

Blocking infrastructure access from MongoDB Support may increase support issue
response and resolution time and negatively impact your database deployment's
availability.

To enable this option, see Configure MongoDB Support Access to Atlas Backend
Infrastructure.

### Encryption at Rest using your Key Management

Atlas supports using AWS KMS, Azure Key Vault, and Google Cloud to encrypt
storage engines and cloud provider backups. To use encryption at rest, see
Encryption at Rest using Customer Key Management.

### Client-Side Field Level Encryption

Atlas supports client-side field level encryption, including automatic
encryption of fields. All Atlas users are entitled to use MongoDB's automatic
client-side field level encryption features.

To learn more, see Client-Side Field Level Encryption Requirements.

## Note

MongoDB Compass, the Atlas UI, and the MongoDB Shell (`mongosh`) do not
support decrypting client-side field level-encrypted fields.

## Tip

### See also:

  * Client-Side Field Level Encryption

  * Use-Case Guide for Client-Side Field Level Encryption

### Database Auditing

Atlas supports auditing all system event actions. To use database auditing,
see Set up Database Auditing.

### Access Tracking

Atlas surfaces authentication logs directly in the Atlas UI so that you can
easily review successful and unsuccesful authentication attempts made against
your database deployments. To view your database access history, see View
Database Access History.

### Multi-Factor Authentication for Atlas UI Access

Atlas supports MFA to help you control access to your Atlas accounts. To set
up MFA, see Manage Your Multi-Factor Authentication Options.

### Allow Access to or from the Atlas Control Plane

If you use any of the following Atlas features, you might have to add Atlas IP
addresses to your network's IP access list:

  * Alert Webhooks

  * Encryption at Rest using Customer Key Management

## Note

If you enable the Encryption at Rest feature, you must allow access from
public IPs for all your hosts in your deployment, including CSRS (Config
Server Replica Sets) if you are using sharded clusters.

#### Required Outbound Access

If your network allows outbound HTTP requests only to specific IP addresses,
you must allow access to the following IP addresses so that your API requests
can reach the Atlas control plane:

    
    
    3.214.160.189  
      
    13.248.140.125  
    13.248.203.97  
    13.248.214.115  
    18.210.185.2  
    18.210.245.203  
    18.232.30.107  
    18.235.209.93  
    34.192.82.120  
    34.194.131.15  
    34.194.251.66  
    34.195.194.204  
    34.227.138.166  
    34.230.213.36  
    34.233.152.179  
    34.233.179.140  
    35.172.148.213  
    35.172.245.18  
    54.147.76.65  
    54.204.237.208  
    75.2.1.110  
    76.223.14.2  
    76.223.77.37  
    76.223.84.31  
    99.83.223.45  
  
#### Required Inbound Access

If your network allows inbound HTTP requests only from specific IP addresses,
you must allow access from the following IP addresses so that Atlas can
communicate with your webhooks and KMS:

    
    
    3.92.113.229  
      
    3.208.110.31  
    3.211.96.35  
    3.212.79.116  
    3.214.203.147  
    3.215.10.168  
    3.215.143.88  
    3.232.182.22  
    18.214.178.145  
    18.235.30.157  
    18.235.48.235  
    18.235.145.62  
    34.193.91.42  
    34.193.242.51  
    34.194.7.70  
    34.196.80.204  
    34.196.151.229  
    34.200.66.236  
    34.235.52.68  
    34.236.228.98  
    34.237.40.31  
    34.238.35.12  
    35.153.40.82  
    35.169.184.216  
    35.171.106.60  
    35.173.54.44  
    35.174.179.65  
    35.174.230.146  
    35.175.93.3  
    35.175.94.38  
    35.175.95.59  
    44.206.200.18  
    44.207.9.197  
    44.207.12.57  
    50.19.91.100  
    52.7.232.43  
    52.71.233.234  
    52.73.214.87  
    52.87.98.128  
    52.203.106.167  
    54.145.247.111  
    54.163.55.77  
    54.167.217.16  
    100.26.2.217  
    107.20.0.247  
    107.20.107.166  
    107.22.44.69  
  
### Allow Access to Data Federation

If your network allows outbound requests to specific IP addresses only, you
must allow access to the following IP addresses on TCP port 27017 so that your
requests can reach the federated database instance:

    
    
    18.204.47.197  
      
    34.237.78.67  
    54.91.120.155  
    34.217.220.13  
    54.203.115.97  
    54.69.142.129  
    108.129.35.102  
    18.200.7.156  
    99.81.123.21  
    3.8.218.156  
    3.9.125.156  
    3.9.90.17  
    18.196.201.253  
    3.122.67.212  
    35.158.226.227  
    13.54.14.65  
    52.64.205.136  
    3.6.3.105  
    65.1.222.250  
  
### OCSP Certificate Revocation Check

If your network allows outbound requests to specific IP addresses only, to
allow SSL or TLS OCSP certificate revocation checking, you must allow access
to Atlas' CA (Certificate Authority) OCSP Responder servers that can be found
in the OCSP URL of the SSL or TLS certificate.

To disable OCSP certificate revocation checking, refer to the documentation
for the MongoDB driver version that your application uses.

← Troubleshoot Connection IssuesConfigure Cluster Access with the Quickstart
Wizard →

