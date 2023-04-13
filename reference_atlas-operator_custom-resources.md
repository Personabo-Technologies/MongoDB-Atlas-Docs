Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Custom Resources

Share Feedback

On this page

  * Atlas Kubernetes Operator Workflow
  * Create and Update Process
  * Delete Process
  * Use Annotations to Skip or Override Defaults

Atlas Kubernetes Operator supports the following custom resources:

Resource

|

Description  
  
|  
  
`AtlasBackupPolicy` Custom Resource

|

Configuration of a backup policy to back up your cluster Atlas.  
  
`AtlasBackupSchedule` Custom Resource

|

Configuration of a backup schedule to back up your cluster Atlas.  
  
`AtlasDeployment` Custom Resource

|

Configuration of a cluster inside some project in Atlas.  
  
`AtlasDatabaseUser` Custom Resource

|

Configuration of a database user inside some project in Atlas.  
  
`AtlasProject` Custom Resource

|

Configuration of a project in Atlas.  
  
`AtlasTeam` Custom Resource

|

Configuration of a project team in Atlas.  
  
## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

## Atlas Kubernetes Operator Workflow

When you use Atlas Kubernetes Operator, you can create a new Atlas project, or
you can work with an existing Atlas project.

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

### Create and Update Process

Each time you change the `spec` field in any of the supported custom
resources, the following workflow begins in Atlas Kubernetes Operator:

  1. Atlas Kubernetes Operator receives an event about the changed custom resource.

  2. Atlas Kubernetes Operator updates the `status.conditions` field to reflect that the resource is not ready:
    
        conditions:  
      
    - lastTransitionTime: "2021-03-13T16:26:17Z"  
      status: "False"  
      type: Ready  
  
  3. To connect to the Atlas Administration API, Atlas Kubernetes Operator reads the organization ID and API keys from one of the following locations:

    * `spec.connectionSecretRef.name` (if specified in the `AtlasProject` Custom Resource).

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

    * `global` Atlas Kubernetes Operator secret `<operator-deployment-name>-api-key` (if `spec.connectionSecretRef.name` is not specified).

  4. To create or update resources in Atlas, Atlas Kubernetes Operator uses the connection information to make API calls to Atlas.

## Note

Sometimes Atlas Kubernetes Operator makes multiple API calls in Atlas during
the reconciliation of a custom resource. For example, `AtlasProject` has an IP
Access List configuration for calling the matching API.

  5. If any errors occur during the reconciliation, `status.conditions` updates to reflect the error.

## Example

    
        - lastTransitionTime: "2021-03-15T14:26:44Z"  
      
       message: 'POST https://cloud.mongodb.com/api/atlas/v1.0/groups/604a47de73cd8cag77239021/accessList:  
          400 (request "INVALID_IP_ADDRESS_OR_CIDR_NOTATION") The address 192.0.2.1dfdfd5  
          must be in valid IP address or CIDR notation.'  
       reason: ProjectIPAccessListNotCreatedInAtlas  
       status: "False"  
       type: IPAccessListReady  
  
  6. If the update succeeds, `status.conditions` reflects that the resource is ready:
    
        conditions:  
      
    - lastTransitionTime: "2021-03-13T16:26:17Z"  
      status: "True"  
      type: Ready  
  

### Delete Process

If you remove a custom resource from Kubernetes, Atlas Kubernetes Operator
tries to clean the state in Atlas, and the following workflow begins:

  1. Atlas Kubernetes Operator receives an event about the deleted custom resource.

  2. To connect to the Atlas Administration API, Atlas Kubernetes Operator reads the organization ID and API keys from one of the following locations:

    * `spec.connectionSecretRef.name` (if specified in the `AtlasProject` Custom Resource).

## Note

By default, Atlas Kubernetes Operator keeps connection secrets in the same
namespace as the `AtlasProject` Custom Resource. To store secrets in another
namespace, specify the `spec.connectionSecretRef.namespace` parameter.

    * `global` Atlas Kubernetes Operator secret `<operator-deployment-name>-api-key` (if `spec.connectionSecretRef.name` is not specified).

  3. To delete the resource from Atlas, Atlas Kubernetes Operator uses the connection information to make API calls to Atlas.

## Note

Atlas Kubernetes Operator removes any related objects created in Kubernetes.
For example, if you remove `AtlasDatabaseUser`, Atlas Kubernetes Operator
removes the related connection secrets.

### Use Annotations to Skip or Override Defaults

You can use annotations to modify the default behaviour of Atlas Kubernetes
Operator.

If you add the `mongodb.com/atlas-resource-policy: "keep"` annotation to a
custom resource's `metadata`, Atlas Kubernetes Operator won't delete the
resource when you delete the Atlas Kubernetes Operator resource.

 **Example**

    
    
     apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasProject  
    metadata:  
      name: my-project  
      annotations:  
        mongodb.com/atlas-resource-policy: "keep"  
  
If you add the `mongodb.com/atlas-reconciliation-policy: "skip"` annotation to
a custom resource's `metadata`, Atlas Kubernetes Operator doesn't start the
reconciliation for the resource. This annotation lets you pause the sync with
the spec until you remove the annotation. You can use this annotation to make
manual changes to a custom resource and avoid Atlas Kubernetes Operator
undoing them during a sync. When you remove this annotation, Atlas Kubernetes
Operator should reconcile the resource and sync it with the spec.

If you add the `mongodb.com/atlas-resource-version-policy: "allow"` annotation
to a custom resource's `metadata`, Atlas Kubernetes Operator lets you use a
resource even if its version label doesn't match the version of Atlas
Kubernetes Operator that you are using. If your resource version is a major
version that is less than your Atlas Kubernetes Operator version, the latest
features might not work. Minor version discrepancies are backward-compatible.

← Configure Project Alerts`AtlasProject` Custom Resource →

