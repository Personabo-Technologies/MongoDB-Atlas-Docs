Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas UI Authorization

Share Feedback

On this page

  * Atlas User Roles
  * Organizations
  * Projects
  * Invitations
  * Programmatic Access

You can manage access to your Atlas database deployments with Atlas User
Roles. You can apply these permissions only on the organization level or the
project level. So, plan the hierarchy of your organizations and projects
carefully.

## Atlas User Roles

Atlas user roles define the actions Atlas users can perform in organizations,
projects, or both. Organization and project `Owners` can manage Atlas users
and their roles within their respective organizations and projects. To learn
more, see Atlas User Roles.

## Organizations

An organization can contain multiple projects (previously referred to as
groups). Under this hierarchy structure:

  * Billing happens at the organization level while preserving visibility into usage in each project.

  * You can view all projects within an organization.

  * You can use teams to bulk assign organization users to projects within the organization.

To learn more, see Manage Organization Access.

## Projects

You can create multiple projects in an organization.

By having multiple projects within an organization, you can:

  * Isolate different environments (for instance, development/qa/prod environments) from each other.

  * Associate different users or teams with different environments, or give different permissions to users in different environments.

  * Maintain separate cluster security configurations. For example:

    * Create/manage different sets of database user credentials for each project.

    * Isolate networks in different VPCs.

  * Create different alert settings. For example, configure alerts for Production environments differently than Development environments.

To learn more, see Manage Project Access.

## Invitations

The Invitations tab allows you to view and accept pending invitations to Atlas
organizations and projects. To learn more, see Invitations to Organizations
and Projects.

## Programmatic Access

To grant programmatic access to an organization or project using only the API,
you can create an API key for the Atlas Administration API. To learn more, see
Grant Programmatic Access to Atlas.

← Legacy Two-Factor AuthenticationAtlas User Roles →

