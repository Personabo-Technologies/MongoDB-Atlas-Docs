Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Database

Share Feedback

On this page

  * How many collections can a single Atlas cluster have?
  * Which versions of MongoDB do Atlas clusters use?
  * When does MongoDB upgrade the database version of free clusters and shared clusters?
  * What happens to Atlas clusters using a MongoDB version nearing end of life?

## How many collections can a single Atlas cluster have?

While there is no hard limit on the number of collections in a single cluster,
the performance of a cluster might degrade if it serves a large number of
collections and indexes. Larger collections have a greater impact on
performance.

The recommended maximum combined number of collections and indexes by Atlas
cluster tier are as follows:

Cluster tier

|

Recommended maximum  
  
|  
  
M10

|

5,000 collections and indexes  
  
M20 / M30

|

10,000 collections and indexes  
  
M40+

|

100,000 collections and indexes  
  
## Which versions of MongoDB do Atlas clusters use?

Atlas supports creating clusters with the following tiers and MongoDB
versions:

MongoDB Version

|

Supported on `M10+`

|

Supported on Free and Shared Tiers (`M0`, `M2`, `M5`)  
  
||  
  
MongoDB 4.2

|

 __

|  
  
MongoDB 4.4

|

 __

|  
  
MongoDB 5.0

|

 __

|

 __  
  
MongoDB 6.0

|

 __

|  
  
Latest Release (auto-upgrades)

|

 __

|  
  
## Important

If your cluster runs a release candidate of MongoDB 6.0, Atlas will upgrade
the cluster to the stable release version when it is generally available.

To use a rapid release MongoDB version, you must select Latest Release for
auto-upgrades. You can't select a specific rapid release version.

As new patch releases become available, Atlas upgrades to these releases via a
rolling process to maintain cluster availability. During the upgrade to the
next rapid release version, the cluster card in the Atlas UI Database
Deployments page might show the `FCV` of your cluster instead of the MongoDB
version to reflect the features that are currently available on your cluster.

To learn more about how Atlas handles end of life of major MongoDB versions,
see What happens to Atlas clusters using a MongoDB version nearing end of
life?

## When does MongoDB upgrade the database version of free clusters and shared
clusters?

Atlas upgrades free clusters and shared clusters to the newest MongoDB version
after several patch versions become available for that version. To learn more
about how MongoDB versions its software, see MongoDB Versioning.

## What happens to Atlas clusters using a MongoDB version nearing end of life?

## Note

### Unsupported MongoDB Versions in Atlas

Atlas no longer supports MongoDB 4.0 and earlier.

MongoDB sends you an email notification at least six months before the MongoDB
version reaches end of life. A few months after you receive this notification,
Atlas:

  * Stops allowing you to deploy new clusters using the end of life version.

  * Notifies you of the version cut-off date. After the cut-off date, Atlas upgrades your clusters to the next MongoDB version unless you request and receive approval for an extension.

## Example

When MongoDB 4.2 reaches end of life, Atlas upgrades each of your clusters
that run MongoDB 4.2 to MongoDB 4.4.

This upgrade happens within your maintenance window if you configured one in
your project settings.

In most cases, this upgrade won't cause downtime or negatively affect your
applications. You should upgrade your cluster before the cut-off date to
ensure that your services and applications experience no downtime or other
issues due to incompatibilities with the new MongoDB version.

To learn about potential issues for the cluster when upgrading MongoDB
versions, see `Compatibility Changes` in the MongoDB Release Notes for the
next MongoDB version.

## Tip

### See also:

To review the end of life date for each MongoDB Server release, see `MongoDB
Server` in the MongoDB Support Policy.

← FAQ: Connection String OptionsFAQ: Deployment →

