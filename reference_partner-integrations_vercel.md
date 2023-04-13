Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with Vercel

Share Feedback

On this page

  * Considerations
  * Add a Vercel Integration
  * Manage a Vercel Integration in the Atlas UI

You can connect your Atlas clusters to applications that you deploy using
Vercel.

Use this page to complete the following tasks:

  * Connect Vercel users and teams to organizations in Atlas.

  * Create links from Vercel projects for these users and teams to Atlas clusters.

  * Enable the Atlas Data API.

To connect the serverless functions that you deployed in Vercel to Atlas
clusters, you can also use the MongoDB Node.js driver or the Mongoose ODM
library.

## Considerations

  * Accounts in Vercel (Personal or Team)

  * Vercel Projects

  * IP Access Lists in Atlas and IP Allow Lists in Vercel

### Accounts in Vercel (Personal or Team)

The integration with Vercel requires that you:

  * Create a new personal account or create a new team in Vercel.

  * Use an existing personal or team account in Vercel.

## Note

You can add a Vercel integration as a personal account user and then add
another Vercel integration as a team user. You can't change the scope of an
existing integration from a personal account to a team level account in
Vercel.

To switch from a MongoDB integration for a personal Vercel account to an
integration with a team scope in the same Atlas organization, disconnect an
existing integration in Atlas, and add a new integration with a team scope.

### Projects in Vercel

You can link one Atlas cluster to more than one project in Vercel.

To configure the integration, you must have one or more projects in your
personal or team Vercel account.

The list of Vercel projects that you can choose for the integration depends on
the user or team scope.

### IP Access Lists in Atlas and IP Allow Lists in Vercel

Vercel deployments use dynamic IP addresses.

To connect to an Atlas cluster, the IP access list of your Atlas cluster must
allow all IP addresses (0.0.0.0/0). If Atlas doesn't find an entry for
0.0.0.0/0 in your Atlas project's IP access list, Atlas adds it on your
behalf, as part of the integration workflow.

When you set up the integration, Atlas performs these actions to secure your
Vercel connections to the cluster:

  * Creates a `MONGODB_URI` environment variable that serves as the Atlas cluster's connection string for all Vercel projects that you link this cluster to.

When your application doesn't specify a database, the `MONGODB_URI` variable
uses `/myFirstDatabase` as the default database name. Replace this name with
your database name, or if you use a library to interface with MongoDB, ensure
that your application's code specifies your database name.

  * Creates a database user, `vercel-admin-user`, in the admin database and grants the built-in readWriteAnyDatabase MongoDB database role to all other non system databases in the cluster.

## Add a Vercel Integration

This procedure allows you to create a new account in Atlas with its
organization, project, and user role, and then create a new cluster, or use an
existing Atlas account, organization, project, and Atlas cluster for
integration with Vercel.

To integrate Vercel applications with Atlas clusters, you begin in the Vercel
UI.

1

### Navigate to the MongoDB Atlas integration.

Go to MongoDB Atlas Integration in Vercel and click Add integration.

2

### Choose the scope of your integration (user or team).

  1. Choose one of the Vercel scopes from the drop-down menu:

    * Personal Account

    * Team

After you set the scope for your integration, you can't change it. To switch
to a scope that differs from your chosen scope, disconnect one integration and
create another one using this procedure.

  2. Click Continue.

3

### Select Vercel projects to link to an Atlas cluster.

You can choose specific projects or all projects. You can later edit the
integration to change the projects. The project list depends on the user or
team scope that you specified in the previous step.

Select one of the following options:

  * All Projects

  * Specific Projects

4

### Create your MongoDB Account, if you don't already have one.

  1. Choose one of the following options:

    * If you're using your Google Accounts, follow the steps for signing into it, or create a new Google account.

    * If you're using your email, it's already filled in and grayed out.

    * If your company uses federated authentication, use your company's email address. Proceed with the verification steps required for your federated user access.

    * If you already have an Atlas account, click Log in now. See Log in to Your Atlas Account.

  2. Enter your first and last names, and choose a password. A password must contain at least 8 characters, contain unique characters, numbers, or symbols, and not contain your email address. See Register a new Atlas Account.

  3. Click the checkbox I accept the Privacy Policy and the Terms of Service.

Review the Terms of Service and the Privacy Policy.

5

### Select an Atlas organization to integrate with Vercel.

  1. Select an Atlas organization from the drop-down, or create a new Atlas organization.

  2. Click Continue.

  3. Confirm access to your Atlas organization.

Atlas creates an organization for you. Click I Acknowledge to confirm that you
grant Vercel access to your Atlas organization.

To remove access from this Vercel integration to your MongoDB Atlas
organization, you must disconnect this integration.

  4. Select an Atlas project to integrate with Vercel from the drop-down, or create a new project.

  5. (Optional). Toggle the Enable the Atlas Data API switch. Enabling the Atlas Data API allows you to use HTTPS to connect to the Atlas databases in this organization.

6

### Create a new free tier cluster, or link an existing cluster to one or more
Vercel projects.

Link an existing cluster

Create a new free tier cluster

If you already have an Atlas account, you can choose an existing organization
and project, and then choose an existing cluster.

Ensure that you have the Atlas `Project Owner` role.

  1. Choose an Atlas cluster from the drop-down on the left side of the mapping.

  2. Choose one or more Vercel projects from the drop-down on the right side. You can map one Atlas cluster to one or more Vercel projects. The drop-down menu shows one project, or all projects, depending on what you chose for this integration earlier in this procedure. You can later link more Vercel projects to the same Atlas cluster in this integration.

If the selected project doesn't have the 0.0.0.0./0 entry in the Atlas access
list, Atlas asks you to acknowledge that you are creating an Atlas cluster
with full access due to dynamic IP addresses in Vercel. Atlas sends you an
email with this information.

7

### Click Return to Vercel and review the integration's details.

Atlas sends you a confirmation email with the details of your integration. The
integration window closes and you return to the Vercel UI where you can update
the Vercel projects in this integration.

## Manage a Vercel Integration in the Atlas UI

To manage the integration with Vercel, use the Integrations page for your
organization in Atlas.

1

### Select your organization from the __ Organizations menu in the navigation
bar.

2

### Click Integrations in the sidebar and then select Vercel.

From here, you can perform these tasks:

  * Link additional Atlas clusters with projects in Vercel

  * Edit or remove the linking from your Atlas cluster to one or all projects in Vercel

  * Disconnect your Vercel integration

### Link Additional Atlas Clusters

To link additional clusters in your organization to projects in Vercel, use
the Link clusters button on the Atlas Integrations page for Vercel.

## Note

Use this procedure for an already configured integration. To configure an
initial integration, see Add a Vercel Integration.

1

#### Go to your organization.

Select your organization from the __ Organizations menu in the navigation bar.

2

#### Go to your Vercel integration.

  1. Click Integrations in the sidebar.

  2. Select Vercel.

3

#### Link another Atlas cluster to one or more Vercel projects.

Click Link Clusters.

The Add Another Cluster Link with Vercel window opens and shows your Atlas
organization.

  1. Select an Atlas project.

  2. In the left drop-down list, select a cluster not linked to Vercel. If your project doesn't have another Atlas cluster, you can create one.

  3. In the right drop-down list, select one or more Vercel projects.

  4. (Optional). Toggle the Enable the Atlas Data API switch. Enabling the Atlas Data API allows you to use HTTPS to connect to the Atlas databases in this organization.

  5. Click Save.

You receive a confirmation email from Atlas with the details of your
integration.

A new linked Atlas cluster appears in the linked clusters list.

To link a cluster from another Atlas project in your organization to Vercel,
repeat this procedure for that project.

### Edit or Remove Links to Atlas Clusters

You can add or remove Vercel projects that you linked to an Atlas cluster.

1

#### Go to your Vercel integration.

Click Integrations in the sidebar.

  1. Select Vercel.

2

#### To add or remove some Vercel projects, click __ Edit next to the linked
Atlas project.

Atlas displays existing linked Vercel projects.

  1. Edit existing links, in the right-side list, choosing a project from the drop-down. You can:

    * Click __next to a Vercel project in the list to add it to this cluster's integration.

    * Click __to remove some Vercel projects from this integration.

  2. (Optional). Toggle the Enable the Atlas Data API switch. Enabling the Atlas Data API allows you to use HTTPS to connect to the Atlas databases in this organization.

3

#### To remove links to all Vercel projects, click __ Unlink next to the
linked Atlas project.

Atlas asks you to confirm that you want to unlink the cluster from the
projects. To confirm, click Unlink. Atlas removes the environment variables
for Vercel projects that it created when you linked the projects to an Atlas
cluster.

If you unlink all projects, Atlas behaves as follows. It:

  * Doesn't remove your data, database users, or IP access lists that you created for this integration.

  * Doesn't delete the cluster, or the integration, even though the Atlas UI might show that you have no linked clusters in your integration. To disable the integration, you must disconnect Vercel.

4

#### Click Save.

### Disconnect a Vercel Integration

Before you disconnect Vercel projects from Atlas clusters, to avoid downtime
to any applications connected to the same Atlas clusters, verify that the
cluster's users and network access rules don't share other projects and
applications connected to this Atlas cluster.

1

#### Go to your Vercel integration in the Atlas UI.

  1. Click Integrations in the sidebar.

  2. Select Vercel.

2

#### Click Disconnect Vercel.

In this step, click __to request Atlas to do these optional tasks for you:

  * Delete the database users created as part of this integration

  * Delete the network access rules created as part of this integration

3

#### Confirm that you want to disconnect this Vercel integration.

Atlas asks you to confirm that you want to disconnect your Atlas organization
from Vercel.

Disconnecting the integration may result in downtime for your Vercel
applications and any other applications connecting to the Atlas clusters that
you linked to Vercel.

To confirm, enter the words `Disconnect Vercel` in capital letters and then
click Disconnect Vercel.

Atlas removes the integration by removing the environment variables for Vercel
projects that it created when you linked the projects to an Atlas cluster.

Vercel also removes the integration and it no longer displays in the Vercel
UI.

After you disconnect the Vercel integration, if you haven't deleted users,
access lists, or Atlas Data API keys, you can:

  * Delete database users

  * Delete IP access lists

  * Delete Data API keys

## Note

When you remove an integration in the Vercel UI, Atlas also removes the
integration and you don't need to disconnect the integration in the Atlas UI.

← Explore the MongoDB EcosystemManage Billing →

