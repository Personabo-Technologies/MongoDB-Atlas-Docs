Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Invoices

Share Feedback

On this page

  * View and Pay Your Current Invoice
  * Download Your Current Invoice
  * View and Pay Your Past Invoices
  * Download Past Invoices
  * Invoice and Payment Status
  * Payment and Usage Details
  * Troubleshoot Invoices and Payments

Atlas charges for services provided at the organization level. Atlas posts
charges the day after you incur the charges.

## View and Pay Your Current Invoice

To view your organization's current invoice:

1

### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

### Click View Current Invoice.

Atlas displays the current invoice. The current invoice page shows the
following sections:

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
  
3

### Pay your invoice.

If you have a subscription with an amount due, your invoice's Payment Details
section displays the PAY NOW action in the Actions column for the subscription
payment method. This allows you to pay your tax invoices for your monthly
commitment or elastic subscription directly from the YayPay website.

  1. In your invoice, navigate to the Payment Details section.

  2. Click PAY NOW action for the row that contains your subscription payment method.

click to enlarge

## Download Your Current Invoice

To download the charges and payments for your current invoice:

1

### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

### Click View Current Invoice.

Atlas displays the current invoice. The current invoice page shows the
following sections:

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
  
3

### Choose the format of your invoice.

  1. Click Export To in the upper right corner of the Invoice page.

  2. Select PDF or CSV.

When you download your invoice as a PDF, the document represents a copy of
your actual bill for the specified billing period.

When you download your invoice as a CSV, the document provides itemized usage
details. If you have credits applied to your invoice, the invoice includes a
row with the following information:

    * A Description that includes the word `Credit`

    * A negative Amount value.

This information helps you calculate when you ran out of credits. When summing
the Amount column, you can filter out this row to calculate your invoice
subtotal.

## View and Pay Your Past Invoices

To view all invoices for your Atlas organization:

1

### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

### Click the Invoices tab.

Atlas displays a list of your invoices. In this list, you can:

  * Filter the invoices by status or date.

  * View the invoice status.

  * Click the link to view the invoice.

  * Download each invoice as PDF or CSV.

3

### Filter your list of invoices, if desired.

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

### Open your invoice to see its payment details.

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

### Pay your invoice.

If you have a subscription with an amount due, your invoice's Payment Details
section displays the PAY NOW action in the Actions column for the subscription
payment method. This allows you to pay your tax invoices for your monthly
commitment or elastic subscription directly from the YayPay website.

  1. In your invoice, navigate to the Payment Details section.

  2. Click PAY NOW action for the row that contains your subscription payment method.

click to enlarge

## Download Past Invoices

To download past invoices for your Atlas organization:

1

### Navigate to the Billing page.

  1. Click your desired organization from the __ Organization menu if you don't see it displayed.

  2. Click Billing in the top navigation bar or in the side bar and then click the Overview tab if it isn't already open.

In the Overview tab, you can explore:

    * The Running Invoice Total section that shows the total invoice for one organization, or for all invoices for linked organizations, per billing period.

    * The billing cost visualization charts.

    * The Available Credits and History sections.

2

### Click the Invoices tab.

Atlas displays a list of your invoices. In this list, you can:

  * Filter the invoices by status or date.

  * View the invoice status.

  * Click the link to view the invoice.

  * Download each invoice as PDF or CSV.

3

### Filter your list of invoices, if desired.

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

### Download your desired invoice.

From your invoice's Download As column, select PDF or CSV.

## Invoice and Payment Status

### Invoices

When you view past invoices, the Payment Status column displays the payment
status of each invoice. Atlas displays one of the following invoice statuses:

Status

|

Description  
  
|  
  
`SUCCESSFUL`

|

MongoDB has received your payment.  
  
`PREPAID`

|

Your prepaid subscription has covered the invoice with credits.  
  
`INVOICED`

|

Your usage has been invoiced with your subscription.  
  
`N/A`

|

The amount turned out to be zero, so you are not charged.  
  
`PENDING`

|

Includes charges for the current subscription cycle. An organization should
never have more than one invoice in this state.  
  
`CLOSED`

|

All charges for the subscription cycle have been finalized, the balance is
more than zero, and you have not been charged yet.  
  
`FORGIVEN`

|

The charge has been forgiven. If the charge succeeded, it has been refunded by
MongoDB.  
  
`FAILED`

|

An attempt to charge your payment method for the amount due failed. To resolve
a failed payment, troubleshoot invoices and payments.  
  
### Payments

Review the status of your payment on its invoice. Atlas displays one of the
following payment statuses:

Status

|

Description  
  
|  
  
`SUCCESSFUL`

|

MongoDB has received your payment.  
  
`NEW`

|

The payment has been calculated, but you have not been charged yet.  
  
`PARTIAL PAID`

|

The payment sent to MongoDB was partially paid. You might have received an
email with additional information. Please refer to that email or contact
MongoDB Support to resolve this issue.  
  
`CANCELLED`

|

The payment was cancelled.  
  
`PENDING`

|

The payment is pending.  
  
`CLOSED`

|

All payments for the subscription cycle have been finalized, the balance is
more than zero, and you have not been charged yet.  
  
`FORGIVEN`

|

The charge has been forgiven. If the charge succeeded, it has been refunded.  
  
`FAILED DUE TO AUTHENTICATION`

|

Strong Customer Authentication (SCA) has failed. Please confirm that your
payment method is authenticated.

To resolve a failed payment, troubleshoot invoices and payments.  
  
`FAILED`

|

The attempt to charge your payment method failed.

To resolve a failed payment, troubleshoot invoices and payments.  
  
## Payment and Usage Details

Current invoices and past invoices include payment details, such as paid and
pending charges, and usage details for each of your MongoDB services.

You can find the following information in the Payment Details and the Usage
Details sections of your invoices:

Section

|

Contents  
  
|  
  
Payment Details

|

Lists payment methods, which may include Atlas credits from a prepaid or
promotional subscription, a monthly commitment subscription, a marketplace
subscription, PayPal, or a credit card.

For each payment method, lists:

  * The Date when Atlas issued the charge.

  * The current payment status.

  * The usage (the amount you have used).

  * The billed usage (the amount you are being billed for).

  * The total amount (the unit price multiplied by billed usage, plus tax).

  * The amount due.

  * The Action that you can click. Actions can be one of the following:

    * PDF for downloading the PDF of the tax invoice that you receive by email.

This PDF contains the charges for the specific payment in the invoice. This
PDF differs from the invoice-level PDF that you download when viewing your
current invoice. The invoice-level PDF provides usage details for the entire
invoice.

    * VIEW DETAILS. View your subscription details.

    * PAY NOW. Pay your bill directly if you are a YayPay customer.

    * RETRY. Retry the failed payment.

  
  
Usage Details

|

Lists all line item details for each month's bill. This is a granular breakout
of all services that are invoiced, including dates used and billed, quantity
(the number of server hours), the project, the unit price, and the amount. You
can download the usage details as a CSV.  
  
## Troubleshoot Invoices and Payments

If a payment fails, try the following:

  1. Retry the failed payment.

  2. Ensure your payment method has sufficient funds and supports payments made in USD.

  3. Speak with your bank or credit card issuer to ensure your payment method is authorized to make transactions with MongoDB.

  4. Use an alternative payment method.

  5. Request support through the Atlas console.

## Note

If you pay with a credit card from a credit card issuer based in India, you
must complete additional payment processing steps that comply with RBI
regulations.

For more information, see Payment Processing in India.

← Manage BillingManage Subscriptions →

