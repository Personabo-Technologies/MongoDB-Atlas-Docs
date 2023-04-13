Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Project IP Access List

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Access List Replaces Whitelist

This resource replaces the whitelist resource. Atlas removed whitelists in
July 2021. Update your applications to use this new resource.

The **Access List** endpoint manages a Atlas project's IP Access List.

The **Access List** endpoint supports creating temporary Access List entries
that automatically expire within a user-configurable 7-day period.

## Considerations

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Atlas audits the creation, deletion, and updates of both temporary and non-
temporary IP access list entries in the project's Activity Feed.

To view the project's Activity Feed, click Activity Feed in the Project
section of the left navigation pane.

## Tip

### See also:

View All Activity.

## Note

### Activity Feed Considerations

  * Atlas does not report updates to an IP access list entry's comment in the Activity Feed.

  * When you modify the address of an IP access list entry, the Activity Feed reports two new activities: one for the deletion of the old entry and one for the creation of the new entry.

## Important

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

## Endpoints

`https://cloud.mongodb.com/api/atlas/v1.0`

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/accessList

|

Get all access list entries in the project associated to **{GROUP-ID}**.  
  
`GET`

|

/groups/{GROUP-ID}/accessList/{ACCESS-LIST-ENTRY}

|

Get the access list entry specified to **{ACCESS-LIST-ENTRY}** from the
project associated to **{GROUP-ID}**.  
  
`GET`

|

/groups/{GROUP-ID}/accessList/{ACCESS-LIST-ENTRY}/status

|

Get the status of one access list entry from the specified project.  
  
`POST`

|

/groups/{GROUP-ID}/accessList

|

Add one or more access list entries to the project associated to **{GROUP-
ID}**.  
  
`DELETE`

|

/groups/{GROUP-ID}/accessList/{ACCESS-LIST-ENTRY}

|

Delete the access list entry specified to **{ACCESS-LIST-ENTRY}** from the
project associated to **{GROUP-ID}**.  
  
What is MongoDB Atlas? →

