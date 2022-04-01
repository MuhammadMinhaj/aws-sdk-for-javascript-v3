--------

Help us improve the AWS SDK for JavaScript version 3 \(V3\) documentation by providing feedback using the **Feedback** link, or create an issue or pull request on [GitHub](https://github.com/awsdocs/aws-sdk-for-javascript-v3)\.

 The [AWS SDK for JavaScript V3 API Reference Guide](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/index.html) describes in detail all the API operations for the AWS SDK for JavaScript version 3 \(V3\)\.

--------

# Deploy the Lambda function<a name="lambda-create-table-deploy-function"></a>

This topic is part of a tutorial that demonstrates how to create, deploy, and run a Lambda function using the AWS SDK for JavaScript\. To start at the beginning of the tutorial, see [Creating and using Lambda functions](lambda-create-table-example.md)\.

In the root of your project, create a `lambda-function-setup.js` file, and paste the content below into it\.

Replace *BUCKET\_NAME* with the name of the Amazon S3 bucket you uploaded the ZIP version of your Lambda function to\. Replace *KEY* with the name of name the ZIP version of your Lambda function\. Replace *ROLE* with the Amazon Resource Number \(ARN\) of the IAM role you created in the [Create the AWS resources ](lambda-create-table-provision-resources.md) topic of this tutorial\. Replace *LAMBDA\_FUNCTION* with the same name you gave the function in the `/Lambda/index.js` in the [Prepare the browser script](lambda-create-table-browser-script.md) topic of this tutorial\.

```
// Load the Lambda client.
const {
        CreateFunctionCommand
} = require("@aws-sdk/client-lambda");
const {lambdaClient} = require("./libs/lambaClient")

// Set the parameters.
const params = {
    Code: {
        S3Bucket: "BUCKET_NAME", // BUCKET_NAME
        S3Key: "ZIP_FILE_NAME", // ZIP_FILE_NAME
    },
    FunctionName: "FUNCTION_NAME",
    Handler: "index.handler",
    Role: "IAM_ROLE_ARN", // IAM_ROLE_ARN; e.g., arn:aws:iam::650138640062:role/v3-lambda-tutorial-lambda-role
    Runtime: "nodejs12.x",
    Description: "Creates an Amazon DynamoDB table.",
};

const run = async () => {
    try {
        const data = await lambdaClient.send(new CreateFunctionCommand(params));
        console.log("Success", data); // successful response
    } catch (err) {
        console.log("Error", err); // an error occurred
    }
};
run();
```

Enter the following at the command line to deploy the Lambda function\.

```
node lambda-function-setup.js
```

This code example is available [here on GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/blob/master/javascriptv3/example_code/lambda/lambda_create_function/src/lambda-function-setup.js)\.

To run the app, open the `index.html` in the Amazon S3 bucket that hosts the application\. To do this, go open the Amazon S3 bucket in the console, select the bucket, and choose the **Object URL**\.