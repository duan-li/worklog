---
layout: page
title: AWS CLI
---

## AWS Regions

Region Name | Region 
----- | ----- 
US East (Ohio) | us-east-2
US East (N. Virginia) | us-east-1
US West (N. California) | us-west-1
US West (Oregon) | us-west-2
Asia Pacific (Tokyo) | ap-northeast-1
Asia Pacific (Seoul) | ap-northeast-2
Asia Pacific (Osaka-Local) | ap-northeast-3
Asia Pacific (Mumbai) | ap-south-1
Asia Pacific (Singapore) | ap-southeast-1
Asia Pacific (Sydney) | ap-southeast-2
Canada (Central) | ca-central-1
China (Beijing) | cn-north-1
China (Ningxia) | cn-northwest-1
EU (Frankfurt) | eu-central-1
EU (Ireland) | eu-west-1
EU (London) | eu-west-2
EU (Paris) | eu-west-3
South America (São Paulo) | sa-east-1

## AWS CLi
* [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)
* [AWS Regions](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html)
* [Python AWS client](https://boto3.readthedocs.io/en/latest/reference/services/lambda.html)


### Lambda

Create Lambda Function Handler[^1]

[^1]: [Lambda Function Handler (Python)](https://docs.aws.amazon.com/lambda/latest/dg/python-programming-model-handler-types.html)
```python
# -*- coding: UTF-8 -*-

def handler(event, context):
	return {
		'message': 'This is just hello world!'
	}

```

**zip file**
```bash
# in the work directory
zip -r hello_serverless.zip *
```

AWS command line[^2]

[^2]: [AWS lambda manual](https://docs.aws.amazon.com/cli/latest/reference/lambda/index.html#cli-aws-lambda)
```bash
aws lambda create-function \
--region $AWSREGION \
--function-name HelloServerless \
--zip-file fileb://hello_serverless.zip \
--role arn:aws:iam::$AWSACCOUNTID:role/lambda_basic_execution  \
--handler hello_serverless.handler \
--runtime python3.6 \
--timeout 15 \
--memory-size 512
```

Return 
```json
{
    "FunctionName": "HelloServerless",
    "FunctionArn": "arn:aws:lambda:ap-northeast-2:$AWSACCOUNTID:function:HelloServerless",
    "Runtime": "python3.6",
    "Role": "arn:aws:iam::$AWSACCOUNTID:role/lambda_basic_execution",
    "Handler": "hello_serverless.handler",
    "CodeSize": 293,
    "Description": "",
    "Timeout": 15,
    "MemorySize": 512,
    "LastModified": "2018-08-27T12:28:13.627+0000",
    "CodeSha256": "x/B6/rsGnFF4tSNdjcO2czVk=",
    "Version": "$LATEST",
    "TracingConfig": {
        "Mode": "PassThrough"
    },
    "RevisionId": "32f9d495-4d73-29725ef6237c"
}

```

**Tips: Bash shell script create/update function**
```bash
#!/bin/bash
rm ./hello_serverless.zip
zip -r hello_serverless.zip *

string=$(aws lambda list-functions)
if [[ $string = *"HelloServerless"* ]]; then
	aws lambda update-function-code --region $AWSREGION --function-name HelloServerless --zip-file fileb://hello_serverless.zip 
else 
	aws lambda create-function --region $AWSREGION --function-name HelloServerless --zip-file fileb://hello_serverless.zip --role arn:aws:iam::$AWSACCOUNTID:role/lambda_basic_execution  --handler hello_serverless.handler --runtime python3.6 --timeout 15 --memory-size 512
fi
```

Working with packages[^3]

```python

```

**Invoke It Manually**
https://docs.aws.amazon.com/lambda/latest/dg/with-on-demand-custom-android-example-upload-deployment-pkg.html


[^3]: [Creating a Deployment Package (Python)](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html)


---
