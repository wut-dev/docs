---
title: Home
layout: home
nav_order: 1
image: /assets/images/cover.png
---

# Wut.Dev Documentation

{: .warning }
Wut.Dev is currently in beta. Please [report any issues](https://github.com/wut-dev/docs/issues/new/choose).

## What is Wut.Dev?

_[w•u•t](https://en.wiktionary.org/wiki/wut) (interjection): A sound or expression made by developers in response to an unexpected or unclear error._

[Wut.Dev](https://wut.dev) is a client-side platform for viewing, managing, and debugging AWS security policies, controls, and access issues related to AWS Organization Service Control Policies (SCPs), IAM policies, and resource policies.

Think of Wut.Dev as a missing link between development and security teams, translating the amalgamation of policies, security controls, and error messages into meaningful next steps to unblock developers as they build their cloud applications.

## What does Wut.Dev do?
Wut.dev's goal is to serve as the first place security and development teams turn to view and debug security, policy, or access issues in their AWS environment. See an issue, ask "wut!?"

Wut.Dev connects to your AWS Organization (and its member accounts) via a read-only audit role to extract Organization and account metadata, relationships, and policies. This information then powers features for both security and development teams:

* **AWS Organizations Viewer** - view all of your AWS Organization OUs and accounts in an interactive tree diagram
    * **Account Move Simulator** - quickly evaluate the policy implications of moving an AWS account between OUs
* **AWS Service Control Policy (SCP) Viewer** - view SCPs, policy content, tags, and targets
    * **Policy Coverage Map** - single pane of glass for viewing SCP coverage across all accounts
* **Access Denied Debugger** - paste an "access denied" error message to view a stack-trace-style overview of the relevant accounts, Organization policies, IAM principals, CloudTrail activity logs, and policy simulators

## Why should I use Wut.Dev?

AWS security controls and IAM policy logic are complex, and your developers are likely spending hundreds of combined engineer-hours each month debugging opaque error messages like "access denied due to an implicit deny in a service control policy."

Establishing secure cloud access patterns often means understanding how org-level, account-level, principal-level, _and_ resource-level security controls apply to a particular request. Developers may not even have access to (or even know where to find) each of these policies (which might be managed by other teams), making designing a successful request a guessing game of frustration.

The result is increased support load on security teams, who now must work backwards to first understand the intent of the request, and then piece together how each of the controls they've written could potentially impact it.

Most cloud security tools today are focused on surfacing and blocking security risks by proposing policy or controls to fix those risks. However, these tools often ignore the potential impact to developer productivity as the cloud environment becomes more locked down.

### Benefits for Developers
* Self-serve debugging of access issues
* Easy-to-understand explanations of common AWS security controls
* Links and redirects to alternative preferred access patterns
* Quickly visualize AWS account environments and their contacts
* Dynamically-updating live view of account relationships

### Benefits for Security Teams
* Less time spent debugging access issues for other teams
* Enhanced operational safety guarantees when making low-level infrastructure changes, such as applying or modifying SCPs
* Improved confidence in applying best-practice security controls