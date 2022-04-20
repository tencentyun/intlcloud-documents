ASR supports two authorization methods:
- Resource-Level authorization: you can use policy syntax to grant sub-accounts permissions to manage individual resources.
- Authorization by tag: you can tag resources and grant sub-accounts permissions to manage resources with particular tags.

## List of APIs Supporting Resource-Level Authorization
ASR supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include (in ascending order):

| API | Description | Resource Type | Six-Segment Example of Resource |
|---------|---------|---------|---------|
| DeleteAsrVocab | Deletes keyword list | Keyword list | `qcs::asr::uin/$account:vocab/$VocabId` |
| DeleteCustomization | Deletes self adaptive learning model | Self adaptive learning model | `qcs::asr::uin/$account:model/$ModelId` |
| DeleteModelsByAppid | Deletes self adaptive learning model by `AppId` | Self adaptive learning model | `qcs::asr::uin/$account:model/$ModelId` |
| DownloadAsrVocab | Downloads keyword list | Keyword list | `qcs::asr::uin/$account:vocab/$VocabId` |
| DownloadCustomization | Downloads self adaptive learning model corpus | Self adaptive learning model | `qcs::asr::uin/$account:model/$ModelId` |
| GetAsrVocab | Gets keyword list | Keyword list | `qcs::asr::uin/$account:vocab/$VocabId` |
| GetAsrVocabList | Gets the list of keyword lists | Keyword list | `qcs::asr::uin/$account:vocab/*` |
| GetCustomizationList | Gets the list of self adaptive learning models | Self adaptive learning model | `qcs::asr::uin/$account:model/*` |
| ModifyCustomization | Modifies self adaptive learning model | Self adaptive learning model | `qcs::asr::uin/$account:model/$ModelId` |
| ModifyCustomizationState | Modifies self adaptive learning model status | Self adaptive learning model | `qcs::asr::uin/$account:model/$ModelId` |
| SetVocabState | Sets keyword list status | Keyword list | `qcs::asr::uin/$account:vocab/$VocabId` |
| UpdateAsrVocab | Updates keyword list | Keyword list | `qcs::asr::uin/$account:vocab/$VocabId` |


## List of APIs Supporting API-Level Authorization
For API operations that support operation-level permission control, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

| API | Description |
|---------|---------|
| CreateAsrUser | Activates the ASR service |
| CreateAsrVocab | Creates keyword list |
| CreateCustomization | Creates self adaptive learning model |
| CreateRecTask | Performs recording file recognition |
| DescribeResource | Queries resource package |
| DescribeStatistics | Queries statistics |
| DescribeTaskStatus | Queries recording file recognition task status |
| DescribeUserStatus | Queries ASR service activation status |
| RealtimeRecognition | Performs real-time recognition |
| SentenceRecognition | Performs one-sentence recognition |
| StartStreamTranscription | Performs global speech recognition |
