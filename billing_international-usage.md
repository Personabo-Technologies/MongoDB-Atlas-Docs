Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# International Usage and Taxation

Share Feedback

On this page

  * Tax ID Number
  * Taxation by Region
  * Payment Processing in India
  * Strong Customer Authentication (SCA) Changes
  * International Currencies

## Tax ID Number

If your organization's billing or invoice address is outside of the United
States (USA), add your VAT or GST Number in the VAT/GST ID field on the
Payment Method or the Billing Profile modal.

Atlas displays the VAT/GST ID field only if you select a country other than
the United States.

## Taxation by Region

VAT and GST vary by region. Your organization's billing address determines
your region.

### Australia

Atlas and Flex Consulting charge GST if you do not enter a valid `GST ID
Number`. Provide a valid `GST ID Number` on your billing profile to incur no
GST charges.

### Canada

## Note

Your `GST ID Number` is your 9-digit Federal Business Number, plus your
2-character program identifier, plus your 4-digit reference number.

Atlas charges GST if you do not enter a valid `GST ID Number`. Provide a valid
`GST ID Number` on your billing profile to incur no GST charges.

## Important

Some Canadian provinces charge a provincial sales tax (PST). Atlas always
charges PST, even with a valid `GST ID Number`.

### European Union (EU)

Atlas and Flex Consulting charge VAT if you do not enter a valid `VAT ID
Number`. Provide a valid `VAT ID Number` on your billing profile to incur no
VAT charges.

## Important

If your billing address is in Ireland, Atlas and Flex Consulting always charge
VAT, even with a valid `VAT ID Number`.

### India

Atlas charges GST if you do not enter a valid `GST ID Number`. Provide a valid
`GST ID Number` on your billing profile to incur no GST charges.

Flex Consulting doesn't charge GST.

### United Kingdom (UK)

Atlas charges VAT if you do not enter a valid `VAT ID Number`. Provide a valid
`VAT ID Number` on your billing profile to incur no VAT charges.

Flex Consulting doesn't charge VAT.

### Saudi Arabia

Atlas and Flex Consulting charge VAT if you do not enter a valid `VAT ID
Number`. Provide a valid `VAT ID Number` on your billing profile to incur no
VAT charges.

### South Africa

Atlas charges VAT.

Flex Consulting doesn't charge VAT.

### Singapore

Atlas charges GST if you do not enter a valid `GST ID Number`. Provide a valid
`GST ID Number` on your billing profile to incur no GST charges.

Flex Consulting doesn't charge GST.

### Switzerland

Atlas and Flex Consulting charge VAT.

## Payment Processing in India

If you pay with a credit card from a credit card issuer based in India, you
must complete additional payment processing steps that comply with RBI
regulations.

The RBI requires a _mandate_ for recurring payments to ensure you aren't
charged above a certain amount each billing period. MongoDB automatically
registers a mandate for $1,400 USD each month when you add a payment method or
retry a payment.

### Mandates

The mandate that MongoDB registers on your behalf permits MongoDB to charge
your credit card up to $1,400 USD per month. This might be presented by your
card issuer or bank in INR instead of USD.

MongoDB charges your credit card for your usage only. The $1,400 mandate is a
limit on the amount you can be charged per month.

You manage your mandates through your card issuer or bank. When you add a
payment method or retry a payment with a credit card from a credit card issuer
based in India, according to RBI regulations, your card issuer or bank
provides a link to manage your mandates.

### Payment Statuses

If your credit card issuer is based in India, you might see two additional
payment statuses:

Status

|

Description  
  
|  
  
`PROCESSING`

|

The payment is pending due to RBI regulations and might require authorization.

A payment might stay in the processing state for several days. During this
time, according to RBI regulations, your card issuer will notify you of the
charge and provide a link for you to revoke your mandate. No action is
required unless the payment is for more than ₹15,000 INR.

If the payment is for more than ₹15,000 INR, the notification you receive from
your card issuer includes a link to authorize that payment. You must authorize
the payment to successfully pay, otherwise the payment fails with the `FAILED`
status.

If you revoke your mandate, attempts to charge your credit card fail until you
register a new mandate. Register a mandate by adding a payment method or
retrying a payment  
  
`PENDING_REVERSAL`

|

The payment is pending, but will be refunded or cancelled as soon as possible.

If the payment succeeds, MongoDB refunds it. If the payment fails, MongoDB
cancels it.  
  
## Important

If you pay with a credit card from a credit card issuer based in India, you
are charged in INR. However, the Atlas UI and MongoDB communications typically
present prices in USD.

MongoDB uses the currency conversion rate at the time your payment moves to
the `PROCESSING` status to convert between INR and USD.

### Adding a Payment Method

When you add a credit card from a credit card issuer based in India as your
payment method, Atlas prompts you to verify your identity. After you verify
your identity, Atlas might take up to 2 minutes to add your credit card.
MongoDB registers a mandate on your behalf.

According to RBI regulations, your card issuer will notify you via SMS that a
mandate was registered on your behalf.

### Retrying a Payment

When you retry a payment from the Atlas UI, MongoDB prompts you to verify your
identity and then registers a new mandate on your behalf.

According to RBI regulations, your card issuer will notify you via SMS that a
mandate was registered on your behalf.

## Strong Customer Authentication (SCA) Changes

SCA is a new European regulatory requirement to reduce fraud and make online
payments more secure. All payment service providers are required to build
additional authentication into their checkout flow once SCA goes into effect.
Customers in European Economic Area (EEA) might be required to authenticate
their credit cards depending on the card's issuer, starting 14 September 2019.
If your credit card issuer requires authentication, review the following
Authentication Process to continue paying for MongoDB Atlas seamlessly with a
credit card.

Marketing emails will be sent out to affected customers announcing the policy
change and the steps necessary to comply with SCA.

### Authentication Process

The following sections cover different ways to authenticate your credit card
to comply with Strong Customer Authentication.

#### Deploy a Paid Database as a New User

New Atlas users who do not have a payment method saved can authenticate a new
credit card when paying for a database deployment on the Create a Database
Deployment page. To learn more, see Create a Database Deployment.

#### Edit Payment Method

Existing users can edit their Payment Method to authenticate a new credit card
or reauthenticate an existing credit card to comply with SCA:

1

##### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

##### Click Edit in the Payment Method card.

3

##### Update your Billing Address details as needed.

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

##### Click Next.

5

##### Update your Payment Method details as needed.

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

##### Accept or decline your changes.

  * To accept your changes, click Submit.

  * To decline your changes, click Cancel.

Once you update your credit card information and authenticate, you will be
automatically charged for all existing failed payments.

#### Failed Payment Email

Atlas sends an email after a payment failure with a link to your invoices.
Existing users can authenticate a credit card when retrying a failed payment.
To retry the failed payment from the failed payment email:

1

##### Click the link in the failed payment email.

2

##### Click the Invoice Date of the failed invoice.

3

##### Click the Invoices tab.

Atlas displays a list of your invoices. In this list, you can:

  * Filter the invoices by status or date.

  * View the invoice status.

  * Click the link to view the invoice.

  * Download each invoice as PDF or CSV.

4

##### Retry the failed payment.

Under the Payments section, click Retry next to the failed payment.

#### Retry Failed Payment

Existing users can authenticate a credit card when retrying a failed payment.
To retry the failed payment from within Atlas:

1

##### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

##### Verify your Payment Method.

View the payment method displayed in the Payment Method card. If this method
appears incorrect, click Edit in that card.

3

##### Filter your list of invoices, if desired.

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

##### Open your invoice to see its payment details.

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

##### Retry the payment.

  1. Locate the Payment Details section in your invoice page.

  2. Review the values in the Actions column to locate the Retry action.

  3. Click Retry.

Customers in the European Economic Area (EEA) may experience payment failures
due to Strong Customer Authentication (SCA), a European regulatory
requirement. To learn how to authenticate a credit card and comply with SCA,
see Strong Customer Authentication (SCA).

#### Contact Support

Contact support for further assistance.

## International Currencies

To pay with Euros, make a request through the sales department.

← Additional ServicesAPIs →

