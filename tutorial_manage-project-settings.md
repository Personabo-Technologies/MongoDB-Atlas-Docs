Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Project Settings

Share Feedback

On this page

  * Required Access
  * Manage Project Settings

## Required Access

To view project settings, you must have `Project Owner` access to the project.

## Manage Project Settings

Project settings apply to all the users in the project [1]. The Project ID
displayed at the top of the page is used by the Atlas Administration API and
the Atlas CLI.

Atlas CLI

Atlas UI

### Update Project Settings

To update settings for the project you specify using the Atlas CLI, run the
following command:

    
    
    atlas projects settings update [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects settings update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View Project Settings

To return the settings details for the project you specify using the Atlas
CLI, run the following command:

    
    
    atlas projects settings describe [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects settings describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Configure Custom DNS on AWS

Use the following commands to configure custom DNS settings on AWS.

#### Enable Custom DNS on AWS

To enable custom DNS configuration for an Atlas cluster deployed to AWS using
the Atlas CLI, run the following command:

    
    
    atlas customDns aws enable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDns aws enable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### Disable Custom DNS on AWS

To disable custom DNS configuration for an Atlas cluster deployed to AWS using
the Atlas CLI, run the following command:

    
    
    atlas customDns aws disable [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDns aws disable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### Return the Details for Your Custom DNS on AWS

To return the custom DNS configuration of an Atlas cluster deployed to AWS
using the Atlas CLI, run the following command:

    
    
    atlas customDns aws describe [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas customDns aws describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Manage Access to a ProjectInvitations to Organizations and Projects →

