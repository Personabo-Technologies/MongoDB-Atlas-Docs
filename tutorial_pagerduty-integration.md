Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with PagerDuty

Share Feedback

On this page

  * How it Works
  * Prerequisites
  * Support
  * Procedure
  * Remove a PagerDuty Integration

You can configure Atlas to send alerts from your project to your PagerDuty
dashboard. With PagerDuty integration, you can:

  * Record incidents and notify on-call responders based on Atlas alerts.

  * Automatically resolve incidents in PagerDuty when an Atlas alert is closed with bidirectional synchronization.

## How it Works

With a PagerDuty integration, you can send Atlas cluster event data to
PagerDuty when Atlas alerts that you specify are triggered. PagerDuty can
create a new incident for the corresponding service, filter additional alerts
from the same source into that incident, and alert on-call PagerDuty users.

Once the Atlas alert has been resolved, PagerDuty resolves the incident.

## Prerequisites

To integrate Atlas with PagerDuty, you must have a PagerDuty account.

If you do not have an existing PagerDuty account, you can sign up at
https://www.pagerduty.com/sign-up/.

## Note

All new PagerDuty keys use their Events API v2.

If you have an Events API v1 key, you can continue to use that key with Atlas.

## Support

If you need help with your Atlas PagerDuty integration, contact MongoDB
Support.

## Procedure

Atlas CLI

Atlas UI

To create or update a PagerDuty integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create PAGER_DUTY [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create PAGER_DUTY.

## Remove a PagerDuty Integration

Atlas CLI

Atlas UI

To delete a third-party integration using the Atlas CLI, run the following
command:

    
    
    atlas integrations delete <integrationType> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Integrate with Microsoft TeamsIntegrate with Prometheus →

