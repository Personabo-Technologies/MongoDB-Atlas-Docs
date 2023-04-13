Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Private Endpoint for a Serverless Instance

Share Feedback

On this page

  * Follow These Steps
  * Take the Next Steps

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

## Note

Serverless instances don't support Private Service Connect. If you need to set
up Private Service Connect, use a dedicated cluster.

MongoDB plans to add support for more configurations and capabilities on
serverless instances over time. To learn which features MongoDB plans to
support for serverless instances in the future, see Serverless Instance
Limitations.

Follow these steps to enable a client to connect to an Atlas serverless
instance using a private endpoint.

To learn more about using private endpoints with Atlas, see Set Up a Private
Endpoint.

To set up a private endpoint for a dedicated cluster, see Set Up a Private
Endpoint for a Dedicated Cluster.

## Follow These Steps

AWS PrivateLink

Azure Private Link

You can set up AWS PrivateLink for serverless instances using the Atlas UI or
the Atlas Administration API. Select an interface to learn more.

Atlas Administration API

Atlas UI

To set up AWS PrivateLink through the Atlas Administration API, configure API
access. Then, complete the following steps:

1

### Create the private endpoint in Atlas.

  1. Run the command to create one private endpoint, replacing the placeholders with your parameters. To learn more about the parameters, see create one private endpoint.
    
        1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2| --header "Accept: application/json" \  
    3| --header "Content-Type: application/json" \  
    4| --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/{INSTANCE-NAME}/endpoint?pretty=true" \  
    5| --data '  
    6|    {  
    7|      "comment" : "example comment"  
    8|    }'  
  
  2. Note the value for the field `_id` in the response.
    
        1| {  
    |  
    2|   "_id": "5f7cac1adf5d6c6306f4b283",  
    3|   "cloudProviderEndpointId": null,  
    4|   "comment": "example comment",  
    5|   "endpointServiceName": null,  
    6|   "errorMessage": null,  
    7|   "status": "RESERVATION_REQUESTED"  
    8| }  
  

2

### Retrieve the service name for the private endpoint.

## Note

It might take Atlas some time to provision the private endpoint. Wait 1-2
minutes before you complete this step.

  1. Run the command to get one private endpoint, replacing the placeholders with the parameters for the endpoint you created. Replace {ENDPOINT-ID} with the `_id` that you retrieved previously. To learn more about the parameters, see get one private endpoint.
    
        1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/{INSTANCE-NAME}/endpoint/{ENDPOINT-ID}?pretty=true"  
  
  2. Note the value for the field `endpointServiceName` in the response.
    
        1| {  
    |  
    2|   "_id": "5f7cac1adf5d6c6306f4b283",  
    3|   "cloudProviderEndpointId": "34985fcac938279cd98dc894",  
    4|   "comment": "example comment",  
    5|   "endpointServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-0afd34ee97e30d43f",  
    6|   "errorMessage": null,  
    7|   "status": "RESERVED"  
    8| }  
  

If `endpointServiceName` is `null`, wait 1-2 more minutes for Atlas to
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

Run the command to update one private endpoint, replacing the placeholders
with the parameters for the endpoint you created. Update the
`cloudProviderEndpointId` field to the VPC Endpoint ID you retrieved
previously. To learn more about the parameters, see update one private
endpoint.

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/{INSTANCE-NAME}/endpoint/{ENDPOINT-ID}" \  
    5|      --data '  
    6|        {  
    7|          "cloudProviderEndpointId" : "vpce-fcac938279cd98dc894",  
    8|          "providerName" : "AWS"  
    9|        }'  
  
## Note

You must include the `providerName` to successfully run this command.

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

You can connect to an Atlas serverless instance using the AWS PrivateLink
private endpoint after Atlas finishes configuring all of the resources and the
private endpoint becomes available.

To verify that the AWS PrivateLink private endpoint is available:

  1. Run the command to get one Private Endpoint for one Serverless Instance, replacing the placeholders with the parameters for the endpoint you created. To learn more about the parameters, see get one Private Endpoint for one Serverless Instance.
    
        1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/serverless/instance/{INSTANCE-NAME}/endpoint/{ENDPOINT-ID}?pretty=true"  
  
  2. Verify that the `status` field's value is `AVAILABLE` as shown in the following example:
    
        1| {  
    |  
    2|   "_id": "5f7cac1adf5d6c6306f4b283",  
    3|   "cloudProviderEndpointId": "vpce-fcac938279cd98dc894",  
    4|   "comment": "example comment",  
    5|   "endpointServiceName": "com.amazonaws.vpce.us-east-1.vpce-svc-0afd34ee97e30d43f",  
    6|   "errorMessage": null,  
    7|   "status": "AVAILABLE"  
    8| }  
  

If `cloudProviderEndpointId` is `Initiating`, wait 1-2 more minutes for Atlas
to configure the private endpoint. Then, try this step again.

## Take the Next Steps

  * Connect to Atlas using a Private Endpoint

  * Remove a Private Endpoint from Atlas

  * Troubleshoot Private Endpoint Connection Issues

