Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Deploy a Free Cluster

Share Feedback

On this page

  * Procedure
  * Next Steps

 _Estimated completion time: 10 minutes_

Atlas free clusters provide a small-scale development environment to host your
data. Free clusters never expire, and provide access to a subset of Atlas
features and functionality.

Paid clusters provide full access to Atlas features, configuration options,
and operational capabilities. For more information on paid clusters, including
deployment instructions, see Create a Cluster.

## Note

You can deploy only one free cluster per Atlas project.

## Procedure

You can create free clusters through the Atlas CLI, Atlas User Interface, and
Atlas Administration API. Select the appropriate tab based on how you would
like to create the free clusters.

Atlas CLI

Atlas Administration API

Atlas UI

To create one cluster, load sample data, add your IP address to your project
IP access list, and create a MongoDB user for your cluster using the Atlas
CLI, run the following command:

    
    
    atlas quickstart [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas quickstart.

For step-by-step instructions on using this command, see Create and Configure
an Atlas Cluster using the Atlas CLI.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Note

If you run `atlas setup` with the default selections, you don't need to run
`atlas quickstart`.

## Next Steps

Now that your cluster is provisioned, proceed to Add Your Connection IP
Address to Your IP Access List.

