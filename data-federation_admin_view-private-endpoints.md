Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# View the List of Private Endpoints

Share Feedback

On this page

  * View List of Private Endpoints Using the UI
  * Retrieve Private Endpoint Using the API
  * Retrieve All Private Endpoints Using the API

You can view the list of private endpoints for the federated database
instances through the Atlas UI and API.

## View List of Private Endpoints Using the UI

To view the list of private endpoints from the Atlas UI:

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

The page displays the private endpoints for your federated database instances.
For each private endpoint, you can see the following information:

Column Name

|

Description  
  
|  
  
VPC Endpoint ID

|

The unique identifier of the peer AWS VPC. This corresponds to the value on
the VPC dashboard in your AWS account.  
  
Comment

|

The comment associated with the endpoint.  
  
Actions

|

The actions you can take on the private endpoint. You can:

  * Edit the Private Endpoint for a Federated Database Instance

  * Delete a Private Endpoint for a Federated Database Instance

  
  
## Retrieve Private Endpoint Using the API

To retrieve a private endpoint through the API, send a `GET` request to the
`privateNetworkSettings/endpointIds/` endpoint with the ID of the private
endpoint to retrieve. To learn more about the syntax and options, see API.

## Retrieve All Private Endpoints Using the API

To retrieve all the private endpoints using the API, send a `GET` request to
the `privateNetworkSettings/endpointIds` endpoint. To learn more about the
syntax and options, see API.

← Set Up a Private Endpoint for a Federated Database InstanceEdit the Private
Endpoint for a Federated Database Instance →

