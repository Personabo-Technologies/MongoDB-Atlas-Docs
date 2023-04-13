Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Audit Logs

Share Feedback

On this page

  * Enable Audit Logs
  * Configure a Custom Auditing Filter

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

You can use Atlas Kubernetes Operator to configure audit logs. To learn more,
see Set Up Database Auditing.

## Note

### Required Privileges

To configure audit logs, you must have the `Organization Owner` role or the
`Project Owner` role for the project that you want to update.

Database auditing lets administrators track system activity for deployments
with multiple users. Atlas administrators can select the actions, database
users, Atlas roles, and LDAP groups that they want to audit. Atlas supports
auditing most of the documented system event actions, with the following
limitations:

  * When an Atlas user performs an action in the Atlas UI on a cluster, both the audit logs and `mongodb.log` file log the `mms-automation` database user as the user performing the auditable auction. However, the Project Activity Feed logs the actual username of the Atlas user responsible for the action.

  * The Atlas audit logs don't track user creation or modification events because Atlas performs these operations directly in the `admin` database.

## Important

### Performing a Full Database Audit

Due to these noted limitations, you must use a combination of audit logs, the
`mongodb.log`, and the Project Activity Feed to perform a full audit.

The `authCheck` event action logs authorization attempts by users trying to
read from and write to databases in the clusters in your project. Atlas audits
the following specific commands:

`authCheck Reads`

|

`authCheck Writes`  
  
|  
  
aggregate

|

aggregate  
  
mapReduce

|

mapReduce  
  
distinct

|

delete  
  
eval [1]

|

eval [1]  
  
count

|

findAndModify  
  
geoNear

|

insert  
  
geoSearch

|

update  
  
group

|

resetError  
  
find

|  
  
getLastError

|  
  
getMore

|  
  
getPrevError

|  
  
parallelCollectionScan [1]

|  
  
[1]|  _(1, 2, 3)_ MongoDB versions 4.2 and later don't support these commands.  
|  
  
Atlas implements the `authCheck` event action as the following four separate
actions:

Event Action

|

Description  
  
|  
  
`authChecksReadFailures`

|

`authCheck` event action for all failed reads with the
auditAuthorizationSuccess parameter set to false. This event action is the
default for read-related event actions.  
  
`authChecksReadAll`

|

`authCheck` event action for all reads, both sucesses and failures. This event
action is the same as `authChecksReadFailures`, but with the
auditAuthorizationSuccess parameter set to true.

## Warning

If you enable auditAuthorizationSuccess, you might severely impact cluster
performance. Enable this option with caution.  
  
`authChecksWriteFailures`

|

`authCheck` event action for all failed writes with the
auditAuthorizationSuccess parameter set to false. This event action is the
default for write-related event actions.  
  
`authChecksWriteAll`

|

`authCheck` event action for all writes, both successes and failures. This
event action is the same as `authChecksWriteFailures`, but with the
auditAuthorizationSuccess parameter set to true.

## Warning

If you enable auditAuthorizationSuccess, you might severely impact cluster
performance. Enable this option with caution.  
  
To learn about how MongoDB writes audit events to disk, see Audit Guarantee in
the MongoDB Manual.

## Enable Audit Logs

## Note

To learn about best practices for auditing the actions of temporary database
users, see Audit Temporary Database Users.

To enable audit logs, set `spec.auditing.enabled` to `true` in the
`AtlasProject` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: TestAuditing  
      connectionSecretRef:  
        name: my-atlas-key  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
        - ipAddress: "128.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
      auditing:  
        enabled: true  
     EOF  
  
To retrieve the audit logs in Atlas, see MongoDB Logs. To retrieve the audit
logs using the API, see Logs.

## Configure a Custom Auditing Filter

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas supports specifying a JSON-formatted audit filter for customizing
MongoDB Auditing.

Custom audit filters lets users forgo the managed Atlas UI auditing filter
builder in favor of hand-tailored granular control of event auditing. Atlas
checks only that the custom filter uses valid JSON syntax, and doesn't
validate or test the filter's functionality.

The audit filter document must resolve to a query that matches one or more
fields in the audit event message. The filter document can use combinations of
query operators and equality conditions to match the desired audit messages.

To view example auditing filters, see Example Auditing Filters. To learn more
about configuring MongoDB auditing filters, see Configure Audit Filter.

## Important

Atlas uses a rolling upgrade strategy for enabling or updating audit
configuration settings across all clusters in the Atlas project. Rolling
upgrades require at least one election per replica set.

To learn more about testing application resilience to replica set elections,
see Test Primary Failover. To learn more about how Atlas provides high
availability, see Atlas High Availability.

To configure a custom auditing filter, specify the `spec.auditing.auditFilter`
setting in the `AtlasProject` Custom Resource. To specify a value for this
setting, you must set `spec.auditing.enabled` to `true`.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: TestAuditing  
      connectionSecretRef:  
        name: my-atlas-key  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
        - ipAddress: "128.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
      auditing:  
        enabled: true  
        auditFilter: "{"atype": "authenticate"}"  
     EOF  
  
To learn more about the configuration parameters available from the API, see
the Atlas Auditing.

← Encrypt Data Using a Key Management ServiceBack Up Your Atlas Cluster →

