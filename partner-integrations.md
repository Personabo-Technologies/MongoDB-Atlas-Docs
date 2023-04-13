Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Partner Integrations

Share Feedback

On this page

  * Application Platforms
  * Cloud Providers
  * Data Access Frameworks
  * Identity Providers
  * Monitoring Services
  * Orchestration Tools
  * Security Tools

While MongoDB Atlas integrates with other technologies through their standard
APIs, MongoDB and partners built specific product integrations to enable
MongoDB Atlas and partner products to interoperate directly and ensure a
seamless experience.

This document lists examples of integrations that MongoDB and partners
developed to enhance Atlas and partner service capabilities.

You can explore a collection of the existing integrations and partner services
in the MongoDB Ecosystem. Each integration has its own page with details about
the integration and links to set up the integration. To learn more, see
Explore the MongoDB Ecosystem.

## Application Platforms

### Vercel

Vercel is a cloud platform for static frontends and serverless functions. It
enables developers to host websites and web applications that deploy
instantly, scale automatically, and require no supervision. Vercel integrates
with the Next.js framework.

You can easily use Vercel with Atlas:

  * To connect to Atlas clusters from Vercel, see Integrate with Vercel.

  * To connect the serverless functions that you deployed in Vercel to Atlas clusters, you can also use the MongoDB Node.js driver or the Mongoose ODM library.

### Netlify

Netlify is a serverless application platform based on Jamstack. Netlify hosts
tools for deploying and managing static content and enables you to write
serverless functions that run atop AWS Lambda and that can integrate with an
application's database.

Netlify is JavaScript-centric (although it supports other languages) and is
easy to use with Atlas. Applications deployed in Netlify can connect to Atlas
clusters using serverless functions that use the MongoDB Node.js driver or the
Mongoose ODM library.

#### Best Practices

Since Netlify functions run on AWS Lambda, use best practices for connecting
from AWS Lambda when building applications that use serverless Netlify
functions that connect to Atlas.

## Cloud Providers

MongoDB Atlas provides multi-cloud clusters on AWS, Google Cloud, and Azure to
support a flexible, global deployment strategy.

Integrations with these cloud providers allow applications built on MongoDB to
take advantage of each cloud provider's regions and capabilities.

### Amazon Web Services (AWS)

  * AWS regions supported on Atlas

  * List of integrations between Atlas and AWS

### Google Cloud Platform (GCP)

  * GCP regions supported on Atlas

  * List of integrations between Atlas and GCP

### Microsoft Azure

  * Azure regions supported on Atlas

  * List of integrations between Atlas and Azure

## Data Access Frameworks

### Prisma

Prisma is a next-generation Node.js and TypeScript Object Relational Mapper
(ORM) with a declarative schema and type-safe database client supporting a
number of databases, including MongoDB.

Prisma provides a server-side library that enables you to build applications
that read and write data to the database in an intuitive and safe way.

Integration:

  * MongoDB Database Connector

## Identity Providers

### SAML SSO Providers

MongoDB supports federated authentication to allow any company with an IdP
that supports the SAML standard to federate access for its employees into all
MongoDB web portals, including the Atlas web interface. As a result, employees
can use their corporate SSO provider to access Atlas.

Notable integrations include:

  * AWS Single Sign-On (SSO): How to integrate AWS Single Sign-On with MongoDB Atlas

  * Azure Active Directory (AD): Configure Federated Authentication from Azure AD

  * Okta: Configure Federated Authentication from Okta

  * OneLogin

  * PingOne for Enterprise

### LDAP Providers

You can manage database user authentication and authorization from all MongoDB
clients using a MongoDB LDAP over TLS.

Notable integrations include:

  * Azure Active Directory (AD): Configure User Authentication and Authorization with Azure AD Domain Services

  * Okta LDAP Interface: Configure User Authentication and Authorization with Okta LDAP Interface

  * OneLogin: Configure User Authentication and Authorization with OneLogin VLDAP

## Monitoring Services

You can configure Atlas to send monitoring data and alerts to:

  * Third-party monitoring services, such as Datadog, PagerDuty, Prometheus, and Splunk On-Call.

  * Third-party collaboration services, such as Slack and Flowdock.

To learn more, see Integrate with Third-Party Monitoring Services.

## Orchestration Tools

### HashiCorp Terraform

Terraform by HashiCorp provides a foundation for cloud infrastructure
automation using infrastructure as code for provisioning and compliance in the
cloud operating model.

You can integrate Atlas into your continuous delivery workflows by using the
official plugin that is verified and tested by HashiCorp. Using this plugin
makes it easy to provision, manage, and control Atlas configurations as code
on any cloud provider. To learn more, see MongoDB & HashiCorp Terraform.

Integration:

  * HashiCorp Terraform MongoDB Atlas Provider

## Security Tools

### HashiCorp Vault

HashiCorp Vault is a secrets management tool by HashiCorp that enables teams
to centrally manage and distribute secrets and other sensitive data through
UI, CLI, or API.

Simplify secrets management for your Atlas databases by using the official
plugins verified and tested by HashiCorp. Using these plugins, you can
programmatically manage API keys and control access by MongoDB users in your
organization to reduce security risks and increase developer productivity. To
learn more, see MongoDB & HashiCorp Vault.

Integrations:

  * MongoDB Atlas Database Users Vault Secrets Engine: Generate Atlas database credentials dynamically

  * MongoDB Atlas Secrets Engine: Generate programmatic API keys on Atlas

← Atlas Kubernetes Operator ChangelogExplore the MongoDB Ecosystem →

