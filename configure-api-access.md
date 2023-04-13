Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Started with the Atlas Administration API

Share Feedback

On this page

  * Required for All Resources: Generate an Organization API Key
  * Required for Select Resources: API Resource Request Access Lists
  * Use API Resources that Require an Access List
  * Require an API Access List for All Requests
  * Grant Programmatic Access to Atlas
  * Manage Programmatic Access to an Organization
  * Manage Programmatic Access to a Project
  * Manage Programmatic Access to Multiple Organizations

## Important

Each Atlas Administration API has its own resources and requires initial
setup. The Atlas Administration API and the App Services Admin API also use
different access keys from the Data API.

You can access the Atlas Administration API servers through the public
internet only. The Atlas Administration API is not available over connections
that use network peering or private endpoints.

To learn more, see APIs.

## Required for All Resources: Generate an Organization API Key

To access the Atlas Administration API, Create an API Key in an Organization.

All API keys belong to the organization. You can give an API key access to a
project. To add the new API key to a project, Invite an Organization API Key
to a Project.

To learn more about managing API keys for your organization or project, see
Grant Programmatic Access to Atlas.

## Required for Select Resources: API Resource Request Access Lists

Atlas allows your API key to make requests from any address on the internet.
Atlas has some exceptions to this rule. These exceptions limit which resources
an API key can use without location-based limits defined in an API access
list.

To add these location-based limits to your API key, create an API access list.
This list limits the internet addresses from which a specific API key can make
API requests.

Any API keys with an API access list require all API requests to come from an
IP address on that list. Your API access list must include entries for all
clients that use the API.

### Use API Resources that Require an Access List

The following API resources require an API access list:

#### Organization API Access List Entries

Create or remove access list entries for an organization API key.

#### Cloud Backup Restores

  * Return a dedicated or serverless cloud backup restore job.

  * Return all dedicated or serverless cloud backup restore jobs.

  * Restore a dedicated or serverless cloud backup snapshot.

  * Cancel the restore of a dedicated or serverless cloud backup snapshot.

#### Cloud Backup Snapshots

Take or remove one replica set or sharded cluster cloud backup snapshot.

#### Cloud Backup Schedules

  * Return the cloud backup schedule for an Atlas cluster.

  * Create or modify the cloud backup schedule for an Atlas cluster.

#### Legacy Backups

  * Restore, remove, or change the expiration date of a legacy backup snapshot.

  * Clear or update legacy backup snapshot schedule.

### Require an API Access List for All Requests

You can require _all_ API requests from an API key to come from an entry on
its API access list. If you require API access lists, API keys can't make any
API requests until you define at least one API access list entry.

#### Procedure

To set your organization to require API access lists for every API key:

1

##### Log in to Atlas.

2

##### Navigate to the Settings page for your organization.

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click the Organization Settings icon next to the Organizations menu.

3

##### Toggle the Require IP Access List for the Atlas Administration API
setting to On.

## Grant Programmatic Access to Atlas

To grant programmatic access to an organization or project using only the API,
create an API key.

  * API keys have two parts: a Public Key and a Private Key. These two parts serve the same function as a username and a personal API key when you make API requests to Atlas.

  * You can't use an API key to log into Atlas through the user interface.

  * You must grant roles to API keys as you would for users to ensure the API keys can call API endpoints without errors.

  * Each API key belongs to only one organization, but you can grant an API key access to any number of projects in that organization.

### Manage Programmatic Access to an Organization

## Note

### Required Permissions

To perform any of the following actions, you must have the `Organization
Owner` role.

#### Create an API Key in an Organization

Atlas CLI

Atlas UI

##### Create an API Key

To create an API key in an organization using the Atlas CLI, run the following
command:

    
    
    atlas organizations apiKeys create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

##### Add an API Access List Entry for the API Key

To create an IP access list entry for your API key using the Atlas CLI, run
the following command:

    
    
    atlas organizations apiKeys accessLists create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists create.

#### View API Keys in an Organization

Atlas CLI

Atlas UI

You can view a list of API keys, the details of an API key, or the access list
for an API key in an organization using the Atlas CLI.

##### View API Keys

To list all API keys in an organization using the Atlas CLI, run the following
command:

    
    
    atlas organizations apiKeys list [options]  
      
  
To return the details for an API key in an organization using the Atlas CLI,
run the following command:

    
    
    atlas organizations apiKeys describe <ID> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas organizations apiKeys list and atlas
organizations apiKeys describe.

##### View API Access List Entries for the API Key

To list IP access list entries for your API key using the Atlas CLI, run the
following command:

    
    
    atlas organizations apiKeys accessLists list <apiKeyID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists list.

#### Change an API Key in an Organization

Atlas CLI

Atlas UI

You can change the roles or access list for an API key in an organization
using the Atlas CLI.

##### Change an API Key's Roles

To update an API key in an organization using the Atlas CLI, run the following
command:

    
    
    atlas organizations apiKeys assign <apiKeyId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys assign.

##### Add an API Access List Entry for the API Key

To create an IP access list entry for your API key using the Atlas CLI, run
the following command:

    
    
    atlas organizations apiKeys accessLists create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists create.

##### Delete an API Access List Entry for the API Key

To delete an IP access list entry for your API key using the Atlas CLI, run
the following command:

    
    
    atlas organizations apiKeys accessLists delete <entry> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists delete.

#### Delete an API Key from an Organization

Atlas CLI

Atlas UI

To delete an API key from an organization using the Atlas CLI, run the
following command:

    
    
    atlas organizations apiKeys delete <ID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys delete.

To delete an access list entry for an API key in an organization, see Change
an API Key in an Organization.

### Manage Programmatic Access to a Project

## Note

### Required Permissions

To perform any of the following actions, you must have the `Project Owner`
role.

#### Invite an Organization API Key to a Project

Atlas CLI

Atlas UI

To assign an API key to a project using the Atlas CLI, run the following
command:

    
    
    atlas projects apiKeys assign <ID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects apiKeys assign.

#### Create an API Key for a Project

Atlas CLI

Atlas UI

To create an API key for your project using the Atlas CLI, run the following
command:

    
    
    atlas projects apiKeys create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects apiKeys create.

After you create the API key for your project, use the Atlas UI to add an API
access list entry. You can't use the API key for the project until you set up
the API access list.

## Note

### Atlas CLI Limitation

You can't edit the API access list for a project API key using the Atlas CLI.

To add an API access list entry using the Atlas UI:

1

##### Add an API Access List Entry.

  1. Click Add Access List Entry.

  2. Enter an IP address from which you want Atlas to accept API requests for this API Key.

You can also click Use Current IP Address if the host you are using to access
Atlas will also make API requests using this API Key.

  3. Click Save.

2

##### Click Done.

#### View the API Keys in a Project

Atlas CLI

Atlas UI

To list all API keys for your project using the Atlas CLI, run the following
command:

    
    
    atlas projects apiKeys list [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects apiKeys list.

You can view the API access list entries for a project API key using an `atlas
organizations` command.

To list IP access list entries for your API key using the Atlas CLI, run the
following command:

    
    
    atlas organizations apiKeys accessLists list <apiKeyID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists list.

#### Change an API Key's Roles in a Project

1

##### Navigate to the Access Manager page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. Select your desired project from the list of projects in the Projects page.

  3. Click the vertical ellipsis ( __) next to your project name in the upper left corner and select Project Settings.

  4. Click Access Manager in the navigation bar, then click your project.

2

##### Click the API Keys tab.

3

##### Edit the Access List.

  1. Click __to the right of the API Key.

  2. Click Edit Permissions.

4

##### Select the new role or roles for the API Key from the Project
Permissions menu.

5

##### Click the __to save.

#### Edit an API Key's Access List

Atlas CLI

Atlas UI

You can edit the API access list entries for a project API key using `atlas
organizations` commands.

##### Add an API Access List Entry for the API Key

To create an IP access list entry for your API key using the Atlas CLI, run
the following command:

    
    
    atlas organizations apiKeys accessLists create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists create.

##### Delete an API Access List Entry for the API Key

To delete an IP access list entry for your API key using the Atlas CLI, run
the following command:

    
    
    atlas organizations apiKeys accessLists delete <entry> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas organizations apiKeys accessLists delete.

#### Delete an API Key from a Project

Atlas CLI

Atlas UI

To delete an API key for your project using the Atlas CLI, run the following
command:

    
    
    atlas projects apiKeys delete <ID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects apiKeys delete.

### Manage Programmatic Access to Multiple Organizations

## Note

### Required Permissions

To perform any of the following actions, you must have the `Organization
Owner` role.

In the organizations and projects hierarchy, an organization can contain
multiple projects (previously referred to as groups). Under this structure:

  * Billing happens at the organization level while preserving visibility into usage in each project.

  * You can view all projects within an organization.

  * You can use teams to bulk assign organization users to projects within the organization.

If you need to scale beyond the existing project limits, you can create
multiple organizations.

#### Create Multiple Organizations

Repeat the following steps to create multiple organizations:

1

##### View all of your organizations.

  1. Expand the Organizations menu in the navigation bar.

  2. Click View All Organizations.

2

##### Click New Organization.

3

##### Enter the name for your organization.

## Important

Don't include sensitive information in your organization name.

4

##### Select Atlas and click Next.

You have the option of adding a new Cloud Manager organization or a new Atlas
organization. For more information on Cloud Manager see the documentation.

5

##### Add members.

  1. For existing Atlas users, enter their username. Usually, this is the email the person used to register.

  2. For new Atlas users, enter their email address to send an invitation.

6

##### Specify the access for the members.

7

##### Click Create Organization.

#### (Optional) Set Up Cross-Organization Billing

You can set up cross-organization billing to share a billing subscription
across multiple organizations.

The following prerequisites and limitations apply:

  * To link a paying organization to another organization, you must have `Organization Billing Admin` or `Organization Owner` privileges for both organizations.

  * A paying organization must have an Atlas subscription.

  * A paying organization and all linked organizations must be in good standing and have no failed payments.

  * A paying organization and any linked organizations must be on the same subscription plan.

  * A paying organization and any linked organizations must have the same minimums, uplifts, and SLA for their subscription plan.

  * A paying organization and any linked organizations can't have an active self-serve support plan.

  * A paying organization and any linked organizations can't have overlapping monthly commitment deals.

  * A paying organization on a prepaid subscription plan and any linked organizations must be on the same current and future subscription plans.

  * You can use the Atlas UI to manually link a paying organization to a maximum of 20 other organizations. To link a paying organization to more than 20 other organizations, contact support.

  * A paying organization can't link more than 100 other organizations.

  * A paying organization can't already be a linked organization.

## Note

To purchase a subscription that enables cross-organization billing, contact
MongoDB Sales.

To configure a paying organization and link other organizations to it:

1

##### Select an organization to configure as a paying organization.

If it is not already displayed, select your desired organization from the
Organizations menu in the navigation bar. If you wish to create a new
organization through which to pay, Create an Organization first.

2

##### Click Billing.

Click Billing in the top navigation bar or in the left navigation panel.

3

##### Click the Linked Organizations tab.

## Note

The Linked Organizations tab only displays if your selected organization is
eligible to be a paying organization for cross-organization billing.

4

##### Start linking.

If you are configuring a new paying organization, click Start Linking.

If your organization is already a paying organization, click Link More
Organizations.

5

##### Select organizations to link to your paying organization.

A dialog displays your selected organization under Paying organization on the
left and a list of organizations you may link to it under Select organizations
to link on the right.

Select each organization you wish to link to your paying organization.

Click Review and Finish.

6

##### Review and finalize your links.

## Important

After you click Finish, you will not be able to unlink organizations unless
you contact Support.

Confirm that your organizations are linked as intended and click Finish.

#### Create API Keys for your Organizations

To manage projects in all your organizations:

1

##### Create an API for each organization.

Repeat the steps to create an API key for an organization for each
organization.

2

##### Invite the organization key to each project within the organization.

For each project within an organization, invite the related organization key.

← Invitations to Organizations and ProjectsView Activity Feed →

