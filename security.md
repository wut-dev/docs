---
title: Security
layout: default
nav_order: 6
---

# Security
Wut.Dev is a read-only, privacy-focused, client-side resource explorer and debugging tool for viewing your AWS resources. There are no ads, trackers, analytics, or third-party hosted libraries. The AWS JavaScript SDK is used to make API calls directly to AWS from your browser. Wut.Dev has no API; you are browsing a static site. You can verify this by opening your browser's network panel and monitoring the network requests.

The AWS JavaScript SDK is used to make these API calls directly to AWS from your browser. Wut.Dev has no API; you are browsing a static site. You can verify this by opening your browser's network panel and monitoring the network requests.

## Summary
We collect as little information as possible to provide this service and have engineered it to work entirely within your browser, without any server-side components or dependencies that would require us to store or process your data.

## Credential Management
When you enter your AWS credentials (access key, secret, and session token) on wut.dev, they are cached in your browser's local storage so that they persist after a page refresh. Credentials are never sent elsewhere, and are used solely by the AWS SDK to sign API calls made to AWS endpoints.

## AWS Permissions

Wut.Dev uses the identity of the credentials you enter, meaning it has whatever AWS permissions belong to that IAM entity. Picture it as the AWS CLI, just in your browser.

For Organization-related features, the IAM entity you create for wut.dev must have access to the following AWS APIs in your Organization management account. We recommend using `organizations:list*` and `organizations:describe*`.

* `organizations:listAccountsForParent`
* `organizations:listTagsForResource`
* `organizations:listOrganizationalUnitsForParent`
* `organizations:listRoots`
* `organizations:listPolicies`
* `organizations:listTargetsForPolicy`
* `organizations:describeOrganization`
* `organizations:describePolicy`

Additionally, to debug IAM access issues, Wut.Dev uses the following API calls:

* `organizations.listParents`
* `organizations.describeAccount`
* `iam.listAccountAliases`
* `organizations.listPoliciesForTarget`
* `iam.getRole`
* `iam.getUser`
* `iam.listAttachedUserPolicies`
* `iam.getPolicy`
* `iam.getPolicyVersion`
* `iam.simulatePrincipalPolicy`
* `cloudtrail.lookupEvents`

To assume the Wut.Dev role in member accounts, the management account role must also be given `sts:Assume` role permission on the resource `arn:aws:iam::*:role/WutDotDevAccessRole`.

## Web Dependencies
Several dependencies are used on Wut.Dev:

* [Tabler + Bootstrap](https://tabler.io/) - Open-source UI kit
* [AWS SDK](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/) - AWS API JavaScript client
* [Dexie.js](https://dexie.org/) - A minimalistic JavaScript library to interact with IndexedDB (wut.dev uses IndexedDB to cache the AWS Organization and policy content locally)
* [Tom Select](https://tom-select.js.org/) - A library to make the select drop-down boxes searchable
* [Ag-Grid](https://www.ag-grid.com/) - A library to display nice looking tables
* [JQuery](https://jquery.com/) - Makes the JS go brrr

These dependencies are minified and served from wut.dev's domain. There are no third-party hosted dependencies.

## Privacy
When you access wut.dev, your IP address and user agent are logged by our CDN (AWS CloudFront). We do not log, or otherwise save, any other information about your usage of this site, including any information entered. There are no analytics, trackers, cookies, or other information used to view or record your session.

If you choose to enter your email address to receive updates, this information is recorded by Google Forms. We do not sell, rent, lease, or otherwise reveal your information to any other parties unless required by law.

## Legal
Wut.Dev is not affiliated with, endorsed by, or in any way associated with AWS. AWS is a registered trademark of Amazon.com, Inc. Your use of Wut.Dev is your responsibility. We are not responsible for any damages or losses that may occur as a result of using this site. By using this site, you agree to indemnify and hold harmless the site owner and its affiliates from any claims, damages, or losses that may occur as a result of using this site.