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

[Wut.Dev](https://wut.dev) is a client-side AWS console alternative for viewing, managing, debugging, and documenting AWS resources, logs, security policies, and controls.

Wut's primary features are:
* Consistent, unified read-only interface to access resources across all AWS services
* Quick sorting, filtering, searching, and exporting of resources
* Privacy-first, client-side execution model with no server-side dependencies
* Multi-region, multi-account support (including switching between Organization member accounts)
* View all of your AWS Organization OUs and accounts in an interactive tree diagram
* Automated resource relationship diagrams (coming soon)
* (Optional) LLM integration for policy analysis and documentation (also client-side via your own LLM API key)

## What does Wut.Dev do?
Wut.Dev provides an alternative means of view and interacting with AWS resources, logs, security policies, and controls with native features built for developers and security teams.

We want Wut.Dev to be the first place infrastructure and security teams turn to view resources, debug security, policy, or access issues, or otherwise gather data about their AWS environment. Need to know something? Ask "wut!?"

Wut.Dev connects to your AWS account(s) via local (in browser only) AWS credentials and uses the client-side AWS SDK to make AWS API calls.

## Why should I use Wut.Dev?

The AWS console is a powerful tool, but it's not always the best tool for the job. It's bloated, slow, inconsistent, single-region, and single-account. Oftentimes, getting from "I know the thing I want to look at" to "I have the thing I want to look at" is a frustrating experience. Once you find the resource, you're then left correlating data sources from other places (logs from CloudTrail, policies from IAM, trusted resources from other accounts, etc.). Wut.Dev aims to bring these resources and data together in a cohesive, well-designed interface.

Wut.Dev is also building the first (optionally) LLM-integrated cloud console. If / when AI is "right for the job," Wut.Dev will expose it in unobtrusive ways. Some examples of places we've found LLMs to be helpful include:
* Summarizing log events
* Explaining moderately-complex IAM and SCP policies
* Understanding the logic in conditional statements in policies