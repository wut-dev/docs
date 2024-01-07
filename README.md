# wut.dev
wut.dev is a 100% client-side, in-browser API explorer for the Amazon Web Services (AWS) API. It is built using the [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS.html).

## Usage
1. Visit [wut.dev](https://wut.dev)
2. Add your AWS credentials (access key ID, secret access key, and optional session token). See [Security](#security) below.
3. Select an AWS service from the dropdown menu
4. Select an API operation from the dropdown menu
5. Enter the required parameters for the operation
6. Click the "Make Request" button to send the request to AWS
7. View the request and response details

## Security
wut.dev is a client-side application. It does not send your AWS credentials to any server, nor store them locally, other than in-memory in your browser. Your credentials are only used to sign requests to AWS. You can verify this by using Chrome's "inspect network" feature.

There are several CSS/JavaScript dependencies:
* [Tabler](https://github.com/tabler/tabler) - an open-source UI kit
* [Tom Select](https://tom-select.js.org/) - an open source select box replacement library
* jQuery v3.6.1
* [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS.html)
    * Note: The _full_ SDK was generated using the [AWS SDK builder](https://sdk.amazonaws.com/builder/js/)

All dependencies are loaded from wut.dev; there are no third-party dependencies, libraries, or CDNs.

Curious about what's happening? Pop open "View Source" and the network console in your browser.

If you're not comfortable entering credentials, you can still browse the available APIs and documentation.

## Other
1. wut.dev is not affiliated with Amazon Web Services, Inc. or Amazon.com, Inc.
2. wut.dev is in alpha; please do not use it in production.
3. Why "wut.dev"? Because it's a "what" for AWS. And "wut" is a fun word to say. Also, the domain was surprisingly available.