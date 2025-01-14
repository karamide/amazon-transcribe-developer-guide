# ListTranscriptionJobs<a name="API_ListTranscriptionJobs"></a>

Lists transcription jobs with the specified status\.

## Request Syntax<a name="API_ListTranscriptionJobs_RequestSyntax"></a>

```
{
   "JobNameContains": "string",
   "MaxResults": number,
   "NextToken": "string",
   "Status": "string"
}
```

## Request Parameters<a name="API_ListTranscriptionJobs_RequestParameters"></a>

For information about the parameters that are common to all actions, see [Common Parameters](CommonParameters.md)\.

The request accepts the following data in JSON format\.

 ** [ JobNameContains ](#API_ListTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListTranscriptionJobs-request-JobNameContains"></a>
When specified, the jobs returned in the list are limited to jobs whose name contains the specified string\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Pattern: `^[0-9a-zA-Z._-]+`   
Required: No

 ** [ MaxResults ](#API_ListTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListTranscriptionJobs-request-MaxResults"></a>
The maximum number of jobs to return in each page of results\. If there are fewer results than the value you specify, only the actual results are returned\. If you do not specify a value, the default of 5 is used\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 100\.  
Required: No

 ** [ NextToken ](#API_ListTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListTranscriptionJobs-request-NextToken"></a>
If the result of the previous request to `ListTranscriptionJobs` is truncated, include the `NextToken` to fetch the next set of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+`   
Required: No

 ** [ Status ](#API_ListTranscriptionJobs_RequestSyntax) **   <a name="transcribe-ListTranscriptionJobs-request-Status"></a>
When specified, returns only transcription jobs with the specified status\. Jobs are ordered by creation date, with the newest jobs returned first\. If you don’t specify a status, Amazon Transcribe returns all transcription jobs ordered by creation date\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED`   
Required: No

## Response Syntax<a name="API_ListTranscriptionJobs_ResponseSyntax"></a>

```
{
   "NextToken": "string",
   "Status": "string",
   "TranscriptionJobSummaries": [ 
      { 
         "CompletionTime": number,
         "ContentRedaction": { 
            "RedactionOutput": "string",
            "RedactionType": "string"
         },
         "CreationTime": number,
         "FailureReason": "string",
         "IdentifiedLanguageScore": number,
         "IdentifyLanguage": boolean,
         "LanguageCode": "string",
         "ModelSettings": { 
            "LanguageModelName": "string"
         },
         "OutputLocationType": "string",
         "StartTime": number,
         "TranscriptionJobName": "string",
         "TranscriptionJobStatus": "string"
      }
   ]
}
```

## Response Elements<a name="API_ListTranscriptionJobs_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ NextToken ](#API_ListTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListTranscriptionJobs-response-NextToken"></a>
The `ListTranscriptionJobs` operation returns a page of jobs at a time\. The maximum size of the page is set by the `MaxResults` parameter\. If there are more jobs in the list than the page size, Amazon Transcribe returns the `NextPage` token\. Include the token in the next request to the `ListTranscriptionJobs` operation to return in the next page of jobs\.  
Type: String  
Length Constraints: Maximum length of 8192\.  
Pattern: `.+` 

 ** [ Status ](#API_ListTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListTranscriptionJobs-response-Status"></a>
The requested status of the jobs returned\.  
Type: String  
Valid Values:` QUEUED | IN_PROGRESS | FAILED | COMPLETED` 

 ** [ TranscriptionJobSummaries ](#API_ListTranscriptionJobs_ResponseSyntax) **   <a name="transcribe-ListTranscriptionJobs-response-TranscriptionJobSummaries"></a>
A list of objects containing summary information for a transcription job\.  
Type: Array of [ TranscriptionJobSummary ](API_TranscriptionJobSummary.md) objects

## Errors<a name="API_ListTranscriptionJobs_Errors"></a>

For information about the errors that are common to all actions, see [Common Errors](CommonErrors.md)\.

 ** BadRequestException **   
Your request didn't pass one or more validation tests\. For example, if the entity that you're trying to delete doesn't exist or if it is in a non\-terminal state \(for example, it's "in progress"\)\. See the exception `Message` field for more information\.  
HTTP Status Code: 400

 ** InternalFailureException **   
There was an internal error\. Check the error message and try your request again\.  
HTTP Status Code: 500

 ** LimitExceededException **   
Either you have sent too many requests or your input file is too long\. Wait before you resend your request, or use a smaller file and resend the request\.  
HTTP Status Code: 400

## See Also<a name="API_ListTranscriptionJobs_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListTranscriptionJobs) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/transcribe-2017-10-26/ListTranscriptionJobs) 