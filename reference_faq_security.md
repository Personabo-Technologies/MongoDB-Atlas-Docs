Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# FAQ: Security

Share Feedback

On this page

  * How does Atlas encrypt my data?
  * Can I disable TLS on my deployment?
  * What versions of TLS does Atlas support?
  * Which certificate authority signs MongoDB Atlas TLS certificates?

## How does Atlas encrypt my data?

Atlas uses whole volume (disk) encryption for any data at rest, including your
cluster data and backups of that data.

Atlas also requires TLS encryption for client data and intra-cluster network
communications.

If your organization requires more specific information regarding Atlas
encryption, please contact Atlas MongoDB Support. From the Atlas project or
cluster view, click Support in the left-hand navigation bar.

## Can I disable TLS on my deployment?

No.

## What versions of TLS does Atlas support?

Atlas requires TLS connections for all Atlas clusters. After July 2020, Atlas
enabled Transport Layer Security (TLS) protocol version 1.2 by default for all
new Atlas clusters regardless of the MongoDB version.

MongoDB 4.0 and later disabled support for TLS 1.0 where TLS 1.1+ is
available. You can manually configure TLS 1.1 or 1.0 by editing your cluster
configuration.

You can read more about timing and reasons for the change from the Payment
Card Industry (PCI) as well as the National Institute of Standards and
Technology (NIST).

If you have questions about TLS support or cannot update your applications to
support TLS 1.2, please contact Atlas MongoDB Support.

To open a Atlas support ticket, log into the your Atlas account. Click the
Support link in the Atlas console and fill in the requested details.

### How do I know if my applications support TLS 1.2?

Applications whose underlying programming languages or security libraries
predate TLS 1.2 may require updating to a more recent version to support TLS
1.2. You may also need to update the application host operating system to
support TLS 1.2.

MongoDB and Atlas don't provide services to audit external applications for
which versions of TLS support they support. Third party services, such as
howsmyssl.com may provide the appropriate tooling. MongoDB doesn't endorse
this service, and its reference is only informational. Use your organization's
procedures for selecting the vendor or service for auditing your applications.

### What do I have to do to update my clusters for TLS 1.2?

  * Conduct an audit of your applications for support of TLS 1.2.

  * Udate all components of your technology stack that don't support TLS 1.2.

  * Modify your cluster configuration to use TLS 1.2.

### Can I force enable TLS 1.0?

Atlas allows you to manually configure TLS 1.0 during cluster modification.

Enabling TLS 1.0 for any Atlas cluster carries significant risks. Consider
enabling TLS 1.0 only for as long as required to update your application stack
to support TLS 1.2.

## Which certificate authority signs MongoDB Atlas TLS certificates?

On 25 February 2020, MongoDB Atlas moved to Let's Encrypt as the new
Certificate Authority for TLS certificates for all Atlas clusters.

Beginning on 1 May 2021, new TLS certificates that MongoDB Atlas creates use
ISRG instead of IdenTrust for their root Certificate Authority in line with
Let's Encrypt's announcement of this transition.

On 17 March 2022, MongoDB Atlas moved to Let's Encrypt as the new Certificate
Authority for TLS certificates for `cloud.mongodb.com`.

Please review the following scenarios to ensure that you don't experience
connectivity issues:

### Hard-coded Certificate Authority

If you hard-coded the IdenTrust's root Certificate Authority (DST Root CA X3)
or an intermediate certificate as the only trusted Certificate Authority for
your application's connection to Atlas, ensure that you add Let's Encrypt's
root Certificate Authority (ISRG Root X1) to your certificate store.

### Java Users

Let's Encrypt's new ISRG root certificate isn't present in the default trust
store for Java version 7 prior to the 7u151 update, or Java version 8 prior to
the 8u141 update. Use a Java release after 18 July 2017.

Ensure your Java client software is up-to-date. Use the latest Java versions
to utilize many improvements beyond these new Certificate Authority
requirements for our TLS certificates.

If you have your own trust store, add the Let's Encrypt certificate to it. To
learn more, see Hard-coded Certificate Authority.

### Windows Server Users

The ISRG Root X1 root Certificate Authority isn't included by default in
Windows Server, but it is available in the Microsoft Trusted Root Program.

To configure Windows Server to download trusted root certificates, including
Let's Encrypt's new ISRG root certificate, see Windows Documentation.

### Amazon Linux AMI Users

Amazon Linux AMI doesn't support the new ISRG Root X1 root Certificate
Authority.

If you are using Amazon Linux AMI, migrate to Amazon Linux 2. After 30
September 2021, the support of ISRG Root X1 certificates is mandatory for
Atlas to avoid certificate compatibility issues.

To continue using Amazon Linux AMI after 30 September 2021, manually install
the new ISRG Root X1 root Certificate Authority.

### Everyone Else

This change shouldn't impact you if you use a recent programming language and
operating system version.

← FAQ: NetworkingFAQ: Storage →

