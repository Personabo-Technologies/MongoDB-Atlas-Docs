Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Private Endpoint for a Federated Database Instance

Share Feedback

On this page

  * Prerequisites
  * Set Up Private Endpoint Through the User Interface
  * Set Up Private Endpoint Through the API

MongoDB supports AWS private endpoints using the AWS PrivateLink feature for
your federated database instance. You can set up the private endpoints from
the Atlas User Interface and API.

## Prerequisites

  1. Have either the `Project Owner` (`GROUP_ATLAS_ADMIN`) or higher role in Atlas.

  2. Have an AWS user account with an IAM user policy that grants permissions to create, modify, describe, and delete endpoints. To learn more about controlling the use of interface endpoints, see the AWS Documentation.

  3. Install the AWS CLI.

  4. If you have not already done so, create your VPC and EC2 instances in AWS. To learn more, see the AWS documentation for guidance.

## Note

You can't use your Atlas cluster private endpoint ID for Atlas Data
Federation. The Atlas Data Federation endpoint ID must be different from your
Atlas cluster endpoint ID, if you have one.

## Set Up Private Endpoint Through the User Interface

You can create a new private endpoint or add an existing private endpoint
through your Atlas User Interface. To set up the private endpoint:

Create New Endpoint

Add Existing Endpoint

1

### Navigate to the Network Access page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

2

### Click the Private Endpoint tab and then the following tab for the
resource.

Data Federation / Online Archive to manage the private endpoint for your
federated database instance or online archive.

3

### Click the following button to set up the private endpoint.

Click Create new endpoint button.

4

### Choose an AWS region.

  1. From the AWS Region list, select the region where you want to create the private endpoint.

You can select one of the following regions:

Data Federation Regions

|

AWS Regions  
  
|  
  
Virginia, USA

|

us-east-1  
  
Oregon, USA

|

us-west-2  
  
Sao Paulo, Brazil

|

sa-east-1  
  
Ireland

|

eu-west-1  
  
London, England

|

eu-west-2  
  
Frankfurt, Germany

|

eu-central-1  
  
Mumbai, India

|

ap-south-1  
  
Singapore

|

ap-southeast-1  
  
Sydney, Australia

|

ap-southeast-2  
  
The following table shows the service names for the various endpoints in each
region:

Region

|

Service Name  
  
|  
  
`us-east-1`

|

`com.amazonaws.vpce.us-east-1.vpce-svc-00e311695874992b4`  
  
`us-west-1`

|

`com.amazonaws.vpce.us-west-2.vpce-svc-09d86b19e59d1b4bb`  
  
`eu-west-1`

|

`com.amazonaws.vpce.eu-west-1.vpce-svc-0824460b72e1a420e`  
  
`eu-west-2`

|

`com.amazonaws.vpce.eu-west-2.vpce-svc-052f1840aa0c4f1f9`  
  
`eu-central-1`

|

`com.amazonaws.vpce.eu-central-1.vpce-svc-0ac8ce91871138c0d`  
  
`sa-east-1`

|

`com.amazonaws.vpce.sa-east-1.vpce-svc-0b56e75e8cdf50044`  
  
`ap-southeast-2`

|

`com.amazonaws.vpce.ap-southeast-2.vpce-svc-036f1de74d761706e`  
  
`ap-south-1`

|

`com.amazonaws.vpce.ap-south-1.vpce-svc-03eb8a541f96d356d`  
  
To learn more, see Atlas Data Federation Regions.

  2. Click Next.

5

### Configure your private endpoint.

  1. Enter the following details about your AWS VPC:

|  
  
|  
  
Your VPC ID

|

Unique 22-character alphanumeric string that identifies the peer AWS VPC. Find
this value on the VPC dashboard in your AWS account.  
  
Your Subnet IDs

|

Unique strings that identify the subnets that your AWS VPC uses. Find these
values on the Subnet dashboard in your AWS account.

## Important

You must specify at least one subnet. If you don't, AWS won't provision an
interface endpoint in your VPC. An interface endpoint is required for clients
in your VPC to send traffic to the private endpoint.  
  
  2. Copy the command the dialog displays and run it using the AWS CLI.

## Note

You can't copy the command until Atlas finishes creating VPC resources in the
background.

See Creating an Interface Endpoint to perform this task using the AWS CLI.

  3. Enter the 22-character alphanumeric string that identifies your private endpoint in the VPC Endpoint ID field. Find this value on the AWS VPC Dashboard under Endpoints > VPC ID.

## Tip

Click and expand Show more instructions in the dialog for a visual clue as to
where you can find the necessary information in the AWS console.

6

### Run the command to create your VPC interface endpoint.

Copy the command the dialog displays and run it using the AWS CLI.

7

### Modify the private DNS name to ensure that the hostname resolves to an
address on your network.

To ensure that the hostname resolves to an address on your network:

  1. Copy the command the dialog displays and run it using the AWS CLI.

  2.  **Optional**. Add a comment to associate with this endpoint.

8

### Click Finish endpoint creation.

9

### Configure your resources' security groups to send traffic to and receive
traffic from the interface endpoint.

For each resource that needs to connect to your federated database instance
using AWS PrivateLink, the resource's security group must allow outbound
traffic to the interface endpoint's private IP(s) on all ports.

See Adding Rules to a Security Group for more information.

10

### Create a security group for your interface endpoint to allow resources to
access it.

This security group must allow inbound traffic on all ports from each resource
that needs to connect to your federated database instance using AWS
PrivateLink:

  1. In the AWS console, navigate to the VPC Dashboard.

  2. Click Security Groups, then click Create security group.

  3. Use the wizard to create a security group. Make sure you select your VPC from the VPC list.

  4. Select the security group you just created, then click the Inbound Rules tab.

  5. Click Edit Rules.

  6. Add rules to allow all inbound traffic from each resource in your VPC that you want to connect to your federated database instance.

  7. Click Save Rules.

  8. Click Endpoints, then click the endpoint for your VPC.

  9. Click the Security Groups tab, then click Edit Security Groups.

  10. Add the security group you just created, then click Save.

To learn more about VPC security groups, see the AWS documentation.

## Set Up Private Endpoint Through the API

To configure a private endpoint from the API, send a `POST` request with the
private endpoint ID to the `privateNetworkSettings` endpoint.

  * If the endpoint ID already exists and there is no change to the comment associated with the endpoint, Atlas makes no change to the endpoint ID list.

  * If the endpoint ID already exists and there is a change to the associated comment, Atlas updates the `comment` value only in the endpoint ID list.

  * If the endpoint ID doesn't exist, Atlas appends the new endpoint to the list of endpoints in the endpoint ID list.

To learn more about the syntax and options, see API.

← Add Your IP Address to the IP Access ListCreate a Database User for Your
Federated Database Instance →

