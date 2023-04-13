Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Kubernetes Operator Changelog

Share Feedback

On this page

  * Atlas Kubernetes Operator 1.7.0
  * Atlas Kubernetes Operator 1.6.1
  * Atlas Kubernetes Operator 1.6.0
  * Atlas Kubernetes Operator 1.5.0
  * Atlas Kubernetes Operator 1.4.1
  * Atlas Kubernetes Operator 1.4.0
  * Atlas Kubernetes Operator 1.3.0
  * Atlas Kubernetes Operator 1.2.0
  * Atlas Kubernetes Operator 1.1.0
  * Atlas Kubernetes Operator 1.0.0
  * Atlas Kubernetes Operator 0.8.0
  * Atlas Kubernetes Operator 0.5.0

## Note

You can find the full list of Atlas Kubernetes Operator releases here.

## Atlas Kubernetes Operator 1.7.0

  * Adds Openshift 4.12 compatibility.

  * Supports Kubernetes 1.25.

`AtlasProject` Custom Resource:

  * A project can now refer to a connection secret in a different namespace with the `spec.connectionSecretRef.namespace` parameter.

  * Supports multiple private endpoints per a single provider and region.

  * Supports storing all private endpoint connection strings.

  * Fixes an issue with Google Cloud KMS for the Encryption at Rest feature.

`AtlasDeployment` Custom Resource:

  * Deprecates the `autoIndexingEnabled` field.

  * Supports snapshot distribution.

## Atlas Kubernetes Operator 1.6.1

`AtlasProject` Custom Resource:

  * Fixes an issue with an IP access list.

`AtlasDeployment` Custom Resource:

  * Fixes reconciliation for the `AtlasBackupSchedule` Custom Resource.

## Atlas Kubernetes Operator 1.6.0

### New Features

`AtlasProject` Custom Resource:

  * Adds an optional `--operatorVersion` parameter. To learn more, see Import Atlas Projects into Atlas Kubernetes Operator.

  * Sets finalizers and support labels for `AtlasBackupSchedule` Custom Resource, `AtlasBackupPolicy` Custom Resource, and Atlas teams custom resources.

`AtlasDeployment` Custom Resource:

  * Adds support for Global Cluster parameters in `spec.advancedDeploymentSpec.*` and `spec.deploymentSpec.*`. To learn more, see AtlasDeployment custom resource parameters. These Global Cluster parameters map zones to geographic regions and allow you to add labels. For a full list of available parameters, see the Atlas Global Clusters API.

  * The Atlas Kubernetes Operator image now supports ARM64.

## Atlas Kubernetes Operator 1.5.0

### New Features

`AtlasProject` Custom Resource:

  * Adds Atlas Teams support.

`AtlasDeployment` Custom Resource:

  * Adds serverless private endpoint support.

### Fixes

  * Fixes an issue with connection secret creation.

  * Fixes the minimum version of Openshift.

`AtlasProject` Custom Resource:

  * Fixes the `InstanceSize` must match issue.

  * Ensures private endpoints are always added to the status.

`AtlasDeployment` Custom Resource:

  * Converts the `OplogMinRetentionHours` field properly.

## Atlas Kubernetes Operator 1.4.1

### New Features

  * Updates the minimum required Openshift version to 4.8.

`AtlasProject` Custom Resource:

  * Adds support for custom database roles via the `spec.customRoles` field.

## Atlas Kubernetes Operator 1.4.0

### New Features

`AtlasProject` Custom Resource:

  * Adds support for audit logs. You can enable auditing with the `spec.auditing.enabled` field. For more information about Atlas Kubernetes Operator auditing, see Configure Audit Logs.

  * Adds support for project settings via the `spec.settings` field.

  * Adds support for alert configurations via the `spec.alertConfigurations` field.

`AtlasDeployment` Custom Resource:

  * Adds support for autoscaling of the `instanceSize` and `diskSizeGB` parameters.

### Fixes

  * Fixes an issue where adding an IP address with CIDR block `/32` to Network Access could leave the IP Access List inactive indefinitely.

  * Fixes an issue where creating project integrations that require namespace references could result in errors when the user provides a namespace other than the project namespace, or does not provide a namespace.

## Atlas Kubernetes Operator 1.3.0

### New Features

`AtlasProject` Custom Resource:

  * Adds support for network peering via the `spec.networkPeers` field.

  * Adds support for cloud provider access via the `spec.cloudProviderAccessRoles` field.

  * Adds support for encryption at rest via the `spec.encryptionAtRest` field.

`AtlasDeployment` Custom Resource:

  * Adds a test to ensure that deleting a CRD does not affect `AtlasDeployment` Custom Resources with the `mongodb.com/atlas-resource-policy: "keep"` annotation.

### Fixes

  * Fixes a resource reconciliation issue that occured when you delete an `AtlasDeployment` Custom Resource after the API key has expired.

  * Fixes an issue where you could change the `instanceSize` and `diskSizeGB` parameters for deployments with autoscaling enabled. To change the `instanceSize` and `diskSizeGB` parameters, you must first disable autoscaling.

  * Fixes an error message that returns when Atlas Kubernetes Operator can't delete a project's backup policy or backup schedule.

## Atlas Kubernetes Operator 1.2.0

### New Features

  * Upgrades Go to 1.18.

  * Adds support for Private Endpoints backwards sync to the AtlasProject Custom Resource.

### Fixes

  * Fixes an issue where the AtlasDeployment Custom Resource was not created successfully when the instance size for a deployed resource changed from M10 to M40.

  * Fixes an issue where creating an AtlasDeployment Custom Resource with `advancedDeploymentSpec` failed with `autoscaling.diskGBEnabled` and adds a new `AdvancedAutoScalingSpec` struct to `AdvancedDeploymentSpecChanges`.

  * Fixes an issue where you could decrease `diskSizeGB` for deployments with autoscaling enabled. To change the `diskSizeGB` parameter, you must first disable autoscaling.

  * Fixes a resource reconciliation issue where the Atlas API returns an empty object for scheduled backups.

## Atlas Kubernetes Operator 1.1.0

### New Features

  * Adds support for `maintenance windows`.

### Fixes

  * Fixes an issue where private endpoint connection strings were missing from Kubernetes secrets.

  * Fixes an issue where Atlas Kubernetes Operator didn't remove conditions for unused resources.

  * Adds missing private endpoint fields to Pod conditions.

## Atlas Kubernetes Operator 1.0.0

### Breaking Changes

  * Renames the `AtlasCluster` Custom Resource to the `AtlasDeployment` Custom Resource.

  * Renames `spec.clusterSpec` to `spec.deploymentSpec`.

  * Renames `spec.advancedClusterSpec` to `spec.advancedDeploymentSpec`.

### New Features

  * Adds log levels and JSON log output for Atlas Kubernetes Operator. To change the log level, you can provide the `—log-level=debug | info | warn | error | dpanic | panic | fatal` flag. To change the output format, you can provide the `—log-encoder=json | console` flag.

`AtlasProject` Custom Resource:

  * Supports third-party integrations including Prometheus integrations.

  * Supports GCP private endpoints.

`AtlasDeployment` Custom Resource:

  * Supports serverless instances via the `spec.serverlessSpec` field.

  * Supports scheduled backups for database deployments.

  * Supports upgrading `M0`, `M2`, and `M5` clusters to `M10+` clusters via the `spec.deploymentSpec.providerSettings.instanceSizeName` parameter.

  * Supports advanced options via the `spec.processArgs` object.

  * Supports omitting the `spec.deploymentSpec.providerSettings.providerName` field for `M0`, `M2`, and `M5` clusters.

  * Supports omitting the `spec.serverlessSpec.providerSettings.providerName` field for serverless instances.

### Fixes

  * Fixes a bug where you couldn't delete the `AtlasProject` Custom Resource if the credentials secret was deleted.

  * Resolves missing epoch timestamps in log messages.

  * Fixes a bug with the incorrect user-agent version.

  * Fixes an improper signature verification with the `golang.org/x/crypto/ssh` module.

## Atlas Kubernetes Operator 0.8.0

### Changes

  * Upgrades the Controller Runtime to v0.11.0.

  * Upgrades Go to 1.17.

  * When you install a cluster using Helm Charts, Helm doesn't exit until the cluster is ready if you set `postInstallHook.enabled` to true.

  * Atlas Kubernetes Operator watches secrets only with the label `atlas.mongodb.com/type=credentials` to avoid watching unnecessary secrets.

  * Supports the `mongodb.com/atlas-reconciliation-policy=skip` annotation for configuring Atlas Kubernetes Operator to skip reconciliations on specific resources.

  * Supports X.509 authentication.

### Bug Fixes

  * Fixes an issue that logged errors for resource deletion.

### `AtlasProject` Custom Resource

#### Changes

  * Atlas Kubernetes Operator no longer marks the `AtlasProject` Custom Resource as ready until the project IP access is successfully created.

### `AtlasCluster` Custom Resource

#### Changes

  * Adds the `spec.advancedClusterSpec` parameter to the AtlasCluster custom resource. The `AtlasCluster` custom resource now has two main configuration options. You must specify either `spec.clusterSpec` or `spec.advancedClusterSpec`. The `spec.clusterSpec` parameter uses the Atlas Cluster API Resource. The `spec.advancedClusterSpec` parameter uses the Atlas Advanced Cluster API Resource.

## Note

To migrate an existing resource to use the `spec.clusterSpec` structure, you
must move all fields currently under `spec.*` to `spec.clusterSpec.*` with the
exception of `spec.projectRef`.

 _You can find the images in the following location:_

https://quay.io/repository/mongodb/mongodb-atlas-operator

## Atlas Kubernetes Operator 0.5.0

This Atlas Kubernetes Operator trial release lets you manage Atlas projects,
clusters, and database users with Kubernetes specifications.

### Changes

  * Introduces `Global` and `per project` Atlas authentication modes. To learn more, see Configure Access to Atlas.

  * Supports installing Atlas Kubernetes Operator clusterwide (all the namespaces in the Kubernetes cluster) or to its own namespace. To learn more, see Quick Start.

  * Introduces the `AtlasProject` Custom Resource. Use this resource to create Atlas projects and configure their IP access lists.

  * Introduces the AtlasCluster custom resource. Use this resource to create clusters in an Atlas project.

  * Introduces the `AtlasDatabaseUser` Custom Resource for creating database users in an Atlas project.

  * Allows you to create or update secrets for each database user and cluster. Applications can use these secrets in Kubernetes to connect to Atlas clusters.

