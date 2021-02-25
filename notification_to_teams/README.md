# about
Send AWS CodePipeline execution status to Microsoft Teams app.

# constitution
![TeamsNoftification](https://user-images.githubusercontent.com/72424558/109098278-5d426780-7764-11eb-8cac-fdcce91e3adf.png)

# how to setup

## :pushpin: Teams
#### Create teams conncter

Create 'Incoming Webhook' connecter on your MS Teams channel which want to recieve notifications.
[…]-[Conneter]-[Incoming webhook]


## :pushpin: AWS Codepipeline

#### 1. Add notification rule

Setting Codepipeline and add notification rule.
Like: teams-notification

You can customize the event to be notified.
Like: 
Succeeded
Canceled
Failed

Set the created SNS topic as the target.

#### 2. Create SNS topic

<strong>You have to create SNS topic in CodePipeline setting page.</strong>

If you create SNS topic in SNS setting page, it dosen't work cause by access policy. 

Set a descriptive name.
Like: codepipeline-finish-notification


## :pushpin: AWS Lambda

#### 1. Create Lambda fnuction

Set a descriptive name.
Like: CodePipelineNotificationToMsTeams

Select 'Python 3.8' for runntime.

#### 2. Imporrt Lambda function

Import the file 'package.zip' in this repository.
(it is my personal file, sorry)

#### 3. Setting an environment variable

Set the following to environment variables of Lambda.
| Name | Value |
| --- | --- |
| TEAMS_ENDPOINT |  https://outlook.office.com/webhook/your-teams-channel-connecter-url |

#### 4. Setting SNS topic as the trigger

Add create SNS topic as the trigger.
