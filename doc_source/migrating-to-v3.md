--------

Help us improve the AWS SDK for JavaScript version 3 \(V3\) documentation by providing feedback using the **Feedback** link, or create an issue or pull request on [GitHub](https://github.com/awsdocs/aws-sdk-for-javascript-v3)\.

 The [AWS SDK for JavaScript V3 API Reference Guide](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/index.html) describes in detail all the API operations for the AWS SDK for JavaScript version 3 \(V3\)\.

--------

# Migrating your code to SDK for JavaScript V3<a name="migrating-to-v3"></a>

There are a number of migration paths to the SDK for JavaScript version 3 \(V3\)\. To take full advantage of the reduction in capacity potential of V3, we recommend using path 3\.

**Important**  
AWS SDK for JavaScript version 3 \(v3\) also comes with modernized interfaces for client configurations and utilities, which include credentials, Amazon S3 multipart upload, DynamoDB document client, waiters, and so forth\)\. You can find what changed in v2 and the v3 equivalents for each change in the [migration guide on the AWS SDK for JavaScript GitHub repo](https://github.com/aws/aws-sdk-js-v3/blob/main/UPGRADING.md)\.

------
#### [ Path 1 ]

Perform minimal changes:
+ Install only the specific AWS Service packages you need\.
+ Create and use V3 service clients, replacing the use of any global configuration values, such as Region, with configuration values passed in as arguments to the client\. 
**Note**  
You can set the AWS Region using an environment variable, or a shared configuration `config` file\. For more information, see [Setting credentials in Node\.js](https://docs.aws.amazon.com/en_us/sdk-for-javascript/v3/developer-guide/setting-credentials-node.html)\.

------
#### [ Path 2 ]

Follow path 1 and remove `.promise`, which are not required in V3\.

------
#### [ Path 3 ]

Follow path 1 and use the async/await programming model\.

------

**Important**  
For information about significant changes from AWS SDK for JavaScript v2 to v3, please see [Upgrading Notes \(2\.x to 3\.x\)](https://github.com/aws/aws-sdk-js-v3/blob/main/UPGRADING.md) on GitHub\.

The following sections describe these paths in detail, with examples\.

## Path 1 example<a name="path1-examples"></a>

The following code installs the AWS Service package for Amazon S3\. 

```
npm install @aws-sdk/client-s3
```

The following code loads the Amazon S3 service\.

```
import {S3} from '@aws-sdk/client-s3';
```

**Note**  
To use this approach you must import the full AWS Service packages, `S3` in this case, and not just the service clients\.

The following code creates an Amazon S3 service object in the `us-west-2` Region\.

```
const client = new S3({region: 'us-west-2'});
```

The following code creates and Amazon S3 bucket using a callback function, using the following syntax from V2\.

```
client.command(parameters)
```

```
import {S3} from '@aws-sdk/client-s3';
const client = new S3({region: 'us-west-2'});
const bucketParams = {
    Bucket : BUCKET_NAME
};
function run(){
         client.createBucket(bucketParams, function(err, data) {
         if (err) {
         console.log("Error", err);
         } else {
         console.log("Success", data.Location);
         }
    })
};
run();
```

## Path 2 example<a name="path2-examples"></a>

Here is a function call in V2 using a `promise`\.

```
const data =  await v2client.command(params).promise()
```

Here is the V3 version\.

```
const data = await v3client.command(params)
```

## Path 3 examples<a name="path3-examples"></a>

The following command installs the AWS Service package for Amazon S3\.

```
npm install @aws-sdk/client-s3; 
```

The following code loads only the Amazon S3 client, reducing the overhead\.

```
import {S3Client, CreateBucketCommand} from '@aws-sdk/client-s3';
```

 If you install only the client of a package, you must also import the V3 commands you want to use\. In this case, the code imports the `CreateBucketCommand`, which enables you to create an Amazon S3 bucket\. You can browse the available commands in your project's `node-modules/@aws-sdk/client-PACKAGE_NAME/commands` folder\. 

The following code creates an Amazon S3 service client object in the `us-west-2` Region\. 

```
const client = new S3Client({region: 'us-west-2'});
```

To call imported commands using the recommended async/await pattern, you must import the commands you want to use, and use the following syntax to run the command\.

```
  CLIENT.send(newXXXCommand)
```

The following example creates an Amazon S3 bucket using the async/await pattern, using only the client of the Amazon S3 service package to reduce overhead\.

```
import {S3Client, CreateBucketCommand} from '@aws-sdk/client-s3';
const client = new S3Client({region: 'us-west-2'});
const bucketParams = {
    Bucket : BUCKET_NAME
};

(async function () {
      try{
        const data = await client.send(new CreateBucketCommand(bucketParams));
        console.log("Success", data);
      } catch (err) {
        console.log("Error", err);
      }
})();
```

For more examples, see [SDK for JavaScript code examples](sdk-code-samples.md)\.