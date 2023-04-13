Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasDatabaseUser` Custom Resource

Share Feedback

On this page

  * Connection Secrets
  * Examples
  * Project and Clusters
  * Database User without Scopes
  * Database User with Scopes
  * Database User with X.509 Authentication
  * Parameters

The `AtlasDatabaseUser` custom resource configures the database user in an
Atlas project. You create database users per project, not per cluster. So, the
`AtlasDatabaseUser` custom resource configuration contains a reference to the
`AtlasProject` Custom Resource. Create the `AtlasProject` Custom Resource
beforehand.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

The following example shows a reference to the `AtlasProject` Custom Resource:

    
    
    spec:  
      
      projectRef:  
        name: my-project  
  
Atlas Kubernetes Operator ensures the database user configuration in Atlas
matches the configuration in Kubernetes.

Atlas Kubernetes Operator does one of the following actions using the Atlas
Database Users API:

  * Creates a new database user.

  * Updates an existing user.

Before you create a database user, you must create a secret with a password to
log into the Atlas cluster database.

## Note

You must create the secret in the same namespace where the `AtlasDatabaseUser`
custom resource is located.

The following example creates a secret:

    
    
    kubectl create secret generic the-user-password --from-literal="password=P@@sword%"  
      
  
## Connection Secrets

After Atlas Kubernetes Operator successfully creates or updates the database
user in Atlas, Atlas Kubernetes Operator creates or updates the connection
secrets in the same namespace where the `AtlasDatabaseUser` custom resource is
located.

Connection secrets contain all the information required to connect to the
Atlas clusters including the following parameters:

Parameter

|

Description  
  
|  
  
`connectionStringStandard`

|

Public `mongodb://` connection URI.  
  
`connectionstringStandardSrv`

|

Public `mongodb+srv://` connection URI.  
  
`username`

|

Name that identifies the database user.  
  
`password`

|

Password of the database user.  
  
Applications running in Kubernetes can use this information to connect to
Atlas clusters. You can mount the secrets to the application pods as files and
the application process can read these files to get data.

The following example shows mounting the secret as an environment variable:

    
    
    spec:  
      
    containers:  
    - name: test-app  
      env:  
        - name: "CONNECTIONSTRING"  
          valueFrom:  
            secretKeyRef:  
              name: project-cluster-basic-theuser  
              key: connectionStringStandardSrv  
  
The following example shows mounting the secret as files:

    
    
    spec:  
      
    containers:  
    - name: test-app  
      volumeMounts:  
      - mountPath: /var/secrets/  
        name: theuser-connection  
    volumes:  
      - name: theuser-connection  
        secret:  
          secretName: project-cluster-basic-theuser  
  
By default, Atlas Kubernetes Operator creates the database user connection
secret for each cluster in the same project that the `AtlasDatabaseUser`
references. You can change this behavior with the `spec.scopes` parameter.
This parameter restricts the clusters where the database user gets created.
The name of the connection secret uses the following format:
`<project_name>-<cluster_name>-<db_user_name>`.

## Examples

### Project and Clusters

The following example shows an Atlas project and the clusters that reference
it:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
     name: my-project  
     labels:  
       app.kubernetes.io/version: 1.6.0  
    spec:  
     name: p1  
     projectIpAccessList:  
       - ipAddress: "192.0.2.15"  
         comment: "IP address for Application Server A"  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
     name: my-aws-cluster  
     labels:  
       app.kubernetes.io/version: 1.6.0  
    spec:  
     name: aws-cluster  
     projectRef:  
       name: my-project  
     providerSettings:  
       instanceSizeName: M10  
       providerName: AWS  
       regionName: US_EAST_1  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
     name: my-gcp-cluster  
     labels:  
       app.kubernetes.io/version: 1.6.0  
    spec:  
     name: gcp-cluster  
     projectRef:  
       name: my-project  
     providerSettings:  
       instanceSizeName: M10  
       providerName: GCP  
       regionName: EASTERN_US  
  
### Database User without Scopes

The following example shows an `AtlasDatabaseUser` custom resource
specification with `spec.scopes` omitted:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDatabaseUser  
    metadata:  
     name: my-database-user  
     labels:  
       app.kubernetes.io/version: 1.6.0  
    spec:  
     roles:  
       - roleName: readWriteAnyDatabase  
         databaseName: admin  
     projectRef:  
       name: my-project  
     username: theuser  
     passwordSecretRef:  
       name: the-user-password  
  
After you create this custom resource, Atlas Kubernetes Operator creates the
following secrets:

  * `p1-aws-cluster-theuser`

  * `p1-gcp-cluster-theuser`

### Database User with Scopes

The following example shows an `AtlasDatabaseUser` custom resource
specification with `spec.scopes` set to the Google Cloud cluster only:

    
    
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
     scopes:  
       - type: CLUSTER  
         name: gcp-cluster  
  
After you update this custom resource, Atlas Kubernetes Operator removes
`theuser` from the `aws-cluster`. It also removes the `p1-aws-cluster-theuser`
secret from the Kubernetes cluster.

### Database User with X.509 Authentication

The following example shows an `AtlasDatabaseUser` custom resource
specification with X.509 authentication.

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDatabaseUser  
    metadata:  
      name: my-database-user  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      username: CN=my-x509-authenticated-user,OU=organizationalunit,O=organization  
      databaseName: "\$external"  
      x509Type: "CUSTOMER"  
      roles:  
        - roleName: "readWriteAnyDatabase"  
          databaseName: "admin"  
      projectRef:  
        name: my-project  
  
## Parameters

This section describes some of the key `AtlasDatabaseUser` custom resource
parameters available. For a full list of parameters available, see the Atlas
Database Users API. Refer to these descriptions, the available examples, and
the API documentation to customize your specifications.

`spec.databaseName`

    

 _Type_ : string

 _Required_

Database against which the database user authenticates. Database users must
provide both a username and authentication database to log into MongoDB.

If the database user authenticates with SCRAM-SHA, this value must be `admin`.

If the database user authenticates with X.509, this value must be
`\$external`.

`spec.passwordSecretRef`

    

 _Type_ : string

 _Conditional_

Reference to the secret that contains the password. The SCRAM-SHA
authentication method requires this parameter.

`spec.projectRef.name`

    

 _Type_ : string

 _Required_

Name of the project where the database user belongs. You must specify an
existing `AtlasProject` Custom Resource.

`spec.roles`

    

 _Type_ : array

 _Required_

List that contains the user's roles and the databases or collections on which
the roles apply. For a full list of parameters available, see the Atlas
Database Users API.

`spec.scopes`

    

 _Type_ : array

 _Optional_

List that contains the clusters where the user gets created.

`spec.scopes.name`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies the cluster that the database user can
access. You must specify this parameter if you specified `spec.scopes`.

`spec.scopes.type`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies the resource type that the database user
can access. Atlas Kubernetes Operator currently supports only `CLUSTER`. You
must specify this parameter if you specified `spec.scopes`.

`spec.username`

    

 _Type_ : string

 _Required_

Human-readable label that identifies the user needed to authenticate to the
MongoDB database or collection.

`spec.x509Type`

    

 _Type_ : string

 _Optional_

X.509 method by which the database authenticates the provided `spec.username`.
If you don't specify a value, Atlas uses the default value of `NONE`.

This parameter accepts:

|  
  
|  
  
NONE

|

User that doesn't use X.509 authentication.  
  
MANAGED

|

User that uses Atlas-managed X.509.

You must specify `\$external` for the `spec.databaseName` parameter.  
  
CUSTOMER

|

User that uses Self-Managed X.509. Users created with this `x509Type` require
a Common Name (CN) in the `spec.username` parameter. To learn more, see RFC
2253.

You must specify `\$external` for the `spec.databaseName` parameter.  
  
For the configuration parameters available from the API, see the Atlas
Database Users API.

Currently, Atlas Kubernetes Operator does not support the following parameters
available from the Atlas Database Users API:

  * `awsIAMType`

  * `ldapAuthType`

Do not specify the following parameters:

  * `groupId`

  * `password`

Specify `spec.passwordSecretRef` instead.

← `AtlasDeployment` Custom Resource`AtlasBackupPolicy` Custom Resource →

