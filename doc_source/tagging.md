# Tagging resources<a name="tagging"></a>

A *tag* is a custom metadata label that you can add to a resource in order to make it easier to identify, organize, and find in a search\. Tags are comprised of two individual parts: A tag key and a tag value\. This is referred to as a key:value pair\.

A *tag key* typically represents a larger category, while a *tag value* represents a subset of that category\. For example you could have *tag key=Color* and *tag value=Blue*, which would produce the key:value pair `Color:Blue`\. Note that you can set the value of a tag to an empty string, but you can't set the value of a tag to null\. Omitting the tag value is the same as using an empty string\.

**Tip**  
AWS Billing can use tags to separate your bills into dynamic categories\. For example, if you add tags to represent different departments within your company, such as `Department:Sales` or `Department:Legal`, AWS can provide you with your cost distribution per department\.

In Amazon Transcribe, you can tag the following resources: 
+ Transcription job
+ Medical transcription job
+ Vocabulary
+ Medical vocabulary
+ Vocabulary filter
+ Custom language model

Tag keys can be up to 128 characters in length and tag values can be up to 256 characters in length; both are case sensitive\. For more information, see [ TagResource ](API_TagResource.md) in the Amazon Transcribe [API Reference](API_Reference.md)\.

Amazon Transcribe supports up to 50 tags per resource\. For a given resource, each tag key must be unique with only one value\.

**Note**  
Your tags cannot begin with `aws:` because AWS reserves this prefix for system\-generated tags\. You cannot add, modify, or delete `aws:*` tags, and they don't count against your tags\-per\-resource limit\.

To learn more about tagging, including best practices, see [Tagging AWS resources](https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html)\.

## Tag\-based access control<a name="tagging-access-control"></a>

You can use tags to control access within your AWS accounts\. For tag\-based access control, you provide tag information in the condition element of an IAM policy\. You can then use tags and their associated tag condition key to control access to:
+ **Resources:** Control access to your Amazon Transcribe resources based on the tags you've assigned to those resources\.
  + Use the `aws:ResourceTag/key-name` condition key to specify which tag key:value pair must be attached to the resource\.
+ **Requests:** Control which tags can be passed in a request\.
  + Use the `aws:RequestTag/key-name` condition key to specify which tags can be added, modified, or removed from an IAM user or role\.
+ **Authorization processes:** Control tag\-based access for any part of your authorization process\.
  +  Use the `aws:TagKeys/` condition key to control whether specific tag keys can be used on a resource, in a request, or by a principal\. In this case, the key value doesn't matter\.

For more detailed information on tag\-based access control, see [Controlling access to AWS resources using tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html)\. 

## Tagging your Amazon Transcribe resources<a name="tagging-how-to"></a>

You can add tags before or after you run your Amazon Transcribe job\. The existing **Create\*** and **Start\*** APIs allow you to add tags with your transcription job\.

You can add, modify or delete tags using the **Amazon Transcribe Console**, **AWS CLI**, or **AWS SDK**; see below for instructions:

### Console<a name="tagging-howto-console"></a>

1. Sign in to the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, choose **Transcription jobs**, then select the **Create job** button \(top right\)\. This opens the **Specify job details** page\.

1. Scroll to the bottom of the **Specify job details** page to find the **Tags \- *optional*** box and click the **Add new tag** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/add-new-tag.png)

1. Enter information for the **Key** field and, optionally, the **Value** field\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/add-new-tag-color.png)

1. Fill in any other fields you wish to include on the **Specify job details** page, then click the **Next** button\. This takes you to the **Configure job \- *optional* page\.**

   Click the **Create job** button to run your transcription job\. 

1. You can view the tags associated with a transcription job by navigating to the **Transcription jobs** page, selecting a transcription job, and scrolling to the bottom of that job's information page\. If you wish to edit your tags, you can do so by clicking the **Manage tags** button\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/view-tags.png)

### AWS SDK for Python \(Boto3\)<a name="tagging-howto-sdk"></a>

The following example uses the AWS SDK for Python \(Boto3\) to add a tag by using the `Tags` argument for the [start\_transcription\_job](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/transcribe.html#TranscribeService.Client.start_transcription_job) method:

```
from __future__ import print_function
import time
import boto3
transcribe = boto3.client('transcribe')
job_name = "your-job-name"
job_uri = "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
transcribe.start_transcription_job(
    TranscriptionJobName=job_name,
    Media={'MediaFileUri': job_uri},
    MediaFormat='wav',
    LanguageCode='en-US', 
    Tags=[{'Key':'string', 'Value':'string'}]
)
while True:
    status = transcribe.get_transcription_job(TranscriptionJobName=job_name)
    if status['TranscriptionJob']['TranscriptionJobStatus'] in ['COMPLETED', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

### AWS CLI<a name="tagging-howto-cli"></a>

This example uses the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command and `Tags` parameter\.

```
aws transcribe start-transcription-job \
--transcription-job-name your-job-name
--media MediaFileUri=s3://your-S3-bucket/S3-prefix/your-filename.file-extension \
--language-code en-US \
--tags Key=color,Value=blue
```

Here's another example using the [start\-transcription\-job](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/transcribe/start-transcription-job.html) command, and a request body that adds tags to that job\.

```
aws transcribe start-transcription-job \
--cli-input-json file://filepath/example-start-command.json
```

The file *example\-start\-command\.json* contains the following request body\.

```
{
  "TranscriptionJobName": "your-job-name",
  "LanguageCode": "en-US",
  "Media": {
        "MediaFileUri": "s3://your-S3-bucket/S3-prefix/your-filename.file-extension"
    },
  "Tags": [ {"Key": "string","Value": "string"} ]
}
```