Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Administration API Error Codes

Share Feedback

Error

|

HTTP Code

|

Description  
  
||  
  
`ALREADY_EXPIRED`

    

|

400

|

Cannot update an entity that has already expired.  
  
`API_KEY_CAN_ONLY_BELONG_TO_ONE_ORG`

    

|

400

|

API keys may only belong to a single organization.  
  
`API_KEY_CREATED_GROUPS_MUST_HAVE_ORG`

    

|

400

|

Projects created by API keys must belong to an existing organization.  
  
`API_KEY_NOT_FOUND`

    

|

400

|

No API key with ID %s exists.  
  
`API_KEY_REQUIRES_DESCRIPTION`

    

|

400

|

All API keys require a non-empty description.  
  
`API_KEY_ROLE_ASSIGNMENT_MISSING_ID`

    

|

400

|

API key role assignments must include an org or group id.  
  
`ATLAS_CLUSTER_VERSION_DEPRECATED`

    

|

400

|

MongoDB version is deprecated in Atlas.  
  
`ATLAS_CUSTOM_ROLE_HAS_NO_PERMISSIONS`

    

|

400

|

Custom roles must have one or more user privilege actions or inherited roles.  
  
`ATLAS_CUSTOM_ROLE_INVALID_NAME`

    

|

400

|

The role name, "%s", is invalid. A custom role name must be a non-empty string
made up of only ASCII letters, numbers, hyphens, and underscores, and should
begin with a letter or number.  
  
`ATLAS_DUPLICATE_CUSTOM_ROLE_ACTION`

    

|

400

|

A custom role cannot have duplicate actions.  
  
`ATLAS_DUPLICATE_CUSTOM_ROLE_RESOURCE`

    

|

400

|

A custom role cannot have duplicate resources applied to the same action.  
  
`ATLAS_FTS_ANALYZER_NAME_CANNOT_REUSED`

    

|

400

|

Stock analyzer name can not be re-used.  
  
`ATLAS_FTS_ANALYZER_NAME_NOT_UNIQUE`

    

|

400

|

Analyzer name is not unique.  
  
`ATLAS_FTS_DUPLICATE_INDEX`

    

|

400

|

Duplicate Index.  
  
`ATLAS_GENERAL_ERROR`

    

|

400

|

Reason: %s.  
  
`ATLAS_GENERATED_CERTS_LIMIT_EXCEEDED`

    

|

400

|

The limit on generated certificates per user has been reached.  
  
`ATLAS_INVALID_AUTH_SETTINGS`

    

|

400

|

Invalid authentication settings. %s.  
  
`ATLAS_INVALID_CIDR_BLOCK`

    

|

400

|

Atlas CIDR %s must be a /%s block for %s.  
  
`ATLAS_INVALID_CIDR_BLOCK_FOR_SMALL_CONTAINER`

    

|

400

|

Atlas CIDR must be between `/21` and `/24` for small Google Cloud network
peering containers. Either omit the `regions` array to create a network
peering container with a larger CIDR block or provide an `atlasCidrBlock`
between `/21` and `/24`, inclusive.  
  
`ATLAS_INVALID_CIDR_RANGE`

    

|

400

|

Atlas CIDR %s must be in private range.  
  
`ATLAS_INVALID_CUSTOM_ROLE_ASSIGNMENT`

    

|

400

|

If assigned a custom DB role, a user can only be assigned one role.  
  
`ATLAS_INVALID_CUSTOM_ROLE_CIRCULAR_DEPENDENCY`

    

|

400

|

One or more of the specified inherited roles creates a circular dependency.  
  
`ATLAS_INVALID_CUSTOM_ROLE_INHERITANCE`

    

|

400

|

One or more of the specified inherited roles do not exist.  
  
`ATLAS_INVALID_CUSTOM_ROLE_INHERITED_SCOPE`

    

|

400

|

One or more of the specified inherited roles have an invalid scope.  
  
`ATLAS_INVALID_CUSTOM_ROLE_RESTRICTED`

    

|

400

|

Cannot create custom role %s because a built-in role with that name already
exists.  
  
`ATLAS_INVALID_CUSTOM_ROLE_SELF_REFERENTIAL`

    

|

400

|

A custom DB role cannot inherit from itself.  
  
`ATLAS_INVALID_DN_METACHARACTERS`

    

|

400

|

The distinguished name specified in the username field, %s, contains illegal
metacharacters.  
  
`ATLAS_INVALID_LDAP_NAME`

    

|

400

|

The distinguished name specified in the username field, %s, is not valid
according to RFC 2253.  
  
`ATLAS_INVALID_MAINTENANCE_WINDOW_DAY_OF_WEEK`

    

|

400

|

Invalid Day of Week. Value should be between 1 and 7 (Sunday = 1).  
  
`ATLAS_INVALID_MAINTENANCE_WINDOW_HOUR_OF_DAY`

    

|

400

|

Invalid Hour of Day. Value should be between 0 and 23.  
  
`ATLAS_INVALID_RESOURCE`

    

|

400

|

One or more of the selected actions was applied to an incorrect resource.  
  
`ATLAS_INVALID_ROLE`

    

|

400

|

The specified role %s@%s does not exist.  
  
`ATLAS_INVALID_ROLE_DATABASE`

    

|

400

|

The specified role %s only exists for database %s.  
  
`ATLAS_INVALID_USERNAME`

    

|

400

|

The specified username %s is not valid for an Atlas database user.  
  
`ATLAS_MAINTENANCE_ALREADY_SCHEDULED`

    

|

400

|

The upcoming maintenance has already been scheduled. The maintenance window
cannot be adjusted until current maintenance is finished.  
  
`ATLAS_MAINTENANCE_NOT_SCHEDULED`

    

|

400

|

There is no maintenance scheduled for this project.  
  
`ATLAS_MAINTENANCE_WINDOW_NOT_DEFINED`

    

|

400

|

No maintenance window defined for project. This action is only supported for
projects with user defined maintenance windows.  
  
`ATLAS_MANAGED_X509_NAME_INVALID`

    

|

400

|

The username %s is invalid for Atlas-managed X.509 user auth. These usernames
must take the form CN=<username> with no additional OIDs.  
  
`ATLAS_NON_CANONICAL_CIDR_BLOCK`

    

|

400

|

The canonical form for the specified Atlas CIDR %s is %s.  
  
`ATLAS_NUM_MAINTENANCE_DEFERRALS_EXCEEDED`

    

|

400

|

Scheduled maintenance for a group cannot be deferred more than twice.  
  
`ATLAS_RESERVED_CLUSTER_NAME`

    

|

400

|

The provided cluster name %s creates a conflict with our internal hostnames,
which are generated using the pattern "atlas-[a-z0-9]{6}".  
  
`ATLAS_RESERVED_CUSTOM_ROLE_RESTRICTED`

    

|

400

|

Cannot create custom role %s because the prefix xgen-" is reserved for built-
in roles.  
  
`ATLAS_RESTRICTED_COLLECTION`

    

|

400

|

The specified collection %s for the role %s@%s is restricted.  
  
`ATLAS_RESTRICTED_ROLE`

    

|

400

|

The specified role %s@%s is restricted.  
  
`ATLAS_USER_NOT_USER_EDITABLE`

    

|

400

|

This user can only be edited by the system.  
  
`ATLAS_X509_USER_CANNOT_BE_TEMPORARY`

    

|

400

|

X.509 users cannot be temporary.  
  
`ATLAS_X509_USER_CANNOT_USE_LDAP`

    

|

400

|

Users cannot be configured for X.509 and LDAP authentication.  
  
`ATLAS_X509_USER_CANNOT_USE_SCRAM`

    

|

400

|

Users cannot be configured for SCRAM and X.509 authentication.  
  
`ATTRIBUTE_NEGATIVE`

    

|

400

|

The attribute %s cannot be negative.  
  
`ATTRIBUTE_NEGATIVE_OR_ZERO`

    

|

400

|

The attribute %s cannot be negative or zero.  
  
`ATTRIBUTE_READ_ONLY`

    

|

400

|

The attribute %s is read-only and cannot be changed by the user.  
  
`AUTH_MECHANISM_REQUIRES_SSL`

    

|

400

|

Authentication mechanism %s requires SSL.  
  
`AUTO_SCALING_NOT_SUPPORTED`

    

|

400

|

Cannot set auto-scaling. %s.  
  
`AUTOMATED_RESTORE_OF_SHARD_NOT_ALLOWED`

    

|

400

|

Not allowed to do an automated restore of individual shard snapshots of a
sharded cluster.  
  
`AUTOMATION_AGENT_VERSION_NOT_SUPPORTED`

    

|

400

|

Automation agent version is not supported.  
  
`AWS_KMS_CUSTOMER_MASTER_KEY_NOT_ENABLED`

    

|

400

|

AWS KMS Customer Master Key is not enabled.  
  
`AWS_KMS_CUSTOMER_MASTER_KEY_PENDING_DELETION`

    

|

400

|

AWS KMS Customer Master Key is pending deletion.  
  
`AWS_KMS_CUSTOMER_MASTER_KEY_PENDING_IMPORT`

    

|

400

|

AWS KMS Customer Master Key is pending import.  
  
`AWS_KMS_REGION_NOT_SUPPORTED`

    

|

400

|

Region is not supported by AWS KMS.  
  
`AZURE_CUSTOMER_NETWORK_VALIDATION_FAILED`

    

|

400

|

Please ensure that the account information provided is correct and that you've
given Atlas the proper permissions to create peering connections in your
account.  
  
`AZURE_KEY_VAULT_ENVIRONMENT_NOT_SUPPORTED`

    

|

400

|

Environment not supported for Azure Key Vault.  
  
`AZURE_KEY_VAULT_KEY_EXPIRED`

    

|

400

|

The key has expired.  
  
`AZURE_KEY_VAULT_KEY_EXPIRING`

    

|

400

|

The key cannot be used because it will expire within the next 48 hours.  
  
`AZURE_KEY_VAULT_KEY_IDENTIFIER_INVALID_FORMAT`

    

|

400

|

Invalid format for Azure Key Vault Key Identifier.  
  
`AZURE_KEY_VAULT_KEY_NOT_ACTIVE`

    

|

400

|

The key must not be used before its "nbf"  
  
`AZURE_KEY_VAULT_KEY_NOT_ENABLED`

    

|

400

|

Key not enabled.  
  
`AZURE_KEY_VAULT_KEY_NOT_FOUND`

    

|

400

|

No Azure Key Vault key found for the provided credentials.  
  
`AZURE_PEERING_MULTIPLE_REGIONS_NOT_ALLOWED`

    

|

400

|

Azure peering is only allowed in one Atlas Azure container per project.  
  
`AZURE_PEERING_MULTIPLE_REGIONS_NOT_ALLOWED`

`_IN_DEPRECATED_PEERING_ONLY_MODE`

|

400

|

This project uses Peering-Only mode which limits peering to one Atlas Azure
region. Disable Peering-Only mode to use Azure multi-region peering.  
  
`BACKUP_COMPLIANCE_POLICY_SETTINGS_INVALID`

    

|

400

|

The Backup Compliance Policy has invalid settings.  
  
`BACKUP_INVALID_FS_PATH`

    

|

400

|

Incorrect path (%s).  
  
`BACKUP_JOB_NOT_FOUND`

    

|

400

|

Backups are not enabled for this cluster.  
  
`BACKUP_KMIP_CERTIFICATE_PATH_REQUIRED`

    

|

400

|

A KMIP Client Certificate path must be specified with the password.  
  
`BACKUP_POLICY_NOT_MEETING_BACKUP_COMPLIANCE`

`_POLICY_REQUIREMENTS`

|

400

|

Backup policy doesn't meet the minimum Backup Compliance Policy requirements.  
  
`BACKUP_SNAPSHOT_RETENTION_VALUE_INVALID`

    

|

400

|

Retention value of snapshot is invalid.  
  
`BACKUP_WRONG_DAEMON_CONFIG_ID`

    

|

400

|

The specified ID for Daemon Config %s is wrong.  
  
`BAD_USERNAME_IN_GROUP_REF`

    

|

400

|

User %s is not in group %s.  
  
`BAD_USERNAME_REF`

    

|

400

|

No user with username %s exists.  
  
`BAD_WHITELIST_ADD_REQUEST`

    

|

400

|

Should not specify both the IP address and the CIDR block.  
  
`BLOCKED_USERNAME`

    

|

400

|

The specified username %s is not allowed.  
  
`CANNOT_ADD_GROUP_ROLE`

    

|

400

|

Adding a group-level role in an organization is not supported.  
  
`CANNOT_ADD_IP_ADDRESS_TO_API_KEY_WHITELIST`

    

|

400

|

The address %s cannot be added to whitelists.  
  
`CANNOT_ADD_IP_ADDRESS_TO_WHITELIST`

    

|

400

|

The address %s cannot be added to user whitelists.  
  
`CANNOT_ADD_ORG_ROLE`

    

|

400

|

Adding an organization-level role in a group is not supported.  
  
`CANNOT_CANCEL_AUTOMATED_RESTORE`

    

|

400

|

Automated restore cannot be cancelled.  
  
`CANNOT_CHANGE_CONTAINER_REGION`

    

|

400

|

The region of a cloud provider container cannot be changed.  
  
`CANNOT_CHANGE_GEOSHARDED_CLUSTER_TYPE`

    

|

400

|

A geo sharded cluster cannot be changed to a different cluster type.  
  
`CANNOT_CREATE_ATLAS_ORG`

    

|

400

|

Atlas organizations cannot be created via Ops Manager.  
  
`CANNOT_CREATE_EMPTY_TEAM`

    

|

400

|

A team must contain at least one user. Add a user to your team to continue.  
  
`CANNOT_CREATE_PAUSED_CLUSTER`

    

|

400

|

Cluster %s cannot be created in a paused state.  
  
`CANNOT_DECREASE_PIT_WINDOW_WITH` `_BACKUP_COMPLIANCE_POLICY`

|

400

|

You can't reduce the Continuous Cloud Backup Restore Window while you have a
Backup Compliance Policy enabled. The security or legal representative
specified for the Backup Compliance Policy must request support to reduce the
Continuous Cloud Backup Restore Window.  
  
`CANNOT_DECREASE_SNAPSHOT_RETENTION_WITH` `_BACKUP_COMPLIANCE_POLICY`

|

400

|

You can't decrease the snapshot rentention while you have a Backup Compliance
Policy enabled.  
  
`CANNOT_DELETE_COPY_SNAPSHOT_WITH_BACKUP` `_COMPLIANCE_POLICY_ENABLED`

|

400

|

You can't delete a snapshot copied to another region if you have a Backup
Compliance Policy enabled that has the Keep all snapshots when removing
additional snapshot regions option set to On.  
  
`CANNOT_DELETE_GROUP_INVITATION`

    

|

400

|

You can't use the /orgs/{ORG-ID}/invites/{INVITATION-ID} endpoint to delete an
invitation to a group. Use /groups/{GROUP-ID}/invites/{INVITATION-ID} instead.  
  
`CANNOT_DELETE_ORG_INVITATION`

    

|

400

|

You can't use the /groups/{GROUP-ID}/invites/{INVITATION-ID} endpoint to
delete an invitation to an organization. Use /orgs/{ORG-
ID}/invites/{INVITATION-ID} instead.  
  
`CANNOT_DELETE_IN_PROGRESS_SNAPSHOT`

    

|

400

|

Cannot delete an in progress snapshot %s.  
  
`CANNOT_DELETE_SNAPSHOT_WITH`

`_BACKUP_COMPLIANCE_POLICY`

|

400

|

You can't delete snapshots while you have a Backup Compliance Policy enabled.  
  
`CANNOT_DISABLE_ENCRYPTION_AT_REST`

`_WITH_BACKUP_COMPLIANCE_POLICY`

|

400

|

You can't disable Encryption at Rest while you have a Backup Compliance Policy
enabled.  
  
`CAN_NOT_DISABLE_ALL_ENCRYPTION_AT_REST_SETTINGS`

`_WHILE_BACKUP_COMPLIANCE_POLICY_ENCRYPTION_ENABLED`

|

400

|

You must keep at least one Encryption at Rest setting enabled while you have a
Backup Compliance Policy enabled.  
  
`CANNOT_DISABLE_CLOUD_BACKUP_WITH_BACKUP`

`_COMPLIANCE_POLICY`

|

400

|

You can't disable Cloud Backup while you have a Backup Compliance Policy
enabled.  
  
`CANNOT_DISABLE_PIT_WITH_BACKUUP_COMPLIANCE_POLICY`

    

|

400

|

You can't disable Continuous Cloud Backup while you have a Backup Compliance
Policy with the the Require Point in Time Restore to all clusters option set
to On.  
  
`CANNOT_DISTRIBUTE_SUBNETS`

    

|

400

|

Cannot distribute subnets. There must be at least one subnet available.  
  
`CANNOT_DOWNLOAD_EXPIRED_JOB`

    

|

400

|

Cannot download job %s, as it has expired and the data has been deleted from
the Application Database.  
  
`CANNOT_DOWNLOAD_JOB_IN_PROGRESS`

    

|

400

|

Cannot download job %s as it is in progress.  
  
`CANNOT_DOWNLOAD_SNAPSHOT_CONCURRENTLY`

    

|

400

|

Cannot create a manual download of a snapshot when there is already an active
download for that snapshot.  
  
`CANNOT_DOWNLOAD_SNAPSHOT_WITH_ENCRYPTION`

    

|

400

|

Cannot download snapshots with Encryption at Rest enabled.  
  
`CANNOT_EXTEND_EXPIRED_JOB`

    

|

400

|

An expired log collection job cannot be extended.  
  
`CANNOT_GENERATE_CERT_IF_ADVANCED_X509`

    

|

400

|

The user cannot create managed X.509 certs if advanced mode is on.  
  
`CANNOT_MODIFY_IN_PROGRESS_SNAPSHOT_RETENTION`

    

|

400

|

Snapshot retention can only be modified once it is completed.  
  
`CANNOT_PAUSE_RECENTLY_RESUMED_CLUSTER`

    

|

400

|

Recently resumed clusters must remain running for %d minutes to process all
queued maintenance.  
  
`CANNOT_PERFORM_RESTORE_ON_CLUSTER_WITH`

`_RUNNING_LIVE_IMPORT`

|

400

|

Cannot perform restore actions on a cluster that is the target of a live
import.  
  
`CANNOT_REMOVE_CALLER_FROM_WHITELIST`

    

|

400

|

Cannot remove caller's IP address %s from whitelist.  
  
`CANNOT_SET_CLUSTER_CHECKPOINT_INTERVAL`

`_FOR_REPLICA_SET`

|

400

|

Cluster checkpoint interval can only be set for sharded clusters, not replica
sets.  
  
`CANNOT_SET_CREDENTIALS_FOR_AUTH_MECHANISM`

    

|

400

|

Username and password fields are only supported for authentication mechanism
MONGODB_CR or PLAIN.  
  
`CANNOT_SET_PASSWORD_FOR_AUTH_MECHANISM`

    

|

400

|

Cannot change password unless authentication mechanism is MONGODB_CR or PLAIN.  
  
`CANNOT_SET_POINT_IN_TIME_WINDOW`

    

|

400

|

Setting the point in time window is not allowed.  
  
`CANNOT_SET_REF_TIME_OF_DAY`

    

|

400

|

Setting the reference point time of day is not allowed.  
  
`CANNOT_SWITCH_CPS_BACKUP_TO_CONTINUOUS`

    

|

400

|

Cannot switch a cluster's backup from Cloud Backups to Legacy Backup.  
  
`CANNOT_UPDATE_PRIVATE_IP_MODE`

    

|

400

|

Group %s has dedicated clusters, so private IP mode cannot be updated.  
  
`CANNOT_UPDATE_SMALL_CONTAINER`

    

|

400

|

Google Cloud network peering container %s is small and can't be updated.  
  
`CANNOT_USE_AWS_SECURITY_GROUP_WITHOUT`

`_VPC_PEERING_CONNECTION`

|

400

|

Cannot use aws security groups as whitelist entries without a vpc peering
connection.  
  
`CANNOT_USE_ENCRYPTION_AT_REST_BACKUP_TYPE`

    

|

400

|

Cannot use Encryption at Rest with clusters running legacy backup.  
  
`CANNOT_USE_ENCRYPTION_AT_REST_TENANT`

    

|

400

|

Cannot use Encryption at Rest with tenant clusters.  
  
`CANT_DELETE_MANAGED_POLICIES`

    

|

400

|

Only custom policies can be deleted.  
  
`CANT_EDIT_MANAGED_POLICIES`

    

|

400

|

Only custom policies can be edited.  
  
`CERT_EXPIRY_CANNOT_EXCEED_TWO_YEARS`

    

|

400

|

Atlas-generated X.509 certificates have a maximum expiration of 24 months.  
  
`CHARTS_STATUS_NOT_UPDATED`

    

|

400

|

Charts status for tenant %s is not updated with error: %s, please try again
later.  
  
`CHECKPOINT_RESTORE_UNSUPPORTED_FOR_REPLICA_SETS`

    

|

400

|

Checkpoint restores are not supported for replica sets.  
  
`CHECKPOINTS_ONLY_ON_CONTINOUS_BACKUP`

    

|

400

|

Checkpoints do not exist for Cloud Backups.  
  
`CLUSTER_ALREADY_REQUESTED_DELETION`

    

|

400

|

The cluster %s has already been requested for deletion.  
  
`CLUSTER_CANNOT_CHANGE_NAME`

    

|

400

|

Cannot change name of cluster during an update.  
  
`CLUSTER_CANNOT_CHANGE_PROVIDER_NAME`

    

|

400

|

Cannot change the cloud provider of a cluster.  
  
`CLUSTER_DISK_IOPS_INVALID`

    

|

400

|

The cluster's disk IOPS of %d is invalid. For a disk of size %s on instance
size %s with a volume type of %s, the IOPS must be %s.  
  
`CLUSTER_DISK_SIZE_INVALID`

    

|

400

|

Invalid disk size: %s.  
  
`CLUSTER_DISK_SIZE_NOT_WHOLE_NUMBER`

    

|

400

|

The cluster's disk size of %.1f GB is invalid. The disk size must be a
positive whole number.  
  
`CLUSTER_GROUP_ID_INVALID`

    

|

400

|

A cluster with group ID %s cannot be added to group %s.  
  
`CLUSTER_HOSTNAMES_UNAVAILABLE`

    

|

400

|

Cluster hostnames are unavailable; cluster (%s) might still be provisioning.  
  
`CLUSTER_MISSING_MESH_HOSTNAMES`

    

|

400

|

Mesh hostnames missing for cluster (%s); backfill pending.  
  
`CLUSTER_NAME_INVALID`

    

|

400

|

The cluster name %s is invalid. The name can only contain ASCII letters,
numbers, and hyphens.  
  
`CLUSTER_NAME_PREFIX_INVALID`

    

|

400

|

Cluster name "%s" is invalid. Atlas truncates cluster names to %d characters
which results in an invalid hostname due to a trailing "-" in the generated
cluster name prefix "%s".  
  
`CLUSTER_NAME_TOO_LONG`

    

|

400

|

Cluster name %s is limited to %d characters.  
  
`CLUSTER_NUM_SHARDS_INVALID`

    

|

400

|

The cluster's shard count must be between 1 and %s.  
  
`CLUSTER_PAUSED_CANNOT_RESTORE`

    

|

400

|

Backup restore cannot occur on a paused cluster. Please unpause the target
cluster or choose another target cluster.  
  
`CLUSTER_REPLICATION_FACTOR_INVALID`

    

|

400

|

The cluster's replication factor must be either 3, 5, or 7.  
  
`CLUSTER_RESTART_IN_PROGRESS`

    

|

400

|

A failover test is already in progress.  
  
`CLUSTER_RESTART_INVALID`

    

|

400

|

The failover test cannot begin, as not all servers in this cluster are in a
healthy state.  
  
`CLUSTER_RESTORE_IN_PROGRESS_CANNOT_UPDATE`

    

|

400

|

The update can not succeed because cluster restore is in progress. Please try
again once the restore is finished.  
  
`CLUSTER_UPGRADE_INVALID`

    

|

400

|

Cluster cannot be upgraded, as specified upgrade version is below the current
version.  
  
`COMMON_PASSWORD`

    

|

400

|

The password provided is too weak, as it can be found in most commonly used
password lists.  
  
`COMPUTE_AUTO_SCALING_INSTANCE_SIZE_RANGE_INVALID`

    

|

400

|

The min instance size (%s) must be less than the max instance size (%s).  
  
`COMPUTE_AUTO_SCALING_MAX_INSTANCE_SIZE_INVALID`

    

|

400

|

The max instance size (%s) must be greater than or equal to proposed instance
size (%s).  
  
`COMPUTE_AUTO_SCALING_MAX_INSTANCE_SIZE_REQUIRED`

    

|

400

|

Compute auto-scaling max instance size required.  
  
`COMPUTE_AUTO_SCALING_MIN_INSTANCE_SIZE_INVALID`

    

|

400

|

The min instance size (%s) must be less than or equal to proposed instance
size (%s).  
  
`COMPUTE_AUTO_SCALING_MIN_INSTANCE_SIZE`

`_INVALID_FOR_SHARDING`

|

400

|

Compute auto-scaling configuration is invalid. %s.  
  
`COMPUTE_AUTO_SCALING_MIN_INSTANCE_SIZE_REQUIRED`

    

|

400

|

Compute auto-scaling min instance size required.  
  
`COMPUTE_AUTO_SCALING_MIN_INSTANCE_SIZE`

`_STORAGE_CONFIGURATION_INVALID`

|

400

|

Compute auto-scaling configuration is invalid. %s.  
  
`COMPUTE_AUTO_SCALING_SCALE_DOWN_ENABLED_INVALID`

    

|

400

|

Compute auto-scaling must be enabled to enable down-scaling.  
  
`CONNECTED_ORG_CONFIG_IDP_NOT_IN_FEDERATION`

    

|

400

|

The specified Identity Provider Id %(s) does not match an Identity Provider in
this Federation."  
  
`CONTINUOUS_BACKUP_NOT_SUPPORTED_ON_CLUSTER_UPDATE`

    

|

400

|

Continuous backup is no longer supported for existing clusters.  
  
`CONTINUOUS_BACKUP_NOT_SUPPORTED_ON_MONGODB_VERSION`

    

|

400

|

Continuous backup is not supported on clusters with MongoDB version 4.2 or
higher.  
  
`CONTINUOUS_BACKUP_NOT_SUPPORTED_ON`

`_MONGODB_VERSION_UPGRADE`

|

400

|

Continuous backup is not supported on clusters with MongoDB version 4.2 or
higher. We recommend that you switch to Cloud Backup backup along with your
version upgrade. Your existing legacy backup snapshots will still be kept
until they expire.  
  
`CONTINUOUS_BACKUP_NOT_SUPPORTED_ON_NEW_AWS_CLUSTERS`

    

|

400

|

Continuous backup is no longer supported for new AWS clusters.  
  
`CONTINUOUS_BACKUP_NOT_SUPPORTED_ON_NEW_CLUSTERS`

    

|

400

|

Continuous backup is no longer supported for new clusters.  
  
`DATA_LAKE_CANNOT_CREATE_WITH_CLOUD_PROVIDER_CONFIG`

    

|

400

|

Data Lake tenant cannot be created with cloud provider config.  
  
`DATA_LAKE_CANNOT_CREATE_WITH_STORAGE`

    

|

400

|

Data Lake tenant cannot be created with storage.  
  
`DATA_LAKE_CANNOT_UPDATE_WITH_STORAGE`

    

|

400

|

Data Lake tenant cannot be updated with storage.  
  
`DATA_LAKE_DATABASE_STORE_REFERENCE_INVALID`

    

|

400

|

Data Lake database store (%s) reference invalid.  
  
`DATA_LAKE_DUPLICATE_STORE`

    

|

400

|

Data Lake store (%s) specified multiple times.  
  
`DATA_LAKE_HOSTNAME_INVALID`

    

|

400

|

Data Lake hostname (%s) invalid.  
  
`DATA_LAKE_TENANT_LIMIT_EXCEEDED`

    

|

400

|

Data lake tenant limit for project exceeded.  
  
`DATA_LAKE_TENANT_NAME_INVALID`

    

|

400

|

Data Lake tenant cannot be created with invalid name %s.  
  
`DATA_LAKE_UNSUPPORTED_CLOUD_PROVIDER`

    

|

400

|

Data Lake does not support the (%s) cloud provider.  
  
`DATABASE_NAME_INVALID_ADMIN`

    

|

400

|

Database name invalid. %s can only be created on the admin database.  
  
`DATABASE_NAME_INVALID_EXTERNAL`

    

|

400

|

Database name invalid. Externally authenticated users can only be created on
the $external database.  
  
`DATABASE_NAME_REQUIRED`

    

|

400

|

Metric %s requires a database name to be provided.  
  
`DATADOG_NOT_SUPPORTED_FOR_CLOUD_MANAGER`

    

|

400

|

Datadog integration is not supported for Cloud Manager projects.  
  
`DB_USAGE_ASSIGNMENT_FEATURE_DISABLED`

    

|

400

|

Cannot trigger license assignment generation from the API when the Licensing
UI is disabled.  
  
`DB_VERSION_NOT_SUPPORTED`

    

|

400

|

MongoDB version not supported.  
  
`DEFAULT_CONFIG_LIMIT_EXCEPTION`

    

|

400

|

The limit check failed while trying to add requested resource. Please try
again.  
  
`DEFAULT_INVITATION_EXCEPTION`

    

|

400

|

Failed to send an invitation to (%s) to join (%s).  
  
`DEPRECATED_EVENT_TYPE`

    

|

400

|

Event type %s is deprecated.  
  
`DEVICE_NAME_REQUIRED`

    

|

400

|

Metric %s requires a device name to be provided.  
  
`DISALLOWED_ATTRIBUTE_TURN_ON_LDAP`

    

|

400

|

Attribute %s not allowed. To enable it, change authentication to LDAP in Ops
Manager Config.  
  
`DISK_SIZE_GB_TOO_SMALL`

    

|

400

|

The selected disk size is smaller than the amount of data currently used.  
  
`DOMAIN_NAME_TOO_LONG`

    

|

400

|

The domain name for the machine is too long. Try shortening the hostname
prefix.  
  
`DOMAIN_NOT_IN_ALLOW_LIST`

    

|

400

|

User cannot be added to Organization because the domain in the User's username
is not in the Organization's Allow List.  
  
`DUAL_REPLICATION_SPEC_SPECIFIED`

    

|

400

|

Both replicationSpec and replicationSpecs fields were specified. Only one of
these two should be provided.  
  
`DUPLICATE_ADDRESSES_IN_INPUT`

    

|

400

|

Two or more of the IP addresses being added to the whitelist are the same.  
  
`DUPLICATE_CLUSTER_NAME`

    

|

400

|

A cluster named %s is already present in group %s.  
  
`DUPLICATE_CLUSTER_NAME_PREFIX`

    

|

400

|

Cluster name %s cannot have same first %d characters as another cluster name
in same group.  
  
`DUPLICATE_DATABASE_ROLES`

    

|

400

|

Duplicate database roles specified for user %s: %s.  
  
`DUPLICATE_GLOBAL_WHITELIST_ENTRY`

    

|

400

|

The provided IP address %s already exists in another global whitelist entry.  
  
`DUPLICATE_MANAGED_NAMESPACE`

    

|

400

|

Managed Namespace %s already exists.  
  
`DUPLICATE_MONGODB_BUILD_NAME`

    

|

400

|

A MongoDB build with the given trueName value ( %s) already exists."  
  
`DUPLICATE_POLICY_NAME`

    

|

400

|

All custom policies must include a unique name.  
  
`DUPLICATE_ROLE_ENTRY_IN_LDAP_MAPPING`

    

|

400

|

Each role name can only appear in one entry. %s was used more than once.  
  
`DUPLICATE_ZONE_NAME`

    

|

400

|

Zone names must be unique across all zones.  
  
`EMAIL_OR_SMS_REQUIRED_FOR_GROUP_NOTIFICATION`

    

|

400

|

Email and/or SMS must be enabled for group notifications.  
  
`EMAIL_OR_SMS_REQUIRED_FOR_USER_NOTIFICATION`

    

|

400

|

Email and/or SMS must be enabled for user notifications.  
  
`ENCRYPTION_AT_REST_NOT_ENABLED`

    

|

400

|

Encryption at Rest is not enabled for group %s.  
  
`ENCRYPTION_AT_REST_PROVIDER_NOT_SUPPORTED`

    

|

400

|

Encryption at Rest Provider cannot be configured on this cluster.  
  
`ENCRYPTION_AT_REST_SETTINGS_INVALID`

    

|

400

|

Atlas is unable to access your encryption key. You cannot change your
encryption key until access to your current encryption key has been restored.  
  
`EVENT_TYPE_UNSUPPORTED_FOR_GROUP_TYPE`

    

|

400

|

The specified event type %s it not supported for the group type of the
specified group.  
  
`EXPIRATION_DATE_EXCEEDS_MAX`

    

|

400

|

The specified expiration date can be at most %d days in the future.  
  
`EXPIRATION_DATE_IN_PAST`

    

|

400

|

The specified expiration date must be in the future.  
  
`EXPIRED_X509_CA_CERTIFICATE`

    

|

400

|

The X.509 CA certificate has expired.  
  
`FEDERATED_USER_ATTRIBUTES_CANNOT_BE_UPDATED`

    

|

400

|

Federated User attributes cannot be updated as they are managed by the
Identity Provider.  
  
`FIELD_UNSUPPORTED_FOR_OPS_MANAGER`

    

|

400

|

Received JSON contains the %s attribute, which is not supported by Ops
Manager.  
  
`FIRST_NAME_EXCEEDS_MAX_LENGTH`

    

|

400

|

First names are limited to %s characters.  
  
`FRACTIONAL_TIMESTAMP`

    

|

400

|

Timestamp must be whole number of seconds.  
  
`GLOBAL_ALERTS_ONLY`

    

|

400

|

The specified event type %s can only be used for global alerts.  
  
`GLOBAL_WHITELIST_ENTRY_REQUIRES_CIDR_BLOCK`

    

|

400

|

All global whitelist entries require a non-empty cidr block.  
  
`GLOBAL_WHITELIST_ENTRY_REQUIRES_DESCRIPTION`

    

|

400

|

All global whitelist entries require a non-empty description.  
  
`GOOGLE_CLOUD_KMS_KEY_VERSION_DESTROY_SCHEDULED`

    

|

400

|

Key version is scheduled for destruction.  
  
`GOOGLE_CLOUD_KMS_KEY_VERSION_DESTROYED`

    

|

400

|

Key version is destroyed.  
  
`GOOGLE_CLOUD_KMS_KEY_VERSION_DISABLED`

    

|

400

|

Key version is disabled.  
  
`GOOGLE_CLOUD_KMS_KEY_VERSION_NOT_FOUND`

    

|

400

|

Cannot find key version.  
  
`GOOGLE_CLOUD_KMS_KEY_VERSION_PENDING_GENERATION`

    

|

400

|

Key version is pending generation.  
  
`GROUP_MISMATCH`

    

|

400

|

The specified group ID %s does not match the URL.  
  
`HIPCHAT_NOT_SUPPORTED`

    

|

400

|

HipChat integration is only supported for Ops Manager projects.  
  
`HOST_ALREADY_EXISTS_IN_ANOTHER_PHSYICAL_HOST`

    

|

400

|

A host is already used un another physical host.  
  
`IDENTITY_PROVIDER_ALREADY_ASSOCIATED`

`_WITH_FEDERATION`

|

400

|

An Identity Provider can only be associated with a single Federation.  
  
`INACTIVE_ORG`

    

|

400

|

Organization %s is inactive.  
  
`INCORRECT_BACKUP_API_ENDPOINT`

    

|

400

|

Incorrect Public API endpoint for Cloud Backups. Please use the following end
point: (%s).  
  
`INCORRECT_PROVIDER_AUTH_CREDENTIALS`

    

|

400

|

Incorrect account credentials were specified for provider %s.  
  
`INCORRECT_SECURITY_GROUP_COUNT`

    

|

400

|

Instance must be created with exactly one SSH-enabled security group.  
  
`INCORRECT_SNMP_PORT`

    

|

400

|

SNMP address must be on port 162.  
  
`INSUFFICIENT_INSTANCE_SIZE`

    

|

400

|

This feature requires instance size %s or larger.  
  
`INVALID_AGENT_TYPE_NAME`

    

|

400

|

An invalid agent type name %s was specified.  
  
`INVALID_ALERT_STATUS`

    

|

400

|

An invalid alert status %s was specified.  
  
`INVALID_API_KEY_DESC`

    

|

400

|

API key descriptions are required and must be less than %d characters.  
  
`INVALID_ATTRIBUTE`

    

|

400

|

Invalid attribute %s specified.  
  
`INVALID_AUTH_MECHANISM`

    

|

400

|

Invalid authentication mechanism %s.  
  
`INVALID_AUTH_TYPE_NAME`

    

|

400

|

An invalid authentication type name %s was specified.  
  
`INVALID_AWS_CREDENTIALS`

    

|

400

|

Invalid AWS credentials.  
  
`INVALID_AZURE_API_REQUEST`

    

|

400

|

One or more provided Azure parameters were invalid.  
  
`INVALID_AZURE_CREDENTIALS`

    

|

400

|

Invalid Azure credentials.  
  
`INVALID_BACKUP_POLICY`

    

|

400

|

Invalid Backup Policy: %s.  
  
`INVALID_BI_CONNECTOR_READ_PREFERENCE_FOR_TOPOLOGY`

    

|

400

|

Specifying the BI Connector Read Preference value "analytics" requires one or
more analytics nodes in the target cluster.  
  
`INVALID_CHARTS_TENANT_ID`

    

|

400

|

An invalid charts tenant id %s was specified. %s.  
  
`INVALID_CHARTS_TENANT_STATUS`

    

|

400

|

An invalid charts tenant status value %s was specified.  
  
`INVALID_CIDR_BLOCK`

    

|

400

|

The cidr block %s must be in valid CIDR notation.  
  
`INVALID_CLUSTER_CHECKPOINT_INTERVAL`

    

|

400

|

Cluster checkpoint interval must be 15, 30, or 60 minutes.  
  
`INVALID_CLUSTER_CONFIGURATION`

    

|

400

|

The specified cluster configuration is not valid.  
  
`INVALID_COLLECTION_NAME`

    

|

400

|

Invalid collection names specified: %s.  
  
`INVALID_COUNTRY_CODE`

    

|

400

|

An invalid country code %s was specified.  
  
`INVALID_CREDIT_ID`

    

|

400

|

An invalid credit id was specified.  
  
`INVALID_DATABASE_NAME`

    

|

400

|

Invalid database name specified: %s.  
  
`INVALID_DATADOG_API_KEY`

    

|

400

|

Datadog API key must consist of 32 hexadecimal digits.  
  
`INVALID_DATE_FORMAT`

    

|

400

|

An invalid date value %s was specified.  
  
`INVALID_DATE_RANGE`

    

|

400

|

An invalid date range minDate=%s, maxDate=%s was specified: maxDate shouldn't
be earlier than minDate.  
  
`INVALID_DATE_RANGE_FOR_SALES_COMP`

    

|

400

|

The end date should be in past, and start date should be before end date.  
  
`INVALID_DELIVERY_SCP`

    

|

400

|

SCP restores are no longer supported.  
  
`INVALID_DIRECTORY`

    

|

400

|

An invalid directory name %s was specified.  
  
`INVALID_DOMAIN_IN_USERNAME`

    

|

400

|

The specific username contains a reserved domain.  
  
`INVALID_EMAIL_ADDRESS`

    

|

400

|

An invalid email address was specified.  
  
`INVALID_ENCRYPTION_AT_REST_PROVIDER`

    

|

400

|

An invalid Encryption at Rest provider %s was specified.  
  
`INVALID_ENUM_VALUE`

    

|

400

|

An invalid enumeration value %s was specified.  
  
`INVALID_EVENT_TYPE_FOR_ALERT`

    

|

400

|

Event type %s not supported for alerts.  
  
`INVALID_EVENT_TYPE_FOR_ESCALATION_SERVICE`

    

|

400

|

Event type %s is not supported for %s.  
  
`INVALID_FILTERLIST`

    

|

400

|

Backup configuration cannot specify both included namespaces and excluded
namespaces.  
  
`INVALID_FLOWDOCK_FLOW_NAME`

    

|

400

|

Flowdock flow name cannot contain spaces.  
  
`INVALID_FORM_PARAMETER`

    

|

400

|

Invalid form parameter %s: %s.  
  
`INVALID_FREQUENCY_TYPE_CHANGE`

    

|

400

|

The frequency type of a policy item must not be changed.  
  
`INVALID_GLOBAL_WHITELIST_DESCRIPTION`

    

|

400

|

API key descriptions must be less than %s characters.  
  
`INVALID_GOOGLE_CLOUD_CREDENTIALS`

    

|

400

|

Invalid Google Cloud credentials.  
  
`INVALID_GRANULARITY`

    

|

400

|

An invalid granularity %s was specified.  
  
`INVALID_GROUP_NAME`

    

|

400

|

An invalid group name "%s" was specified.  
  
`INVALID_GROUP_NAME_10GEN`

    

|

400

|

Group name cannot contain 10gen-" or "-10gen".  
  
`INVALID_GROUP_ROLE_UPDATE`

    

|

400

|

Cannot update a project role for a user that will be removed from the
organization.  
  
`INVALID_GROUP_TOKEN`

    

|

400

|

A group tag must be a string alphanumeric, periods, underscores, and dashe(s)
of length %d characters or less."  
  
`INVALID_HOST_PORT`

    

|

400

|

Invalid host port %d.  
  
`INVALID_HOSTNAME`

    

|

400

|

Invalid hostname %s.  
  
`INVALID_HOSTNAME_PREFIX`

    

|

400

|

Invalid hostname prefix %s. It must contain only alphanumeric characters and
hyphens, may not begin or end with a hyphen "-"), and must not be more than 63
characters long.  
  
`INVALID_HOURLY_SNAPSHOT_INTERVAL_OR`

`_RETENTION_PERIOD`

|

400

|

Hourly snapshot rules must have both interval and duration.  
  
`INVALID_INSTANCE_COUNT`

    

|

400

|

Invalid instance count %s. It must be between %s and %s.  
  
`INVALID_INSTANCE_TYPE_NAME`

    

|

400

|

Invalid instance type %s. It must be one of the listed instance types returned
in the machine configuration options.  
  
`INVALID_INTEGRATION_SETTINGS`

    

|

400

|

The provided settings for the %s integration were invalid: %s.  
  
`INVALID_INVITATION_ID`

    

|

400

|

The invitation you tried to delete does not exist or has already been
accepted.  
  
`INVALID_INVOICE_CREDIT_PAIR`

    

|

400

|

Credit does not apply to provided invoice.  
  
`INVALID_INVOICE_ID`

    

|

400

|

An invalid invoice id was specified.  
  
`INVALID_IOPS_INVALID_RATIO`

    

|

400

|

The IOPS value %s is not valid. The maximum ratio between the IOPS value and
the volume size is 30 : 1.  
  
`INVALID_IOPS_OUT_OF_BOUNDS`

    

|

400

|

The IOPS value %s is not valid. It must be between the minimum and maximum
values returned in the machine configuration options.  
  
`INVALID_IP_ADDRESS_OR_CIDR_NOTATION`

    

|

400

|

The address %s must be in valid IP address or CIDR notation.  
  
`INVALID_JSON`

    

|

400

|

Received JSON does not match expected format.  
  
`INVALID_JSON_ATTRIBUTE`

    

|

400

|

Received JSON for the %s attribute does not match expected format.  
  
`INVALID_LOCATION_CODE`

    

|

400

|

Invalid location code %s. A list of valid codes is available at
https://cloud.mongodb.com/static/atlas/country_iso_codes.txt.  
  
`INVALID_LOG_REQUEST_SIZE`

    

|

400

|

Log request size has to be a positive number.  
  
`INVALID_LOG_REQUEST_TYPES`

    

|

400

|

The list of requested log types must not be empty.  
  
`INVALID_MACHINE_IMAGE`

    

|

400

|

The specified machine image is invalid.  
  
`INVALID_MONGODB_BUILD_NAME`

    

|

400

|

The given trueName value (%s) is not valid. The name must be 3 digits
separated by ".", with an optional String appended separated by a hyphen. For
example: "4.0.0-ent".  
  
`INVALID_MONGODB_USERNAME`

    

|

400

|

The username %s is not a valid MongoDB login.  
  
`INVALID_MONGODB_VERSION_CONFIG`

    

|

400

|

The MongoDB version is not valid. %s.  
  
`INVALID_MOUNT_LOCATION`

    

|

400

|

An invalid mount location %s was specified. The mount location must be equal
to or a parent of %s.  
  
`INVALID_NAMESPACE`

    

|

400

|

Database name + collection names too long: %s.  
  
`INVALID_NETWORK_PERMISSION_COMMENT`

    

|

400

|

The comment %s must be 80 characters or less.  
  
`INVALID_NUM_OF_POLICIES`

    

|

400

|

Must have exactly one policy.  
  
`INVALID_NUM_OF_POLICY_ITEMS`

    

|

400

|

Must have at least one policy item.  
  
`INVALID_NUM_OF_SNAPSHOTS_TO_RETAIN`

    

|

400

|

Number of snapshots to retain must be greater than 0.  
  
`INVALID_OPERATOR_FOR_EVENT_TYPE`

    

|

400

|

Operator %s is not compatible with event type %s.  
  
`INVALID_ORG_NAME`

    

|

400

|

An invalid org name "%s" was specified.  
  
`INVALID_PAGER_DUTY_SERVICE_KEY`

    

|

400

|

PagerDuty service key must consist of 32 hexadecimal digits.  
  
`INVALID_PATH_PARAMETER`

    

|

400

|

Invalid path parameter %s specified.  
  
`INVALID_PERIOD`

    

|

400

|

An invalid period was specified.  
  
`INVALID_PIT_RESTORE_TIME`

    

|

400

|

Please provide a valid UTC time or an operation time (ts).  
  
`INVALID_POLICY_ID`

    

|

400

|

The policy id %s is invalid.  
  
`INVALID_POLICY_ITEM_ID`

    

|

400

|

The specified policy item id %s does not exist.  
  
`INVALID_PROVIDER`

    

|

400

|

No provider %s exists.  
  
`INVALID_PROVIDER_PARAMETERS`

    

|

400

|

Invalid parameter combination specified for provider %s.  
  
`INVALID_QUERY_PARAMETER`

    

|

400

|

Invalid query parameter %s specified.  
  
`INVALID_REFERENCE_HOUR_OF_DAY`

    

|

400

|

Snapshot schedule reference hour must be between 0 and 23, inclusive.  
  
`INVALID_REFERENCE_MINUTE_OF_HOUR`

    

|

400

|

Snapshot schedule reference minute must be between 0 and 59, inclusive.  
  
`INVALID_REFERENCE_TIME_OF_DAY_MISSING_FIELDS`

    

|

400

|

To specify snapshot schedule reference time of day, both the hour and minute
must be specified.  
  
`INVALID_REFERENCE_TIMEZONE_OFFSET`

    

|

400

|

Snapshot schedule timezone offset must conform to ISO-8601 time offset format,
such as "+0000".  
  
`INVALID_REGION`

    

|

400

|

No region %s exists for provider %s.  
  
`INVALID_RESTORE_WINDOW`

    

|

400

|

The restore window days should be a positive number.  
  
`INVALID_ROLE_FOR_GLOBAL_KEY`

    

|

400

|

API Key Role %s is not in the allowlist.  
  
`INVALID_ROLE_FOR_GROUP`

    

|

400

|

Role %s is invalid for group %s.  
  
`INVALID_ROLE_FOR_ORG`

    

|

400

|

Role %s invalid for organization %s.  
  
`INVALID_ROOT_VOLUME_SIZE`

    

|

400

|

Invalid root volume size %s. It must be between the minimum and maximum values
returned in the machine configuration options.  
  
`INVALID_ROUTE_TABLE_CIDR`

    

|

400

|

The address %s must be within the private ranges ["10.0.0.0/8",
"172.16.0.0/12", "192.168.0.0/16"].  
  
`INVALID_RSYNC_REQUEST`

    

|

400

|

Conditions are not met for beginning Rsync Initial Sync.  
  
`INVALID_SAMPLE_REFRESH_INTERVAL_BI_CONNECTOR`

    

|

400

|

Your BI Connector sample refresh interval must be greater than or equal to
zero.  
  
`INVALID_SAMPLE_SIZE_BI_CONNECTOR`

    

|

400

|

Your BI Connector schema sample size must be greater than or equal to zero.  
  
`INVALID_SECURITY_GROUP`

    

|

400

|

Security group %s is invalid. It must be one of the security groups returned
in the machine configuration options.  
  
`INVALID_SNAPSHOT_RESTORE_ENCRYPTION`

    

|

400

|

Encryption settings of target cluster and source snapshot are different.  
  
`INVALID_SNAPSHOT_SCHEDULE`

    

|

400

|

Invalid snapshot schedule: %s.  
  
`INVALID_SSH_KEY`

    

|

400

|

An invalid SSH key was specified.  
  
`INVALID_TEAM_NAME`

    

|

400

|

An invalid team name "%s" was specified.  
  
`INVALID_TENANT_BACKUP_ENABLED`

    

|

400

|

The `tenantBackupField` field must be omitted or set to %s on %s clusters.  
  
`INVALID_TENANT_CONFIGURATION`

    

|

400

|

Instance size %s with version %s is not supported in region %s. %s Clusters
with MongoDB version %s are only supported in %s.  
  
`INVALID_URL`

    

|

400

|

Invalid URL %s.  
  
`INVALID_USER`

    

|

400

|

No user %s exists.  
  
`INVALID_USERNAME`

    

|

400

|

The specified username is not a valid email address.  
  
`INVALID_VOLUME_NAME`

    

|

400

|

Invalid volume name %s. It must be one of the listed volume names returned in
the machine configuration options.  
  
`INVALID_VPC_OR_SUBNET`

    

|

400

|

Invalid or unavailable VPC %s or subnet %s.  
  
`INVALID_ZONE`

    

|

400

|

No zone %s exists for region %s.  
  
`IPV6_PERMISSION_ENTRY_NOT_SUPPORTED`

    

|

400

|

IPv6 addresses are not supported for the global whitelist entries.  
  
`IPV6_UNSUPPORTED`

    

|

400

|

The entry %s is an IPv6 value and is not supported.  
  
`JOB_EXPIRATION_DATE_EXCEEDS_MAX`

    

|

400

|

The specified expiration date can be at most %d months after the creation
date.  
  
`JOB_EXPIRATION_DATE_IN_PAST`

    

|

400

|

The specified expiration date must be in the future.  
  
`LAST_NAME_EXCEEDS_MAX_LENGTH`

    

|

400

|

Last names are limited to %s characters.  
  
`LDAP_VERIFY_CONNECTIVITY_NO_AVAILABLE_CLUSTERS`

    

|

400

|

No clusters available to perform LDAP connectivity verification for groupId:
%s. At least one active cluster running MongoDB version 3.4 or greater is
required.  
  
`LDAP_VERIFY_CONNECTIVITY_NO_AVAILABLE_INSTANCES`

    

|

400

|

No cluster nodes are available to perform LDAP connectivity verification for
groupId: %s.  
  
`LDAP_VERIFY_CONNECTIVITY_NO_AVAILABLE`

`_MONGODB_PACKAGE`

|

400

|

No MongoDB package available to perform LDAP connectivity verification for
group: %s.  
  
`LEGACY_PIT_RESTORE_UNSUPPORTED`

    

|

400

|

Non-automated non-client PIT restores are not supported via API for this
group.  
  
`LEGACY_SLACK_CONFIGURATION_UNSUPPORTED`

    

|

400

|

Legacy configurations for Slack are not permitted; OAuth2 must be configured
via the UI.  
  
`MACHINE_CONFIG_PARAMS_NOT_FOUND`

    

|

400

|

No machine configuration parameters exist for provider %s.  
  
`MAINTENANCE_WINDOW_START_DATE_AFTER_END_DATE`

    

|

400

|

Maintenance window configurations must specify a start date before their end
date.  
  
`MALFORMED_JSON`

    

|

400

|

Received JSON is malformed.  
  
`MANAGED_NAMESPACE_CANNOT_ALREADY_BE_SHARDED`

    

|

400

|

Collection %s seems to already have been sharded. If this collection was
recently deleted and recreated, it can take some time for our system to catch
up. If this is the case, please wait a few minutes and try again.  
  
`MAX_ALERT_CONFIGS_PER_GROUP_EXCEEDED`

    

|

400

|

Maximum number of alert configurations per group (%s) in %s exceeded while
trying to add alert configurations.  
  
`MAX_API_KEYS_PER_ORG_EXCEEDED`

    

|

400

|

Maximum number of API keys per org (%s) in %s exceeded while trying to add API
keys.  
  
`MAX_CUSTOM_POLICIES_PER_ORG_EXCEEDED`

    

|

400

|

The maximum number of org policies was exceeded while trying to add the new
policy.  
  
`MAX_GROUPS_PER_ORG_EXCEEDED`

    

|

400

|

Maximum number of groups per organization (%s) in %s exceeded while trying to
add group.  
  
`MAX_GROUPS_PER_USER_EXCEEDED`

    

|

400

|

Maximum number of groups per user (%s) for %s exceeded while trying to add
user to group.  
  
`MAX_NOTIFICATIONS_PER_ALERT_EXCEEDED`

    

|

400

|

Maximum number of notification methods per alert configuration (%s) exceeded
while trying to add notification methods.  
  
`MAX_ORGS_PER_USER_EXCEEDED`

    

|

400

|

Maximum number of organizations per user (%s) for %s exceeded while trying to
add user to organization.  
  
`MAX_TEAMS_PER_GROUP_EXCEEDED`

    

|

400

|

Maximum number of teams per group (%s) in %s exceeded while trying to add
teams.  
  
`MAX_TEAMS_PER_ORG_EXCEEDED`

    

|

400

|

Maximum number of teams per organization (%s) in %s exceeded while trying to
add team.  
  
`MAX_TEAMS_PER_USER_EXCEEDED`

    

|

400

|

Maximum number of teams per user (%s) for %s exceeded while trying to add user
to team.  
  
`MAX_USERS_PER_GROUP_EXCEEDED`

    

|

400

|

Maximum number of users per group (%s) in %s exceeded while trying to add
users.  
  
`MAX_USERS_PER_ORG_EXCEEDED`

    

|

400

|

Maximum number of users per org (%s) in %s exceeded while trying to add users.  
  
`MAX_USERS_PER_TEAM_EXCEEDED`

    

|

400

|

Maximum number of users per team (%s) in %s exceeded while trying to add
users.  
  
`METRIC_THRESHOLD_PRESENT`

    

|

400

|

The metric threshold should only be specific for host metric alerts.  
  
`METRIC_TYPE_UNSUPPORTED`

    

|

400

|

The metric type %s is not supported.  
  
`MISSING_API_KEY_ROLES`

    

|

400

|

API keys must have at least one role.  
  
`MISSING_ATTRIBUTE`

    

|

400

|

The required attribute %s was not specified.  
  
`MISSING_ATTRIBUTES`

    

|

400

|

The required attributes %s were not specified.  
  
`MISSING_AUTH_ATTRIBUTES`

    

|

400

|

The attributes %s and %s must be specified for authentication type %s.  
  
`MISSING_CREDENTIALS_FOR_AUTH_MECHANISM`

    

|

400

|

Authentication mechanism %s requires username and password.  
  
`MISSING_ENCRYPTION_AT_REST_PROVIDER`

    

|

400

|

At least one Encryption at Rest provider must be specified.  
  
`MISSING_MAINTENANCE_WINDOW_ALERT_TYPE_NAME`

    

|

400

|

Maintenance window configurations must specify at least one alert type.  
  
`MISSING_MAINTENANCE_WINDOW_END_DATE`

    

|

400

|

Maintenance window configurations must specify an end date.  
  
`MISSING_MAINTENANCE_WINDOW_START_DATE`

    

|

400

|

Maintenance window configurations must specify a start date.  
  
`MISSING_METRIC_THRESHOLD`

    

|

400

|

A metric threshold must be specified for host metric alerts.  
  
`MISSING_NOTIFICATIONS`

    

|

400

|

At least one notification must be specified for an alert configuration.  
  
`MISSING_ONE_OF_ATTRIBUTES`

    

|

400

|

Either the %s attribute or the %s attribute must be specified.  
  
`MISSING_ONE_OF_MANY_ATTRIBUTES`

    

|

400

|

One of the following required attributes may not have been specified: %s.  
  
`MISSING_ONE_OF_THREE_ATTRIBUTES`

    

|

400

|

Either the %s attribute, the %s attribute, or the %s attribute must be
specified.  
  
`MISSING_OR_INVALID_ATTRIBUTE`

    

|

400

|

The required attribute %s was incorrectly specified or omitted.  
  
`MISSING_PASSWORD`

    

|

400

|

Username cannot be changed without specifying password.  
  
`MISSING_POLICY_ITEM_PARAMETERS`

    

|

400

|

Each policy item must contain all required fields.  
  
`MISSING_QUERY_PARAMETER`

    

|

400

|

The required query parameter %s was not specified.  
  
`MISSING_ROLE_ENTRY_IN_LDAP_MAPPING`

    

|

400

|

Missing %s role or missing its value in LDAP Group Mapping.  
  
`MISSING_ROLES_FOR_GROUP_NOTIFICATION`

    

|

400

|

Group notifications cannot specify an empty list of roles.  
  
`MISSING_THRESHOLD`

    

|

400

|

A threshold must be specified for the specified event type.  
  
`MONGODB_BUILD_IN_USE`

    

|

400

|

The specified MongoDB build %(s) is still in use by at least one cluster in
the environment."  
  
`MONGODB_VERSION_INVALID`

    

|

400

|

An invalid MongoDB version %s was specified.  
  
`MUST_RECONFIGURE_SLACK_OAUTH2`

    

|

400

|

Slack API Tokens and Teams can only be modified by reconfiguring OAuth2 via
the UI.  
  
`MULTI_CLOUD_CLUSTER_INVALID`

    

|

400

|

Multi-Cloud clusters are not currently supported by the API.  
  
`MULTIPLE_VALUES_SPECIFIED_FOR_ONE`

`_NETWORK_PERMISSION_ENTRY`

|

400

|

Should not specify both the IP address and the CIDR block.  
  
`MUTUALLY_EXCLUSIVE_QUERY_PARAMETERS`

    

|

400

|

Either the %s query parameter or the %s query parameter but not both should be
specified.  
  
`NETWORK_PERMISSION_EXPIRATION_NOT_SUPPORTED`

    

|

400

|

Expiration dates are only supported for IP addresses.  
  
`NO_CIDR_BLOCK_OR_DESCRIPTION`

    

|

400

|

Editing a global whitelist entry requires a cidr block and/or description.  
  
`NO_COMMON_INSTANCE_FAMILY`

    

|

400

|

Cluster configuration is invalid. There is no common supported instance family
in the selected regions.  
  
`NO_ORG_NOTIFICATION_FOR_GROUP_ALERT`

    

|

400

|

Organization notification cannot be specified for group alert.  
  
`NO_PERMISSION_TO_ENCRYPT_DECRYPT`

    

|

400

|

The provided credentials do not have permission to encrypt or decrypt with the
key.  
  
`NO_PROVIDER_AVAILABILITY_ZONES`

    

|

400

|

Could not retrieve availability zones from %s account.  
  
`NO_PROVIDER_AVAILABLE_INSTANCE_TYPES`

    

|

400

|

Could not retrieve available instance types from %s account.  
  
`NO_PROVIDER_SECURITY_GROUPS`

    

|

400

|

Could not retrieve security groups from %s account.  
  
`NON_COMPLIANT_ATLAS_MAINTENANCE_WINDOW`

    

|

400

|

Your requested maintenance time change cannot be satisfied because your
project has pending maintenance that must be done by %s.  
  
`NONZERO_DELAY_REQUIRED`

    

|

400

|

The specified metric requires a nonzero delay for all notifications.  
  
`NOT_IN_PRIVATE_IP_MODE`

    

|

400

|

This action requires private IP mode to be enabled.  
  
`NOT_SHARDED`

    

|

400

|

Only sharded clusters and replica sets can be patched.  
  
`NOTIFICATION_INTERVAL_OUT_OF_RANGE`

    

|

400

|

Notifications must have an internal of at least 5 minutes.  
  
`NOTIFICATION_TYPE_IS_GLOBAL_ONLY`

    

|

400

|

At least one notification is a type that is only available for global alert
configurations.  
  
`NVME_STORAGE_CONTINUOUS_BACKUP_UNSUPPORTED`

    

|

400

|

Continuous backup is enabled for this project and is unsupported for
deployments with NVMe storage.  
  
`NVME_STORAGE_PROVIDER_BACKUP_REQUIRED`

    

|

400

|

Cloud Backup backups must be enabled for deployments with NVMe storage.  
  
`ONLY_FAILED_JOB_CAN_BE_RESTARTED`

    

|

400

|

A job can only be restarted if it is in the FAILED state.  
  
`OPLOG_RESTORE_ONLY_SUPPORTED_FOR_REPLICA_SETS`

    

|

400

|

Oplog restores are only supported for replica sets.  
  
`OPLOG_SIZE_MB_LESS_THAN_990`

    

|

400

|

Your oplog size cannot be changed to < 990 MB on MongoDB 3.6+.  
  
`OPLOG_SIZE_MB_LESS_THAN_EQUAL_ZERO`

    

|

400

|

Your oplog size cannot be <= 0.  
  
`OPLOG_SIZE_MB_TOO_BIG`

    

|

400

|

Your oplogSizeMB is too big. %s.  
  
`OPLOG_SIZE_MB_TOO_SMALL`

    

|

400

|

Your oplogSizeMB is too small. %s.  
  
`ORG_ALREADY_ASSOCIATED_WITH_FEDERATION`

    

|

400

|

An Organization can only be associated with a single Federation.  
  
`PERMANENT_ENTITY_CANNOT_BE_MADE_TEMPORARY`

    

|

400

|

A permanent entity cannot be made temporary.  
  
`PHYSICAL_HOST_ALREADY_EXISTS`

    

|

400

|

A physical host with name %s already exists.  
  
`PHYSICAL_HOST_CONTAINS_DUPLICATE_HOST_ENTRIES`

    

|

400

|

The physical host contains duplicate entries.  
  
`PHYSICAL_HOST_CONTAINS_NON_EXISTENT_HOST`

    

|

400

|

A provided host does not exist.  
  
`PHYSICAL_HOST_NOT_FOUND`

    

|

400

|

The physical host with id %s could not be found.  
  
`PIT_RESTORE_ONLY_SUPPORTED_FOR_REPLICA_SETS`

    

|

400

|

PIT restores are only supported for replica sets (please specify a checkpoint
instead).  
  
`POLICY_DESCRIPTION_OVER_LENGTH`

    

|

400

|

The policy description is over the maximum allowed length.  
  
`POLICY_DOCUMENT_MALFORMED`

    

|

400

|

The json policy document is malformed.  
  
`POLICY_NAME_OVER_LENGTH`

    

|

400

|

The policy name is over the maximum allowed length.  
  
`POLICY_NOT_FOUND`

    

|

400

|

The requested policy could not be found.  
  
`POST_AUTH_ROLE_GRANTS_MUST_CONTAIN_ORG_ROLES`

    

|

400

|

Post auth role grants can only consist of Organization roles.  
  
`PROVIDER_BACKUP_NOT_SUPPORTED`

    

|

400

|

Provider snapshot backups are not supported for this type of provider.  
  
`RATE_LIMITED_IP`

    

|

400

|

Rate limit of %s invitations per %s minutes exceeded.  
  
`REPLICATION_SPECS_INVALID`

    

|

400

|

The replicationSpecs array contains a document with missing fields. All fields
must be specified in the replicationSpecs array.  
  
`RESOURCE_NOT_FOUND_FOR_JOB`

    

|

400

|

The resource %s of type %s wasn't found.  
  
`ROLE_NEEDS_GROUP_ID`

    

|

400

|

Role %s requires a group ID.  
  
`ROLE_NEEDS_NO_GROUP_ID`

    

|

400

|

Role %s cannot be specified with a group ID.  
  
`ROLE_NEEDS_NO_ORG_ID`

    

|

400

|

Role %s cannot be specified with an organization ID.  
  
`ROLE_NEEDS_ORG_ID`

    

|

400

|

Role %s requires an organization ID.  
  
`SHARDED_CLUSTER_CANT_BECOME_REPLICA_SET`

    

|

400

|

A sharded cluster cannot become a replica set.  
  
`SHARDING_NOT_SUPPORTED`

    

|

400

|

Sharding is not supported for the selected instance size %s.  
  
`SLACK_OAUTH2_NOT_CONFIGURED`

    

|

400

|

Slack OAuth2 is not yet configured, and must be configured via the UI.  
  
`SNAPSHOT_RETENTION_LESS_THAN`

`_BACKUP_COMPLIANCE_POLICY`

|

400

|

You can't create a snapshot with a retention less than the Backup Compliance
Policy setting while you have a Backup Compliance Policy enabled.  
  
`START_DATE_AFTER_END_DATE`

    

|

400

|

The specified start date must be earlier than the specified end date.  
  
`TENANT_CLUSTER_PROCESS_ARGS_NOT_SUPPORTED`

    

|

400

|

Cannot set custom process args for tenant clusters.  
  
`TENANT_CLUSTER_TEST_FAILOVER_NOT_SUPPORTED`

    

|

400

|

Test failover not supported on tenant clusters.  
  
`TENANT_CLUSTER_UPDATE_UNSUPPORTED`

    

|

400

|

Cannot update a M0/M2/M5 cluster through the public API.  
  
`TENANT_RESTORE_DESTINATION_ENCRYPTION`

    

|

400

|

M2/M5 Snapshots cannot be restored into Dedicated clusters with Encryption at
Rest.  
  
`TENANT_RESTORE_DESTINATION_UNAVAILABLE`

    

|

400

|

The target cluster for the tenant restore is currently unavailable. Please try
again.  
  
`TENANT_RESTORE_INCOMPATIBLE_TOPOLOGY`

    

|

400

|

Tenant backups can not be restored into sharded clusters.  
  
`TENANT_RESTORE_VERSION_MISMATCH`

    

|

400

|

The specified snapshot and target cluster have mismatched versions of MongoDB.  
  
`THRESHOLD_PRESENT`

    

|

400

|

A threshold should not be present for the specified event type.  
  
`TOO_MANY_GROUP_NOTIFICATIONS`

    

|

400

|

At most one group notification can be specified for an alert configuration.  
  
`TOO_MANY_GROUP_TOKENS`

    

|

400

|

Groups are limited to %d tags.  
  
`TOO_MANY_ORG_NOTIFICATIONS`

    

|

400

|

At most one organization notification can be specified for an alert
configuration.  
  
`TOO_MANY_SNAPSHOT_DOWNLOADS`

    

|

400

|

Cannot create a manual download of a snapshot when the project is at its limit
for active downloads.  
  
`TOTAL_MODE_DEPRECATED`

    

|

400

|

Mode TOTAL is no longer supported.  
  
`UNFINISHED_ON_DEMAND_SNAPSHOT`

    

|

400

|

Another on-demand snapshot is queued or in progress.  
  
`UNITS_MISMATCH`

    

|

400

|

Threshold units cannot be converted to metric units.  
  
`UNSUPPORTED_DELIVERY_METHOD`

    

|

400

|

The specified delivery method is not supported.  
  
`UNSUPPORTED_FOR_PRIVATE_IP_MODE`

    

|

400

|

An error regarding private IP mode: %s.  
  
`UNSUPPORTED_MONGODB_VERSION_FOR_FTS`

    

|

400

|

FTS is only available for clusters running MongoDB version 4.2 or higher.  
  
`UNSUPPORTED_NOTIFICATION_TYPE`

    

|

400

|

Notification type %s is unsupported.  
  
`UNSUPPORTED_ROLE`

    

|

400

|

The provided role is not supported.  
  
`UNSUPPORTED_VERSION_FOR_LDAP_AUTHENTICATION`

    

|

400

|

LDAP authentication requires all clusters to run MongoDB version 3.4 or
higher.  
  
`USER_NOT_MANAGED_X509`

    

|

400

|

The user does not have managed mode X509 enabled.  
  
`VALIDATION_ERROR`

    

|

400

|

The request content produced the validation error: %s.  
  
`VOLUME_ENCRYPTION_NOT_AVAILABLE`

    

|

400

|

Volume encryption is not available on instances of type %s.  
  
`VOLUME_OPTIMIZATION_NOT_AVAILABLE`

    

|

400

|

Volume optimization is not available on instances of type %s.  
  
`WEAK_PASSWORD`

    

|

400

|

The specified password is not strong enough.  
  
`WEBHOOK_NOTIFICATIONS_PRESENT`

    

|

400

|

Webhook settings cannot be deleted when notifications for this integration are
present.  
  
`WEBHOOK_URL_NOT_SET`

    

|

400

|

Webhook URL must be set in the group before adding webhook notifications.  
  
`EXPORT_BUCKET_NAME_INVALID`

    

|

400

|

Export Bucket name is invalid.  
  
`EXPORT_BUCKET_DELETE_FAILED`

    

|

400

|

Failed to delete export Bucket with ID %s.  
  
`SERVER_POOL_PROPERTY_ID_UNAVAILABLE`

    

|

401

|

Attribute %s unavailable.  
  
`NO_CURRENT_USER`

    

|

401

|

No current user.  
  
`USER_UNAUTHORIZED`

    

|

401

|

Current user is not authorized to perform this action.  
  
`NOT_SELF`

    

|

401

|

The currently logged in user is not the same as the user being modified.  
  
`NOT_USER_ADMIN`

    

|

401

|

The currently logged in user does not have the user administrator role for any
group, team, or organization containing user %s.  
  
`NOT_GLOBAL_USER_ADMIN`

    

|

401

|

The currently logged in user does not have the global user administrator role.  
  
`NOT_GLOBAL_USER_ADMIN_OR_SELF`

    

|

401

|

The currently logged in user is not the same as the user being modified and
does not have the global user administrator role.  
  
`NOT_GROUP_USER_ADMIN`

    

|

401

|

The currently logged in user does not have the user administrator role in
group %s.  
  
`NOT_ORG_GROUP_CREATOR`

    

|

401

|

The currently logged in user does not have the group creator role in
organization %s.  
  
`NOT_ORG_OWNER`

    

|

401

|

The currently logged in user does not have the owner role in organization %s.  
  
`NOT_ORG_USER_ADMIN`

    

|

401

|

The currently logged in user does not have the user administrator role in
organization %s.  
  
`WHITELIST_ACCESS_DENIED`

    

|

401

|

Cannot access whitelist for user %s, which is not currently logged in.  
  
`NOT_IN_GROUP`

    

|

401

|

The current user is not in the group, or the group does not exist.  
  
`BILLING_UNSUPPORTED`

    

|

401

|

Billing administrator roles are not supported by Ops Manager.  
  
`PROVIDER_AUTH_FAILED`

    

|

401

|

Account failed to authenticate with %s.  
  
`USER_CANNOT_ACCESS_GROUP`

    

|

401

|

User cannot access this group.  
  
`USER_CANNOT_ACCESS_ORG`

    

|

401

|

User cannot access this organization.  
  
`NOT_API_KEY_ADMIN`

    

|

401

|

The currently logged in user does not have user administrator role in
organization or group that API key with ID %s belongs to.  
  
`API_KEY_WHITELIST_ACCESS_DENIED`

    

|

401

|

API key whitelists are only accessible by the API key or by a user
administrator.  
  
`TENANT_SNAPSHOT_ACCESS_DENIED`

    

|

401

|

Not authorized to access specified tenant snapshot.  
  
`ACCOUNT_SUSPENDED`

    

|

402

|

Organization has an unpaid invoice that is more than 30 days old.  
  
`CANNOT_START_BACKUP_NO_BILLING_INFO`

    

|

402

|

Cannot start backup without providing billing information.  
  
`NO_PAYMENT_INFORMATION_FOUND`

    

|

402

|

No payment information was found for group %s.  
  
`CANNOT_DELETE_ORG_FAILED_PAYMENTS`

    

|

402

|

Cannot delete organization because it has failed payments.  
  
`FAILED_TO_DELETE_ORG_CHARGE_FAILED`

    

|

402

|

Charge failed attempting to delete organization.  
  
`ACCESS_FORBIDDEN`

    

|

403

|

Access to this resource is forbidden for current user.  
  
`INVITATION_ONLY_MODE_OR_LDAP`

    

|

403

|

Forbidden when using an LDAP backend or when the creating subsequent users
beyond the first in invitation-only mode.  
  
`IP_ADDRESS_NOT_ON_WHITELIST`

    

|

403

|

IP address %s is not allowed to access this resource.  
  
`RESOURCE_REQUIRES_WHITELIST`

    

|

403

|

This resource requires access through a whitelist of ip ranges.  
  
`ORG_REQUIRES_WHITELIST`

    

|

403

|

This organization requires access through a whitelist of ip ranges.  
  
`FEATURE_UNSUPPORTED`

    

|

403

|

Feature not supported by current account level.  
  
`CANNOT_MODIFY_MANAGED_HOST`

    

|

403

|

Cannot modify host %s because it is managed by Automation.  
  
`CANNOT_DELETE_LAST_OWNER`

    

|

403

|

Cannot remove the last owner from the group. If you are trying to close the
group by removing all users and teams, please delete the group instead.  
  
`CANNOT_DELETE_LAST_ADMIN`

    

|

403

|

An organization or project needs to have at least one owner. You cannot demote
or remove the last owner.  
  
`CANNOT_DEMOTE_LAST_OWNER`

    

|

403

|

Cannot demote the last owner of the group.  
  
`NO_ROLES_IN_ASSIGNMENT`

    

|

403

|

You cannot remove all project roles a team has.  
  
`CANNOT_DEMOTE_LAST_ORG_OWNER`

    

|

403

|

Cannot demote the last owner of the organization.  
  
`NO_FREE_TIER_API`

    

|

403

|

The API is not supported for the Free Tier of Cloud Manager.  
  
`UNSUPPORTED_FOR_CURRENT_PLAN`

    

|

403

|

Operation not supported for current plan.  
  
`UNSUPPORTED_SET_BACKUP_STATE`

    

|

403

|

Setting the backup state to %s is not supported.  
  
`CANNOT_CHANGE_GROUP_NAME`

    

|

403

|

Current user is not authorized to change group name.  
  
`CANNOT_DELETE_FROM_CLUSTER_SNAPSHOT`

    

|

403

|

Cannot individually delete a snapshot that is part of a cluster snapshot.  
  
`ROLES_SPECIFIED_FOR_USER`

    

|

403

|

Roles specified for user.  
  
`UNSUPPORTED_FOR_CURRENT_CONFIG`

    

|

403

|

Operation not supported for current configuration.  
  
`CANNOT_ADD_GLOBAL_ROLE`

    

|

403

|

Adding a global role is not supported.  
  
`HOURLY_BILLING_LIMIT_EXCEEDED`

    

|

403

|

The hourly billing limit has been exceeded.  
  
`GROUP_USERS_LIMIT_EXCEEDED`

    

|

403

|

Groups can contain at most %d database users.  
  
`COLLECTION_ROLES_LIMIT_EXCEEDED`

    

|

403

|

Exceeded maximum number of collection level permissions. This group can define
at most %d collection level roles.  
  
`CUSTOM_ROLES_LIMIT_EXCEEDED`

    

|

403

|

Exceeded maximum number of custom roles.  
  
`MAX_PUBLIC_API_KEY_REACHED`

    

|

403

|

You have reached the limit of max number of API keys. You can have at most %s
API keys.  
  
`CROSS_REGION_NETWORK_PERMISSIONS_LIMIT_EXCEEDED`

    

|

403

|

Cannot have more than %d cross-region network permissions.  
  
`ATLAS_NETWORK_PERMISSIONS_LIMIT_EXCEEDED`

    

|

403

|

Too many network permission entries. Only %d entries are supported.  
  
`ATLAS_NETWORK_PERMISSIONS_SIZE_EXCEEDED`

    

|

403

|

This project's IP whitelist is too large for tenant backups to be downloaded.
Consider restoring to a new cluster and using mongodump or contact support.  
  
`CANNOT_MODIFY_CHARTS_USER`

    

|

403

|

Cannot modify the Charts user.  
  
`GLOBAL_USER_OUTSIDE_SUBNET`

    

|

403

|

Global user is from outside whitelisted subnets.  
  
`CANNOT_MODIFY_SNAPSHOT`

    

|

403

|

Cannot modify snapshot %s because of invalid fields.  
  
`CANNOT_MODIFY_CLUSTER_SNAPSHOT`

    

|

403

|

Cannot individually modify a snapshot %s that is part of a cluster snapshot.  
  
`CANNOT_RESTORE_TO_TARGET`

    

|

403

|

Cannot restore with insufficient permission on source snapshot or target
cluster.  
  
`API_KEY_CANNOT_CREATE_ORG`

    

|

403

|

API keys cannot create organizations.  
  
`CANNOT_CREATE_FIRST_USER_USERS_ALREADY_EXIST`

    

|

403

|

Cannot create the user: there are already users in the system.  
  
`DATA_LAKE_AUTH_TO_ATLAS_CLUSTER_GROUP`

`_DOES_NOT_MATCH_TENANT_GROUP`

|

403

|

The tenant group (%s), does not match the group of the cluster %(s) for which
user access has been requested."  
  
`USER_ORGS_RESTRICTED`

    

|

403

|

This user cannot create or join organizations becaues of federation
organization restrictions.  
  
`MONGODB_BUILD_DOES_NOT_EXIST`

    

|

404

|

The specified MongoDB build (%s) does not exist.  
  
`RESOURCE_NOT_FOUND`

    

|

404

|

Cannot find resource %s.  
  
`CLOUD_PROVIDER_CONTAINER_NOT_FOUND`

    

|

404

|

An invalid cloud provider container ID %s was specified.  
  
`SERVER_POOL_SERVER_ID_NOT_FOUND`

    

|

404

|

An invalid server pool server ID %s was specified.  
  
`SERVER_POOL_REQUEST_ID_NOT_FOUND`

    

|

404

|

An invalid server pool request ID %s was specified.  
  
`SERVER_POOL_PROPERTY_ID_NOT_FOUND`

    

|

404

|

An invalid server pool property ID %s was specified.  
  
`SERVER_POOL_PROPERTY_VALUE_NOT_FOUND`

    

|

404

|

An invalid value %s of server pool property ID %s was specified.  
  
`SERVER_POOL_SERVER_HOSTNAME_NOT_FOUND`

    

|

404

|

An invalid server pool server hostname %s was specified.  
  
`SERVER_POOL_DISABLED`

    

|

404

|

This feature is disabled. If you use this feature, please contact MongoDB
support.  
  
`INVALID_ALERT_CONFIG_ID`

    

|

404

|

An invalid alert configuration ID %s was specified.  
  
`MISSING_ALERT_CONFIG_ID`

    

|

404

|

No alert configuration ID was found.  
  
`INVALID_ALERT_ID`

    

|

404

|

An invalid alert ID %s was specified.  
  
`INVALID_CHECKPOINT_ID`

    

|

404

|

An invalid checkpoint ID %s was specified.  
  
`INVALID_CLUSTER_ID`

    

|

404

|

An invalid cluster ID %s was specified.  
  
`INVALID_GROUP_ID`

    

|

404

|

An invalid group ID %s was specified.  
  
`INVALID_LOG_COLLECTION_JOB_ID`

    

|

404

|

An invalid log collection job ID %s was specified.  
  
`INVALID_JOB_ID`

    

|

404

|

An invalid restore job ID %s was specified.  
  
`INVALID_KEY_ID`

    

|

404

|

An invalid key ID %s was specified.  
  
`INVALID_MACHINE_ID`

    

|

404

|

An invalid machine ID %s was specified.  
  
`INVALID_ORG_ID`

    

|

404

|

An invalid organization ID %s was specified.  
  
`INVALID_TEAM_ID`

    

|

404

|

An invalid team ID %s was specified.  
  
`INVALID_SNAPSHOT_ID`

    

|

404

|

An invalid snapshot ID %s was specified.  
  
`INVALID_USER_ID`

    

|

404

|

An invalid user ID %s was specified.  
  
`INVALID_PEER_ID`

    

|

404

|

An invalid peer ID %s was specified.  
  
`INVALID_WINDOW_ID`

    

|

404

|

An invalid maintenance window ID %s was specified.  
  
`GROUP_NOT_FOUND`

    

|

404

|

No group with ID %s exists.  
  
`GROUP_NAME_NOT_FOUND`

    

|

404

|

No group with name "%s" exists.  
  
`AGENT_API_KEY_NOT_FOUND`

    

|

404

|

No group with API key %s exists.  
  
`ORG_NOT_FOUND`

    

|

404

|

No organization with ID %s exists.  
  
`ORG_NAME_NOT_FOUND`

    

|

404

|

No organization with name %s exists.  
  
`EXPECTED_NON_ATLAS_ORG`

    

|

404

|

The organization with id %s is an Atlas organization.  
  
`PROVISION_MACHINE_JOB_NOT_FOUND`

    

|

404

|

No provision machine job with ID %s exists in group %s.  
  
`PROVISIONED_MACHINE_NOT_FOUND`

    

|

404

|

No provisioned machine with ID %s exists in group %s.  
  
`HOST_NOT_FOUND`

    

|

404

|

No host with ID %s exists in group %s.  
  
`HOSTNAME_AND_PORT_NOT_FOUND`

    

|

404

|

No host with hostname and port %s exists in group %s.  
  
`INVALID_METRIC_NAME`

    

|

404

|

An invalid metric name %s was specified.  
  
`NOT_CONFIG_SERVER`

    

|

404

|

Host %s is not an SCCC config server.  
  
`ALERT_NOT_FOUND`

    

|

404

|

No alert with ID %s exists in group %s.  
  
`GLOBAL_ALERT_CONFIG_NOT_FOUND`

    

|

404

|

No global alert configuration with ID %s exists.  
  
`ALERT_CONFIG_NOT_FOUND`

    

|

404

|

No alert configuration with ID %s exists in group %s.  
  
`USER_NOT_FOUND`

    

|

404

|

No user with ID %s exists.  
  
`USERNAME_NOT_FOUND`

    

|

404

|

No user with username %s exists.  
  
`CANNOT_ADD_PENDING_USER`

    

|

404

|

The user cannot be added to any group or teams in this organization as it is a
pending user/the user has not accepted the invite to this organization.  
  
`CLUSTER_NOT_FOUND`

    

|

404

|

No cluster named %s exists in group %s.  
  
`CLUSTER_NAME_NOT_FOUND`

    

|

404

|

No cluster with name "%s" exists in group %s.  
  
`SNAPSHOT_NOT_FOUND`

    

|

404

|

No snapshot with ID %s exists for cluster %s.  
  
`UNABLE_T0_FIND_SNAPSHOT_PRIOR_TO_PIT_RESTORE_OPTIME`

    

|

404

|

Unable to find snapshot prior to pit restore optime.  
  
`CONFIG_SNAPSHOT_NOT_FOUND`

    

|

404

|

No snapshot with ID %s exists for config server %s.  
  
`RESTORE_JOB_NOT_FOUND`

    

|

404

|

No restore job with ID %s exists for cluster %s.  
  
`RESTORE_JOB_NOT_FOUND_IN_GROUP`

    

|

404

|

No restore job with ID %s exists in group %s.  
  
`CONFIG_RESTORE_JOB_NOT_FOUND`

    

|

404

|

No restore job with ID %s exists for config server %s.  
  
`CHECKPOINT_NOT_FOUND`

    

|

404

|

No checkpoint with ID %s exists for cluster %s.  
  
`WHITELIST_NOT_FOUND`

    

|

404

|

IP address %s not on whitelist for user %s.  
  
`ATLAS_NETWORK_PERMISSION_ENTRY_NOT_FOUND`

    

|

404

|

IP Address %s not on Atlas whitelist for group %s.  
  
`ATLAS_WHITELIST_NOT_FOUND`

    

|

404

|

IP Address %s not on Atlas whitelist for group %s.  
  
`USER_NOT_IN_GROUP`

    

|

404

|

User %s is not in group %s.  
  
`USER_NOT_IN_ORG`

    

|

404

|

User %s is not in organization %s.  
  
`BACKUP_CONFIG_NOT_FOUND`

    

|

404

|

No backup configuration exists for cluster %s in group %s.  
  
`SSH_KEY_NOT_FOUND`

    

|

404

|

No SSH key with ID %s exists.  
  
`SSH_KEY_NAME_NOT_FOUND`

    

|

404

|

No SSH key with name "%s" exists.  
  
`NO_SSH_KEYS_IN_GROUP`

    

|

404

|

No SSH keys found in group %s.  
  
`PROVIDER_NOT_FOUND`

    

|

404

|

No provider %s exists.  
  
`PROVIDER_UNSUPPORTED`

    

|

404

|

Provider %s not currently supported.  
  
`PROVIDER_CONFIG_NOT_FOUND`

    

|

404

|

No provider configuration exists for provider %s.  
  
`PROVIDER_CONFIG_ID_NOT_FOUND`

    

|

404

|

No provider configuration with ID %s exists for provider %s.  
  
`MAINTENANCE_WINDOW_NOT_FOUND`

    

|

404

|

No maintenance window with ID %s exists in group %s.  
  
`AUTOMATION_CONFIG_NOT_FOUND`

    

|

404

|

No automation configuration exists for group %s.  
  
`LAST_PING_NOT_FOUND`

    

|

404

|

No last ping exists for group %s.  
  
`NOT_DATABASE_OR_DISK_METRIC`

    

|

404

|

Metric %s is neither a database nor a disk metric.  
  
`DEVICE_NOT_FOUND`

    

|

404

|

No device with name %s exists on host %s.  
  
`HOST_LAST_PING_NOT_FOUND`

    

|

404

|

No last ping exists for host %s in group %s.  
  
`ATLAS_GROUP`

    

|

404

|

Group %s is an Atlas group; use the Atlas Public API at /api/atlas/v1.0 to
access it.  
  
`NOT_ATLAS_GROUP`

    

|

404

|

Group %s is not an Atlas group; use the Cloud Manager Public API at
/api/public/v1.0 to access it.  
  
`INVALID_ATLAS_GROUP`

    

|

404

|

Atlas group %s is in an invalid state and cannot be loaded.  
  
`NOT_ATLAS_ORG`

    

|

404

|

Organization %s is not an Atlas organization; use the Cloud Manager Public API
at /api/public/v1.0 to access it.  
  
`ATLAS_GROUP_TAG_NOT_SUPPORTED`

    

|

404

|

Atlas group %s is does not support the tag %s.  
  
`NO_BACKUP_ENCRYPTION_KEY_FOR_SHARDED_CLUSTER`

    

|

404

|

No backup encryption key is available for a sharded cluster; keys can be
accessed for each shard individually.  
  
`PEER_NOT_FOUND`

    

|

404

|

No peer with ID %s exists in project %s.  
  
`AZURE_CUSTOMER_NETWORK_UNREACHABLE`

    

|

404

|

External Azure subscription unreachable.  
  
`BACKUP_DEPLOYMENT_NOT_FOUND`

    

|

404

|

Deployment ID %s not found.  
  
`DAEMON_MACHINE_CONFIG_NOT_FOUND`

    

|

404

|

Daemon machine config %s not found.  
  
`S3_SNAPSHOT_CONFIG_NOT_FOUND`

    

|

404

|

S3 snapshot config %s not found.  
  
`MONGO_SNAPSHOT_CONFIG_NOT_FOUND`

    

|

404

|

Mongo snapshot config %s not found.  
  
`FILESYSTEM_SNAPSHOT_CONFIG_NOT_FOUND`

    

|

404

|

Filesystem snapshot config %s not found.  
  
`S3_OPLOG_CONFIG_NOT_FOUND`

    

|

404

|

S3 oplog config %s not found.  
  
`MONGO_OPLOG_CONFIG_NOT_FOUND`

    

|

404

|

Mongo oplog config %s not found.  
  
`MONGO_SYNC_CONFIG_NOT_FOUND`

    

|

404

|

Mongo sync config %s not found.  
  
`LDAP_VERIFY_CONNECTIVITY_REQUEST_NOT_FOUND`

    

|

404

|

LDAP connectivity verification request %s not found for group %s.  
  
`TEAM_NOT_FOUND`

    

|

404

|

No team with ID %s exists.  
  
`TEAM_NAME_NOT_FOUND`

    

|

404

|

No team with name "%s" exists.  
  
`TEAM_NOT_IN_ORG`

    

|

404

|

Team %s is not in Organization %s.  
  
`TEAM_NOT_IN_GROUP`

    

|

404

|

The team in your request is not assigned to this group.  
  
`CANNOT_DELETE_TEAM_ASSIGNED_TO_PROJECT`

    

|

404

|

You cannot delete a team that has at least one project assigned to it. Make
sure to remove the team from all project before deleting it.  
  
`INVOICE_NOT_FOUND`

    

|

404

|

No invoice with ID %s exists in organization %s.  
  
`PENDING_INVOICE_NOT_FOUND`

    

|

404

|

No pending invoice exists in organization %s.  
  
`EVENT_NOT_FOUND`

    

|

404

|

No event with ID %s exists for group %s.  
  
`ORG_EVENT_NOT_FOUND`

    

|

404

|

No event with ID %s exists for organization %s.  
  
`GLOBAL_EVENT_NOT_FOUND`

    

|

404

|

No event with ID %s exists.  
  
`AWS_CUSTOMER_MASTER_KEY_NOT_FOUND`

    

|

404

|

No AWS customer master key found for group %s.  
  
`ATLAS_CUSTOM_ROLE_NOT_FOUND`

    

|

404

|

The specified custom db role %s does not exist.  
  
`LOG_COLLECTION_JOB_NOT_FOUND_IN_GROUP`

    

|

404

|

No log collection job with ID %s exists in group %s.  
  
`DATA_EXPORT_METADATA_NOT_FOUND`

    

|

404

|

No Data Export Metadata exists for S3 Object Key %s.  
  
`API_KEY_WHITELIST_NOT_FOUND`

    

|

404

|

IP address %s not on whitelist for API key %s.  
  
`DATA_LAKE_TENANT_NOT_FOUND_FOR_ID`

    

|

404

|

Data Lake tenant with tenantId %s not found.  
  
`DATA_LAKE_TENANT_NOT_FOUND_FOR_NAME`

    

|

404

|

Data Lake tenant for project %s and name %s not found.  
  
`DATA_LAKE_TENANT_INVALID_STATE`

    

|

404

|

Data Lake tenant is not in a valid state <%s> for the requested operation.  
  
`DATA_LAKE_CANNOT_ACCESS_TEST_S3_BUCKET`

    

|

404

|

Data Lake cannot access the specified test S3 bucket (%s) via the provided IAM
role. Ensure that the IAM role provides access to retrieve the bucket's
location and read its contents. %s.  
  
`DATA_LAKE_CANNOT_ASSUME_ROLE`

    

|

404

|

Data Lake cannot assume the specified role (%s).  
  
`DATA_LAKE_AUTH_TO_ATLAS_NOT_SUPPORTED_FOR_MONGODB_VERSION`

    

|

404

|

Auth to Atlas is not supported on cluster %s in group %s because the MongoDB
version, %s, is not supported.  
  
`TENANT_SNAPSHOT_NOT_FOUND`

    

|

404

|

No M2/M5 snapshot with ID %s exists for cluster %s.  
  
`TENANT_RESTORE_NOT_FOUND`

    

|

404

|

No M2/M5 restore with ID %s exists for cluster %s.  
  
`TENANT_CANNOT_DEFINE_ANALYZERS`

    

|

404

|

Cannot define custom analyzers for a shared cluster.  
  
`GLOBAL_WHITELIST_ENTRY_NOT_FOUND`

    

|

404

|

No existing global whitelist entries match the provided id %s.  
  
`IDENTITY_PROVIDER_DOES_NOT_EXIST`

    

|

404

|

The given 'oktaIdpId' does not correspond to an existing Identity Provider in
Okta.  
  
`CERTIFICATE_DOES_NOT_EXIST`

    

|

404

|

Certificate does not exist. It may have expired or been revoked.  
  
`INTEGRATION_NOT_CONFIGURED`

    

|

404

|

The integration of type '%s' is not configured for this group.  
  
`PRIVATELINK_NOT_FOUND`

    

|

404

|

A PrivateLink with id %s does not exist.  
  
`PRIVATELINK_INTERFACE_ENDPOINT_NOT_FOUND`

    

|

404

|

A PrivateLink interface endpoint with id %s does not exist.  
  
`PRIVATELINK_INTERFACE_ENDPOINT_ID_MALFORMED`

    

|

404

|

AWS interface endpoint ids must begin with 'vpce-' followed by a series of
alphanumeric characters.  
  
`EXPORT_BUCKET_NOT_FOUND`

    

|

404

|

No export Bucket with ID %s does not exist.  
  
`ATLAS_BACKUP_CANCEL_SHARD_RESTORE_JOB_NOT_ALLOWED`

    

|

405

|

Cannot cancel a restore job of an individual shard. Please cancel the entire
sharded cluster restore job.  
  
`WRITES_NOT_ALLOWED_DURING_APP_UPGRADES`

    

|

405

|

Create, update, and delete API endpoints are disabled while the system is
being upgraded.  
  
`SERVER_POOL_SERVER_INVALID_STATE`

    

|

409

|

The specified server pool server %s cannot be deleted with an invalid state.  
  
`SERVER_POOL_REQUEST_INVALID_STATE`

    

|

409

|

The specified server pool request %s cannot be cancelled with an invalid
state.  
  
`SERVER_POOL_SERVER_PROPERTY_IN_USE`

    

|

409

|

The specific server property %s cannot be deleted because it is still in use.  
  
`GROUP_ALREADY_EXISTS`

    

|

409

|

A group with name "%s" already exists.  
  
`USER_ALREADY_EXISTS`

    

|

409

|

A user with username %s already exists.  
  
`SSH_KEY_ALREADY_EXISTS`

    

|

409

|

An SSH key with the name "%s" already exists.  
  
`CANNOT_MODIFY_SHARD_BACKUP_CONFIG`

    

|

409

|

Cannot modify backup configuration for individual shard; use cluster ID %s for
entire cluster.  
  
`CANNOT_START_BACKUP_INVALID_STATE`

    

|

409

|

Cannot start backup unless the cluster is in the INACTIVE or STOPPED state.  
  
`CANNOT_STOP_BACKUP_INVALID_STATE`

    

|

409

|

Cannot stop backup unless the cluster is in the STARTED state.  
  
`CANNOT_TERMINATE_BACKUP_INVALID_STATE`

    

|

409

|

Cannot terminate backup unless the cluster is in the STOPPED state.  
  
`CANNOT_GET_BACKUP_CONFIG_INVALID_STATE`

    

|

409

|

Cannot get backup configuration without cluster being monitored.  
  
`UPGRADE_FOR_EXCLUDED_NAMESPACES`

    

|

409

|

Excluded namespaces are not supported by this Backup Agent version; please
upgrade.  
  
`UPGRADE_FOR_INCLUDED_NAMESPACES`

    

|

409

|

Included namespaces are not supported by this Backup Agent version; please
upgrade.  
  
`MISSING_SYNC_SOURCE`

    

|

409

|

Requested changes will require a sync or resync, so a sync source must be
provided.  
  
`CANNOT_SET_BACKUP_AUTH_FOR_MANAGED_CLUSTER`

    

|

409

|

Username and password cannot be manually set for a managed cluster.  
  
`UPGRADE_FOR_CLUSTER_CHECKPOINT_INTERVAL`

    

|

409

|

Cluster checkpoint interval not supported by this Backup Agent version; please
upgrade.  
  
`CANNOT_CLOSE_GROUP_ACTIVE_BACKUP`

    

|

409

|

Cannot close group while it has active backups; please terminate all backups.  
  
`CANNOT_CLOSE_GROUP_ACTIVE_ATLAS_CLUSTERS`

    

|

409

|

Cannot close group while it has active clusters; please terminate all
clusters.  
  
`CANNOT_CLOSE_GROUP_ACTIVE_BACKUP_COMPLIANCE_POLICY`

    

|

409

|

You can't terminate a project if it has a Backup Compliance Policy enabled and
active snapshots. Remove the snapshots.  
  
`NO_GROUP_SSH_KEY`

    

|

409

|

No group SSH key exists for group %s.  
  
`CANNOT_START_RESTORE_JOB_FOR_DELETED_SNAPSHOT`

    

|

409

|

Cannot start restore job for deleted snapshot.  
  
`CANNOT_START_RESTORE_JOB_FOR_DELETED_CLUSTER_SNAPSHOT`

    

|

409

|

Cannot start restore job for deleted cluster snapshot.  
  
`CANNOT_START_RESTORE_JOB_FOR_INCOMPLETE_CLUSTER_SNAPSHOT`

    

|

409

|

Cannot start restore job for incomplete cluster snapshot.  
  
`CANNOT_DOWNLOAD_INCOMPLETE_SNAPSHOT`

    

|

409

|

Cannot download incomplete cluster snapshot.  
  
`LINK_EXPIRATION_AFTER_SNAPSHOT_DELETION`

    

|

409

|

Cannot set HTTP link expiration time after snapshot deletion time.  
  
`NO_CHECKPOINT_FOR_PIT_RESTORE`

    

|

409

|

A suitable checkpoint could not be found for the specified continuous cloud
backup.  
  
`INVALID_RESTORE_PROCESS`

    

|

409

|

Process is not valid for automated restore.  
  
`RESTORE_INITIATION_FAILED`

    

|

409

|

Restore process initiation failed: %s.  
  
`INVALID_RESTORE_SNAPSHOT_FILTER_LIST`

    

|

409

|

The requested restore could not be started. An associated snapshot either has
a blacklist or whitelist.  
  
`PROVISIONED_MACHINE_COULD_NOT_TERMINATE`

    

|

409

|

Provisioned machine with ID %s could not terminate because a MongoDB process,
Monitoring Agent, or Backup Agent is currently running on the machine.  
  
`ADDRESS_ALREADY_IN_WHITELIST`

    

|

409

|

The address %s is already on the whitelist.  
  
`CANNOT_ROTATE_KEY_ENCRYPTION_DISABLED`

    

|

409

|

Cannot rotate encryption key because encryption is disabled.  
  
`OVERLAPPING_CIDR_BLOCK`

    

|

409

|

The CIDR block %s overlaps with another peer's CIDR block.  
  
`OVERLAPPING_ATLAS_CIDR_BLOCK`

    

|

409

|

The CIDR block %s overlaps with an Atlas CIDR block.  
  
`PEER_ALREADY_EXISTS`

    

|

409

|

The peer with AWS Account ID %s and VPC ID %s already exists.  
  
`PEER_ALREADY_EXISTS_GCP`

    

|

409

|

The peer with GCP Project ID %s and network name %s already exists.  
  
`PEER_ALREADY_EXISTS_AZURE`

    

|

409

|

The peer with Azure Subscription ID %s and Virtual Network name %s already
exists.  
  
`PEER_ALREADY_REQUESTED_DELETION`

    

|

409

|

The peer with ID %s has already been requested for deletion.  
  
`PEER_INVALID_STATE`

    

|

409

|

The peer with ID %s in group %s cannot be updated in its current state.  
  
`PEER_MAXIMUM_REACHED`

    

|

409

|

The maximum number of peering connections (%s) has been reached.  
  
`CONTAINERS_IN_USE`

    

|

409

|

Cannot modify in use containers. %s.  
  
`CONTAINER_ALREADY_EXISTS`

    

|

409

|

A container already exists for group %s.  
  
`NO_CAPACITY`

    

|

409

|

Cannot find the %s capacity for group %s.  
  
`OUT_OF_CAPACITY`

    

|

409

|

The requested region is currently out of capacity for the requested instance
size.  
  
`REGION_UNAVAILABLE`

    

|

409

|

The selected region %s is unavailable for use.  
  
`MULTIPLE_GROUPS`

    

|

409

|

Multiple groups exist with the specified name.  
  
`BACKUP_GROUP_MISCONFIGURED_ENV`

    

|

409

|

Environment is incorrectly configured %s)."  
  
`BACKUP_ACTIVE_BACKUP_JOBS`

    

|

409

|

This group has active backup jobs, can't update deployment id.  
  
`BACKUP_S3_CONNECTION_FAILED`

    

|

409

|

S3 connectivity problems: %s.  
  
`BACKUP_S3_VALIDATION_FAILED`

    

|

409

|

S3 validation problems: %s.  
  
`BACKUP_S3_TOS_NOT_ACCEPTED`

    

|

409

|

Must accept the terms of service.  
  
`BACKUP_MONGO_CONNECTION_FAILED`

    

|

409

|

MongoDB connectivity problems: %s.  
  
`BACKUP_CANNOT_REMOVE_S3_STORE_CONFIG`

    

|

409

|

Cannot delete the s3 snapshot config. Please make sure no jobs are bound to
config and no snapshots are in it before deleting.  
  
`BACKUP_CANNOT_REMOVE_S3_OPLOG_STORE_CONFIG`

    

|

409

|

Cannot delete the s3 oplog config. Please make sure no jobs are bound to it.  
  
`BACKUP_CANNOT_REMOVE_OPLOG_STORE_CONFIG`

    

|

409

|

Cannot delete the mongo oplog config. Please make sure no jobs are bound to
it.  
  
`BACKUP_CANNOT_REMOVE_SYNC_STORE_CONFIG`

    

|

409

|

Cannot delete the mongo sync config. Please make sure no jobs are bound to it.  
  
`BACKUP_CANNOT_REMOVE_DAEMON_CONFIG`

    

|

409

|

Cannot delete the daemon config. Please make sure no jobs are bound to it.  
  
`BACKUP_CANNOT_REMOVE_DB_STORE_CONFIG`

    

|

409

|

Cannot delete the mongo snapshot config. Please make sure no jobs are bound to
config and no snapshots are in it before deleting.  
  
`BACKUP_CANNOT_REMOVE_FS_STORE_CONFIG`

    

|

409

|

Cannot delete the file system snapshot config. Please make sure no jobs are
bound to config and no snapshots are in it before deleting.  
  
`CLUSTER_ALREADY_PAUSED`

    

|

409

|

Cannot pause a cluster that is already paused.  
  
`CANNOT_UPDATE_PAUSED_CLUSTER`

    

|

409

|

Cannot update cluster %s while it is paused or being paused.  
  
`CANNOT_UPDATE_AND_PAUSE_CLUSTER`

    

|

409

|

Cannot update and pause cluster %s at the same time.  
  
`CANNOT_PAUSE_CLUSTER_WITH_PENDING_CHANGES`

    

|

409

|

Cannot pause a cluster with pending changes.  
  
`CANNOT_PAUSE_NVME_CLUSTER`

    

|

409

|

Cannot pause an NVMe Cluster.  
  
`ORG_NOT_EMPTY`

    

|

409

|

Organization cannot be deleted because it still contains active groups.  
  
`CANNOT_MODIFY_CLUSTER_WITH_RUNNING_LIVE_IMPORT`

    

|

409

|

Cannot modify a cluster with a running live import.  
  
`CANNOT_CREATE_TEAM_WITH_LDAP_ENABLED`

    

|

409

|

Cannot create a team if LDAP is enabled.  
  
`TEAM_NAME_NOT_AVAILABLE`

    

|

409

|

Cannot create a team named %s in organization %s.  
  
`DATABASE_USERNAME_CANNOT_BE_CHANGED`

    

|

409

|

Cannot modify the username of an existing database user.  
  
`DATABASE_NAME_CANNOT_BE_CHANGED`

    

|

409

|

Cannot modify the authentication database of an existing database user.  
  
`AUTH_TYPE_CANNOT_BE_CHANGED`

    

|

409

|

Cannot modify the authentication type of an existing database user.  
  
`TEAM_EXISTS_IN_GROUP`

    

|

409

|

Cannot add a team that already exists in group.  
  
`USER_ALREADY_IN_TEAM`

    

|

409

|

The user with ID %s in team %s already exists.  
  
`ATLAS_BACKUP_CONFLICTING_OPTIONS`

    

|

409

|

Cannot turn backupEnabled and providerBackupEnabled on at the same time.  
  
`CANNOT_DISABLE_ENCRYPTION_AT_REST`

    

|

409

|

Cannot disable Encryption at Rest on the group because it is still enabled on
one or more clusters in the group.  
  
`CANNOT_CHANGE_ENCRYPTION_AT_REST_PROVIDER`

    

|

409

|

To choose a different Encryption at Rest provider, please disable and re-
enable this feature. This will decrypt your data and allow you to encrypt it
with a different Encryption at Rest provider.  
  
`UNSUPPORTED_FEATURE`

    

|

409

|

This feature is not yet supported.  
  
`ATLAS_CUSTOM_ROLE_NAME_ALREADY_EXISTS`

    

|

409

|

A custom role with the name %s already exists.  
  
`ATLAS_CUSTOM_ROLE_IN_USE_BY_USERS`

    

|

409

|

Deleting specified custom role would leave the following users without a role:
%s.  
  
`ATLAS_CUSTOM_ROLE_IN_USE_BY_ROLES`

    

|

409

|

Deleting specified custom role would leave the following roles with no actions
or inherited roles: %s.  
  
`AUTOMATION_CONFIG_CONCURRENT_MODIFICATION`

    

|

409

|

Another session or user has already published changes.  
  
`CUSTOM_ROLE_ACTIONS_INVALID_FOR_EXISTING_CLUSTERS`

    

|

409

|

Cannot create or edit role as the following custom role action (s) are not
supported for your %s cluster (s): %s."  
  
`CLUSTER_VERSION_INCOMPATIBLE_WITH_EXISTING_CUSTOM_ROLES`

    

|

409

|

Cannot create cluster due to incompatible existing custom roles with version
(s): %s."  
  
`DATA_LAKE_TENANT_NAME_ALREADY_EXISTS`

    

|

409

|

A Data Lake tenant with the name %s already exists.  
  
`ATLAS_CLUSTER_RESTORE_IN_PROGRESS`

    

|

409

|

Cluster restore already in progress.  
  
`INTEGRATION_ALREADY_CONFIGURED`

    

|

409

|

The integration of type '%s' is already configured for this group.  
  
`PRIVATELINK_ENDPOINT_SERVICE_ALREADY_EXISTS_FOR_REGION`

    

|

409

|

A PrivateLink Endpoint Service already exists for AWS region %s.  
  
`PRIVATELINK_INTERFACE_ENDPOINT_ALREADY_EXISTS`

    

|

409

|

The PrivateLink already contains an interface endpoint with the specified id
%s.  
  
`PRIVATELINK_INCOMPATIBLE_TOO_MANY_NODES`

    

|

409

|

Project has too many addressable nodes in region %s to use PrivateLink.  
  
`MULTIPLE_PRIVATE_ENDPOINTS_RESTRICTED_TO_SINGLE_REGION`

    

|

409

|

Projects with multiple private endpoints in the same region cannot support
private endpoints in other regions.  
  
`CLUSTER_INCOMPATIBLE_WITH_EXISTING_PRIVATELINK`

    

|

409

|

The requested operation would result in more addressable nodes in region %s
than can be supported by PrivateLink. The maximum number supported is %s.  
  
`CANNOT_DELETE_PRIVATELINK_WITH_ENDPOINTS`

    

|

409

|

A PrivateLink with endpoints cannot be deleted. Please delete all endpoints
and retry.  
  
`PRIVATELINK_CANNOT_ACCEPT_ENDPOINTS`

    

|

409

|

The PrivateLink with the specified id %s is not ready to accept endpoint
connection requests.  
  
`PERSONAL_API_KEYS_DEPRECATED`

    

|

410

|

You can no longer create Personal API Keys. Please create a Programmatic API
Key.  
  
`RATE_LIMITED`

    

|

429

|

Resource %s is limited to %s requests every %s minutes.  
  
`UNEXPECTED_ERROR`

    

|

500

|

Unexpected error.  
  
`PROVISIONING_FAILED_FROM_PROVIDER`

    

|

500

|

Unable to retrieve configuration options from the provider.  
  
`CANNOT_GET_VOLUME_SIZE_LIMITS`

    

|

500

|

Cannot get volume size limits for volume type %s.  
  
`CANNOT_DECREASE_DISK_SIZE`

    

|

500

|

Not enough data to determine if decreasing disk size is safe.  
  
← Get Started with the Atlas Administration APIMore API Resources →

