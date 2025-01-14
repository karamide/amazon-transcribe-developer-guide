# Step 3: Getting started using the console<a name="getting-started-console"></a>

The easiest way to get started with Amazon Transcribe is to submit a job using the console to transcribe an audio file\. If you haven't reviewed the concepts and terminology in [How Amazon Transcribe works](how-it-works.md), we recommend that you do that before proceeding\.

**Topics**
+ [Create a transcription job](#console-create-job)
+ [View a transcription job](#console-view-job)

## Create a transcription job<a name="console-create-job"></a>

Use the [Amazon Transcribe console](https://console.aws.amazon.com/transcribe/) to create a transcription job for your audio files\.

1. Provide the following information:
   + **Transcription job name**—A name for the job\. The name must be unique within your AWS account\.
   + **Amazon S3 input URL**—The Amazon S3 location of your input audio file\. The location must be in the same region as the endpoint that you are calling\. 
   + **Language**—Choose the language of your input file\.
   + **Format**—The format of the audio file\. For best results you should use a lossless format such as FLAC or WAV with PCM 16\-bit encoding\.
   + **Media sampling rate \(Hz\)**—Optional\. The bit sampling rate of the audio file\. Amazon Transcribe accepts sample rates between 8,000 Hz and 48,000 Hz\. For best results, you should use 8,000 Hz for low\-fidelity audio and 16,000 for high\-fidelity audio\.

   The following shows the **Create Transcription Job** filled out for a sample job\.  
![\[The Create Transcription Job form filled out for a sample job.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/gs-10.png)![\[The Create Transcription Job form filled out for a sample job.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

1. Choose **Create** to submit the job for processing\.

## View a transcription job<a name="console-view-job"></a>

Completed transcription jobs are displayed in a list that contains a brief description of the job\. The **Availability** column shows the remaining time that the job results are kept on the server\. Jobs are kept for 90 days and then deleted from the system\.

![\[A list of transcription jobs.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/gs-20.png)

Choose a job in the list to see information about the job\.

The information page about the transcription job has three sections\. The **Detail** section provides details about the transcription job, including the name, information about when the job is deleted from the server, and the input and output URLs\. Use the output URL to download the output from your transcription job\.

The **Output** section contains the transcription of the audio submitted to Amazon Transcribe\. You can download the transcription by choosing the **Download transcription** button\.

![\[The first two sections of the job description page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/gs-30.png)

The **Code samples** section contains the JSON input for the [ StartTranscriptionJob ](API_StartTranscriptionJob.md)API and the output from the [ GetTranscriptionJob ](API_GetTranscriptionJob.md) API\.

![\[The code samples section of the job description page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/images/gs-40.png)![\[The code samples section of the job description page.\]](http://docs.aws.amazon.com/transcribe/latest/dg/)

**Next step**  
[Step 4: Getting started using the API](getting-started-api.md)