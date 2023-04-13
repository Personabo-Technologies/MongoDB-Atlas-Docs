Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete a Private Endpoint for a Federated Database Instance

Share Feedback

On this page

  * Delete Private Endpoint Through the User Interface
  * Delete a Private Endpoint Through the API

You can delete a private endpoint for your federated database instances from
the Atlas User Interface and API.

## Delete Private Endpoint Through the User Interface

To delete a private endpoint from the Atlas UI:

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

### Click Delete for the private endpoint that you wish to delete.

4

### Click Confirm in the confirmation window to delete the private endpoint.

## Delete a Private Endpoint Through the API

To delete a private endpoint through the API, send a `DELETE` request to the
`privateNetworkSettings/endpointIds` endpoint with the ID of the private
endpoint to delete. To learn more about the syntax and options, see API.

← Edit the Private Endpoint for a Federated Database InstanceUpdate a
Federated Database Instance Region →

