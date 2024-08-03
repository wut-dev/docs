---
title: Tips & Tricks
layout: default
nav_order: 5
---

# Tips & Tricks

## Authenticate with Wut.Dev from a CLI Alias
Wut.Dev has a page, `/auth`, which accepts the URL parameter `?auth=` containing base64-encoded JSON credential payload (the output of `aws sts assume-role`). You can create a local CLI alias to make re-authenticating super simple.

Be sure to replace `AccountId` in the command below.

```bash
alias wut-auth='open "http://wut.dev/auth?auth=$(aws sts assume-role --role-arn arn:aws:iam::{AccountId}:role/WutDotDev-Mgmt --role-session-name WutDotDev --output json --policy '\''{"Version": "2012-10-17","Statement": {"Effect": "Allow","Action": "*","Resource": "*","Condition": {"IpAddress": {"aws:SourceIp": "'\''$(curl -s http://checkip.amazonaws.com)'\''"}}}}'\'' | base64)"'
```

The above command:
1. Assumes the `WutDotDev-Mgmt` role
1. Passes a session policy locking the credentials to your IP address
1. Converts the output to base64
1. Passes this to the `/auth?auth=` Wut.Dev endpoint

You can then save the credentials and use Wut.Dev.

## Send Errors from the CLI to Wut.Dev
If you are getting an error with an AWS command, like the following:

```bash
$ aws ecr create-repository --repository-name project-a/nginx-web-app

An error occurred (AccessDeniedException) when calling the CreateRepository operation: User: arn:aws:iam::123456789101:user/example is not authorized to perform: ecr:CreateRepository on resource: arn:aws:ecr:us-east-1:123456789101:repository/project-a/nginx-web-app because no permissions boundary allows the ecr:CreateRepository action
```

You can create a bash alias to pipe the error directly to Wut.Dev's `/error` page.

Open `~/.bash_profile` and add:

```bash
# Function to open wut with a search query
wut() {
    local query
    # Read from stdin if input is piped
    if [ -p /dev/stdin ]; then
        query=$(cat -)
    else
        query=$1
    fi
    # Open the URL in the default web browser
    open "https://wut.dev/error?error=$query"
}

# Alias to use the function
alias wut=wut
```

Then, you can re-run commands like the above, piping the error to `wut`:

```bash
aws ecr create-repository --repository-name project-a/nginx-web-app 2>&1 | wut
```