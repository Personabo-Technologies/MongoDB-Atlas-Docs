Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Custom Database Roles

Share Feedback

On this page

  * Add Custom Roles
  * View Custom Roles
  * Modify Custom Roles
  * Delete Custom Roles
  * Assign Custom Roles
  * Considerations

You can create custom roles in Atlas when the built-in roles don't include
your desired set of privileges. Atlas applies each database user's custom
roles together with:

  * Any built-in roles you assign when you add a database user or modify a database user.

  * Any specific privileges you assign when you add a database user or modify a database user.

You can assign multiple custom roles to each database user.

## Note

### Free Cluster, Shared Cluster, and Serverless Instance Limitation

Changes to custom roles might take up to 30 seconds to deploy in `M0` free
clusters, `M2/M5` shared clusters, and serverless instances.

The privilege actions available for custom roles and the custom roles API
represent a subset of the privilege actions available for built-in roles.

To review the list of custom role privileges, see the API reference.

## Add Custom Roles

Atlas CLI

Atlas Administration API

Atlas UI

To create a custom database role for your project using the Atlas CLI, run the
following command:

    
    
    atlas customDbRoles create <roleName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDbRoles create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View Custom Roles

Atlas CLI

Atlas Administration API

Atlas UI

To list all custom database roles for your project using the Atlas CLI, run
the following command:

    
    
    atlas customDbRoles list [options]  
      
  
To return the details for a single custom database role in the project you
specify using the Atlas CLI, run the following command:

    
    
    atlas customDbRoles describe <roleName> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas customDbRoles list and atlas
customDbRoles describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Modify Custom Roles

Atlas CLI

Atlas Administration API

Atlas UI

To update a custom database role for your project using the Atlas CLI, run the
following command:

    
    
    atlas customDbRoles update <roleName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDbRoles update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Delete Custom Roles

Atlas CLI

Atlas Administration API

Atlas UI

To delete a custom database role from your project using the Atlas CLI, run
the following command:

    
    
    atlas customDbRoles delete <roleName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDbRoles delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

You cannot delete a custom role in the following scenarios:

  * When deleting the role would leave one or more child roles with no parent roles or actions.

  * When deleting the role would leave one or more database users with no roles.

## Assign Custom Roles

You can assign custom roles in the Atlas UI when you add a database user or
modify a database user. To assign custom roles through the Atlas
Administration API, see Create a Database User or Update a Database User.

## Considerations

  * You can assign up to 20 custom roles to a single database user and can create up to 100 custom roles per project. If you require more custom roles per database user or per project, contact Atlas support.

  * Atlas rolls back any role modifications not made through the UI or custom roles API. You must use the Atlas UI or API to add, modify, or delete custom roles on Atlas database deployments.

  * Atlas audits the creation, deletion, and updates of custom MongoDB roles in the project's Activity Feed.

  * If you assign multiple roles to a user and those roles grant conflicting permissions for an object, Atlas honors the highest permissions within any role.

## Example

You create two custom roles and assign both to User A:

    * The first custom role grants only `read` privileges on your database. It also grants bypassDocumentValidation on your database.

    * The second role grants `dbAdmin` privileges on your database. It doesn't grant bypassDocumentValidation, which is an implicit denial of bypass permissions.

User A would have all of the `dbAdmin` privileges for your database, since
`dbAdmin` is the higher database access permission. User A would also have
bypassDocumentValidation, since bypassDocumentValidation is the higher bypass
permission.

← Configure Database UsersSet Up Passwordless Authentication with AWS IAM →

