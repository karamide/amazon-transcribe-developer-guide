# Using a text file to create a medical custom vocabulary<a name="create-med-custom-vocabulary"></a>

To create a custom vocabulary, you must have prepared a text file that contains a collection a words or phrases\. Amazon Transcribe Medical uses this text file to create a custom vocabulary that you can use to improve the transcription accuracy of those words or phrases\. You can create a custom vocabulary using the [ CreateMedicalVocabulary ](API_CreateMedicalVocabulary.md) API or the Amazon Transcribe Medical console\.

## Console<a name="create-med-custom-vocab-console"></a>

**To create a custom vocabulary \(console\)**

To use the console to create a custom vocabulary, you provide the Amazon S3 URI of the text file containing your words or phrases\.

1. Sign in to AWS Management Console and open the Amazon Transcribe Medical console at [Amazon Transcribe Medical console](https://console.aws.amazon.com/transcribe/)\.

1. In the navigation pane, under Amazon Transcribe Medical, choose **Custom vocabulary**\.

1. For **Name**, under **Vocabulary settings**, choose a name for your custom vocabulary\.

1. Specify the location of your audio file or video file in Amazon S3:
   + For **Vocabulary input file location on S3** under **Vocabulary settings**, specify the Amazon S3 URI that identifies the text file you will use to create your custom vocabulary\.
   + For **Vocabulary input file location in Amazon S3**, choose **Browse S3** to browse for the text file and choose it\.

1. Choose **Create vocabulary**\.

You can see the processing status of your custom vocabulary in the console\.

## API<a name="create-med-custom-vocab-api"></a>

**To create a medical custom vocabulary \(API\)**
+ For the [ StartTranscriptionJob ](API_StartTranscriptionJob.md) API, specify the following\.

  1. For `LanguageCode`, specify `en-US`\.

  1. For `VocabularyFileUri`, specify the Amazon S3 location of the text file that you use to define your custom vocabulary\.

  1. For `VocabularyName`, specify a name for your custom vocabulary\. The name you specify must be unique within your AWS account\.

To see the processing status of your custom vocabulary, use the [ GetMedicalVocabulary ](API_GetMedicalVocabulary.md) API\.

The following is an example request using the AWS SDK for Python \(Boto3\) to create a custom vocabulary\.

```
from __future__ import print_function
import time
import boto3
  
transcribe = boto3.client('transcribe')
vocab_name = "example-med-custom-vocab"
text_file_uri = "https://DOC-EXAMPLE-BUCKET1.s3-Region.amazonaws.com/example_custom_vocabulary.txt"
transcribe.create_medical_vocabulary(
    VocabularyName = vocab_name,
    VocabularyFileUri = text_file_uri,
    LanguageCode = 'en-US',
  )
  
while True:
    status = transcribe.get_medical_vocabulary(VocabularyName=vocab_name)
    if status['VocabularyState'] in ['READY', 'FAILED']:
        break
    print("Not ready yet...")
    time.sleep(5)
print(status)
```

## AWS CLI<a name="create-med-custom-vocab-cli"></a>

**To identify the speakers in an audio file using a batch transcription job \(AWS CLI\)**
+ Run the following code\.

  ```
  aws transcribe create-medical-vocabulary \
      --vocabulary-name your-custom-medical-vocabulary-name \
      --language-code en-US \
      --vocabulary-file-uri https://DOC-EXAMPLE-BUCKET1.AWS-Region.amazonaws.com/your-medical-custom-vocabulary
  ```

  The following is the response from running the preceding CLI command\.

  ```
  {
      "VocabularyName": "cli-medical-vocab-1",
      "LanguageCode": "en-US",
      "VocabularyState": "PENDING"
  }
  ```