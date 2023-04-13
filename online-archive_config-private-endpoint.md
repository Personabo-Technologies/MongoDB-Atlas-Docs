Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up a Private Endpoint for Online Archives

Share Feedback

On this page

  * Prerequisites
  * Set Up Private Endpoint Through the User Interface
  * Set Up Private Endpoint Through the API
  * Set Up Private Endpoint Through the Atlas CLI

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

MongoDB supports AWS private endpoints using the AWS PrivateLink feature for
Online Archives. You can set up the private endpoints from the Atlas User
Interface and API.

## Note

You can set up private endpoints for a dedicated cluster. To learn more, see
Set Up a Private Endpoint.

## Prerequisites

  1. Have either the `Project Owner` (`GROUP_ATLAS_ADMIN`) or higher role in Atlas.

  2. Have an AWS user account with an IAM user policy that grants permissions to create, modify, describe, and delete endpoints. For more information on controlling the use of interface endpoints, see the AWS Documentation.

  3. Install the AWS CLI.

  4. If you have not already done so, create your VPC and EC2 instances in AWS. See the AWS documentation for guidance.

## Note

You can't use your Atlas cluster private endpoint ID for an Online Archive.
The Online Archive endpoint ID must be different from your Atlas cluster
endpoint ID, if you have one.

## Set Up Private Endpoint Through the User Interface

You can create a new private endpoint or add an existing private endpoint for
the online archives through your Atlas User Interface. To set up the private
endpoint:

Create New Endpoint

Add Existing Endpoint

1

### Navigate to the Network Access page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

2

### Click the Private Endpoint tab and then the following tab.

Click Federated Database Instance / Online Archive for a private endpoint for
your federated database instance or online archive.

3

### Click the button to set up the private endpoint.

Click Create New Endpoint button.

4

### Choose an AWS region.

  1. From the AWS Region list, select the region where you want to create the private endpoint.

You can select one of the following regions:

Atlas Data Federation Regions

|

AWS Regions  
  
|  
  
Northern Virginia, North America

|

us-east-1  
  
Oregon, North America

|

us-west-2  
  
Ireland, Europe

|

eu-west-1  
  
London, Europe

|

eu-west-2  
  
Frankfurt, Europe

|

eu-central-1  
  
Mumbai, Asia

|

ap-south-1  
  
Sydney, Australia

|

ap-southeast-2  
  
To learn more, see Atlas Data Federation Regions.

  2. Click Next.

## Note

If your organization has no payment information stored, Atlas prompts you to
add it before continuing.

5

### Configure your private endpoint.

  1. Enter the following details about your AWS VPC:

|  
  
|  
  
Your VPC ID

|

Unique identifier of the peer AWS VPC. Find this value on the VPC dashboard in
your AWS account.  
  
Your Subnet IDs

|

Unique identifiers of the subnets your AWS VPC uses. Find these values on the
Subnet dashboard in your AWS account.

## Important

You must specify at least one subnet. If you don't, AWS won't provision an
interface endpoint in your VPC. An interface endpoint is required for clients
in your VPC to send traffic to the private endpoint.  
  
  2. Copy the command the dialog displays and run it using the AWS CLI.

See Creating an Interface Endpoint to perform this task using the AWS CLI.

  3. Enter your VPC Endpoint ID. This is a 22-character alphanumeric string that identifies your private endpoint. Find this value on the AWS VPC Dashboard under Endpoints > VPC ID.

## Tip

Click and expand Show instruction for a screenshot of the AWS VPC dashboard
where you can find the necessary information.

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

## Set Up Private Endpoint Through the API

To configure a private endpoint for an online archive from the API, send a
`POST` request with the private endpoint ID to the privateNetworkSettings
endpoint.

  * If the endpoint ID already exists and there is no change to the comment associated with the endpoint, Atlas makes no change to the endpoint ID list.

  * If the endpoint ID already exists and there is a change to the associated comment, Atlas updates the `comment` value only in the endpoint ID list.

  * If the endpoint ID doesn't exist, Atlas appends the new endpoint to the list of endpoints in the endpoint ID list.

To learn more about the syntax and options, see API.

## Set Up Private Endpoint Through the Atlas CLI

To create a new online archive private endpoint for the project you specify
using the Atlas CLI, run the following command:

    
    
    atlas privateEndpoints onlineArchive aws create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints onlineArchive aws create.

← Configure Online ArchiveConnect to Your Online Archive →

