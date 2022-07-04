ASR supports authorization by tag.
- Authorization by tag: You can tag resources and grant sub-accounts permissions to manage resources with particular tags.


## List of APIs Supporting API-Level Authorization
For API operations that support operation-level permission control, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

| API | Description |
|---------|---------|
| CreateAsrUser | Activates the ASR service |
| DescribeResource | Queries resource package |
| DescribeStatistics | Queries statistics |
| DescribeUserStatus | Queries ASR service activation status |
| RealtimeRecognition | Performs real-time recognition |
| StartStreamTranscription | Performs global speech recognition |
