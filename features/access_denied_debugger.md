---
title: Access Denied Debugger
layout: default
nav_order: 1
parent: Features
---

# Access Denied Debugger

You can access the debugger at [wut.dev/error](https://wut.dev/error).

Wut.Dev helps debug AWS access denied error messages by:
* Extracting the relevant parts of the message
* Providing an interface for quickly viewing account details, Organization details, SCPs, IAM inline and managed policies, permissions boundaries, and resource policies that may affect the request
* Directly linking to the AWS console for relevant resources
* Loading CloudTrail activity logs related to the IAM principal and request

## Error Types
Wut.Dev currently supports many of the `User: {arn} is not authorized to perform {action}` error message types. For example:

* `User: arn:aws:iam::777788889999:user/JohnDoe is not authorized to perform: codecommit:ListRepositories because no service control policy allows the codecommit:ListRespositories action`
* `User: arn:aws:iam::777788889999:user/JohnDoe is not authorized to perform: codecommit:ListRepositories with an explicit deny in a service control policy`
* `User: arn:aws:iam::123456789012:user/JohnDoe is not authorized to perform: codecommit:ListRepositories because no VPC endpoint policy allows the codecommit:ListRepositories action`

##  How to Use the Debugger

1. Ensure you have configured Wut.Dev with the correct permissions in your account.
    1. See [Getting Started](/getting_started.html)
    1. If your error involves a single AWS account, and you want to get started quickly with your own credentials, you can use [Simple Mode](/getting_started/simple_mode.html)
    1. Otherwise, Wut.Dev will use the `WutDotDev-Mgmt` and `WutDotDev-Member` (read-only audit) roles in your Organization management and member accounts to run the diagnosis
1. Paste your error in the search bar on the [wut.dev/error](https://wut.dev/error) page.
1. Use the tree diagram to navigate the different parts of the decomposed error message.