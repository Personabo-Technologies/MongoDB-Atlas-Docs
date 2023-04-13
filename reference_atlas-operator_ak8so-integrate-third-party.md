Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with Third-Party Services

Share Feedback

On this page

  * Prerequisites
  * Procedure

You can use Atlas Kubernetes Operator to integrate Atlas with third-party
services to:

  * Receive Atlas alerts in various third-party services.

  * View and analyze performance metrics that Atlas collects about your cluster.

To learn more, see Integrate with Third-Party Services.

## Note

Currently, serverless instance metrics don't support any third-party services
(for example, Datadog).

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

To integrate Atlas with a third-party service, configure the `AtlasProject`
Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: TestDatadogIntegration  
      connectionSecretRef:  
        name: my-atlas-key  
      projectIpAccessList:  
        - ipAddress: "0.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
        - ipAddress: "128.0.0.0/1"  
          comment: "Everyone has access. For test purposes only."  
      integrations:  
        - type: "DATADOG"  
          apiKeyRef:  
            name: key-name  
            namespace: key-namespace  
          region: "US"  
     EOF  
  
The parameters that you must specify in the `AtlasProject` Custom Resource
depend on the third-party service that you want to configure:

Service

|

Settings  
  
|  
  
All

|

  * `spec.integrations.type`

  
  
Datadog

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.apiKeyRef.namespace`

  * `spec.integrations.region`

  
  
Flowdock

|

  * `spec.integrations.apiTokenRef.name`

  * `spec.integrations.apiTokenRef.namespace`

  * `spec.integrations.flowName`

  * `spec.integrations.orgName`

  
  
Microsoft Teams

|

  * `spec.integrations.microsoftTeamsWebhookURL`

  
  
Opsgenie

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.apiKeyRef.namespace`

  * `spec.integrations.region`

  
  
PagerDuty

|

  * `spec.integrations.serviceKeyRef.name`

  * `spec.integrations.serviceKeyRef.namespace`

  
  
Prometheus

|

  * `spec.integrations.enabled`

  * `spec.integrations.passwordRef.name`

  * `spec.integrations.passwordRef.namespace`

  * `spec.integrations.scheme`

  * `spec.integrations.serviceDiscovery`

  * `spec.integrations.username`

  
  
Slack

|

  * `spec.integrations.apiTokenRef.name`

  * `spec.integrations.apiTokenRef.namespace`

  
  
VictorOps

|

  * `spec.integrations.apiKeyRef.name`

  * `spec.integrations.routingKeyRef.name`

  * `spec.integrations.routingKeyRef.namespace`

  
  
Webhook Settings

|

  * `spec.integrations.secretRef.name`

  * `spec.integrations.secretRef.namespace`

  * `spec.integrations.url`

  
  
For another example, see Prometheus Example.

## Note

Atlas Kubernetes Operator offers a sample Grafana dashboard that you can
import into Grafana.

To learn more about the configuration parameters available from the API, see
the Atlas Third-Party Integration Settings.

← Back Up Your Atlas ClusterConfigure Project Alerts →

