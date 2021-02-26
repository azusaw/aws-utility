# about
Apply basic authentication to static web pages delivered by AWS CloudFront.

# constitution


# how to setup

## :pushpin: AWS Lambda
#### 1. Create function

Create Lambda@Edge function on your AWS account.

Be sure to create it in <strong>the US East (N. Virginia) Region</strong>.

:warning: Lambda@Edge is only supported in the US East (N. Virginia) Region.

```javascript:index.js
'use strict';
exports.handler = (event, context, callback) => {

    // Get request and request headers
    const request = event.Records[0].cf.request;
    const headers = request.headers;

    // Configure authentication
    const authUser = 'yourUserName';
    const authPass = 'yourPassword';

    // Construct the Basic Auth string
    const authString = 'Basic ' + new Buffer(authUser + ':' + authPass).toString('base64');

    // Require Basic authentication
    if (typeof headers.authorization == 'undefined' || headers.authorization[0].value != authString) {
        const body = 'Unauthorized';
        const response = {
            status: '401',
            statusDescription: 'Unauthorized',
            body: body,
            headers: {
                'www-authenticate': [{key: 'WWW-Authenticate', value:'Basic'}]
            },
        };
        callback(null, response);
    }

    // Continue request processing if authentication passed
    callback(null, request);
};
```

#### 2. Deploy to Lambda@Edge

[Actions]-[Deploy to Lambda@Edge]
Select your Cloudfront distribution as "Distribution".


## :pushpin: AWS CloudFront
#### Check settings

[Behaviors]-[Edit]

Make sure that the ARN of the Lambda＠Edge you created is set in Lambda Function Associations

