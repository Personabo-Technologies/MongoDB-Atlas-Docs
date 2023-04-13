Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Private Endpoints for Serverless Instances

Share Feedback

On this page

  * Procedure

Atlas Kubernetes Operator supports managing private endpoints for serverless
instances on the following platforms:

  * AWS using the AWS PrivateLink feature.

  * Azure using the Azure Private Link feature.

## Note

Serverless instances don't support Private Service Connect. If you need to set
up Private Service Connect, use a dedicated cluster.

MongoDB plans to add support for more configurations and capabilities on
serverless instances over time. To learn which features MongoDB plans to
support for serverless instances in the future, see Serverless Instance
Limitations.

Before you begin, see Manage Private Endpoints.

## Procedure

To enable clients to connect to Atlas serverless instances using private
endpoints:

AWS PrivateLink

Azure Private Link

1

### Specify the `spec.serverlessSpec.privateEndpoints` parameter.

Specify the `spec.serverlessSpec.privateEndpoints` parameter for the
`AtlasDeployment` Custom Resource. In the
`spec.serverlessSpec.privateEndpoints.name` field, specify a unique label to
identify the private endpoint and run the following command:

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
      name: atlas-deployment-serverless  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      serverlessSpec:  
        name: serverless-instance  
        providerSettings:  
          providerName: SERVERLESS  
          backingProviderName: AWS  
          regionName: US_EAST_1  
        privateEndpoints:  
        - name: "{unique-private-endpoint-label}"  
    EOF  
  
Atlas creates the VPC resources. This might take several minutes to complete.

2

### Find the service names for your private endpoints.

  1. Run the following command:
    
        kubectl get atlasdeployment atlas-deployment-serverless -o yaml  
      
  
  2. Note the service name string for each private endpoint within the `status.serverlessPrivateEndpoints.EndpointServiceName` field of the `AtlasDeployment` Custom Resource.

3

### Use the AWS CLI to configure each private endpoint.

To create your application VPC interface endpoint:

  1. Copy the following command:
    
        aws ec2 create-vpc-endpoint --vpc-id {your-application-vpc-id} --region {aws-region} --service-name {service-name-string} --vpc-endpoint-type Interface --subnet-ids {your-application-subnet-ids}  
      
  
  2. Replace the following placeholders with the details about your AWS VPC:

|  
  
|  
  
`your-application-vpc-id`

|

Unique string that identifies the peer AWS VPC. Find this value on the VPC
dashboard in your AWS account.  
  
`aws-region`

|

Label that identifies the AWS region of the private endpoint.  
  
`service-name-string`

|

Unique string that identifies the service name for your private endpoint. Find
this value within the `status.serverlessPrivateEndpoints.EndpointServiceName`
field of the `AtlasDeployment` Custom Resource.  
  
`your-application-subnet-ids`

|

Unique strings that identify the subnets your AWS VPC uses. Separate each
subnet with a space. Find these values on the Subnet dashboard in your AWS
account.

## Important

You must specify at least one subnet. If you don't, AWS won't provision a
interface endpoint in your VPC. An interface endpoint is required for clients
in your VPC to send traffic to the private endpoint.  
  
  3. Run the command with the AWS CLI.

  4. Note the `VpcEndpointId` value in the output.

 **Example**

    
         "VpcEndpoint": {  
      
             "VpcEndpointId": "vpce-XXXXXX”,  
             "VpcEndpointType": "Interface",  
             "VpcId": "vpc-XXXXX”,  
             "ServiceName": "com.amazonaws.vpce.{aws-region}.vpce-svc-XXXX”,  
             "State": "pendingAcceptance",  
  

To learn more, see Creating an Interface Endpoint in the AWS documentation.

4

### Update the `spec.serverlessSpec.privateEndpoints` parameter.

Update the `spec.serverlessSpec.privateEndpoints` parameter for the
`AtlasDeployment` Custom Resource. Replace the `vpce-id` with the
`VpcEndpointId` values for your private endpoints and run the following
command:

## Note

You can find the unique identifier of the peer AWS VPC on the VPC dashboard in
your AWS account.

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasDeployment  
    metadata:  
      name: atlas-deployment-serverless  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      serverlessSpec:  
        name: serverless-instance  
        providerSettings:  
          providerName: SERVERLESS  
          backingProviderName: AWS  
          regionName: US_EAST_1  
        privateEndpoints:  
        - name: "{unique-private-endpoint-label}"  
          cloudProviderEndpointID: "{vpce-id}"  
    EOF  
  
5

### Check the status of your private endpoints using Atlas Kubernetes
Operator.

Run the following command:

    
    
    kubectl get atlasdeployment atlas-deployment-serverless -o yaml  
      
  
6

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

Your connection strings will differ from the following example. If you have
multiple private endpoints, the secret contains multiple
`connectionStringPrivate` and `connectionStringPrivateSvr` fields with the
appropriate numeric suffix (for example, `connectionStringPrivate1`,
`connectionStringPrivate2`, and so on).

    
        {  
      
      "connectionStringPrivate": "mongodb://pl-0-eastus2.uzgh6.gcp.mongodb.net:1024,pl-0-eastus2.uzgh6.gcp.mongodb.net:1025,pl-0-eastus2.uzgh6.gcp.mongodb.net:1026/?ssl=truereplicaSet=atlas-18bndf-shard-0",  
      "connectionStringPrivateSrv": "mongodb+srv://cluster0-pl-0.uzgh6.gcp.mongodb.net",  
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
              name: my-project-my-atlas-cluster-my-database-user  
              key: connectionStringPrivate  
  

← Manage Private Endpoints for Dedicated ClustersSet Up X.509 Authentication →

