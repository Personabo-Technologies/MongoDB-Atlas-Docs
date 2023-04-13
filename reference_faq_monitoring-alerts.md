Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Monitoring and Alerts

Share Feedback

On this page

  * How do I modify alerts?
  * Why has Atlas stopped monitoring my cluster?

## How do I modify alerts?

To modify existing alert settings:

  1. Click Alerts in the Project section of the left navigation.

  2. Click Alert Settings.

  3. Click __to the right of the alert you want to modify (edit, clone, disable, delete).

## Why has Atlas stopped monitoring my cluster?

Atlas pauses monitoring for `M0` free clusters which have had no connection
activity for 7 days. Monitoring resumes once a successful connection occurs
through the Atlas Administration API, Driver, `mongosh`, or Data Explorer.

← FAQ: DeploymentFAQ: Networking →

