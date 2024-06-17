# wut.dev
wut.dev is a 100% client-side, in-browser management tool for Amazon Web Services (AWS) Organizations and Service Control Policies (SCPs). It's built using the [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS.html).

![](demo.gif)

# Features
* Tree-style visualization for AWS Organizations, Organization Units (OUs), and accounts
* Table view with per-field search/filtering
* Visualize SCP (policy) attachments and their impact to downstream accounts in the OU tree
* Search across all OUs, accounts, and policies
* Pre-fetching and client-side caching of data for instant navigation
* Demo mode
* No sign up required
* 100% client-side (wut.dev does not operate an API)
* 100% free of ads, trackers, and analytics

# Usage
1. Visit [wut.dev](https://wut.dev)
1. Click "Manage Connection"
1. Enable Demo Mode OR enter credentials
1. Add your AWS credentials (access key ID, secret access key, and optional session token). See [Security](#security) below.
1. Browse your Organization, OUs, accounts, and policies

## Generating Credentials

wut.dev needs permission to query the AWS APIs for your Organization management account (see AWS Permissions required below). There are several ways to provide this access:

### Option 1 - Temporary IAM Session (Preferred)
1. Use the AWS CLI to log into your management account _with a read-only identity_ however you normally would (you should be able to run `aws sts get-caller-identity` and see your management account ID in the response).
1. Generate a temporary session by [running](https://docs.aws.amazon.com/cli/latest/reference/sts/get-caller-identity.html):
    ```
    aws sts get-session-token --duration-seconds 86400
    ```
1. Copy the access key, secret key, and session token into the wut.dev credentials screen
1. Note: you can use a different session duration, but may need to generate a new session and re-enter the credentials when refreshing data in wut.dev.

### Option 2 - IAM Role
1. Create a new IAM role for wut.dev and assign it the permissions below
1. Configure the role's trust relationship to allow your human user to assume it
1. [Run](https://docs.aws.amazon.com/cli/latest/reference/sts/assume-role.html) `aws sts assume-role --role-arn <your-role-arn>`
1. Copy the access key, secret key, and session token into the wut.dev credentials screen

### Additional Options

Because wut.dev is a client-side service, we do not operate an IAM role that can assume your role (the traditional pattern used in third-party SaaS applications for cross-account AWS access). We are working on additional options for self-hosted authentication.

# Security
wut.dev is a client-side application. It does not send your AWS credentials to any server, nor store them locally, other than in-memory in your browser. Your credentials are only used to sign requests to AWS. You can verify this by using Chrome's "inspect network" feature.

## AWS Permissions

Wut.dev makes the following AWS API calls:

```
organizations:listAccountsForParent
organizations:listTagsForResource
organizations:listOrganizationalUnitsForParent
organizations:listRoots
organizations:listPolicies
organizations:listTargetsForPolicy
organizations:describeOrganization
organizations:describePolicy
```

The credentials you enter must belong to an IAM entity that have these permissions.

## Web Dependencies

There are several CSS/JavaScript dependencies:
* [Tabler](https://github.com/tabler/tabler) - an open-source UI kit
* [Tom Select](https://tom-select.js.org/) - an open source select box replacement library
* jQuery v3.6.1
* [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS.html)
    * Note: The _full_ SDK was generated using the [AWS SDK builder](https://sdk.amazonaws.com/builder/js/)

* [Tabler + Bootstrap](https://tabler.io) - Open-source UI kit
* [AWS SDK](https://aws.amazon.com) - AWS API JavaScript client
* [Dexie.js](https://dexie.org) - A minimalistic JavaScript
library to interact with IndexedDB
    * wut.dev uses IndexedDB to cache the AWS Organization and policy content locally
* [Tom Select](https://tom-select.js.org/) - A library to make the select
drop-down boxes searchable</li>
* [Ag-Grid](https://www.ag-grid.com/) - A library to display nice looking tables
* [JQuery](https://jquery.com/) - Makes the JS go brrr

All dependencies are loaded from wut.dev; there are no third-party dependencies, libraries, or CDNs.

Curious about what's happening? Pop open "View Source" and the network console in your browser.

If you're not comfortable entering credentials, you can still use demo mode.

# Other
1. wut.dev is not affiliated with Amazon Web Services, Inc. or Amazon.com, Inc.
2. wut.dev is in alpha; please do not use it in production.
3. Why "wut.dev"? Because it's a "what" for AWS. And "wut" is a fun word to say. Also, the domain was surprisingly available.
