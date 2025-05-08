---
title: FAQ
layout: default
nav_order: 4
---

# FAQ

## Q. What is Wut.Dev?
[Wut.Dev](https://app.wut.dev) is a client-side AWS console alternative for viewing, managing, debugging, and documenting AWS resources, logs, security policies, and controls.

## Q. What do you mean by "client-side?"
Wut.Dev is delivered via CDN as a static HTML/JavaScript/CSS page to your browser and all data is stored and processed locally. Communication with AWS occurs via the AWS JavaScript SDK. Wut.Dev does not have an API, or server-side component, meaning your data, and AWS credentials, never leave your local machine.

## Q. How can I be sure my credentials are safe?
Wut.Dev aims to provide as many safeguards as possible to ensure your AWS credentials are kept safe:
1. Wut.Dev does not have an API, or server-side component, of the application (see above). Your credentials are never sent anywhere.
1. Our documentation and setup automation strongly recommends the use of (temporary) IAM role sessions
1. Our documentation includes the use of IP-restricted session policies; the credentials you paste into Wut.Dev can be locked to your IP only
1. Our documentation recommends attaching the `SecurityAudit` policy, which is a well-scoped read-only AWS IAM policy created for security tools
1. Wut.Dev does not load any third-party dependencies; all code is served directly from our domain
1. Since Wut.Dev runs entirely in your browser, you can view all of the network traffic via the network tab
1. You can verify in AWS CloudTrail the API calls that your credentials made, and that these calls originated from your IP address

## Q. What are the minimum requirements to use Wut.Dev?
You need a browser, internet connection (to AWS), and IAM credentials to access certain read-only AWS APIs. We recommend the `SecurityAudit` managed policy, which grants limited access to your AWS account and resource metadata.

## Q. I don't use AWS Organizations, can I still use Wut.Dev?
Yes, although features will be more limited. Simply enter credentials belonging to the AWS account you wish to use. Note that Wut.Dev will not be able to debug cross-account access, or other AWS Organization-related issues (e.g., SCPs). See [Standalone Mode](/getting_started/standalone_mode).

## Q. Can I give my developers access to Wut.Dev?
Yes! We're making this easier in the future, but in the meantime, the process looks like this:
1. Deploy the `WutDotDev-Mgmt` role
1. Update this role's trust policy so that your developers can assume it
1. When they want to use Wut.Dev, they run `aws sts assume-role` to get temporary credentials, which they can load into Wut.Dev's interface.
1. They can then use Wut.Dev for ~12 hours (or however long the session is configured for)

## Q. Is Wut.Dev a security tool or a developer tool?
Both. For security teams, Wut.Dev aims to make managing AWS policies simpler. For development teams, Wut.Dev can help debug and translate the vast array of confusing AWS policies, helping unblock access issues experienced during application and infrastructure development.