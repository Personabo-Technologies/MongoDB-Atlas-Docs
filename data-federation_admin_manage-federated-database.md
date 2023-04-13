Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage a Federated Database Instance

Share Feedback

On this page

  * Administration Commands
  * Authentication Options

The Atlas Data Federation configuration defines mappings between your data
stores and Atlas Data Federation. This section describes the commands you can
use to create, update, retrieve, and remove stores, databases, collections,
and views in your federated database instance storage configuration.

## Administration Commands

## Note

Any MongoDB user in the Atlas project with the atlasAdmin role can retrieve
and update the federated database instance configuration.

### Stores

The Data Federation CLI lets you create, remove, and retrieve stores in your
federated database instance storage configuration using the following
commands:

  * `createStore`

  * `dropStore`

  * `listStores`

### Database

The Data Federation CLI lets you remove a database from your federated
database instance storage configuration using the following commands:

  * `dropDatabase`

### Collections and Views

The Data Federation CLI lets you create, remove, and/or rename collections and
views in your federated database instance storage configuration using the
following commands:

  * `create`

  * `drop`

  * `renameCollection`

## Authentication Options

Data Federation uses SCRAM-SHA or x509 for authentication. It doesn't support
LDAP.

← Administer Federated Database Instances`createStore` →

