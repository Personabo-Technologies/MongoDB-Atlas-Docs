Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Customer Keys with Azure Key Vault

Share Feedback

On this page

  * Enable Customer-Managed Keys with Azure Key Vault
  * Rotate your Azure Key Identifier
  * Related Topics

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas uses your Azure Key Identifier (AKI) from your Azure Key Vault (AKV) to
encrypt and decrypt your MongoDB master keys. These MongoDB master keys are
used to encrypt cluster database files and cloud providers snapshots.

When you use your own cloud provider KMS, Atlas automatically rotates the
MongoDB master keys every 90 days. These keys are rotated on a rolling basis
and the process does not require the data to be rewritten.

Atlas encrypts your data at rest using encrypted storage media. Using keys you
manage with AKV, Atlas encrypts your data a second time when it writes it to
the MongoDB encrypted storage engine. You use your AKI to encrypt the MongoDB
master encryption keys.

This page covers configuring customer key management using AKV on your Atlas
project.

You must configure customer key management for the Atlas project before
enabling it on clusters in that project.

## Enable Customer-Managed Keys with Azure Key Vault

### Prerequisites

To enable customer-managed keys with Azure Key Vault for a MongoDB project,
you must:

  * Use an M10 or larger cluster.

  * Use Cloud Backups to encrypt your backup snapshots. Legacy Backups are not supported.

  * Have the Tenant ID (or Directory ID) for an Active Directory tenant.

  * Have the Client ID (or Application ID) and a non-expired application Password for an Azure Application associated to the Active Directory tenant.

  * Have the Resource Group name of an Azure Resource Group containing the Key Vault.

  * Have an Active Directory Application with the role of Azure key Vault Reader assigned to it.

  * Have the Subscription ID and Key Vault Name of an Azure Key Vault. Ensure the Key Vault resource group matches the resource group name specified to Resource Group.

The Key Vault must have the following Access Policies:

    * Key Management Operations

      * `GET`

      * `LIST`

    * Cryptographic Operations

      * `ENCRYPT`

      * `DECRYPT`

  * Have the Key Identifier for a key in the specified Azure Key Vault.

Atlas uses these resources when enabling encryption at rest for a cluster in
the Atlas project. Consider creating an Azure Application, Resource Group, and
Key Vault specifically for use with the Atlas project.

To learn how to configure the referenced Azure components, see the Azure
Documentation.

  * To help users easily create or change a cluster, you can allow public access to the key. To narrow the scope of the key and mitigate risks, use controls such as TLS and authentication.

  * For restricted access to defined IP ranges, allow access from Atlas IP addresses and the public IP addresses of your cluster nodes. Ensure Atlas can communicate with your key vault. To avoid connectivity interruptions, update your configuration whenever node IP addresses change.

    * If you restrict access to the key vault, you create more complexity when IP addresses change. For example, when you create or update a cluster, you must grant access in the Azure Key Vault to any new IP addresses. You should implement a process to remove IP addresses and keys when you delete a cluster or remove nodes.

### Enable Customer-Managed Keys for a Project

You must enable customer key management for a project before you can enable it
on a cluster in that project.

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Toggle the button next to Encryption at Rest using your Key Management to
On.

3

#### Select Azure Key Vault.

4

#### Enter your Account Credentials.

|  
  
|  
  
Client ID

|

Enter the Client ID (or Application ID) of the Azure application.  
  
Tenant ID

|

Enter the Tenant ID (or Directory ID) of the Active Directory tenant.  
  
Secret

|

Enter one of the application's non-expired Passwords.  
  
Azure Environment

|

Select the Azure cloud your Active Directory tenant lives in.  
  
5

#### Enter the Key Vault Credentials.

|  
  
|  
  
Subscription ID

|

Enter the Subscription ID of the Key Vault.  
  
Resource Group Name

|

Enter the Resource Group of the Key Vault.  
  
Key Vault Name

|

Enter the name of the Key Vault.  
  
6

#### Enter the Encryption Key.

|  
  
|  
  
Key Identifier

|

Enter the full URL for the key created in the Key Vault.

## Important

The key identifier must be provided in the full Azure general format

    
    
    | https://{keyvault-name}.vault.azure.net/{object-type}/{object-name}/{object-version}  
      
  
7

#### Click Save.

Atlas displays a banner in the Atlas console during the encryption process.

### Enable Customer Key Management for an Atlas Cluster

After you Enable Customer-Managed Keys for a Project, you must enable customer
key management for each Atlas cluster that contains data that you want to
encrypt.

## Note

You must have the `Project Owner` role to enable customer key management for
clusters in that project.

For new clusters, toggle the Manage your own encryption keys setting to Yes
when you create the cluster.

For existing clusters:

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Modify the cluster's configuration.

For the cluster that contains data that you want to encrypt, click the
ellipses ..., then select Edit Configuration.

3

#### Enable cluster encryption.

  1. Expand the Additional Settings panel.

  2. Toggle the Manage your own encryption keys setting to Yes.

4

#### Review and apply your changes.

  1. Click Review Changes.

  2. Review your changes, then click Apply Changes to update your cluster.

### Disable Customer-Managed Keys for a Project

You must disable customer key management on each cluster in a project before
you can disable the feature for the project.

## Important

Do _not_ disable or delete any AKV keys that any cluster in your Atlas project
uses before you have disabled customer key management within the Atlas
project. If Atlas cannot access an AKV key, any data that key encrypted
becomes inaccessible.

### Revoke Access to an Encryption Key

You can revoke Atlas's access to an encryption key from within AKV. Atlas
automatically pauses your clusters when you revoke access to the encryption
key unless your AKV IP access list restricts the Atlas control plane.

To allow automatic pausing of your cluster, you must either:

  * Disable the IP access list for your AKV

  * Allow access to your AKV from the Atlas control plane.

## Note

MongoDB adds new Atlas control plane IP addresses over time. You must keep the
IP access list updated to allow automatic cluster pausing while using an IP
access list for your AKV.

If the IP access list for your AKV restricts access from the Atlas control
plane when you revoke access to an encryption key, you must pause your
clusters manually to revoke Atlas's access.

### Alerts

Atlas automatically creates an `encryption key rotation alert` once you
configure customer key management for a project.

To reset this alert, Rotate your Azure Key Identifier.

## Rotate your Azure Key Identifier

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

When you use your own cloud provider KMS, Atlas automatically rotates the
MongoDB master keys every 90 days. These keys are rotated on a rolling basis
and the process does not require the data to be rewritten.

Atlas does _not_ automatically rotate the Key Identifier used for Azure-
provided key management.

Atlas automatically creates an `encryption key rotation alert` to remind you
to rotate your Azure Key Identifier every 90 days by default when you enable
Encryption at Rest for an Atlas project.

### Prerequisites

You must create a new key in the Azure Key Vault associated to the Atlas
project.

### Procedure

The following procedure documents how to rotate your Atlas project Key
Identifier by specifying a new key identifier in Atlas.

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Click Rotate Keys __.

3

#### Update the Azure credentials.

  1. Click Azure Key Vault if the Azure Key Vault selector is not already active.

  2. Click Encryption Key if the Encryption Key selector is not already active.

  3. Enter the Azure Key Identifier in the Key Identifier field.

Include the full URL to the new encryption key identifier. For example:

    
        https://mykeyvault.vault.azure.net/keys/AtlasKMSKey/a241124e3d364e9eb99fbd3e11124b23  
      
  
## Important

The encryption key **must** belong to the Key Vault configured for the
project. Click the Key Vault section to view the currently configured Key
Vault for the project.

  4. Click Update Credentials.

Atlas displays a banner in the Atlas UI during the Key Identifier rotation
process. Do **not** delete or disable the original Key Identifier until your
changes have deployed.

If the cluster uses Back Up Your Database Deployment, do **not** delete or
disable the original Key Identifier until you validate that no snapshots used
that key for encryption.

### Alerts

Atlas resets the `encryption key rotation alert` alert at the completion of
this procedure.

## Related Topics

  * To enable Encryption at Rest using your Key Management when deploying an Atlas cluster, see Manage Your Own Encryption Keys.

  * To enable Encryption at Rest using your Key Management for an existing Atlas cluster, see Enable Encryption at Rest.

  * To learn more about Encryption at Rest using your Key Management in Atlas, see Encryption at Rest using Customer Key Management.

  * To learn more about MongoDB Encryption at Rest, see Encryption at Rest in the MongoDB server documentation.

  * To learn more about Encryption at Rest with Cloud Backups, see Storage Engine and Cloud Backup Encryption.

← Manage Customer Keys with AWS KMSManage Customer Keys with Google Cloud KMS
→

