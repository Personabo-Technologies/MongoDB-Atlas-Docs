Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Access to a Project

Share Feedback

On this page

  * Add Users or Teams to a Project
  * View Who Can Access a Project
  * View User Invitations
  * Cancel or Update User Invitations
  * Remove Users or Teams from a Project
  * Edit a User's or Team's Role in a Project

You can grant Atlas users and teams access to Atlas projects. Assign user
roles to enforce permission levels for Atlas users and teams.

## Note

### Required Permissions

To perform any of the following actions, you must have the `Project Owner`
role.

## Add Users or Teams to a Project

## Important

Adding a user to a project also adds that user to the organization.

Atlas limits the number of teams to a maximum of:

  * 100 teams per project and

  * 250 teams per organization.

Atlas also limits Atlas user membership to a maximum of:

  * 500 per project and

  * 500 per organization, which includes the combined membership of all projects in the organization.

Atlas raises an error if an operation exceeds these limits.

## Example

You have an organization with five projects. Each project has 100 Atlas users.
Each Atlas user belongs to only one project. You cannot add any Atlas users to
this organization or any project in that organization without first removing
existing Atlas users from the organization or project membership.

Atlas CLI

Atlas UI

To using the Atlas CLI, run the following command:

    
    
    atlas accessLists create [entry] [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas accessLists create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View Who Can Access a Project

Atlas CLI

Atlas UI

To list all users in the project you specify using the Atlas CLI, run the
following command:

    
    
    atlas projects users list [options]  
      
  
To list all teams for a project using the Atlas CLI, run the following
command:

    
    
    atlas projects teams list [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas projects users list and atlas projects
teams list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View User Invitations

Atlas CLI

Atlas UI

To list all pending invitations to the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas projects invitations list [options]  
      
  
To return the details for one pending invitation to the project you specify
using the Atlas CLI, run the following command:

    
    
    atlas projects invitations describe <invitationId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas projects invitations list and atlas
projects invitations describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Cancel or Update User Invitations

Atlas CLI

Atlas UI

To using the Atlas CLI, run the following command:

    
    
    atlas accessLists create [entry] [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas accessLists create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Remove Users or Teams from a Project

## Important

Projects must have at least one user or team. You can't delete the last member
(user or team) from the project. You must instead close the project.

You also can't delete the last `Project Owner` (user or team) remaining in the
project. You must first assign the role to at least one other user before
deleting the original user.

Atlas CLI

Atlas UI

To delete a user from a project using the Atlas CLI, run the following
command:

    
    
    atlas projects users delete <ID> [options]  
      
  
To remove a team from the project you specify using the Atlas CLI, run the
following command:

    
    
    atlas projects teams delete <teamId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas projects users delete and atlas projects
teams delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Edit a User's or Team's Role in a Project

## Note

You can't edit roles for specific users on the Access Manager page if you
configure role mappings for IdP groups.

Atlas CLI

Atlas UI

To update roles for a team in the project you specify using the Atlas CLI, run
the following command:

    
    
    atlas projects teams update <teamId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects teams update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

### Atlas CLI Limitation

You can't update a user's role in a project using the Atlas CLI.

← Manage Project AccessManage Project Settings →

