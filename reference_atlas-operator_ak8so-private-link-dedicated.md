Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Private Endpoints for Dedicated Clusters

Share Feedback

On this page

  * Procedure

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas Kubernetes Operator supports managing private endpoints for dedicated
clusters on the following platforms:

  * AWS using the AWS PrivateLink feature.

  * Azure using the Azure Private Link feature.

  * Google Cloud using the Private Service Connect feature.

Before you begin, see Manage Private Endpoints.

## Procedure

To enable clients to connect to Atlas dedicated clusters using private
endpoints:

AWS PrivateLink

Azure Private Link

Private Service Connect

1

### Specify the `spec.privateEndpoints` parameter.

Specify the `spec.privateEndpoints` parameter for the `AtlasProject` Custom
Resource. In the `spec.privateEndpoints.provider` field, specify `AWS`.
Replace the placeholder `{aws-region}` with the AWS region information for
your private endpoints and run the following command:

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      privateEndpoints:  
      - provider: "AWS"  
        region: "{aws-region}"  
    EOF  
  
Atlas creates the VPC resources in the region you selected. This might take
several minutes to complete.

2

### Find the service names for your private endpoints.

  1. Run the following command:
    
        kubectl get atlasproject my-project -o yaml  
      
  
  2. Note the service name string for each private endpoint within the `status.privateEndpoints.serviceName` field of the `AtlasProject` Custom Resource.

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
this value within the `status.privateEndpoints.serviceName` field of the
`AtlasProject` Custom Resource.  
  
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

### Update the `spec.privateEndpoints` parameter.

Update the `spec.privateEndpoints` parameter for the `AtlasProject` Custom
Resource. Specify the AWS region and replace `vpce-id` with the
`VpcEndpointId` values for your private endpoints and run the following
command:

## Note

You can find the unique identifier of the peer AWS VPC on the VPC dashboard in
your AWS account.

    
    
    cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      privateEndpoints:  
      - provider: "AWS"  
        region: "{aws-region}"  
        id: "{vpce-id}"  
    EOF  
  
5

### Check the status of your private endpoints using Atlas Kubernetes
Operator.

Run the following command:

    
    
    kubectl get atlasproject my-project -o yaml  
      
  
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
  

← Manage Private EndpointsManage Private Endpoints for Serverless Instances →

