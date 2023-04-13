Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Integrate with Third-Party Services

Share Feedback

On this page

  * Required Access
  * View or Modify Third-Party Settings

You can integrate Atlas with third-party monitoring services to receive Atlas
alerts in various external monitoring services, and to view and analyze
performance metrics that Atlas collects about your cluster.

## Note

Currently, serverless instance metrics don't support any third-party services
(for example, Datadog).

## Required Access

To view third-party integration settings, you must have `Organization Owner`
or `Project Owner` access to the project.

## View or Modify Third-Party Settings

Atlas CLI

Atlas UI

## Note

Before you run any Atlas CLI commands, you must:

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Datadog

To create or update a Datadog integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create DATADOG [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create DATADOG.

### Opsgenie

To create or update an Opsgenie integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create OPS_GENIE [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create OPS_GENIE.

### PagerDuty

To create or update a PagerDuty integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create PAGER_DUTY [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create PAGER_DUTY.

### VictorOps

To create or update a VictorOps integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create VICTOR_OPS [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create VICTOR_OPS.

### Webhook

To create or update a webhook integration using the Atlas CLI, run the
following command:

    
    
    atlas integrations create WEBHOOK [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations create WEBHOOK.

#### View Third-Party Integrations

To list all third-party integrations for a project using the Atlas CLI, run
the following command:

    
    
    atlas integrations list [options]  
      
  
To return the details for one third-party integration using the Atlas CLI, run
the following command:

    
    
    atlas integrations describe <integrationType> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas integrations list and atlas integrations
describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

#### Delete a Third-Party Integration

To delete a third-party integration using the Atlas CLI, run the following
command:

    
    
    atlas integrations delete <integrationType> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas integrations delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Review Available MetricsIntegrate with Datadog →

