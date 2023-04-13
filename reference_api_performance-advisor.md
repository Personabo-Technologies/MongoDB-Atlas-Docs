Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Query Analysis

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Use the following resources to retrieve existing and suggested indexes for a
deployment, as well as the namespaces on which slow queries were run and the
queries that were slow.

To learn more about slow queries and possible performance improvements, see
Performance Advisor or Query Profiler.

To view field values in a sample query, you must be a user with at least one
of the following project roles:

  * `Project Owner`

  * `Project Data Access Admin`

  * `Project Data Access Read/Write`

  * `Project Data Access Read Only`

Users without one of these roles see redacted data rather than the field
values.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/namespaces

|

Retrieves the namespaces for collections experiencing slow queries for a
specified host.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/slowQueryLogs

|

Get log lines for slow queries that the Performance Advisor and Query Profiler
identified.  
  
`GET`

|

/groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/suggestedIndexes

|

Get suggested indexes that the Performance Advisor identified.  
  
`POST`

|

/groups/{GROUP-ID}/managedSlowMs/enable

|

Enable the Atlas managed slow operation threshold for your project.  
  
`DELETE`

|

/groups/{GROUP-ID}/managedSlowMs/disable

|

Disable the Atlas managed slow operation threshold for your project.  
  
What is MongoDB Atlas? →

