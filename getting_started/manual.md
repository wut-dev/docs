---
title: Manual Setup
layout: default
nav_order: 2
parent: Getting Started
---

# Manual Setup

## 1. Create the Wut.Dev IAM Role

In this step, we'll create an IAM role, called `WutDotDev-Mgmt` in your AWS Organization management account.

1. Create a new IAM role, called `WutDotDev-Mgmt`

## 2. Assign Limited Read-Only Permissions

In this step, we'll assign the role a limited set of IAM permissions that grant it read-only access to access metadata about your Organization and accounts.

1. Attach two managed policies:
    1. `AWSOrganizationsReadOnlyAccess`
    1. `SecurityAudit`
1. Attach an inline policy with the following content (this allows the role to assume the `Wut` role in member accounts):
    ```
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Action": "sts:AssumeRole",
          "Resource": "arn:aws:iam::*:role/WutDotDev-Member",
          "Effect": "Allow"
        }
      ]
    }
    ```

## 3. Configure the Role Trust Policy

In this step, we'll update the role's trust policy so that your engineers can assume, and use, the role via the Wut.Dev application.

1. Attach the following trust relationship to the role, replacing `{YOUR ORG HERE}` and `{YOUR ROLE HERE}`:
    ```
    {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Principal": {
                  "AWS": "*"
              },
              "Action": "sts:AssumeRole",
              "Condition": {
                  "StringEquals": {
                      "aws:PrincipalOrgID": "{YOUR ORG HERE}"
                  },
                  "StringLike": {
                      "aws:PrincipalArn": "arn:aws:iam::*:role/{YOUR ROLE HERE}"
                  }
              }
          }
      ]
    }
    ```

## 4. Use the Role

In this step, we'll use the STS "Assume Role" capability to obtain the temporary IAM permissions for use in Wut.Dev.

```bash
aws sts assume-role --role-arn arn:aws:iam::{AccountId}:role/WutDotDev-Mgmt --role-session-name WutDotDev
```

The access key ID, secret ID, and session token can then be copied into Wut.Dev.

{: .note }
You'll need to provide the above command/instructions to your engineers to whom you want to grant access to the Wut.Dev interface. We recommend creating an alias, like `wut` on the CLI to do so.

## 5. Deploy the Member Account Roles

In this (optional) step, we'll deploy an IAM role, called `WutDotDev-Member` to member accounts in your Organization. The `WutDotDev-Mgmt` role can assume this role, which will be used for debugging policies and access issues spanning multiple accounts.

{: .warning }
We strongly recommend using CloudFormation StackSets for this step; creating an IAM role in every member account can be very tedious.

1. Log into each member account using an entity that has permission to create and manage IAM roles.
1. Create an IAM role, called `WutDotDev-Member`
1. Attach the `SecurityAudit` managed IAM policy
1. Assign the following trust policy, replacing `{AWS MGMT ACCOUNT}` with the account ID of your AWS Organization management account
    ```
    {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Principal": {
                  "AWS": "arn:aws:iam::{AWS MGMT ACCOUNT}:role/WutDotDev-Mgmt"
              },
              "Action": "sts:AssumeRole"
          }
      ]
    }
    ```