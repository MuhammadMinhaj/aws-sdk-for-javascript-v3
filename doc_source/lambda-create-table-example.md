--------

Help us improve the AWS SDK for JavaScript version 3 \(V3\) documentation by providing feedback using the **Feedback** link, or create an issue or pull request on [GitHub](https://github.com/awsdocs/aws-sdk-for-javascript-v3)\.

 The [AWS SDK for JavaScript V3 API Reference Guide](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/index.html) describes in detail all the API operations for the AWS SDK for JavaScript version 3 \(V3\)\.

--------

# Creating and using Lambda functions<a name="lambda-create-table-example"></a>

The tutorial describes how to create and execute from the browser a Lambda function that creates a DynamoDB table\.

The tutorial should take about 20 minutes to complete\.

**To build the app:**

1. [Prerequisite tasks ](#lambda-create-table-prerequisites)

1. [Create the AWS resources ](lambda-create-table-provision-resources.md)

1. [Create the HTML ](lambda-create-table-create-html.md)

1. [Prepare the browser script ](lambda-create-table-browser-script.md)

1. [Create and upload Lambda function ](lambda-create-table-create-lambda-function.md)

1. [Deploy the Lambda function ](lambda-create-table-deploy-function.md)

1. [Delete the resources](lambda-create-table-destroy.md)

## Prerequisite tasks<a name="lambda-create-table-prerequisites"></a>

To set up and run this example, you must first complete these tasks:
+ Set up the project environment to run these Node TypeScript examples, and install the required AWS SDK for JavaScript and third\-party modules\. Follow the instructions on[ GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/javascriptv3/example_code/lambda/lambda_create_function/README.md)\.
+ Create a shared configurations file with your user credentials\. For more information about providing a credentials JSON file, see [Loading credentials in Node\.js from the shared credentials file](loading-node-credentials-shared.md)\.