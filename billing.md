Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Billing

Share Feedback

On this page

  * Your Billing Profile
  * Payment Method
  * Invoices
  * Cost Visualizations
  * Cross-Organization Billing
  * Billing Quota Management

Billing settings are configured at the organization level and apply to all
projects within that organization. You can examine costs at the organization
level or the project level.

To configure the payment method and billing profile for an organization, or to
view the most recent and pending charges for an organization, access the
organization's Billing section through Atlas.

Atlas:

  * charges by the hour for your MongoDB clusters

  * charges for usage of your MongoDB serverless instances

  * tabulates costs daily

  * displays your current monthly costs on the Invoices page

To view line-item charges, view all of your invoices.

As you configure a database deployment, you can view the total cost, except
for data transfer, before applying your settings.

## Your Billing Profile

### View and Edit Your Billing Profile

To view and edit your billing profile:

1

#### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

#### Click Edit in the Payment Method card.

3

#### Update your Billing Address details as needed.

Field

|

Necessity

|

Action  
  
||  
  
Billing Email Address

|

Optional

|

Type the email address to which Atlas should send billing alerts.

By default, Atlas sends billing alerts to the Organization Owners and Billing
Admins.

  * If you leave the Billing Email Address blank, Atlas sends billing alerts to the Organization Owners and Billing Admins.

  * If you specify a billing email address and uncheck Only send invoice emails to the Billing Email Address, Atlas sends billing alerts to the billing email address, Organization Owners, and Billing Admins.

  * If you specify a billing email address and check the box for Only send invoice emails to the Billing Email Address, Atlas send billing alerts to the billing email address only.

  
  
Company Name

|

Optional

|

Type the name of the company for your billing address.  
  
Country

|

Required

|

Select the country for your billing address. You can also start typing the
name of the country and then select it from the filtered list of countries.  
  
Street Address

|

Required

|

Type the street address for your billing address.  
  
Apt/Suite/Floor

|

Optional

|

Type an the apartment, suite, or floor for your billing address.  
  
City

|

Required

|

Type the name of the city for your billing address.  
  
State/Province/Region

|

Required

|

Type or select the political subdivision in which your billing address exists.
The label and field change depending on what you selected as your **Country**
:

  * If you select **United States** as your **Country** , this label changes to **State**. The field changes to a dropdown menu of U.S. states. You can also start typing the name of the state and then select it from the filtered list of states.

  * If you select **Canada** as your **Country** , this label changes to **Province**. The field changes to a dropdown menu of Canadian provinces. You can also start typing the name of the province and then select it from the filtered list of provinces.

  * If you select any other country as your **Country** , this label changes to **State/Province/Region**. The field changes to a text box. Type the name of your province, state, or region in this box.

  
  
ZIP or Postal Code

|

Required

|

Type the ZIP (U.S.) or Postal Code (other countries) for your billing address.  
  
VAT Number

|

Conditional

|

Atlas displays the VAT ID field if you select a country other than the United
States.

To learn more about VAT, see VAT ID.

If your company's billing address is in a country other than the United States
(USA), Atlas typically charges VAT if you do not enter a valid `VAT ID Number`
on your billing profile.

## Important

If your billing address is in Ireland or certain Canadian provinces, Atlas
always charges VAT, even with a valid `VAT ID Number`.

To learn more about VAT by region, see International Usage and Taxation.  
  
4

#### Accept or decline your changes.

  * To accept your changes, click Submit.

  * To decline your changes, click Cancel.

## Payment Method

To pay for your Atlas usage, you can:

  * Pay with an accepted payment method.

  * Pay with a MongoDB Atlas subscription.

Contact MongoDB Sales to:

  * Purchase a subscription. Your subscription level determines your access to support and other entitlements.

  * Review alternative billing methods.

## Important

To confirm your credit card information, Atlas charges $1.00 when you first
connect a credit card to your account. After Atlas confirms your information,
it refunds the $1.00 charge. If you encounter any issues with connecting a
credit card to your account, reach out to your card provider or banking
institution. Verify whether they declined the initial charge, which would
prevent Atlas from confirming your information.

### Set Payment Method

MongoDB accepts the following payment methods through the Atlas console:

  * Credit card

  * PayPal

To set a payment method, you must be an `Organization Owner` or an
`Organization Billing Admin`.

To set your payment method:

1

#### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

#### Click Edit in the Payment Method card.

3

#### Update your Billing Address details as needed.

Field

|

Necessity

|

Action  
  
||  
  
Country

|

Required

|

Select the country for your billing address. You can also start typing the
name of the country and then select it from the filtered list of countries.  
  
VAT ID

|

Conditional

|

Atlas displays the VAT ID field if you select a country other than the United
States.

To learn more about VAT, see VAT ID.

If your company's billing address is in a country other than the United States
(USA), Atlas typically charges VAT if you do not enter a valid `VAT ID Number`
on your billing profile.

## Important

If your billing address is in Ireland or certain Canadian provinces, Atlas
always charges VAT, even with a valid `VAT ID Number`.

To learn more about VAT by region, see International Usage and Taxation.  
  
Address Line 1

|

Required

|

Type the mailing address for your billing address.  
  
Address Line 2

|

Optional

|

Type an additional line for the mailing address for your billing address.  
  
City

|

Required

|

Type the name of the city for your billing address.  
  
State/Province/Region

|

Required

|

Type or select the political subdivision in which your billing address exists.
The label and field change depending on what you selected as your **Country**
:

  * If you select **United States** as your **Country** , this label changes to **State**. The field changes to a dropdown menu of U.S. states. You can also start typing the name of the state and then select it from the filtered list of states.

  * If you select **Canada** as your **Country** , this label changes to **Province**. The field changes to a dropdown menu of Canadian provinces. You can also start typing the name of the province and then select it from the filtered list of provinces.

  * If you select any other country as your **Country** , this label changes to **State/Province/Region**. The field changes to a text box. Type the name of your province, state, or region in this box.

  
  
ZIP or Postal Code

|

Required

|

Type the ZIP (U.S.) or Postal Code (other countries) for your billing address.  
  
4

#### Click Next.

5

#### Update your Payment Method details as needed.

  1. Click the radio button for Credit Card or Paypal.

    * If you selected Credit Card, type values for the following fields:

Field

|

Necessity

|

Action  
  
||  
  
Name on Card

|

Required

|

Type the name that appears on your credit card.  
  
Card Number

|

Required

|

Type the 16-digit number that appears on your credit card. American Express
uses a 15-digit number.  
  
Expiration Date

|

Required

|

Type the expiration date for your credit card in the two-digit month and two-
digit year format.  
  
CVC

|

Required

|

Type the three-digit number on the back of your credit card. American Express
uses a 4-digit number found on the front of the credit card.  
  
    * If you selected PayPal:

      1. Click Pay with PayPal.

      2. Complete the actions on the PayPal website.

All projects within your organization share the same billing settings,
including payment method.

6

#### Accept or decline your changes.

  * To accept your changes, click Submit.

  * To decline your changes, click Cancel.

Through MongoDB Sales, you can pay using a:

  * Currency other than USD.

  * Method other than a credit card or PayPal.

### Retry a Failed Payment

To retry a failed payment:

1

#### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

#### Verify your Payment Method.

View the payment method displayed in the Payment Method card. If this method
appears incorrect, click Edit in that card.

3

#### Filter your list of invoices, if desired.

You can filter the invoices by status and date.

  * To filter by status, click the Status drop-down and select the status to which you want to limit the results:

Status

|

Invoice Type  
  
|  
  
Pending

|

Invoices still pending payment.  
  
Free

|

Invoices with a total charge of `$0.00`.  
  
Successful

|

Invoices that are paid.  
  
  * To filter by invoice date, set the From or To date inputs to the required date range.

    * If you leave From blank, Atlas sets the lower date boundary to the organization's creation date.

    * If you leave To blank, Atlas sets the upper date boundary to the current date.

4

#### Open your invoice to see its payment details.

To open a specific invoice, click its link in Invoice Date or Invoice Period.
The invoice page shows the following sections:

Invoice Section

|

Contents  
  
|  
  
Running Total table

|

The invoice status, the running total amount, the billing period the invoice
number, and the billing address. In this card, you can export the invoice to
PDF or CSV.  
  
Total Usage chart

|

The total usage by your Atlas usage over the billing period. You can filter
usage by service. To learn more, see Invoice Charts.  
  
By Deployment chart

|

The proportion of your usage incurred by each of your deployments for one or
all projects. To learn more, see Invoice Charts.  
  
Summary By Project table

|

A summarized list of usage costs per project, excluding subscription charges.  
  
Summary by Service table

|

List of all Atlas services, App Services, MongoDB Charts, and Atlas
Subscription Plans with corresponding usage costs for each service, and the
total usage amount.  
  
Payment Details

|

Payments that are itemized by the payment method. The table lists:

  * Payment methods, which may include Atlas credits from a prepaid subscription or promotional subscription, a monthly commitment subscription, a marketplace subscription, a credit card, or PayPal.

  * Date: the date when Atlas issued the charge.

  * Payment status.

  * Usage: the amount you have used.

  * Billed Usage: the amount you are being billed for. Billed Usage amount can differ from the usage amount in a number of cases, such as when a month's usage is below the monthly minimum on your Atlas subscription, or a month's billed usage encompasses usage for multiple months.

  * Total Amount: the unit price multiplied by billed usage, plus taxes. Taxes represent the amount of taxes collected by MongoDB. If you have a marketplace subscription, taxes are imposed by your Cloud Provider. To learn more, see Taxation by Region.

  * Amount Due.

  * Action that you can click. Actions can be one of the following:

    * PDF: download the PDF of the tax invoice that you receive by email.

    * VIEW DETAILS: view your subscription's monthly commitment details.

    * PAY NOW: pay your bill directly if you are a YayPay customer.

    * RETRY: retry the failed payment.

To learn more, see Payment and Usage Details.  
  
Usage Details

|

List of all line item details for each month's bill. This is a granular
breakout of all services that are invoiced, including dates used and billed,
quantity (the number of server hours), the project, the unit price, and the
amount. You can download the usage details as a CSV. To learn more, see
Payment and Usage Details.  
  
5

#### Retry the payment.

  1. Locate the Payment Details section in your invoice page.

  2. Review the values in the Actions column to locate the Retry action.

  3. Click Retry.

Customers in the European Economic Area (EEA) may experience payment failures
due to Strong Customer Authentication (SCA), a European regulatory
requirement. To learn how to authenticate a credit card and comply with SCA,
see Strong Customer Authentication (SCA).

### Activate a Subscription

To activate a MongoDB subscription, see Activate a Subscription.

## Invoices

For each of your invoices, including your current invoice, you can:

  * View the running usage total, the billing period, the invoice number and your current billing address.

  * Export the invoice to PDF or CSV.

  * Pay the invoice if you have a subscription.

  * Explore invoice cost visualization charts that show total usage costs by service and by deployment.

  * Review usage summaries by project and by service.

  * Examine payment and usage details that explain usage, as well as paid and pending charges per service.

To learn more, see Manage Invoices.

## Cost Visualizations

### Year-to-Date Usage Chart

On the Billing Overview page, a Usage chart displays the costs incurred by
your organization's Atlas usage over the last 12 months. It does not include
subscription charges.

You can view usage data by service, by project, or by deployment:

#### By Service

The Usage chart displays stacked columns representing the total cost for each
type of Atlas service you have used across all of your projects each month.

Atlas services include:

  * Clusters

  * Serverless instances

  * MongoDB Charts

  * Data Federation

  * Backup

  * Data transfer

  * Other Atlas features

#### By Project

The Usage chart displays stacked columns representing the total cost incurred
by each of your projects each month.

## Note

The By Project view is unavailable for organizations using 20 or more
projects.

#### By Deployment

The Usage chart displays stacked columns representing the costs incurred by
each of your clusters and serverless instances each month. It does not include
data transfer costs for Charts and Data Federation.

## Note

The By Deployment view is unavailable for:

  * Organizations using 20 or more deployments

  * Cloud Manager

### Invoice Charts

Each of your invoices displays Total Usage and By Deployment charts. The
charts do not include subscription charges.

#### Total Usage Chart

The Total Usage chart displays the costs incurred by your Atlas usage over the
invoice period. You can filter usage by service to view charges incurred by a
particular Atlas service.

Atlas services include:

  * Clusters

  * Serverless instances

  * MongoDB Charts

  * Data Federation

  * Backup

  * Data transfer

  * Other Atlas features

#### By Deployment Chart

The By Deployment chart displays the proportion of your usage incurred by each
of your deployments across all your projects. Deployments are clusters and
serverless instances.

You can filter the chart by project to view charges incurred by deployments in
a particular project.

## Cross-Organization Billing

 _Cross-organization billing_ is an Atlas subscription feature that enables
you to share a billing subscription across many organizations and to pay a
single invoice for them. After configuring a paying organization, you pay
invoices for the paying organization that include a list of charges incurred
for all linked organizations.

A paying organization's Overview tab includes the Running Invoice Total.

The Running Invoice Total shows:

  * the paying organization's charges, or

  * if you have linked organizations, the paying and linked organizations' combined charges.

To display linked organizations and their contributions to the Running Invoice
Total, view the payment details section of your organization's invoice.

Linked organizations are subject to the subscription agreement of the paying
organization, including the level of support, the charges associated with the
subscription, discounts, and payment terms.

### Linked Organization Invoices

You pay for all linked organization usage through the paying organization. To
help you account for usage, each linked organization has its own monthly
invoice.

Linked organization invoices include:

  * All charges incurred by that organization.

  * A percentage of your total cross-organization billing subscription cost proportional to that organization's usage.

Each day, Atlas bills linked and paying organizations for subscription uplift
based on their own usage.

At the end of a paying organization's billing period, Atlas bills linked and
paying organizations proportionally to their usage for the unmet monthly
minimum, if there is one.

## Example

A paying organization has an Atlas Pro subscription and two linked
organizations. The paying organization incurs no charges.

Linked organization #1 incurs $400 in subscription uplift charges while linked
organization #2 incurs $200 in subscription uplift charges. The paying
organization has a monthly minimum of $799, so at the end of the month, the
unmet $199 is proportionally distributed across invoices for linked
organizations #1 and #2:

  * Atlas charges linked organization #1 $132.70 of the unmet $199 because it incurred 2/3 of the total charges.

  * Atlas charges linked organization #2 $66.30 of the unmet $199 because it incurred 1/3 of the total charges.

You still pay all charges through the paying organization.

## Note

At the end of the paying organization's billing period, simultaneous charges
for daily subscription uplift and an unmet minimum could trigger daily maximum
billing alerts.

### Use Cases

Use cross-organization billing to:

  * Create broad levels of authorization using Atlas organizations.

  * Exceed the 250-project limit on Atlas organizations.

## Example

A company with sales and engineering teams requires that each team has
different organization-level authorization. At the same time, the company
prefers to receive a single invoice for the company's database use.

To pay all costs through that paying organization and maintain control over
the authorizations of each team organization, the company can:

  1. Create two organizations for sales and engineering.

  2. Link these organizations to a paying organization.

A company with over 250 projects might create new organizations for new
projects, then link all organizations to a paying organization to maintain a
single source of invoicing.

### Configure a Paying Organization

#### Prerequisites and Limitations

  * To link a paying organization to another organization, you must have `Organization Billing Admin` or `Organization Owner` privileges for both organizations.

  * A paying organization must have an Atlas subscription.

  * A paying organization and all linked organizations must be in good standing and have no failed payments.

  * A paying organization and any linked organizations must be on the same subscription plan.

  * A paying organization and any linked organizations must have the same minimums, uplifts, and SLA for their subscription plan.

  * A paying organization and any linked organizations can't have an active self-serve support plan.

  * A paying organization and any linked organizations can't have overlapping monthly commitment deals.

  * A paying organization on a prepaid subscription plan and any linked organizations must be on the same current and future subscription plans.

  * You can use the Atlas UI to manually link a paying organization to a maximum of 20 other organizations. To link a paying organization to more than 20 other organizations, contact support.

  * A paying organization can't link more than 100 other organizations.

  * A paying organization can't already be a linked organization.

## Note

To purchase a subscription that enables cross-organization billing, contact
MongoDB Sales.

To configure a paying organization and link other organizations to it:

1

##### Select an organization to configure as a paying organization.

If it is not already displayed, select your desired organization from the
Organizations menu in the navigation bar. If you wish to create a new
organization through which to pay, Create an Organization first.

2

##### Click Billing.

Click Billing in the top navigation bar or in the left navigation panel.

3

##### Click the Linked Organizations tab.

## Note

The Linked Organizations tab only displays if your selected organization is
eligible to be a paying organization for cross-organization billing.

4

##### Start linking.

If you are configuring a new paying organization, click Start Linking.

If your organization is already a paying organization, click Link More
Organizations.

5

##### Select organizations to link to your paying organization.

A dialog displays your selected organization under Paying organization on the
left and a list of organizations you may link to it under Select organizations
to link on the right.

Select each organization you wish to link to your paying organization.

Click Review and Finish.

6

##### Review and finalize your links.

## Important

After you click Finish, you will not be able to unlink organizations unless
you contact Support.

Confirm that your organizations are linked as intended and click Finish.

The Linked Organizations tab displays your linked organizations. To link
additional organizations, click Link More Organizations.

## Billing Quota Management

You can use billing alerts to help manage your billing quotas. Billing alerts
notify a designated person when a bill has exceeded a USD limit, or when a
credit card is about to expire.

To configure billing alerts, click Organization Alerts in the Organization
view.

