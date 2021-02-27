# about
Send an email when the contact form on the website submitted

# constitution


# how to setup

## :pushpin: Amazon API Gateway
#### 1. Create the API for POST



## :pushpin: SES
#### Verify the email address

[Email Adresses]-[Verify a New Email Address]

Register the email address you want to send from.

## :pushpin: AWS Lambda
#### 1. Create Lambda function

```javascritp:index.js
'use strict'
const SDK = require('aws-sdk');

exports.handler = (event, context, callback) => {
	// set your region
    const ses = new SDK.SES({ region: 'us-west-2' });
    const email = {
    	// From
        Source: "no-reply@hoge.hoge",
        // To
        Destination: { ToAddresses: ["your-address@hoge.hoge"] },
        
        Message: {
            Subject: { Data: "New inquiry from the website" },
            Body: {
                Text: { Data: [
                    '[contact type] ' + event.contactType,
                    '[email] ' + event.email,
                    '[name] ' + event.name,
                    '[phone number] ' + event.phoneNumber,
                    '[company] ' + event.company,
                    '[department] ' + event.department,
                    '[details] : ' + event.details
                ].join("\n")}
            },
        }
    };
    ses.sendEmail(email, callback);
};

```

