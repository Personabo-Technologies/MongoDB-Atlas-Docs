Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Kubernetes Operator

Share Feedback

On this page

  * What is Atlas Kubernetes Operator?
  * What Can You Do?
  * Get Hands-On Experience with Atlas Kubernetes Operator

## What is Atlas Kubernetes Operator?

Atlas Kubernetes Operator is a new service that integrates Atlas resources
with your Kubernetes cluster. You can now deploy and manage the lifecycle of
your cloud-native applications that need data services in a single control
plane with secure enterprise platform integration.

To learn more, see Quick Start.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

## What Can You Do?

You can use Atlas Kubernetes Operator to manage resources in Atlas without
leaving Kubernetes. You deploy Atlas Kubernetes Operator into Kubernetes
clusters. Atlas Kubernetes Operator manages resources in Atlas based on
Kubernetes custom resources. It ensures that the state of the projects,
database deployments, and database users in Atlas matches the configurations
in each `AtlasProject` Custom Resource, `AtlasDeployment` Custom Resource, and
`AtlasDatabaseUser` Custom Resource that you create in your Kubernetes
cluster.

Atlas Kubernetes Operator supports many advanced features within the Custom
Resources, such as X509 authentication, private endpoints in Azure and AWS,
and advanced multi-cloud and multi-region clusters.

## Get Hands-On Experience with Atlas Kubernetes Operator

Goal

|

Action  
  
|  
  
Create your first cluster in Atlas with Atlas Kubernetes Operator.

|

See one of the following tutorials:

  * Quick Start

  * Helm Charts Quick Start

  
  
Configure Atlas Kubernetes Operator access to Atlas.

|

See Configure Access to Atlas.  
  
Manage resources.

|

See Custom Resources.  
  
Set up X509 authentication.

|

Configure the `AtlasProject` Custom Resource and `AtlasDatabaseUser` Custom
Resource.  
  
Manage private endpoints.

|

  * For dedicated clusters, specify the `spec.privateEndpoints` parameter for the `AtlasProject` Custom Resource.

  * For serverless instances, specify the `spec.serverlessSpec.privateEndpoints` parameter for the `AtlasDeployment` Custom Resource.

  
  
Set up network peering.

|

Configure the `AtlasProject` Custom Resource.  
  
Set up unified access for an AWS IAM role.

|

Configure the `AtlasProject` Custom Resource.  
  
Create or update custom database roles.

|

Configure the `AtlasProject` Custom Resource.  
  
Encrypt data at rest using a key management service.

|

Configure the `AtlasProject` Custom Resource and the `AtlasDeployment` Custom
Resource.  
  
Set up database auditing.

|

Configure the `AtlasProject` Custom Resource.  
  
Set up cloud backup.

|

Configure the `AtlasBackupPolicy` Custom Resource, `AtlasBackupSchedule`
Custom Resource, and `AtlasDeployment` Custom Resource.  
  
Set up teams.

|

Configure the `AtlasTeam` Custom Resource and `AtlasProject` Custom Resource.  
  
Configure the maintenance window during which Atlas starts weekly maintenance
on your database deployments.

|

Configure the `AtlasProject` Custom Resource.  
  
Integrate with third-party services.

|

Configure the `AtlasProject` Custom Resource.  
  
← Integrate Products and ServicesQuick Start →

