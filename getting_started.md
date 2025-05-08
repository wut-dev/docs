---
title: Getting Started
layout: default
nav_order: 2
has_children: true
---

# Getting Started

## Requirements
Wut.Dev is a client-side application that works by using the AWS JavaScript SDK in your browser. As such, the primary requirement is that your load AWS credentials into memory that have access to make the AWS API requests necessary to enable wut.dev's features.

Some things you'll need:

1. A browser (preferably the latest version of Chrome)
2. An internet connection (to communicate with the AWS APIs)
3. AWS credentials with read-only "SecurityAudit" access to your AWS account(s)

## Access Patterns

Technically, Wut.Dev can work with any AWS account, but since many of its features are oriented around AWS Organizations, it's more useful to connect the management account. If you have multiple accounts, Wut.Dev can use the primary (or management) account's role to assume a role into each applicable member account, eliminating the need to load credentials for all of your accounts individually.

### Standalone Mode

In standalone mode, you pass credentials for a single AWS account to Wut.Dev and browse as that user. See [Standalone Mode](/getting_started/standalone_mode) for more details.

### Organization Mode

![Data Flow Diagram](assets/images/data-flow.png)

Wut.Dev users (i.e. human engineers via an IAM entity) assume the `WutDotDev-Mgmt` role, passing the temporary credentials to Wut.Dev. The Wut.Dev application then transparently assumes the `WutDotDev-Member` role, in other accounts, when required.

## Wut.Dev Setup

{: .warning }
The following steps are for the Organization mode configuration. To get started quickly with a single account, we recommend [Standalone Mode](/getting_started/standalone_mode).

There are several steps involved, which we'll walk through below:

1. Create an IAM role in the management account
2. Give it the necessary (limited, read-only) permissions (e.g., `organizations:Describe*`)
3. Configure the role's trust policy so that your engineers (Wut.Dev users) can use the role
4. Assume the role and load the temporary credentials in Wut.Dev
5. (Optionally) deploy roles in relevant member accounts for the management role to assume

We've created CloudFormation templates to help automate these steps, but manual steps are included below.

### Pre-Requisites

1. You must be able to log into your AWS Organization management account using an IAM principal that has permission to deploy CloudFormation templates and IAM roles. If you don't have this access, ask the team that manages your AWS environment.
1. You must decide which IAM entities belonging to (human) engineers in your AWS environment can use the Wut.Dev tool. This should be an AWS IAM ARN (e.g., `arn:aws:iam::{AccountId}:role/human-engineers`).

## Via CloudFormation (Recommended)

See [CloudFormation Setup](/getting_started/cloudformation)

## Manual Setup (Not Recommended)

See [Manual Setup](/getting_started/manual)
