---
layout: post
title: "Host static website on AWS S3"
date: 2018-04-28 18:50 +1000
---

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket/*"
            ]
        }
    ]
}
```

https://docs.aws.amazon.com/AmazonS3/latest/user-guide/static-website-hosting.html

https://docs.aws.amazon.com/AmazonS3/latest/dev/website-hosting-custom-domain-walkthrough.html

https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteEndpoints.html