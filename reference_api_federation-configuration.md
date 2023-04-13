Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Federated Authentication Configuration

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Use the following endpoints to return, add, edit, and remove federation-
related features such as role mappings and connected organization
configurations.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-
ID}/roleMappings/{ROLE-MAPPING-ID}

|

Return one role mapping from the specified organization in the specified
federation.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-
ID}/roleMappings

|

Return all role mappings from the specified organization in the specified
federation.  
  
`POST`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-
ID}/roleMappings

|

Add one role mapping to the specified organization in the specified
federation.  
  
`PUT`

|

/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings/{ROLE-
MAPPING-ID}

|

Update one role mapping in the specified organization of the specified
federation.  
  
`DELETE`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-
ID}/roleMappings/{ROLE-MAPPING-ID}

|

Remove one role mapping from the specified organization in the specified
federation.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}

|

Return one connected organization for a federated authentication
configuration.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs

|

Return all connected organizations for a federated authentication
configuration.  
  
`DELETE`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}

|

Remove one organization from the specified federation.  
  
`PATCH`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}

|

Update one connected organization for a federated authentication
configuration.  
  
`GET`

|

/orgs/{ORG-ID}/federationSettings

|

Return the federated authentication configuration for one organization.  
  
`DELETE`

|

/federationSettings/{FEDERATION-SETTINGS-ID}

|

Remove one federation and all associated data, including the identity
providers and domains that the federation describes.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders

|

Return all identity providers for a federated authentication configuration.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}

|

Return one identity provider for a federated authentication configuration.  
  
`PATCH`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-ID}

|

Update one identity provider for a federated authentication configuration.  
  
`GET`

|

/federationSettings/{FEDERATION-SETTINGS-ID}/identityProviders/{IDP-
ID}/metadata.xml

|

Return the contents of the SAML metadata XML file for the specified identity
provider in the specified federation.  
  
What is MongoDB Atlas? →

