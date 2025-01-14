# Step 5: Viewing and updating your custom language models<a name="view-update-lang"></a>

The speech recognition capabilities of Amazon Transcribe are constantly improving\. Specifically, Amazon Transcribe continually updates the base models used in custom language models\.

To see if you're running the latest base model in your custom language model:

1. Use the [ DescribeLanguageModel ](API_DescribeLanguageModel.md) API and check the `UpgradeAvailability` field\.

1. If `UpgradeAvailability` is `true`, you're not running the latest version of the base model in your custom language model\.

To use the latest base model in a custom language model, you must create a new custom language model\. That custom language model will have the updated base model\.