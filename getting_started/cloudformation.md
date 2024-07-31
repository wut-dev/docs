---
title: CloudFormation Setup
layout: default
nav_order: 1
parent: Getting Started
---

# CloudFormation Setup

We recommend using the Wut.Dev-provided CloudFormation templates, which will configure the correct roles, policies, and trust relationships for Wut.Dev to work properly and securely.

## 1. Deploy the Management Template

This step will create an IAM role in your management account, called `WutDotDev-Mgmt` and give it the permissions necessary to assume _other_ Wut.Dev roles deployed in your member accounts, as well as call read-only `organizations` APIs.

1. Click the link below to open the CloudFormation Stack creation wizard
1. The following parameters are required:
    1. `AssumeRolePrincipalArn`
        1. The `WutDotDev-Mgmt` role needs to be assumed by (human) engineers in your organization. Because every company manages AWS access differently, we can't pre-populate this for you.
        1. You should set this to the role name associated with human engineers that you want to grant access to Wut.Dev.
        1. You can use wildcards if engineers in multiple accounts should be granted access. Example: `arn:aws:iam::*:role/engineers`.
        1. **Security Note**: the template already includes a condition statement that limits assume role access to entities in your organization only (see the next parameter).
    1. `OrganizationUnitId`
        1. The trust policy for the `WutDotDev-Mgmt` is configured to only trust IAM entities that match the pattern defined in `AssumeRolePrincipalArn`. Because this can include wildcards, the `OrganizationUnitId` is used to provide an added layer of security.
        1. You can find your Organization ID in the [Organizations AWS console](https://console.aws.amazon.com/organizations/v2/home/accounts). It should look like `o-abcdef1234`.
    1. `IncludeSecurityAudit`
        1. Whether the `SecurityAudit` policy should be attached to the `WutDotDev-Mgmt` role. This is useful if you're debugging access issues _in the management account_ but otherwise can be set to `false` if you're only debugging member accounts.

[Create CloudFormation Stack](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://wut-dev-templates.s3.amazonaws.com/cfn-wut-dot-dev-mgmt-role.json&stackName=WutDotDev-Mgmt&param_AssumeRolePrincipalArn=replace-me&param_OrganizationUnitId=replace-me){: .btn .btn-purple }

## 2. Use the Role

When you're done, the IAM entities defined in `AssumeRolePrincipalArn` can now assume and use this role in Wut.Dev by running:

```bash
aws sts assume-role --role-arn arn:aws:iam::{AccountId}:role/WutDotDev-Mgmt --role-session-name WutDotDev
```

The access key ID, secret ID, and session token can then be copied into Wut.Dev.

{: .note }
You'll need to provide the above command/instructions to your engineers to whom you want to grant access to the Wut.Dev interface. We recommend creating an alias, like `wut` on the CLI to do so.

## 3. Deploy the Member Templates

{: .note }
If you haven't used CloudFormation StackSets in your Organization you may need to [configure the initial access](https://docs.aws.amazon.com/organizations/latest/userguide/services-that-can-integrate-cloudformation.html).

This step will create an IAM role in each of your member accounts, called `WutDotDev-Member` and give it the permissions necessary to call read-only APIs required for debugging and policy management (using the `SecurityAudit` policy). Its trust relationship will be configured to trust the `WutDotDev-Mgmt` role we created above.

1. Open the [CloudFormation StackSet creation wizard](https://console.aws.amazon.com/cloudformation/home?#/stacksets/create)
1. Use the following options:
    1. **Permissions**: Service-managed permissions
    1. **Prerequisite - Prepare template**: Template is ready
    1. **Specify template**: Amazon S3 URL
        1. Paste the following URL: `https://wut-dev-templates.s3.amazonaws.com/cfn-wut-dot-dev-member-role.json`
    1. **StackSet name**: `WutDotDev-Members`
    1. **StackSet description**: `Member account access for Wut.Dev`
    1. **Parameters: OrganizationMgmtAccountId**: Enter the AWS account ID of your AWS Organization management account
    1. **Execution configuration**: Inactive
    1. **Add stacks to stack set**: Deploy new stacks
    1. **Deployment targets**: Deploy to organization
        1. Note: If you prefer to only enable Wut.Dev on certain OUs, you can specify those here instead
    1. **Auto-deployment options**:
        1. **Automatic deployment**: Activated
        1. **Account removal behavior**: Delete stacks
    1. **Specify regions**: `us-east-1` (or your choice; only specify a single region)
    1. **Deployment options**
        1. **Maximum concurrent accounts - optional**: 1
        1. **Failure tolerance - optional**: 0
        1. **Region concurrency**: Sequential
        1. **Concurrency mode**: Strict failure tolerance
1. Review and deploy the template