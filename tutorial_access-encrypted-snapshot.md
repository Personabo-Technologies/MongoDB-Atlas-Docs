Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Access an Encrypted Snapshot

Share Feedback

On this page

  * Considerations
  * Procedure

When you use Encryption at Rest using Customer Key Management, Atlas encrypts
the `mongod` data files in your snapshots. If you want to download and restore
a snapshot, the `mongod` can't read these data files unless it has access to a
KMIP server that can provide the appropriate decryption key. You can use the
KMIP Proxy Standalone to access the `mongod` data files. You download the KMIP
Proxy Standalone as a binary for your specific operating system.

## Considerations

By default, the KMIP Proxy Standalone uses the credentials stored in the
`/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file.

  * If you rotate keys, these credentials reflect the latest key rotation.

  * If the KMIP Proxy Standalone binary is unable to decrypt the snapshots using these credentials, the binary shows an error message stating that you must update the metadata files on disk that contain the old credentials. You can update the metadata file with any text editor.

  * If you use role-based access to your encryption key, the `/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file won't contain valid credentials.

Take one of the following actions:

    * Update the `/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file. Use an empty `roleId`. Provide temporary credentials based on the IAM role that can access your encryption key in the `accessKeyId` and `secretAccessKey` fields:
        
                {  
          
          "accessKeyId": "TemporaryAccessKeyId",  
          "secretAccessKey": "TemporarySecretAccessKey",  
          "roleId": "",  
          "region": "us-east-1"  
        }  
  
    * Start the KMIP Proxy Standalone binary with the following options:

      * `awsAccessKey`

      * `awsSecretAccessKey`

      * `awsSessionToken`

      * `awsRegion`

To generate temporary credentials based on an IAM role, see the AWS
documentation.

## Procedure

1

### Download the encrypted snapshot.

  1. Click Databases in the top-left corner of Atlas.

  2. In the Database Deployments view, click the name of the database deployment for which you want to download a snapshot.

  3. Click the Backup tab.

  4. Click Download next to the snapshot you want to download.

Atlas prepares the snapshot. When it is ready to download, Atlas generates a
one-time use download link that expires after four hours. Atlas emails you the
download link and displays it in the Restores & Downloads tab.

2

### Download the KMIP Proxy Standalone.

In the Preparing Snapshot Download modal, click Download KMIP Proxy and select
the binary for your operating system.

## Tip

You can also download the KMIP Proxy Standalone from the following locations
in the Atlas user interface:

  * On the Security __ Advanced page, in the Encryption at Rest using your Key Management section.

  * In the Backup __ Restores & Downloads tab of the cluster.

3

### Start the KMIP Proxy Standalone.

  1. Open a terminal or command prompt window.

  2. Invoke the following command with the specified parameters:

AWS

Azure and GCP

    
        kmipProxyStandalone  
      
      -awsAccessKey <accessKey> -awsSecretAccessKey <secretAccessKey> \  
      -awsSessionToken <token> -awsRegion <region> -cloudProvider aws \  
      -dbpath <dbpath> -kmipPort <kmipPort> -mongodPort <mongodPort>  
  
Parameter

|

Description  
  
|  
  
`awsAccessKey`

|

IAM access key ID with permissions to access the customer master key.

Required only if you didn't specify an `accessKeyId` in the
`/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file.  
  
`awsSecretAccessKey`

|

IAM secret access key with permissions to access the customer master key.

Required only if you didn't specify a `secretAccessKey` in the
`/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file.  
  
`awsSessionToken`

|

Token to use when granting temporary AWS security credentials.  
  
`awsRegion`

|

AWS region in which the AWS customer master key exists.

Required only if you didn't specify a `region` in the
`/<dbPath>/cloudProviderCredentials/<keyID>.<cloudProvider>.metadata` file.  
  
`cloudProvider`

|

Your cloud service provider. Value must be `aws`.  
  
`dbpath`

|

Path to the `mongod` data directory for which you want to create a proxy.  
  
`kmipPort`

|

Port on which to run the KMIP proxy.  
  
`mongodPort`

|

Port on which to run the `mongod`.  
  

The KMIP Proxy Standalone generates a KMIP certificate for `localhost` and
writes it to the `dbpath`.

4

### Start a `mongod` process.

Invoke the following command with the specified parameters:

    
    
    mongod --dbpath <dbpath> --port  <mongodPort> --enableEncryption --kmipPort <kmipPort> --kmipServerName 127.0.0.1 --kmipServerCAFile <dbpath>/kmipCA.pem --kmipActivateKeys false --kmipClientCertificateFile <dbpath>/kmipClient.pem  
      
  
Parameter

|

Description  
  
|  
  
`dbpath`

|

Path to the directory where the `mongod` stores its data.  
  
`port`

|

Port on which the `mongod` listens for client connections.  
  
`kmipPort`

|

Port on which the KMIP server listens.  
  
`kmipServerCAFile`

|

Path to the CA File used to validate secure client connection to the KMIP
server.  
  
`kmipActivateKeys`

|

For MongoDB server v5.2 or later, flag that specifies whether to activate or
disable keys for the MongoDB server. Value for this parameter must be `false`
when you start the MongoDB server.  
  
`kmipClientCertificateFile`

|

Path to the client certificate used for authenticating MongoDB to the KMIP
server.  
  
The `mongod` acts as a KMIP server bound to `127.0.0.1` and runs on the
specified `kmipPort`.

5

### Connect to the `mongod` process.

Access your data files by connecting to the `mongod` through the `mongosh`,
MongoDB Compass, or through standard utilities such as mongodump or
mongorestore.

What is MongoDB Atlas? →

