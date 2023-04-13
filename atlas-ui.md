Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Interact with Your Data

Share Feedback

On this page

  * Overview
  * Atlas UI Read Behavior
  * Disable Atlas UI Data Interaction

## Overview

After loading your data or our sample data, you can use the Atlas UI to
interact with the data in the following ways:

  * Manage Databases in your database deployments.

  * Manage Collections in your database deployments.

  * Manage Documents in your collections.

  * Manage Indexes on your collections.

  * Create and run aggregation pipelines to process data in your collections.

  * Shard Global Clusters to distribute large datasets evenly.

  * Build charts to visualize data in your databases and collections.

## Note

The Atlas UI supports all features for serverless instances except the Search
tab.

To learn more, see Serverless Instance Limitations.

## Atlas UI Read Behavior

The Atlas UI reads from the primary unless the primary is unavailable. If the
primary is unavailable, the Atlas UI reads from a non-hidden, non-delayed
secondary member.

## Disable Atlas UI Data Interaction

To interact with your data in the Atlas UI as described in the Overview
section, the Data Explorer needs to be enabled.

## Important

### Required Privileges

To enable or disable Data Explorer for a project, you must have the `Project
Owner` role for the project or the `Organization Owner` role on its parent
organization.

Data Explorer is enabled by default. To disable Data Explorer:

1

### Click Settings.

2

### Set the Data Explorer toggle to Off.

## Important

When Data Explorer is disabled, you cannot:

  * Terminate slow operations from the Real-Time Performance Panel.

  * Create indexes from the Performance Advisor. You can still view Performance Advisor recommendations, but you must create those indexes from `mongosh`.

To enable Data Explorer, set the toggle to On.

← Load File with `mongoimport`Create, View, and Drop Databases →

