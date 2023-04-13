Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Project Alerts

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Procedure

You can use Atlas Kubernetes Operator to configure alerts to help you monitor
access to and the state of the database deployments in your Atlas projects.

To learn more, see Configure Alert Settings.

## Considerations

In your `AtlasProject` Custom Resource, use the
`spec.alertConfigurationSyncEnabled` and `spec.withDefaultAlertsSettings`
settings to manage Atlas alert configurations. The following table describes
the action that Atlas Kubernetes Operator takes based on how you configure
these settings:

spec.alertConfigurationSyncEnabled

|

spec.withDefaultAlertsSettings

|

Behavior  
  
||  
  
 **true**

|

 **true**

|

Atlas Kubernetes Operator creates a project using the default alert
configuration. After Atlas Kubernetes Operator creates the project, the alert
confgurations that you define in your `AtlasProject` Custom Resource override
the alert configurations on Atlas for your project.  
  
 **true**

|

 **false**

|

Atlas Kubernetes Operator creates a project without adding the default alert
configurations. After Atlas Kubernetes Operator creates the project, the alert
confgurations that you define in your `AtlasProject` Custom Resource override
the alert configurations on Atlas for your project.  
  
 **false**

|

 **true**

|

Atlas Kubernetes Operator creates a project using the default alert
configuration. Atlas Kubernetes Operator doesn't syncronize alert definitions
on Atlas with those you define in your `AtlasProject` Custom Resource.  
  
 **false**

|

 **false**

|

Atlas Kubernetes Operator creates a project without adding the default alert
configurations. Atlas Kubernetes Operator doesn't syncronize alert definitions
on Atlas with those you define in your `AtlasProject` Custom Resource.  
  
## Prerequisites

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

To learn more, see Configure Access to Atlas.

## Procedure

To configure project alerts, configure the `AtlasProject` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: TestAlertConfig  
      connectionSecretRef:  
        name: my-atlas-key  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
        - ipAddress: "128.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
      alertConfigurations:  
      - eventTypeName: "REPLICATION_OPLOG_WINDOW_RUNNING_OUT",  
        enabled: true,  
        notifications:  
          -  delayMin: 0  
             emailEnabled: true  
             intervalMin: 60  
             roles: [ "GROUP_OWNER" ]  
             smsEnabled: false  
             typeName: “GROUP”  
          threshold:  
             operator: "LESS_THAN",  
             threshold: 1,  
             units: "HOURS"  
      alertConfigurationSyncEnabled: true  
      withDefaultAlertsSettings: false  
     EOF  
  
The parameters that you must specify in the `AtlasProject` Custom Resource
depend on the alert that you want to configure.

To learn more about the configuration parameters available from the API, see
Alert Configurations.

← Integrate with Third-Party ServicesCustom Resources →

