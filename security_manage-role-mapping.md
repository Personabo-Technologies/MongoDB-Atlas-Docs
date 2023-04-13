Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Mapping Atlas Roles to IdP Groups

Share Feedback

On this page

  * Role Mapping Process
  * Prerequisites
  * Add Role Mappings in Your Organization and its Projects
  * Edit Role Mappings in Your Organization and its Projects
  * Remove One Role Mapping in Your Organization and its Projects

You can map your IdP groups to Atlas roles. This streamlines authorization
setup. You can grant one IdP group one or more roles to simplify their access
to Atlas organizations, projects, and clusters.

## Note

You can't edit roles for specific users on the Access Manager page if you
configure role mappings for IdP groups.

## Role Mapping Process

  1. Atlas applies the role mappings when you log in.

  2. Atlas compares the IdP groups named **memberOf** to role mappings defined for your organizations. These organizations must use the same IdP that the user did to authenticate.

    * Atlas applies the mapped roles to federated users if you defined role mappings.

    * Atlas applies the default role if:

      * You don't have defined role mappings

      * Role mappings would result in a user without any roles

    * Organization role mappings define federated users' Atlas access. If a federated user logs in but doesn't belong to an IdP group mapped to a desired organization, Atlas removes the mapped role from the user in that organization and its projects. The federated user may still have other IdP groups.

## Example

Consider a scenario where a user belongs to the **admin** IdP group. You have
configured a role mapping of **admin** to the `Organization Owner` in
**Organization A**. If you remove that user from the **admin** IdP group,
Atlas deletes that users' `Organization Owner` role when the user next logs
in.

    * Every project must have at least one user that has the `Project Owner` role. If removing a role removes the last owner from a project, the removal fails.

    * Every organization must have at least one user that has the `Organization Owner` role. If removing a role removes the last owner from an organization, the removal fails.

## Prerequisites

To complete this tutorial, you must have:

  * Created an IdP application. This application must have a SAML attribute named to **memberOf**. Map this attribute to the IdP source attributes for groups. This attribute links the IdP groups with your Atlas roles.

  * Linked an IdP to Atlas.

  * Mapped an Atlas organizations to your IdP.

  * Created at least one group in your IdP.

  * Add at least one user in your IdP application to a group you created.

## Add Role Mappings in Your Organization and its Projects

1

### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

### Choose an organization in which you want to map roles.

  1. Click Manage Organizations.

Atlas displays all organizations where you are an `Organization Owner` in a
table.

    * Organizations connected to federated authentication display __in the Actions column.

    * Organizations unconnected to federated authentication display Connect in the Actions column.

  2. To map roles in an organization:

    1. Click Connect to enable federated authentication for that organization if needed.

    2. Click __and select View.

3

### Navigate to the Create Role Mapping For Your Users page.

  1. Click Create Role Mappings.

Atlas displays the Organization Role Mappings page.

  2. Click Create A Role Mapping.

Atlas displays the Create Role Mapping For Your Users page.

4

### Assign Atlas organization roles to the desired IdP group.

At the Map Group and Assign Roles stage:

Section

|

Action  
  
|  
  
Enter Group Name

|

Type the name of the group as it is displayed in your IdP in this field. Atlas
assigns this group to your Atlas role.

## Note

If the IdP group doesn't exist, you can't enter a new group name to create a
new IdP group.

If you use Azure AD as your IdP and you selected Group Id as your source
attribute, enter the group's Object ID in this field instead of the group's
name. To learn more, see Configure Azure AD as an Identity Provider.  
  
Assign Organization Roles

|

Click on each Atlas organization role that you want to assign to the IdP
group.  
  
  * If you don't need to assign any Atlas project roles to this IdP group, click Finish. You can skip the rest of this procedure.

  * If you need to assign Atlas project roles to this IdP group, click Next.

5

### Assign Atlas project roles to the desired IdP group.

The Assign Project Roles stage displays a table. This table includes project
names and the roles you can assign for those projects. For each project, click
the project roles that you want to assign to the IdP group.

  * If you don't need to review the roles assigned to this IdP group, click Finish. You can skip the rest of this procedure.

  * If you need to review the roles assigned to this IdP group, click Next.

6

### Verify which Atlas roles have been assigned to the desired IdP group.

The Review and Confirm stage displays the organization and project roles
assigned to the IdP group.

  * If you agree with the roles assigned to this IdP group, click Finish.

  * If you need to change the roles assigned to this IdP group, click __ Edit. Atlas returns to the Map Group and Assign Roles stage.

## Edit Role Mappings in Your Organization and its Projects

1

### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

### Choose an organization in which you want to edit role mappings.

  1. Click Manage Organizations.

Atlas displays all organizations where you are an `Organization Owner` in a
table.

  2. Click __next to the desired IdP Group Name and select View.

3

### Navigate to the Create Role Mapping For Your Users page.

  1. Click Create Role Mappings.

Atlas displays the Organization Role Mappings page.

  2. Click __ Edit to the right of the IdP group you want to change.

Atlas displays the Edit Your Role Mapping For This Organization page.

4

### Change Atlas organization roles in the desired IdP group.

At the Map Group and Assign Roles stage:

Section

|

Action  
  
|  
  
Enter Group Name

|

Type the name of the group as it is displayed in your IdP in this field. Atlas
assigns this group to your Atlas role.

## Note

If the IdP group doesn't exist, you can't enter a new group name to create a
new IdP group.

If you use Azure AD as your IdP and you selected Group Id as your source
attribute, enter the group's Object ID in this field instead of the group's
name. To learn more, see Configure Azure AD as an Identity Provider.  
  
Assign Organization Roles

|

Click on each Atlas organization role that you want to assign to the IdP
group.  
  
  * If you don't need to assign any Atlas project roles to this IdP group, click Finish. You can skip the rest of this procedure.

  * If you need to assign Atlas project roles to this IdP group, click Next.

5

### Assign Atlas project roles to the desired IdP group.

The Assign Project Roles stage displays a table. This table includes project
names and the roles you can assign for those projects. For each project, click
the project roles that you want to assign to the IdP group.

  * If you don't need to review the roles assigned to this IdP group, click Finish. You can skip the rest of this procedure.

  * If you need to review the roles assigned to this IdP group, click Next.

6

### Verify which Atlas roles have been assigned to the desired IdP group.

The Review and Confirm stage displays the organization and project roles
assigned to the IdP group.

  * If you agree with the roles assigned to this IdP group, click Finish.

  * If you need to change the roles assigned to this IdP group, click __ Edit. Atlas returns to the Map Group and Assign Roles stage.

## Remove One Role Mapping in Your Organization and its Projects

1

### Open the Federation Management Console.

  1. Log in to Atlas.

  2. Use the dropdown at the top-left of Atlas to select the organization for which you want to manage federation settings.

  3. Click Settings in the left navigation pane.

  4. In Manage Federation Settings, click Visit Federation Management App.

2

### Choose an organization in which you want to remove role mappings.

  1. Click Manage Organizations.

Atlas displays all organizations where you are an `Organization Owner` in a
table.

    * Organizations connected to federated authentication display __in the Actions column.

    * Organizations unconnected to federated authentication display Connect in the Actions column.

  2. To map roles in an organization:

    1. Click Connect to enable federated authentication for that organization if needed.

    2. Click __and select View.

3

### Navigate to the Organization Role Mappings page.

  1. Click Create Role Mappings.

Atlas displays the Organization Role Mappings page.

  2. Click __ Delete to the right of the IdP group you want to remove.

Atlas displays the Delete role mappings for this group modal.

  3. Click Delete to remove all role mappings from this IdP group.

If you don't want to remove all role mappings, click Cancel.

← Manage Organization Mapping for Federated AuthenticationConfigure Federated
Authentication from Azure AD →

