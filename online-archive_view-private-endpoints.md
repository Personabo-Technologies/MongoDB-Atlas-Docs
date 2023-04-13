Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Private Endpoints for Online Archives

Share Feedback

On this page

  * View List of Private Endpoints Using the UI
  * Navigate to the Network Access page for your project.
  * Click the Private Endpoint tab and then the following tab.
  * Retrieve Private Endpoint Using the API
  * Retrieve All Private Endpoints Using the API
  * View Private Endpoints Using the Atlas CLI
  * Edit the Private Endpoint for Online Archives
  * Edit Private Endpoint Through the User Interface
  * Edit Private Endpoint Through the API
  * Delete a Private Endpoint for an Online Archive
  * Delete Private Endpoint Through the User Interface
  * Delete a Private Endpoint Through the API
  * Delete a Private Endpoint Through the Atlas CLI

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can view the list of private endpoints for the online archives on the
Atlas cluster through the Atlas UI and API.

## View List of Private Endpoints Using the UI

To view the list of private endpoints for the Online Archives:

1

### Navigate to the Network Access page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

2

### Click the Private Endpoint tab and then the following tab.

Click Federated Database Instance / Online Archive for a private endpoint for
your federated database instance or online archive.

The page displays the private endpoints for your online archives. For each
private endpoint, you can see the following information:

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

  * Edit the Private Endpoint for Online Archives

  * Delete a Private Endpoint for an Online Archive

  
  
## Retrieve Private Endpoint Using the API

To retrieve a private endpoint for an online archive through the API, send a
`GET` request to the privateNetworkSettings/endpointIds/ endpoint with the ID
of the private endpoint to retrieve. To learn more about the syntax and
options, see API.

## Retrieve All Private Endpoints Using the API

To retrieve all the private endpoints for the online archives using the API,
send a `GET` request to the privateNetworkSettings/endpointIds endpoint. To
learn more about the syntax and options, see API.

## View Private Endpoints Using the Atlas CLI

To return the details of the online archive private endpoint you specify using
the Atlas CLI, run the following command:

    
    
    atlas privateEndpoints onlineArchive aws describe <privateEndpointId> [options]  
      
  
To list all online archive private endpoints in a project using the Atlas CLI,
run the following command:

    
    
    atlas privateEndpoints onlineArchive aws list [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas privateEndpoints onlineArchive aws
describe and atlas privateEndpoints onlineArchive aws list.

## Edit the Private Endpoint for Online Archives

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

MongoDB supports AWS private endpoints using the AWS PrivateLink feature only
for Online Archives. You can edit the comment associated with a private
endpoint for online archives from the Atlas UI and API.

## Note

You can edit the private endpoints for a dedicated cluster. To learn more, see
Set Up a Private Endpoint.

### Edit Private Endpoint Through the User Interface

To edit the comment associated with a private endpoint from your Atlas UI:

1

#### Navigate to the Network Access page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

2

#### Click the Private Endpoint tab and then the following tab.

Click Federated Database Instance / Online Archive for a private endpoint for
your federated database instance or online archive.

3

#### Click Edit for the VPC endpoint ID that you wish to modify.

4

#### Make changes to the comment associated with the VPC endpoint ID shown in
the Edit Private Endpoint dialog.

5

#### Click Confirm for the changes to take effect.

### Edit Private Endpoint Through the API

To edit a private endpoint for an online archive through the API, send a
`POST` request to the privateNetworkSettings endpoint with the unique ID of
the private endpoint to edit. If you change the comment associated with the
specified endpoint, Atlas makes no change to the endpoint ID list. If you
change the comment associated with the specified endpoint, Atlas updates the
`comment` value only in the endpoint ID list.

To learn more about the syntax and options, see API.

## Delete a Private Endpoint for an Online Archive

You can delete a private endpoint for online archives from the Atlas UI and
API.

## Note

You can delete the private endpoints for a dedicated cluster. To learn more,
see Set Up a Private Endpoint.

### Delete Private Endpoint Through the User Interface

To delete a private endpoint from the Atlas UI:

1

#### Navigate to the Network Access page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Network Access in the sidebar.

2

#### Click the Private Endpoint tab and then the following tab.

Click Federated Database Instance / Online Archive for a private endpoint for
your federated database instance or online archive.

3

#### Click Delete for the private endpoint that you wish to delete.

4

#### Click Confirm in the confirmation window to delete the private endpoint.

### Delete a Private Endpoint Through the API

To delete a private endpoint through the API, send a `DELETE` request to the
privateNetworkSettings/endpointIds endpoint with the ID of the private
endpoint to delete. To learn more about the syntax and options, see API.

### Delete a Private Endpoint Through the Atlas CLI

To remove the online archive private endpoint you specify using the Atlas CLI,
run the following command:

    
    
    atlas privateEndpoints onlineArchive aws delete <privateEndpointId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas privateEndpoints onlineArchive aws delete.

← Manage Online ArchivesPause and Resume Archiving →

