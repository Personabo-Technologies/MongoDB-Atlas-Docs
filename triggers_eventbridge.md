Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Send Trigger Events to AWS EventBridge

Share Feedback

## Overview

MongoDB offers an AWS Eventbridge partner event source that lets you send
trigger events to an event bus instead of calling a function. You can
configure any trigger to send events to EventBridge.

All you need to send trigger events to EventBridge is an AWS account ID. This
guide walks through finding your account ID, configuring the trigger, and
associating the trigger event source with an event bus.

## Note

### Official AWS Partner Event Source Guide

This guide is based on Amazon's Receiving Events from an SaaS Partner
documentation.

## Procedure

1

### Begin Setup of the MongoDB Partner Event Source

To send trigger events to AWS EventBridge, you need the AWS account ID of the
account that should receive the events.

Open the Amazon EventBridge console and click Partner event sources in the
navigation menu. Search for the MongoDB partner event source and then click
Set up.

click to enlarge

On the MongoDB partner event source page, click Copy to copy your AWS account
ID to the clipboard.

click to enlarge

2

### Configure the Trigger

Once you have the AWS account ID, you can configure a trigger to send events
to EventBridge. In the Atlas UI, create and configure a new database trigger
or scheduled trigger and select the EventBridge event type.

Paste in the AWS Account ID that you copied from EventBridge and select an AWS
Region to send the trigger events to.

click to enlarge

## Note

### Supported AWS Regions

For a full list of supported AWS regions, refer to Amazon's Receiving Events
from an SaaS Partner guide.

3

### Associate the Trigger Event Source with an Event Bus

Go back to the EventBridge console and choose Partner event sources in the
navigation pane. In the Partner event sources table, find and select the
Pending trigger source and then click Associate with event bus.

click to enlarge

On the Associate with event bus screen, define any required access permissions
for other accounts and organizations and then click Associate.

click to enlarge

Once confirmed, the status of the trigger event source changes from Pending to
Active, and the name of the event bus updates to match the event source name.
You can now start creating rules that trigger on events from that partner
event source. For more information, see Creating a Rule That Triggers on an
SaaS Partner Event.

click to enlarge

← Trigger Configuration ParametersCRON Expressions →

