# Setting up call analytics transcription jobs<a name="start-call-analytics"></a>

To get analytics data, you must run call analytics jobs\. Call analytics jobs not only transcribe the audio of the recordings between your agents and customers, but they provide meaningful information \(in the form of *analytics*\) about these conversations\. If you choose not to create any categories before running a call analytics job, the output only includes the following information:
+ Detected customer issues
+ Sentiment of the agent and the customer
+ Non\-talk time
+ Interruptions
+ Speaking volume

If you create categories, you can flag your analytics job based on the conversational characteristics you define\. These conversational characteristics can include:
+ Customer or agent sentiment during specific periods of time
+ Matching a portion of the transcript to a phrase you've specified
+ The customer or agent interrupting the other person
+ Neither the customer nor the agent spoke for a defined period of time

Once you create categories, Amazon Transcribe flags your call analytics jobs with a label indicating that the call matches all the rules you've defined in a given category\. For more information on creating categories, see [Using categories and rules](create-categories.md)\.

**Note**  
Call analytics jobs can't be classified retroactively with categories\. Only the categories you created *before* running a call analytics job can be applied to that job\.

## Console<a name="start-call-analytics-console"></a>

Use the following procedure to start a call analytics job\. The calls that match all the characteristics defined by a category are labeled with that category\.

**To start a call analytics job \(console\)**

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Call Analytics, choose **Call analytics jobs**\.

1. Choose **Create job**\.

1. On the **Specify job details** page, provide information about your call analytics job\.

1. Choose **Next**\.

1. For **Configure job**, turn on any optional features you want to specify\.

1. Choose **Create job**\.

## API<a name="start-call-analytics-api"></a>

The following shows the request parameters to start a call analytics job\. The calls that match all of the rules defined in a category are labeled with that category\.

**To start a call analytics job \(API\)**
+ For the [StartCallAnalyticsJob](API_StartCallAnalyticsJob.md) API, specify the following\.

  1. `CallAnalyticsJobName` – Specify a name unique to your AWS account\.

  1. `MediaFileUri` \(parameter of the `Media` object\) – Name of the media file you want to transcribe\.

  1. `DataAccessRoleArn` – the Amazon Resource Name \(ARN\) that provides access to the Amazon S3 location of your recordings\.

  The following is an example call analytics job request using the AWS SDK for Python \(Boto3\)\.

  ```
  #!/usr/bin/python
    
   from __future__ import print_function
   import time
   import boto3
   transcribe = boto3.client(service_name='transcribe')
   job_name = "your-call-analytics-job-name"
   job_uri = "Amazon-S3-object-URL-of-your-media-file"
   output_location = "Amazon-S3-URL-of-your-output"
   data_access_role = "arn:aws:iam::account-id:role/your-IAM-role"
   transcribe.start_call_analytics_job(
       CallAnalyticsJobName=job_name,
       Media={'MediaFileUri': job_uri},
       DataAccessRoleArn=data_access_role,
       OutputLocation=output_location,
       ChannelDefinitions=[{'ChannelId': 0, 'ParticipantRole': 'AGENT'},{'ChannelId': 1, 'ParticipantRole': 'CUSTOMER'}]
       )
   while True:
     status = transcribe.get_call_analytics_job(CallAnalyticsJobName=job_name)
     if status['CallAnalyticsJob']['CallAnalyticsJobStatus'] in ['COMPLETED', 'FAILED']:
       break
     print("Not ready yet...")
     time.sleep(5)
   print(status)
  ```

## AWS CLI<a name="start-call-analytics-cli"></a>

**To start a call analytics job \(AWS CLI\)**
+ Run the following code\.

  ```
                      
  aws transcribe start-call-analytics-job --cli-input-json file://example-start-command.json
  ```

  The following is the code of `example-start-command.json`\.

  ```
  {
        "CallAnalyticsJobName": "Example-Call-Analytics-Job",
        "OutputLocation": "s3://DOC-EXAMPLE-BUCKET1",
        "DataAccessRoleArn": "arn:aws:iam::accountId:role/your-IAM-role",
        "Media": {
            "MediaFileUri": "s3://DOC-EXAMPLE-BUCKET2"
        },
        "ChannelDefinitions": [
            {
                "ChannelId": 0,
                "ParticipantRole": "AGENT"
            },
            {
                "ChannelId": 1,
                "ParticipantRole": "CUSTOMER"
            }
        ]
  }
  ```