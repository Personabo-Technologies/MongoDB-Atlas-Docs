Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Access to the Atlas UI

Share Feedback

On this page

  * Organizations and Projects
  * Users and Teams
  * More Information

To access Atlas, you must have an Atlas user account. If you are an existing
MongoDB Cloud Manager user, you can use your Cloud Manager credentials.

To access an organization or a project within that organization, a user must
be a member of that organization. Depending on the user's role in the
organization, the Atlas user may be required to be a member of the project as
well to access a project.

To access database deployments in a project, users must belong to that
project. Users can belong to multiple projects.

Within an organization, you can group users into teams. Users can belong
multiple teams. Teams can be assigned to multiple projects, and team members'
access to the project is determined by the team's project role.

## Important

Atlas users are separate from database users. Database users can access
MongoDB databases, while Atlas users can access the Atlas application itself.

## Organizations and Projects

Atlas provides a hierarchy based on organizations and projects to facilitate
the management of your Atlas database deployments. Groups are now known as
Projects. You can put multiple Projects under an Organization.

### Organizations

In the organizations and projects hierarchy, an organization can contain
multiple projects (previously referred to as groups). Under this structure:

  * Billing happens at the organization level while preserving visibility into usage in each project.

  * You can view all projects within an organization.

  * You can use teams to bulk assign organization users to projects within the organization.

Previously, users managed deployments by groups, where each group was managed
separately even if a user belonged multiple groups.

## Tip

### See also:

Manage Organization Access

### Projects

Groups are now projects in the organizations and projects hierarchy. With the
organizations projects hierarchy, you can create multiple projects in an
organization.

By having multiple projects within an organization, you can:

  * Isolate different environments (for instance, development/qa/prod environments) from each other.

  * Associate different users or teams with different environments, or give different permissions to users in different environments.

  * Maintain separate cluster security configurations. For example:

    * Create/manage different sets of database user credentials for each project.

    * Isolate networks in different VPCs.

  * Create different alert settings. For example, configure alerts for Production environments differently than Development environments.

#### Database Deployments

Database Deployments are now associated with projects. As before, database
deployments must have unique names within projects.

Each Atlas project supports up to 25 database deployments. Please contact
Atlas support for questions or assistance regarding the database deployment
limit. To contact support, select Support from the left-hand navigation bar of
the Atlas UI.

## Tip

### See also:

  * Manage Project Access

  * Manage Project Settings

  * View All Database Deployments

## Users and Teams

User must be a member of an organization to access the organization or a
project within that organization. Depending on the user's role in the
organization, the Atlas user may be also required to be a member of the
project in order to access a project.

At the organization level, you can group users into teams. You can use teams
to bulk assign organization users to projects within the organization.

## More Information

To learn more about managing access to your Atlas organizations and projects,
see the following pages:

  * Manage Organization Users

  * Manage Organization Teams

  * Manage Access to a Project

  * Manage Programmatic Access to a Project

  * Delete an Atlas Account

← View Database Access HistoryAtlas UI Authentication →

