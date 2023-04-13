Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Import Atlas Projects into Atlas Kubernetes Operator

Share Feedback

On this page

  * Overview
  * Compatibility
  * Examples
  * Applying the Configuration

If you have existing Kubernetes deployments and wish to start using Atlas
Kubernetes Operator, you can use the Atlas CLI to export Atlas projects,
deployments, and database users with the new `atlas kubernetes config
generate` command.

With this command, you can export your configuration in an Atlas Kubernetes
Operator-compatible format. Once exported, you can import this configuration
into the Kubernetes or Openshift cluster on which Atlas Kubernetes Operator
runs.

## Overview

The `atlas kubernetes config generate` command outputs a `.yaml` configuration
to `stdout` which includes the following Atlas Kubernetes Operator resources:

  * An `AtlasDeployment` Custom Resource

  * An `AtlasBackupSchedule` Custom Resource

  * An `AtlasBackupPolicy` Custom Resource

  * An `AtlasProject` Custom Resource

  * An `AtlasDatabaseUser` Custom Resource

  * An `AtlasTeam` Custom Resource

  * Optionally with `--includeSecretsData`, an Atlas credentials secret. These credentials will be imported as plain text.

The command takes the following parameters:

Parameter

|

Description  
  
|  
  
`--projectId`

|

The ID of the Atlas project to export. If you do not set this explicitly, it
will default to the `projectId` value in your `atlascli` configuration file.
Required.  
  
`--clusterName`

|

A comma-separated list of names of the clusters to export. These must be
clusters in the project specified in the `projectId` parameter. If you don't
pass in this parameter, the command exports all clusters in the specified
project. Optional.  
  
`--includeSecrets`

|

Populates an entry in the configuration file for an Atlas credentials secret.
If you don't pass in this parameter, the command creates a secret, but does
not populate it with data.  
  
`--targetNamespace`

|

The Kubernetes namespace to export resources to. The command fills the
`metadata.namespace` field of each exported Atlas entity with the value of
this parameter. Required.  
  
`--operatorVersion`

|

The version of Atlas Kubernetes Operator for which to export your files. If
omitted, the command exports files compatible with Atlas Kubernetes Operator
v1.5.1. Optional.  
  
## Compatibility

`atlascli` exports configurations from Atlas in a format that is version-
dependent on Atlas Kubernetes Operator. The following table describes which
versions of `atlascli` support which versions of Atlas Kubernetes Operator:

`atlascli` version

|

Atlas Kubernetes Operator versions  
  
|  
  
1.4.0

|

1.5.0  
  
## Examples

The following examples assume a project named `sampleProject`, with clusters
named `sample1`, `sample2`, and `sample3`, a Project ID of
63500d1139dd494b92fe4376, and a target namespace of `sampleNamespace`.

To export the entire project, including all Atlas deployments and secrets with
credentials, run the following command:

    
    
    atlas kubernetes config generate --projectId=63500d1139dd494b92fe4376 \  
      
    --includeSecrets --targetNamespace=sampleNamespace  
  
To export two specific Atlas deployments from the project without secret
credentials, run the following command:

    
    
    atlas kubernetes config generate --projectId=63500d1139dd494b92fe4376 \  
      
    --clusterName=sample1,sample2 --targetNamespace=sampleNamespace  
  
In either of the above examples, you can apply the generated configuration to
your Kubernetes or Openshift cluster by piping the output into the `kubectl
apply` command. The following example illustrates this with the above command:

    
    
    atlas kubernetes config generate --projectId=63500d1139dd494b92fe4376 \  
      
    --clusterName=sample1,sample2 --targetNamespace=sampleNamespace \  
    | kubectl apply -f -  
  
Alternatively, you can save the generated configuration by redirecting
`stdout` to a `.yaml` file. The following command imports a single Atlas
deployment from the project without secret credentials and saves the output to
`myAtlasProject.yaml`.

    
    
    atlas kubernetes config generate --projectId=63500d1139dd494b92fe4376 \  
      
    --clusterName=sample3 --targetNamespace=sampleNamespace \  
    > myAtlasProject.yaml  
  
## Applying the Configuration

To apply the generated configuration to your Kubernetes or Openshift cluster
in this scenario, pass the `.yaml` file as an argument to the `kubectl apply`
command.

    
    
    kubectl apply -f myAtlasProject.yaml  
      
  
← CompatibilityConfigure Access to Atlas →

