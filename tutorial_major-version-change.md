Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Upgrade Major MongoDB Version for a Cluster

Share Feedback

On this page

  * Considerations
  * Procedure
  * Support for Major Version Upgrades

Atlas enables you to upgrade the major version of an Atlas cluster at any time
by modifying the cluster.

This procedure guides you through creating a staging cluster for the purpose
of testing your applications against the new MongoDB version. While optional,
we strongly recommend using this procedure to ensure your production
application experiences the smoothest possible transition to the new MongoDB
version.

## Considerations

There are a few things to be aware of before starting the upgrade procedure:

  * Your cluster must be in a healthy state before upgrading.

  * You can only upgrade your Atlas cluster one major version at a time. You cannot skip any major versions when upgrading your cluster.

  * Each major version contains some features which may not be backward-compatible with previous versions. When upgrading to a new major version, check the Release Notes for changes which may affect your applications.

  * After upgrading the MongoDB major version, you will not be able to downgrade to previous versions.

  * As of MongoDB version 4.2, Legacy Backups are deprecated in favor of Cloud Backups. When you upgrade to version 4.2 or later, your backup system upgrades to cloud backup if it is currently set to legacy backup. After this upgrade:

    * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

    * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

  * If the FCV of your cluster is set and if the FCV is below the MongoDB version of your cluster, the cluster in the Atlas UI Database Deployments page shows the `FCV` of your cluster to reflect the features that are currently available on your cluster during the upgrade. After Atlas upgrades your cluster to the new version, the cluster in the Atlas UI Database Deployments page shows the new MongoDB version of your cluster.

## Procedure

1

### Log into Atlas.

Once you log in, open your organization and find your project.

## Important

The Atlas user you log in as _must_ have the `Project Owner` role in the Atlas
project that contains the cluster you want to upgrade.

2

### Create an Atlas cluster for your staging environment.

## Note

You can skip this step if you already have an Atlas cluster as your staging
environment.

  1. If the Database Deployments page is not already displayed, click Database in the sidebar.

  2. In the Database Deployments view, click the Create button to open the cluster creation modal. Configure the staging cluster to match your production cluster. You do not have to enable backups for the staging cluster.

To learn how to create a new cluster, see Create a Cluster.

## Important

If selecting a smaller cluster tier for the staging cluster, take into
consideration that any performance tests run may not be representative of the
performance of the upgraded production cluster. You may also need to select a
larger storage size depending on the amount of data you want to mirror to your
staging cluster.

3

### Refresh the staging cluster with production cluster data.

## Note

You can skip this step if you already have an up-to-date Atlas cluster as a
staging environment.

If you have backups enabled for the production cluster, restore the most
recent snapshot and choose the staging cluster as the destination.

If you do _not_ have backups enabled for the production cluster, use Atlas
Live Import to mirror data from your production cluster to the staging
cluster. The live migration documentation includes specific instructions for
creating staging environments.

4

### Point your staging application at the staging cluster.

Update your staging application to point at your staging cluster. For
instructions on retrieving the MongoDB driver-friendly connection string for
the staging cluster, see Connect via Your Application.

Confirm that your application can connect successfully to the staging cluster
_and_ that the application operates as expected.

5

### (Optional) Upgrade your application to the latest MongoDB drivers.

Upgrading your application to the latest MongoDB drivers for your cluster's
MongoDB version enables full access to the features provided by the newer
MongoDB version. You may also find better performance or stability with newer
driver versions. See Connect via Your Application for documentation on the
recommended MongoDB driver for a given MongoDB version and connection
examples.

If you encounter a bug after upgrading your application, file a ticket in the
JIRA project for your MongoDB driver.

6

### Update the staging cluster to the new major MongoDB version.

  1. Click __for your staging cluster to open the cluster modification modal.

  2. Select Edit Configuration.

  3. Change the cluster version to the desired major MongoDB Version.

## Important

You cannot downgrade the MongoDB version of a Atlas cluster. If you want to
redeploy the staging environment with the original MongoDB version, you must
terminate and re-create the cluster.

  4. Click Confirm & Deploy to deploy your changes.

Atlas automatically begins upgrading the cluster. Consider measuring the time
required by Atlas to upgrade the cluster to set a general expectation for your
production cluster upgrade.

File a support ticket if you encounter version-specific issues with the
upgraded staging cluster.

7

### Test your application against the upgraded staging cluster.

Perform any required performance and operational testing of the staging
cluster.

File a support ticket if you encounter version-specific issues with the
upgraded staging cluster.

## Important

The major version upgrade requires at least one replica set election. Use the
staging cluster as an opportunity to test your application's resiliance to
primary failover. See Test Primary Failover for complete documentation.

8

### Upgrade your production cluster to the target MongoDB version.

Once you are confident in the performance and operation of your staging
cluster, repeating the upgrade procedure for your production cluster.

Once Atlas completes the upgrade process, check that your production
applications are still connected and operating normally.

If you upgraded your staging application with newer MongoDB drivers _and_ are
satisfied with the performance and operation, consider scheduling a
maintenance period for upgrading your production applications.

If you encounter problems with the upgraded production cluster, file a High
Priority support ticket using the procedure in the following section.

## Support for Major Version Upgrades

If you have any questions regarding migration support beyond what is covered
in this documentation, or if you encounter an error during migration, file a
support ticket through the Atlas user interface.

To file a support ticket:

  1. Click Support in the left-hand navigation.

  2. For Atlas Issue Category, select `Other`.

  3. For Priority, select `Medium Priority`. If the issue affects your production cluster, select `High Priority`.

  4. For Request Summary, include `Major Version Upgrade` in the summary.

  5. For More details, include any other relevant details to your question or major version upgrade error.

← Reconfigure a Replica Set During a Regional OutageConfigure Maintenance
Window →

