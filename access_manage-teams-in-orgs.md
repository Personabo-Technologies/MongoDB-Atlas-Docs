Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Organization Teams

Share Feedback

On this page

  * Create a Team
  * View Teams
  * Add Team Members
  * Remove Team Members
  * Rename a Team
  * Delete a Team

You can use teams to grant project access roles to multiple users. Add any
number of organization users to a team. Grant a team roles for specific
projects. All members of a team share the same project access.

Organization users can belong to multiple teams.

## Note

### Required Permissions

To perform any of the following actions, you must have the `Organization
Owner` role.

## Create a Team

## Important

Atlas limits the number of users to a maximum of 100 teams per project and a
maximum of 250 teams per organization.

Atlas CLI

Atlas UI

To create one team in your organization using the Atlas CLI, run the following
command:

    
    
    atlas teams create <name> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas teams create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

To add users to your team, see Add Team Members.

## View Teams

Atlas CLI

Atlas UI

To list all teams in your organization using the Atlas CLI, run the following
command:

    
    
    atlas teams list [options]  
      
  
To return the details for the team you specify using the Atlas CLI, run the
following command:

    
    
    atlas teams describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas teams list and atlas teams describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Add Team Members

## Important

Atlas limits Atlas user membership to a maximum of 250 Atlas users per team.

Atlas CLI

Atlas UI

To add one user to the team you specify using the Atlas CLI, run the following
command:

    
    
    atlas teams users add <userId>... [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas teams users add.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Remove Team Members

Atlas CLI

Atlas UI

To delete one user from the team you specify using the Atlas CLI, run the
following command:

    
    
    atlas teams users delete <userId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas teams users delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Rename a Team

## Note

### Atlas CLI Limitation

You can't rename a team using the Atlas CLI.

1

### Navigate to the Access Manager page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Access Manager in the sidebar, or click Access Manager in the navigation bar, then click your organization.

2

### Click the Teams tab.

3

### Rename the team.

For the team you want to rename:

  1. Click the ellipsis (`...`) button under the Actions column.

  2. Click Rename Team.

  3. Enter a new name for the team.

The team name must be unique within the organization.

  4. Click Rename Team.

## Delete a Team

Atlas CLI

Atlas UI

To delete one team from your organization using the Atlas CLI, run the
following command:

    
    
    atlas teams delete <teamId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas teams delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Manage Organization UsersManage Organization Settings →

