Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Organization Users

Share Feedback

On this page

  * Add Users to an Organization
  * View Active Users and Outgoing Invitations in an Organization
  * Edit User's Role in an Organization
  * Remove Users from an Organization

You can grant Atlas users access to Atlas organizations. Assign user roles to
enforce permission levels for Atlas users.

## Note

### Required Permissions

To perform any of the following actions, you must have the `Organization
Owner` role.

It is recommended that you create a minimum of two users with the
`Organization Owner` role to ensure that access to an organization does not
depend on a single user.

## Add Users to an Organization

## Important

Atlas limits Atlas user membership to a maximum of 500 Atlas users per
organization.

Atlas CLI

Atlas UI

To invite a user to your organization using the Atlas CLI, run the following
command:

    
    
    atlas users invite [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas users invite.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View Active Users and Outgoing Invitations in an Organization

Atlas CLI

Atlas UI

### View Active Users

To list all users in your organization using the Atlas CLI, run the following
command:

    
    
    atlas organizations users list [options]  
      
  
To return the details for a user you specify using the Atlas CLI, run the
following command:

    
    
    atlas users describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas organizations users list and atlas users
describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Pending User Invitations

To list all pending invitations to the organization you specify using the
Atlas CLI, run the following command:

    
    
    atlas organizations invitations list [options]  
      
  
To return the details for one pending invitation to the organization you
specify using the Atlas CLI, run the following command:

    
    
    atlas organizations invitations describe <invitationId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas organizations invitations list and atlas
organizations invitations describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Modify or Cancel a Pending User Invitation

To update one pending invitation to the organization you specify using the
Atlas CLI, run the following command:

    
    
    atlas organizations invitations update [invitationId] [options]  
      
  
To delete one pending invitation to the organization you specify using the
Atlas CLI, run the following command:

    
    
    atlas organizations invitations delete <invitationId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas organizations invitations update and
atlas organizations invitations delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Edit User's Role in an Organization

## Note

You can't edit roles for specific users on the Access Manager page if you
configure role mappings for IdP groups.

To edit a user's role in an organization:

1

### Navigate to the Access Manager page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Access Manager in the sidebar, or click Access Manager in the navigation bar, then click your organization.

2

### If it is not already displayed, click the Users tab.

3

### For the organization user to modify, click Edit Permissions.

4

### Select the new role or roles for the user from the menu.

5

### Click the checkmark to save your changes.

## Remove Users from an Organization

## Note

You cannot remove the last `Organization Owner` from an organization.

To remove a user from an organization:

1

### Navigate to the Access Manager page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Access Manager in the sidebar, or click Access Manager in the navigation bar, then click your organization.

2

### If it is not already displayed, click the Users tab.

3

### Click __to the right of the user to remove.

4

### To confirm a user removal, click Remove User from Organization.

← Manage OrganizationsManage Organization Teams →

