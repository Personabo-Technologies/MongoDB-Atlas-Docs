Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Access to Atlas

Share Feedback

On this page

  * Atlas Kubernetes Operator Secrets
  * Parameters
  * Prerequisites
  * Procedure

To connect to the Atlas Administration API, Atlas Kubernetes Operator reads
the organization ID and API keys from Atlas Kubernetes Operator secrets. You
can also configure the following features:

  * private endpoints

  * x509 authentication

  * Unified Cloud Provider Access

To learn more about creating an Atlas account, see Register a new Atlas
Account.

## Atlas Kubernetes Operator Secrets

Depending on your configuration, Atlas Kubernetes Operator reads from one of
the following Atlas Kubernetes Operator secrets:

Scope

|

Location

|

Description  
  
||  
  
Global

|

Atlas Kubernetes Operator secret `<operator-deployment-name>-api-key` created
in the same namespace where you installed Atlas Kubernetes Operator.

|

Atlas Kubernetes Operator uses this secret data to connect to the Atlas
Administration API unless the `AtlasProject` Custom Resource specifies
`spec.connectionSecretRef.name`.

`global` Atlas Kubernetes Operator secrets let you use one API key for all the
projects in an organization. Any new `AtlasProject` Custom Resource uses the
same API key for reduced overhead.

The default name of the Atlas Kubernetes Operator deployment is `mongodb-
atlas-operator`. So, the secret should be named `mongodb-atlas-operator-api-
key`.  
  
Project

|

Atlas Kubernetes Operator secret referenced with
`spec.connectionSecretRef.name` in the `AtlasProject` Custom Resource.

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

|

Atlas Kubernetes Operator uses this secret data to connect to the Atlas
Administration API for any `AtlasDeployment` Custom Resource and
`AtlasDatabaseUser` custom resource that references the project.

If you do not specify `spec.connectionSecretRef.name`, Atlas Kubernetes
Operator uses the `global` Atlas Kubernetes Operator secret.

Atlas Kubernetes Operator secrets per project allow for more granular access.
You may want a single API key to have access to a single Atlas project.  
  
## Parameters

Both `global` and `project` secrets require the following information:

Parameter

|

Description  
  
|  
  
`orgId`

|

Unique 24-digit hexadecimal string used to identify your Atlas organization.  
  
`publicAPIKey`

|

Public part of the API key.  
  
`privateAPIKey`

|

Private part of the API key.  
  
## Prerequisites

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

## Procedure

To configure Atlas Kubernetes Operator access to Atlas, do one of the
following steps.

  * For a `global` Atlas Kubernetes Operator secret, run the following commands:

## Note

The name of the `global` Atlas Kubernetes Operator secret must conform to the
predefined format. The default name of the Atlas Kubernetes Operator
deployment is `mongodb-atlas-operator`. So, the secret should be named
`mongodb-atlas-operator-api-key`.

    
        kubectl create secret generic mongodb-atlas-operator-api-key \  
      
       --from-literal="orgId=<the_atlas_organization_id>" \  
       --from-literal="publicApiKey=<the_atlas_api_public_key>" \  
       --from-literal="privateApiKey=<the_atlas_api_private_key>" \  
       -n <operator_namespace>  
      
    kubectl label secret mongodb-atlas-operator-api-key atlas.mongodb.com/type=credentials -n mongodb-atlas-system  
  
  * For a `project` Atlas Kubernetes Operator secret, run the following commands:
    
        kubectl create secret generic my-project-connection \  
      
       --from-literal="orgId=<the_atlas_organization_id>" \  
       --from-literal="publicApiKey=<the_atlas_api_public_key>" \  
       --from-literal="privateApiKey=<the_atlas_api_private_key>" \  
       -n <atlas_project_namespace>  
      
    kubectl label secret mongodb-atlas-operator-api-key atlas.mongodb.com/type=credentials -n mongodb-atlas-system  
  

← Import Atlas Projects into Atlas Kubernetes OperatorManage Private Endpoints
→

