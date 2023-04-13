Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure IP Access List Entries

Share Feedback

On this page

  * View IP Access List Entries
  * Add IP Access List Entries
  * Modify IP Access List Entries
  * Delete IP Access List Entries

Atlas only allows client connections to the database deployment from entries
in the project's IP access list. Each entry is either a single IP address or a
CIDR-notated range of addresses. For AWS clusters with one or more VPC Peering
connections to the same AWS region, you can specify a Security Group
associated with a peered VPC.

For Atlas clusters deployed on Google Cloud Platform (GCP) or Microsoft Azure,
add the IP addresses of your Google Cloud or Azure services to Atlas project
IP access list to grant those services access to the cluster.

The IP access list applies to all database deployments in the project and can
have up to 200 IP access list entries, with the following exception: projects
with an existing sharded cluster created _before_ August 25, 2017 can have up
to 100 IP access list entries.

Atlas supports creating temporary IP access list entries that expire within a
user-configurable 7-day period.

## Note

You must be a `Project Owner` to manage IP Access List entries.

Atlas audits the creation, deletion, and updates of both temporary and
permanent IP access list entries in the project's Activity Feed.

To view the project's Activity Feed, click Activity Feed in the Project
section of the left navigation pane.

## Tip

### See also:

View All Activity

## Note

### Activity Feed Considerations

  * Atlas does not report updates to a IP access list entry's comment in the Activity Feed.

  * When you modify the address of a IP access list entry, the Activity Feed reports two new activities: one for the deletion of the old entry and one for the creation of the new entry.

## View IP Access List Entries

Atlas CLI

Atlas UI

To list IP access list entries for your project using the Atlas CLI, run the
following command:

    
    
    atlas accessLists list [options]  
      
  
To return the details for the IP access list entry you specify using the Atlas
CLI, run the following command:

    
    
    atlas accessLists describe <entry> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas accessLists list and atlas accessLists
describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Add IP Access List Entries

Atlas CLI

Atlas Administration API

Atlas UI

To create an IP access list for your project using the Atlas CLI, run the
following command:

    
    
    atlas accessLists create [entry] [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas accessLists create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Modify IP Access List Entries

Atlas CLI

Atlas Administration API

Atlas UI

You can't modify IP access list entries with the Atlas CLI. Select a different
interface to learn how to modify IP access list entries.

## Delete IP Access List Entries

## Important

When you remove an entry from the IP access list, existing connections from
the removed address(es) may remain open for a variable amount of time. How
much time passes before Atlas closes the connection depends on several
factors, including:

  * how the connection was established

  * how the application or driver using the address behaves

  * which protocol (like TCP or UDP) the connection uses

Atlas CLI

Atlas Administration API

Atlas UI

To delete an IP access list from your project using the Atlas CLI, run the
following command:

    
    
    atlas accessLists delete <entry> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas accessLists delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Configure Cluster Access with the Quickstart WizardSet Up a Network Peering
Connection →

