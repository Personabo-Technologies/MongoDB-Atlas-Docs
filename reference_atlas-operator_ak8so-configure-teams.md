Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Teams

Share Feedback

On this page

  * Limitations
  * Prerequisites
  * Procedure
  * Create the team.
  * Grant the team access to a project.

Atlas Kubernetes Operator supports teams for controlling access to your Atlas
projects.

You can use teams to grant project access roles to multiple users. Add any
number of organization users to a team. Grant a team roles for specific
projects. All members of a team share the same project access.

Organization users can belong to multiple teams.

To manage teams with Atlas Kubernetes Operator, specify and update the
following custom resources:

Custom Resource

|

Purpose  
  
|  
  
`AtlasTeam` Custom Resource

|

Defines the team name and the users who belong to it.  
  
`AtlasProject` Custom Resource

|

Defines the team's access roles for this project. You must set the
`spec.teams.teamRef.name` field to match the `metadata.name` of the
`AtlasTeam` Custom Resource to assign the team to this project.  
  
Each time you change any of the supported custom resources, such as updating
or removing a team, Atlas Kubernetes Operator creates or updates the
corresponding Atlas configuration.

## Limitations

You must assign the team to a project by configuring both the `AtlasTeam`
Custom Resource and the `AtlasProject` Custom Resource for the team to appear
in the Atlas UI.

For other limitations that apply to teams, see Manage Organization Teams.

## Prerequisites

To enable teams for your Atlas Kubernetes Operator-managed cluster, you must:

  * Have a running Kubernetes cluster with Atlas Kubernetes Operator deployed.

  * Ensure your IP address is in the organization's API access list.

## Procedure

Follow these steps to enable teams for your Atlas Kubernetes Operator-managed
projects:

1

### Create the team.

Create an `AtlasTeam` Custom Resource for each team using the following
example. Specify a `metadata.name` so that you can reference this file from
the `AtlasProject` Custom Resource and a `spec.name` so you can differentiate
this team from other teams in your organization.

Add only users who are part of the organization.

To learn more about the parameters for a team, see the `AtlasTeam` Custom
Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
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
     EOF  
  
2

### Grant the team access to a project.

To assign this team to a project, set the `spec.teams.teamRef.name` field in
the `AtlasProject` Custom Resource to match the `metadata.name` from the
previous step.

In the `spec.teams.teamRef.roles` field, specify the team's Atlas User Roles
for this project.

You can add more than one team. The following example shows two teams with
different access roles for the same project.

To learn about the other parameters for a team, see `AtlasProject` Custom
Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test project  
      teams:  
        - teamRef:  
            name: green-leaf-team  
          roles:  
          - GROUP_OWNER  
        - teamRef:  
            name: no-leaf-team  
          roles:  
          - GROUP_CLUSTER_MANAGER  
          - GROUP_DATA_ACCESS_ADMIN  
      
    EOF  
  
← Set Up Unified Cloud Provider AccessConfigure Custom Database Roles →

