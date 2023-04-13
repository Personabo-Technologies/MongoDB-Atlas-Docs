Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Auto-Index Creation for Performance Advisor

Share Feedback

On this page

  * Auto-Index Creation Availability
  * How Auto-Index Creation Creates Indexes
  * Enable Auto-Index Creation
  * Review Automatically Created Indexes
  * Drop Automatically Created Indexes

Auto-index creation for Performance Advisor periodically checks for index
recommendations and automatically creates indexes deemed to have a high impact
on cluster performance.

## Auto-Index Creation Availability

You can enable auto-index creation if your cluster meets all of the following
criteria:

  * Runs MongoDB 4.4 or later.

  * Uses tiers `M10` and `M30` (inclusive).

  * Does not run as a sharded cluster.

## How Auto-Index Creation Creates Indexes

Auto-index creation prioritizes creating indexes with the highest Impact
score. Atlas defines _impact_ as the estimated performance improvement that
the index would bring.

To learn more about the Impact score and how the Performance Advisor ranks
indexes, see Review Index Ranking.

Performance Advisor doesn't show individual index recommendations by default.
Performance Advisor shows the number of index recommendations per impact level
(high and medium). To view the individual indexes that the auto-index creation
would create, click View Recommendations. Atlas only creates high-impact
indexes automatically.

## Enable Auto-Index Creation

Auto-index creation defaults to _off_. You can enable auto-index creation for
your cluster through either the Atlas console or Atlas Administration API.

Atlas Console

Atlas Administration API

To enable auto-index creation for your cluster:

  1. Open Performance Advisor.

  2. In the Create Indexes panel, toggle Auto-Index Creation to on.

If you click View Recommendations, you can enable auto-index creation from the
individual recommendations view.

Once you enable auto-index creation, Atlas begins creating high-impact indexes
if Atlas suggests them.

## Review Automatically Created Indexes

Atlas sends an email alert when it creates an index automatically. You can
view automatically created indexes from the Atlas UI Indexes view. The Atlas
UI shows indexes that auto-index creation generated with the Auto-Created
property.

## Drop Automatically Created Indexes

You can drop auto-created indexes as you would any other index. To drop an
auto-created index, click Drop Index. If you drop an auto-created index, auto-
index creation doesn't recreate that index. Performance Advisor may still
recommend that index.

What is MongoDB Atlas? →

