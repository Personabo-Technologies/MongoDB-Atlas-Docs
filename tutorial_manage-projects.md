Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Project Access

Share Feedback

On this page

  * Create a Project
  * View Projects
  * Move a Project
  * Delete a Project

Groups are now projects in the organizations and projects hierarchy.

You can create multiple projects in an organization.

By having multiple projects within an organization, you can:

  * Isolate different environments (for instance, development/qa/prod environments) from each other.

  * Associate different users or teams with different environments, or give different permissions to users in different environments.

  * Maintain separate cluster security configurations. For example:

    * Create/manage different sets of database user credentials for each project.

    * Isolate networks in different VPCs.

  * Create different alert settings. For example, configure alerts for Production environments differently than Development environments.

## Create a Project

### Prerequisites

To create a project for an organization, you must be either an `Organization
Owner` or an `Organization Project Creator`.

When you create a project, you are added as an `Project Owner` for the
project.

### Procedure

Atlas CLI

Atlas UI

To create a new project using the Atlas CLI, run the following command:

    
    
    atlas projects create <projectName> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View Projects

### Prerequisites

To view a project, you must either:

  * Be an `Organization Owner` or `Project Owner`

  * Receive an invitation that grants access to the project. An `Organization Owner` or `Project Owner` can invite users to projects.

### Procedure

Atlas CLI

Atlas UI

To list all projects using the Atlas CLI, run the following command:

    
    
    atlas projects list [options]  
      
  
To return the details for the project you specify using the Atlas CLI, run the
following command:

    
    
    atlas projects describe <ID> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas projects list and atlas projects
describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Move a Project

When you move a project to another Atlas organization, Atlas copies the
project users and their respective roles to the same project in the
destination organization. However, Atlas doesn't carryover teams assigned to
the project because you define teams at the organization level.

When you move projects across organizations, your changes take effect
immediately. The move doesn't:

  * Impact cluster uptime or current cluster configuration.

  * Cause downtime for your database deployment or changes to your connection string.

## Important

Atlas removes existing API Keys after moving the Project. You must create a
new API Key after moving the Project.

### Prerequisites

To move a project to another Atlas organization, you must be an `Organization
Owner` for both the current and the destination organization.

### Procedure

To move a project for an organization:

1

#### View all of your projects.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. Click the Leaf icon in the upper left corner of the page. You can also expand the Projects menu in the navigation bar, then click View All Projects.

2

#### Select the project you want to move.

For the project you want to move:

  1. Click __.

  2. Click Move Project.

The Move Project dialog appears.

3

#### Select the target organization. Click Next: Confirm to go to the
confirmation screen.

4

#### Click Confirm & Move.

## Note

### Billing a Moved Project

An `Organization Owner` of two different Organizations can move projects
between those Organizations at any time. Usage in any particular project
during any particular hour is accrued to the Organization under which the
project was at that time.

## Example

An `Organization Owner` owns the **Telecomm** and **Storage** Organizations in
Atlas. They decide to move their **Backup** project from **Telecomm** to
**Storage** at 11:40 am.

The **Telecomm** project is billed for the full 11:00 to 11:59 am hour.
**Storage** starts getting billed at 12:00 pm.

## Delete a Project

## Note

If you have a Backup Compliance Policy enabled, you can't delete the project
if any snashots exist.

### Prerequisites

  * To delete a project for an organization, you must either have the `Project Owner` role for the project or have the `Organization Owner` role for the project's organization.

  * The project has no outstanding invoices.

  * The project has no active database deployments. Terminate active clusters or serverless instances in the project before you delete it.

  * The project has no configured private endpoint connections.

  * The project has no active federated database instances.

### Procedure

Atlas CLI

Atlas UI

To delete a project using the Atlas CLI, run the following command:

    
    
    atlas projects delete <ID> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas projects delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Manage Organization SettingsManage Access to a Project →

