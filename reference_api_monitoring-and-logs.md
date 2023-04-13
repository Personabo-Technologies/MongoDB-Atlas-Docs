Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Monitoring and Logs

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The following resources provide access to cluster monitoring and logging data.
Each resource requires at minimum your Project ID.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/processes

|

Get all processes for the specified group.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}

|

Get information for the specified process in the specified group.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}/measurements

|

Get measurements for the specified host.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}/databases

|

Get the list of databases for the specified host.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}/databases/{DATABASE-
NAME}/measurements

|

Get measurements of the specified database for the specified host.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks

|

Get the list of disks or partitions for the specified host.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks/{DISK-NAME}/measurements

|

Get measurements of specified disk for the specified host.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{HOSTNAME}/logs/mongodb.gz

|

Get the log file for a host in the cluster.  
  
What is MongoDB Atlas? →

