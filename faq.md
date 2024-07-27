---
title: FAQ
layout: default
nav_order: 4
---

# FAQ

## Q. What is Wut.Dev?
[Wut.Dev](https://wut.dev) is a client-side platform for viewing, managing, and debugging AWS security policies, controls, and access issues related to AWS Organization Service Control Policies (SCPs), IAM policies, and resource policies.

## Q. What do you mean by "client-side?"
Wut.Dev is delivered via CDN as a static HTML/JavaScript/CSS page to your browser and all data is stored and processed locally. Communication with AWS occurs via the AWS JavaScript SDK. Wut.Dev does not have an API, or server-side component, meaning your data, and AWS credentials, never leave your local machine.

## Q. What are the minimum requirements to use Wut.Dev?
You need a browser, internet connection (to AWS), and IAM credentials to access certain read-only AWS APIs. We recommend the `SecurityAudit` managed policy, which grants limited access to your AWS account and resource metadata.

## Q. I don't use AWS Organizations, can I still use Wut.Dev?
Yes, although features will be more limited. Simply enter credentials belonging to the AWS account you wish to use. Note that Wut.Dev will not be able to debug cross-account access, or other AWS Organization-related issues (e.g., SCPs).

## Q. Can I give my developers access to Wut.Dev?
Yes! We're making this easier in the future, but in the meantime, the process looks like this:
1. Deploy the `WutDotDev-Mgmt` role
1. Update this role's trust policy so that your developers can assume it
1. When they want to use Wut.Dev, they run `aws sts assume-role` to get temporary credentials, which they can load into Wut.Dev's interface.
1. They can then use Wut.Dev for ~12 hours (or however long the session is configured for)

## Q. Is Wut.Dev a security tool or a developer tool?
Both. For security teams, Wut.Dev aims to make managing AWS policies simpler. For development teams, Wut.Dev can help debug and translate the vast array of confusing AWS policies, helping unblock access issues experienced during application and infrastructure development.