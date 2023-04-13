Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Quick Start

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Register for an Atlas account or log in.
  * Create API keys for your organization.
  * Deploy Atlas Kubernetes Operator.
  * Create a secret with your API keys and organization ID.
  * Create the `AtlasProject` custom resource.
  * Create the `AtlasDeployment` custom resource.
  * Create a secret with a password to log into the Atlas cluster database.
  * Create the `AtlasDatabaseUser` custom resource.
  * Check the status of your database user.
  * Retrieve the secret that Atlas Kubernetes Operator created to connect to the cluster.

You can use Atlas Kubernetes Operator to manage resources in Atlas without
leaving Kubernetes. This tutorial demonstrates how to create your first
cluster in Atlas from Kubernetes configuration files with Atlas Kubernetes
Operator.

## Note

### Would you prefer to start with Helm?

To create your first cluster in Atlas from Helm Charts with Atlas Kubernetes
Operator, see Helm Charts Quick Start.

## Prerequisites

This tutorial requires:

  * A running Kubernetes cluster with nodes running processors with the x86-64, AMD64, or ARM64 architecture.

  * `jq` 1.6 or higher

You can access the Atlas Kubernetes Operator project on GitHub:

  * https://github.com/mongodb/mongodb-atlas-kubernetes

## Procedure

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

1

### Register for an Atlas account or log in.

Register a new Atlas Account or Log in to Your Atlas Account.

2

### Create API keys for your organization.

## Note

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

Create an API Key in an Organization and configure the API Access List.

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

3

### Deploy Atlas Kubernetes Operator.

In one of the following scenarios, replace `<version>` with the latest release
number:

  * If you want Atlas Kubernetes Operator to watch all the namespaces in the Kubernetes cluster, run the following command:
    
        kubectl apply -f https://raw.githubusercontent.com/mongodb/mongodb-atlas-kubernetes/<version>/deploy/all-in-one.yaml  
      
  
  * If you want Atlas Kubernetes Operator to watch only its namespace, you must install the configuration files from the `deploy/namespaced` directory:
    
        kubectl apply -f https://raw.githubusercontent.com/mongodb/mongodb-atlas-kubernetes/<version>/deploy/namespaced/crds.yaml  
      
      
        kubectl apply -f https://raw.githubusercontent.com/mongodb/mongodb-atlas-kubernetes/<version>/deploy/namespaced/namespaced-config.yaml  
      
  

4

### Create a secret with your API keys and organization ID.

To create and label a secret, run the following commands with your API keys
and organization ID:

    
    
    kubectl create secret generic mongodb-atlas-operator-api-key \  
      
        --from-literal="orgId=<atlas_organization_id>" \  
        --from-literal="publicApiKey=<atlas_api_public_key>" \  
        --from-literal="privateApiKey=<atlas_api_private_key>" \  
        -n mongodb-atlas-system  
      
    
    kubectl label secret mongodb-atlas-operator-api-key atlas.mongodb.com/type=credentials -n mongodb-atlas-system  
      
  
5

### Create the `AtlasProject` custom resource.

Run the following command to create the `AtlasProject` Custom Resource:

## Note

The following example does not specify `spec.connectionSecretRef.name`. If
unspecified, Atlas Kubernetes Operator uses the default connection secret
previously set with your API keys and organization ID.

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/0"  
          comment: "Allowing access to database from everywhere (only for Demo!)"  
    EOF  
  
## Warning

The IP address in the example, `0.0.0.0/0`, allows any client to connect to
the Atlas cluster. Do not use this IP address in production.

6

### Create the `AtlasDeployment` custom resource.

Run the following command to create an `AtlasDeployment` Custom Resource and
create a cluster:

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      deploymentSpec:  
        name: "Test-cluster"  
        providerSettings:  
          instanceSizeName: M10  
          providerName: AWS  
          regionName: US_EAST_1  
    EOF  
  
To create a serverless instance, see the serverless instance example.

7

### Create a secret with a password to log into the Atlas cluster database.

Replace `P@@ssword%` with your password and run the following commands:

    
    
    kubectl create secret generic the-user-password --from-literal="password=P@@sword%"  
      
      
    
    kubectl label secret the-user-password atlas.mongodb.com/type=credentials  
      
  
8

### Create the `AtlasDatabaseUser` custom resource.

Run the following command to create the `AtlasDatabaseUser` Custom Resource:

## Note

`spec.passwordSecretRef` must reference the password that you created
previously.

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDatabaseUser  
    metadata:  
      name: my-database-user  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      roles:  
        - roleName: "readWriteAnyDatabase"  
          databaseName: "admin"  
      projectRef:  
        name: my-project  
      username: theuser  
      passwordSecretRef:  
        name: the-user-password  
    EOF  
  
9

### Check the status of your database user.

Run the following command until you recieve a `True` response, which indicates
the database user is ready:

## Note

The `AtlasDatabaseUser` Custom Resource waits until the cluster is ready.
Creating a new cluster can take up to 10 minutes.

    
    
    kubectl get atlasdatabaseusers my-database-user -o=jsonpath='{.status.conditions[?(@.type=="Ready")].status}'  
      
  
10

### Retrieve the secret that Atlas Kubernetes Operator created to connect to
the cluster.

  1. Copy the following command:

## Important

The following command requires `jq` 1.6 or higher.

    
        kubectl get secret {my-project}-{my-atlas-cluster}-{my-database-user} -o json | jq -r '.data | with_entries(.value |= @base64d)';  
      
  
  2. Replace the following placeholders with the details for your custom resources:

|  
  
|  
  
`my-project`

|

Specify the value of the `metadata` field of your `AtlasProject` Custom
Resource.  
  
`my-atlas-cluster`

|

Specify the value of the `metadata` field of your `AtlasDeployment` Custom
Resource.  
  
`my-database-user`

|

Specify the value of the `metadata` field of your `AtlasDatabaseUser` Custom
Resource.  
  
  3. Run the command.

## Note

Your connection strings will differ from the following example.

    
        {  
      
       "connectionStringStandard": "mongodb://theuser:P%40%40sword%25@test-cluster-shard-00-00.peqtm.mongodb.net:27017,test-cluster-shard-00-01.peqtm.mongodb.net:27017,test-cluster-shard-00-02.peqtm.mongodb.net:27017/?ssl=true&authSource=admin&replicaSet=atlas-pk82fl-shard-0",  
       "connectionStringStandardSrv": "mongodb+srv://theuser:P%40%40sword%25@test-cluster.peqtm.mongodb.net",  
       "password": "P@@sword%",  
       "username": "theuser"  
     }  
  
You can use this secret in your application:

    
        containers:  
      
     - name: test-app  
       env:  
        - name: "CONNECTION_STRING"  
          valueFrom:  
            secretKeyRef:  
              name: test-atlas-operator-project-test-cluster-theuser  
              key: connectionStringStandardSrv  
  

← Atlas Kubernetes OperatorHelm Charts Quick Start →

