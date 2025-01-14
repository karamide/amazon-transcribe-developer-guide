# Monitoring Amazon Transcribe API calls with AWS CloudTrail<a name="monitoring-transcribe-cloud-trail"></a>

Amazon Transcribe is integrated with AWS CloudTrail, a service that provides a record of actions taken in Amazon Transcribe by an AWS Identity and Access Management \(IAM\) user or role, or by an AWS service\. CloudTrail captures all API calls for Amazon Transcribe, including calls from the Amazon Transcribe console and from code calls to the Amazon Transcribe APIs, as events\. By creating a trail, you can enable continuous delivery of CloudTrail events, including events for Amazon Transcribe, to an Amazon Simple Storage Service \(Amazon S3\) bucket\. If you don't create a trail, you can still view the most recent events in the CloudTrail console in **Event history**\. Using the information collected by CloudTrail, you can see each request that was made to Amazon Transcribe, the IP address from which the request was made, who made the request, when it was made, and additional details\. 

To learn more about CloudTrail, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## Amazon Transcribe information in CloudTrail<a name="transcribe-info-in-cloudtrail"></a>

CloudTrail is enabled on your AWS account when you create the account\. When activity occurs in Amazon Transcribe, that activity is recorded in a CloudTrail event along with other AWS service events in the CloudTrail **Event history**\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing Events with CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\. 

For an ongoing record of events in your AWS account, including events for Amazon Transcribe, create a trail\. A *trail* is a configuration that enables CloudTrail to deliver events as log files to a specified S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all Regions in the AWS partition and delivers the log files to the S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs\. For more information, see: 
+ [Overview for Creating a Trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [CloudTrail Supported Services and Integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html#cloudtrail-aws-service-specific-topics-integrations)
+ [Configuring Amazon SNS Notifications for CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)
+ [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

CloudTrail logs all Amazon Transcribe actions, which are documented in the [API Reference](API_Reference.md)\. For example, calls to the [ CreateVocabulary ](API_CreateVocabulary.md), [ GetTranscriptionJob ](API_GetTranscriptionJob.md), and [ StartTranscriptionJob ](API_StartTranscriptionJob.md) APIs generate entries in the CloudTrail log files\.

Every event or log entry contains information about who generated the request\. This information helps you determine the following: 
+ Whether the request was made with root or IAM user credentials
+ Whether the request was made with temporary security credentials for an IAM role or federated user
+ Whether the request was made by another AWS service

For more information, see the [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

## <a name="aws-transcribe-info-in-cloudtrail"></a>

You can also aggregate Amazon Transcribe log files from multiple AWS Regions and multiple AWS accounts into a single S3 bucket\. For more information, see [Receiving CloudTrail Log Files from Multiple Regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\. 

### Example: Amazon Transcribe log file entries<a name="cloud-trail-log-entry"></a>

A *trail* is a configuration that enables delivery of events as log files to a specified S3 bucket\. CloudTrail log files contain one or more log entries\. An *event* represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. CloudTrail log files aren't an ordered stack trace of the public API calls, so they don't appear in any specific order\. 

Calls to the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) and [ GetTranscriptionJob ](API_GetTranscriptionJob.md) APIs create the following entry\.

```
{
    "Records": [
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "AssumedRole | FederatedUser | IAMUser | Root | SAMLUser | WebIdentityUser",
                "principalId": "principal ID",
                "arn": "ARN",
                "accountId": "account ID",
                "accessKeyId": "access key",
                "userName": "user name"
            },
            "eventTime": "timestamp",
            "eventSource": "transcribe.amazonaws.com",
            "eventName": "StartTranscriptionJob",
            "awsRegion": "region",
            "sourceIPAddress": "source IP address",
            "userAgent": "user agent",
            "requestParameters": {
                "mediaFormat": "flac | mp3 | mp4 | wav",
                "languageCode": "en-US | es-US",
                "transcriptionJobName": "unique job name",
                "media": {
                    "mediaFileUri": ""
                }
            },
            "responseElements": {
                "transcriptionJob": {
                    "transcriptionJobStatus": "IN_PROGRESS",
                    "mediaFormat": "flac | mp3 | mp4 | wav",
                    "creationTime": "timestamp",
                    "transcriptionJobName": "unique job name",
                    "languageCode": "en-US | es-US",
                    "media": {
                        "mediaFileUri": ""
                    }
                }
            },
            "requestID": "request ID",
            "eventID": "event ID",
            "eventType": "AwsApiCall",
            "recipientAccountId": "account id"
        },
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "AssumedRole | FederatedUser | IAMUser | Root | SAMLUser | WebIdentityUser",
                "principalId": "principal ID",
                "arn": "ARN",
                "accountId": "account ID",
                "accessKeyId": "access key",
                "userName": "user name"
            },
            "eventTime": "timestamp",
            "eventSource": "transcribe.amazonaws.com",
            "eventName": "GetTranscriptionJob",
            "awsRegion": "region",
            "sourceIPAddress": "source IP address",
            "userAgent": "user agent",
            "requestParameters": {
                "transcriptionJobName": "unique job name"
            },
            "responseElements": {
                "transcriptionJob": {
                    "settings": {
                        
                    },
                    "transcriptionJobStatus": "COMPLETED | FAILED | IN_PROGRESS",
                    "mediaFormat": "flac | mp3 | mp4 | wav",
                    "creationTime": "timestamp",
                    "transcriptionJobName": "unique job name",
                    "languageCode": "en-US | es-US",
                    "media": {
                        "mediaFileUri": ""
                    },
                    "transcript": {
                        "transcriptFileUri": ""
                    }
                }
            },
            "requestID": "request ID",
            "eventID": "event ID",
            "eventType": "AwsApiCall",
            "recipientAccountId": "account id"
        }        
    ]
}
```