Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up X.509 Authentication

Share Feedback

On this page

  * Prerequisites
  * Generate an X.509 Certificate with cert-manager
  * Generate an X.509 Certificate with a Custom Script
  * Procedure
  * Configure a project to use the certificate.
  * Add a database user that uses X.509 authentication.

X.509 client certificates provide database users access to the database
deployments in your project. You can use Atlas Kubernetes Operator to enable
X.509 authentication for the `AtlasProject` Custom Resource and the
`AtlasDatabaseUser` Custom Resource.

Options for X.509 authentication include Atlas-managed X.509 authentication
and self-managed X.509 authentication. To learn more about self-managed X.509
authentication, see Set Up Self-Managed X.509 Authentication.

To set up X.509 authentication:

  1. Generate an X.509 certificate.

  2. Configure the `AtlasProject` Custom Resource to use the certificate.

  3. Configure the `AtlasDatabaseUser` Custom Resource to use Atlas-managed or self-managed X.509 authentication.

## Prerequisites

## Note

To use self-managed X.509 certificates, you must have a Public Key
Infrastructure to integrate with MongoDB Atlas.

  * You need the following public API key, private API key, and the organization ID information to configure Atlas Kubernetes Operator access to Atlas.

    * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

    * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

To learn more, see Configure Access to Atlas.

  * Generate an X.509 certificate with cert-manager or the create_X.509.go script.

### Generate an X.509 Certificate with cert-manager

To generate an X.509 certificate with cert-manager, do the following steps:

1

#### Install cert-manager.

To install cert-manager, see the cert-manager installation documentation.

2

#### Create an `Issuer`.

To create a cert-manager `Issuer`, see the cert-manager configuration
documentation.

To learn more, see the example.

3

#### Creat a certificate.

To create a certificate, see the cert-manager usage documentation.

To learn more, see the example.

### Generate an X.509 Certificate with a Custom Script

To generate an X.509 certificate with the create_X.509.go script, do the
following steps:

1

#### Run the custom script.

Run the create_X.509.go script:

    
    
    go run scripts/create_x509.go --path={pem-file-path}  
      
  
 **Example:**

    
    
     go run scripts/create_x509.go --path=tmp/x509/  
      
  
2

#### Add the certificate to a secret.

To add the certificate to a secret, run the following commands:

    
    
    kubectl create secret generic {secret-name} --from-file={pem-file-directory}  
      
      
    
    kubectl label secret {secret-name} atlas.mongodb.com/type=credentials  
      
  
 **Example:**

    
    
     kubectl create secret generic my-x509-cert --from-file=./tmp/x509/cert.pem  
      
      
    
    kubectl label secret my-x509-cert atlas.mongodb.com/type=credentials  
      
  
## Procedure

1

### Configure a project to use the certificate.

Specify the secret within the `spec.X509CertRef.name` parameter for the
`AtlasProject` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Project  
      projectIpAccessList:  
        - ipAddress: "192.0.2.15"  
          comment: "IP address for Application Server A"  
        - ipAddress: "203.0.113.0/24"  
          comment: "CIDR block for Application Servers B - D"  
      x509CertRef:  
        name: my-x509-cert  
    EOF  
  
2

### Add a database user that uses X.509 authentication.

Specify the `x509Type` parameter for the `AtlasDatabaseUser` Custom Resource.

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
a Common Name (CN) in the `username` field. To learn more, see RFC 2253.

You must specify `\$external` for the `spec.databaseName` parameter.  
  
To learn more about the configuration parameters available from the API, see
the Atlas Database Users API.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
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
    EOF  
  
← Manage Private Endpoints for Serverless InstancesConfigure Network Peering →

