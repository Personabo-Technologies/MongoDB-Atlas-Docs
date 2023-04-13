Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Private Endpoints

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Atlas Kubernetes Operator supports private endpoints to connect to dedicated
clusters and serverless instances.

When you use Atlas Kubernetes Operator to configure private links in Atlas,
Atlas creates its own VPC or a Private Link service and places dedicated
clusters or serverless instances within a region behind a load balancer in the
Atlas VPC or Atlas VNet. To learn more, see the Private Endpoint Overview.

To manage your private endpoints with Atlas Kubernetes Operator, you can
specify and update one of the following parameters:

  * For dedicated clusters, specify the `spec.privateEndpoints` parameter for the `AtlasProject` Custom Resource.

  * For serverless instances, specify the `spec.serverlessSpec.privateEndpoints` parameter for the `AtlasDeployment` Custom Resource.

Each time you change the `spec` field in any of the supported custom
resources, Atlas Kubernetes Operator creates or updates the corresponding
Atlas configuration.

Certain considerations and limitations apply to private endpoints. To learn
more, see Set Up a Private Endpoint.

## Prerequisites

To enable connections with Atlas Kubernetes Operator to Atlas using private
endpoints, you must:

Dedicated Clusters

Serverless Instances

AWS PrivateLink

Azure Private Link

Private Service Connect

  * Have a running Kubernetes cluster with Atlas Kubernetes Operator deployed.

  * Have either the `Project Owner` or `Organization Owner` role in Atlas.

  * Have an AWS user account with an IAM user policy that grants permissions to create, modify, describe, and delete endpoints. For more information on controlling the use of interface endpoints, see the AWS Documentation.

  *  **(Recommended)** : Install the AWS CLI.

  * If you have not already done so, create your VPC and EC2 instances in AWS. See the AWS documentation for guidance.

## Procedure

To enable clients to connect to Atlas dedicated clusters or serverless
instances using private endpoints, see the following procedures:

  * Manage Private Endpoints for Dedicated Clusters

  * Manage Private Endpoints for Serverless Instances

← Configure Access to AtlasManage Private Endpoints for Dedicated Clusters →

