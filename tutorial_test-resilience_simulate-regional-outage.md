Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Simulate Regional Outage

Share Feedback

On this page

  * Simulate Regional Outage Process
  * Simulate Regional Outage Using the Atlas UI
  * Simulate Regional Outage Using the API
  * Verify the Outage

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

You can use the Atlas UI and API to simulate an outage on your Atlas multi-
region cluster and observe how your application handles an outage in one or
more regions.

## Simulate Regional Outage Process

When you submit a request to test an outage using the Atlas UI or API, Atlas
simulates an outage event. During this process, Atlas removes network
connectivity to nodes in the selected regions.

## Simulate Regional Outage Using the Atlas UI

To simulate a Regional Outage in the Atlas UI:

  1. Log in to the Atlas UI.

  2. Click Database.

  3. For the cluster you wish to perform outage testing, click the ... button.

  4. Click Test Resilience.

  5. Select Regional Outage. Atlas displays a Test Resilience modal with the steps Atlas takes to simulate an outage event. To learn more, see Simulate Regional Outage Process.

  6. Click Select Regions.

  7. Select the tab corresponding to the type of outage you want to simulate:

Minority of Electable Nodes

Majority of Electable Nodes

Select fewer than half of your electable nodes.

  8. Select Simulate Regional Outage to begin the test. Atlas notifies you when the outage occurs.

  9. Select a tab corresponding to the type of outage you are performing:

Minority of Electable Nodes

Majority of Electable Nodes

When you finish testing the outage, click End Simulation.

## Simulate Regional Outage Using the API

You can use the Test Outage API endpoint to simulate an outage event. To learn
more about the outage process, see Simulate Regional Outage Process.

## Verify the Outage

To verify that the outage is successful, monitor your application and ensure
your read and write operations are working as expected.

← Test Primary FailoverManage Connections with AWS Lambda →

