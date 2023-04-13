Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasTeam` Custom Resource

Share Feedback

On this page

  * Example
  * Parameters

The `AtlasTeam` custom resource defines a team of Atlas users. To give this
team access to one or more projects, you must reference the `AtlasTeam` custom
resource from the `AtlasProject` Custom Resource and configure access roles
for the team.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

Atlas Kubernetes Operator does one of the following actions using the Atlas
Teams API Resource:

  * Creates a new team.

  * Updates an existing team.

## Example

The following example shows an `AtlasTeam` custom resource that defines the
`green-leaf-team`, comprised of four users. This custom resource must be
referenced from the `AtlasProject` Custom Resource before this team can access
an Atlas project:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasTeam  
    metadata:  
      name: green-leaf-team  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: "greenLeafTeam"  
      usernames:  
        - "atlas.user1@example.com"  
        - "atlas.user2@example.com"  
        - "atlas.user3@example.com"  
        - "atlas.user4@example.com"  
  
## Parameters

This section describes the `AtlasTeam` custom resource parameters available.

`metadata.name`

    

 _Type_ : string

 _Required_

Name that the `AtlasProject` Custom Resource uses to add this team to a
project.

`metadata.namespace`

    

 _Type_ : string

 _Optional_

Namespace other than `default` that you want to contain the `atlasTeam` custom
resource. If you define a custom namespace, you must add it to the
`AtlasProject` Custom Resource in the `spec.teams.teamRef.namespace` field.

`spec.name`

    

 _Type_ : string

 _Required_

Human-readable label that identifies your team. This name appears wherever you
view, add, or edit teams to help you differentiate between multiple teams.

`spec.usernames`

    

 _Type_ : string

 _Required_

List that contains the Atlas usernames for the members of this team.

← `AtlasBackupSchedule` Custom ResourceProduction Notes →

