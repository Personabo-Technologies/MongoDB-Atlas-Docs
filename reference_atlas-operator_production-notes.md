Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Production Notes

Share Feedback

On this page

  * Atlas Account
  * API Keys
  * Namespaces
  * AWS Security Groups
  * Deprecated Configuration Parameters
  * Cluster Creation
  * Connection Strings
  * Connection Information

You can access the Atlas Kubernetes Operator project on GitHub:

  * https://github.com/mongodb/mongodb-atlas-kubernetes

## Atlas Account

Before you deploy Atlas Kubernetes Operator, you must create an Atlas account.
To learn more, see Register a new Atlas Account.

## API Keys

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

To learn more, see Configure Access to Atlas.

## Namespaces

You can deploy Atlas Kubernetes Operator to watch all the namespaces in the
Kubernetes cluster, or only its namespace.

## AWS Security Groups

You must configure VPC peering for your project before you can add an AWS
security group to an access list. You can't set AWS security groups as
temporary access list entries.

## Deprecated Configuration Parameters

The following parameters are deprecated in the Atlas API and Atlas Kubernetes
Operator doesn't support them:

  * `replicationSpec`

  * `replicationFactor`

## Cluster Creation

Creating a new cluster can take up to 10 minutes.

## Connection Strings

You can't use a connection URL directly. Atlas clusters require
authentication. You must create at least one `AtlasDatabaseUser` Custom
Resource before the application in your Kubernetes cluster can connect to the
Atlas cluster. Atlas Kubernetes Operator creates a special secret for each
cluster and database user combination in the project. The application in your
Kubernetes cluster can use this secret to connect to the Atlas cluster. The
`spec.scopes` parameter in the `AtlasDatabaseUser` custom resource restricts
the clusters that create the database user.

## Connection Information

To connect to the Atlas Administration API, Atlas Kubernetes Operator reads
the organization ID and API keys from one of the following locations:

  * `spec.connectionSecretRef.name` (if specified in the `AtlasProject` Custom Resource).

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

  * `global` Atlas Kubernetes Operator secret `<operator-deployment-name>-api-key` (if `spec.connectionSecretRef.name` is not specified).

To create or update resources in Atlas, Atlas Kubernetes Operator uses the
connection information to make API calls to Atlas.

## Note

Sometimes Atlas Kubernetes Operator makes multiple API calls in Atlas during
the reconciliation of a custom resource. For example, `AtlasProject` has an IP
Access List configuration for calling the matching API.

If any errors occur during the reconciliation, `status.conditions` updates to
reflect the error.

## Example

    
    
    - lastTransitionTime: "2021-03-15T14:26:44Z"  
      
       message: 'POST https://cloud.mongodb.com/api/atlas/v1.0/groups/604a47de73cd8cag77239021/accessList:  
          400 (request "INVALID_IP_ADDRESS_OR_CIDR_NOTATION") The address 192.0.2.1dfdfd5  
          must be in valid IP address or CIDR notation.'  
       reason: ProjectIPAccessListNotCreatedInAtlas  
       status: "False"  
       type: IPAccessListReady  
  
← `AtlasTeam` Custom ResourceAtlas Kubernetes Operator Changelog →

