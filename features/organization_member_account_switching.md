---
title: Organization Member Account Switching
layout: default
nav_order: 2
parent: Features
---

# Organization Member Account Switching

If you have configured Wut.Dev using [Organization Mode](../getting_started.html#organization-mode) (adding credentials and defining your Organization management account), you can easily switch between member accounts using the "Select AWS Account" dropdown. Clicking this dropdown will dynamically load all member accounts in the Organization.

## Deploy the Role to the Organization Management Account

See [Getting Started](../getting_started.html#organization-mode). Be sure to follow the steps to deploy the CloudFormation template to your AWS Organization management account.

## Deploy the Role to Member Accounts

Follow the steps in [Deploy the Member Templates](../getting_started/cloudformation.html#3-deploy-the-member-templates) to deploy the CloudFormation stacks (via StackSets) to all the applicable member accounts.

## Authenticate to the Organization Management Account

Using an IAM entity that you have access to, and that you specified to be trusted in the Wut.Dev management account stack, [authenticate to obtain your temporary credentials](../getting_started/authenticating.html). Pass those credentials to Wut.Dev via the "Manage AWS Connection" button.

## Enable Organization Mode

Click "Config" in the Wut.Dev console footer. In the popup, select your AWS Organization management account from the dropdown next to "AWS Organizations Mode".

## Switch Accounts

Now, when you select the account dropdown at the top of the page, Wut.Dev will use your Organization management account's session to list the available member accounts. When you select one, it will assume the previously-created role to generate a temporary session to use in your browser.