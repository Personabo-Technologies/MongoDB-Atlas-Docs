Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Private Endpoint for a Dedicated Cluster

Share Feedback

On this page

  * Follow These Steps
  * Take the Next Steps

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Follow these steps to enable a client to connect to a Atlas dedicated cluster
using private endpoints.

To learn more about using private endpoints with Atlas, see Set Up a Private
Endpoint.

To set up a private endpoint for a serverless instance, see Set Up a Private
Endpoint for a Serverless Instance.

## Follow These Steps

AWS PrivateLink

Azure Private Link

Private Service Connect

Atlas CLI

Atlas UI

To set up AWS PrivateLink through the Atlas CLI, install the Atlas CLI and
connect from the Atlas CLI. Then, complete the following steps:

1

### Create the private endpoint service in Atlas.

  1. Run the Atlas CLI command to create a private endpoint and private endpoint service in Atlas:
    
        atlas privateEndpoints aws create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws create.

  2. Note the private endpoint service's ID in the response. In this example, the ID is `6344ac8f51b94c6356527881`.
    
        Private endpoint '6344ac8f51b94c6356527881' created.  
      
  

2

### Retrieve the private endpoint service name.

## Note

It might take Atlas some time to provision the private endpoint. Wait 1-2
minutes before you complete this step.

  1. Run the Atlas CLI command to describe the private endpoint using its service ID:
    
        atlas privateEndpoints aws describe <privateEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws describe.

  2. Note the value for `ENDPOINT SERVICE` in the response, which shows the endpoint service name. In this example, the endpoint service name is `com.amazonaws.vpce.us-east-1.vpce-svc-0705499aae25ac77c`:
    
        ID                         ENDPOINT SERVICE                                           STATUS         ERROR  
      
    6344ac8f51b94c6356527881   com.amazonaws.vpce.us-east-1.vpce-svc-0705499aae25ac77c   AVAILABLE  
  
If the `STATUS` value is `INITIATING`, wait 1-2 more minutes for Atlas to
provision the private endpoint. Then, try this step again.

3

### Create the interface endpoint in AWS.

  1. Run the command in the AWS CLI, replacing the following placeholders with your values:

Placeholder

|

Description  
  
|  
  
{VPC-ID}

|

Unique string that identifies the peer AWS VPC. Find this value on the VPC
dashboard in your AWS account.  
  
{REGION}

|

AWS region in which your database deployment resides.  
  
{SUBNET-IDS}

|

Unique string that identifies the subnets that your AWS VPC uses. Find these
values on the Subnet dashboard in your AWS account.

## Important

You must specify at least one subnet. If you don't, AWS won't provision an
interface endpoint in your VPC. An interface endpoint is required for clients
in your VPC to send traffic to the private endpoint.  
  
{SERVICE-NAME}

|

Unique string identifying the private endpoint service that you retrieved
previously.  
      
        aws ec2 create-vpc-endpoint --vpc-id {VPC-ID} \  
      
    --region {REGION} --service-name {SERVICE-NAME} \  
    --vpc-endpoint-type Interface --subnet-ids {SUBNET-IDS}  
  
To learn more about the AWS CLI, see Creating an Interface Endpoint.

  2. Note the value in the response for the field `VpcEndpointId`. This is a 22-character alphanumeric string that identifies your private endpoint. You can also find this value on the AWS VPC Dashboard under Endpoints > VPC ID.

4

### Update your private endpoint with the VPC Endpoint ID.

  1. Run the Atlas CLI command to create an interface endpoint in Atlas using the Atlas endpoint service ID and the VPC Endpoint ID. In this example, you would set the following parameters:

Parameter

|

Type

|

Example Value  
  
||  
  
`endpointServiceId`

|

Argument

|

`6344ac8f51b94c6356527881`  
  
`privateEndpointId`

|

Option

|

`vpce-00713b5e644e830a3`  
      
        atlas privateEndpoints aws interfaces create <endpointServiceId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws interfaces create.

5

### Configure your resources' security groups to send traffic to and receive
traffic from the interface endpoint.

For each resource that needs to connect to your Atlas clusters using AWS
PrivateLink, the resource's security group must allow outbound traffic to the
interface endpoint's private IP(s) on all ports.

See Adding Rules to a Security Group for more information.

6

### Create a security group for your interface endpoint to allow resources to
access it.

This security group must allow inbound traffic on all ports from each resource
that needs to connect to your Atlas clusters using AWS PrivateLink:

  1. In the AWS console, navigate to the VPC Dashboard.

  2. Click Security Groups, then click Create security group.

  3. Use the wizard to create a security group. Make sure you select your VPC from the VPC list.

  4. Select the security group you just created, then click the Inbound Rules tab.

  5. Click Edit Rules.

  6. Add rules to allow all inbound traffic from each resource in your VPC that you want to connect to your Atlas cluster.

  7. Click Save Rules.

  8. Click Endpoints, then click the endpoint for your VPC.

  9. Click the Security Groups tab, then click Edit Security Groups.

  10. Add the security group you just created, then click Save.

To learn more about VPC security groups, see the AWS documentation.

7

### Verify the private endpoint's availability.

You can connect to the database deployment using the AWS PrivateLink private
endpoint after Atlas finishes configuring all of the resources and the private
endpoint becomes available.

To verify that the AWS private endpoint is available:

  1. Run the Atlas CLI command to describe the interface endpoint using its ID. In this example, you would set the following parameters:

Parameter

|

Type

|

Example Value  
  
||  
  
`interfaceEndpointId`

|

Argument

|

`vpce-00713b5e644e830a3`  
  
`endpointServiceId`

|

Option

|

`6344ac8f51b94c6356527881`  
      
        atlas privateEndpoints aws interfaces describe <interfaceEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints aws interfaces describe.

  2. Verify that the `STATUS` field's value is `AVAILABLE` as shown in the following example:
    
        ID                         STATUS         ERROR  
      
    vpce-00713b5e644e830a3     AVAILABLE  
  

## Take the Next Steps

  * Connect to Atlas using a Private Endpoint

  * Remove a Private Endpoint from Atlas

  * Troubleshoot Private Endpoint Connection Issues

← Set Up a Private EndpointSet Up a Private Endpoint for a Serverless Instance
→

