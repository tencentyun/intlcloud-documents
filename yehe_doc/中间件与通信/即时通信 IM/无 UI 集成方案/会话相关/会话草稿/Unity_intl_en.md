## Feature Description
When sending a message, the user may want to switch to another chat window before finishing the message. The unfinished message can be saved through the `ConvSetDraft` API, so that the user can get back to it through the `conv_draft` field of the `ConvInfo` object and finish it.

>!
>1. A draft can contain only text.
>2. A draft will be stored only in the local database and not on the server. Therefore, it cannot be synced across devices and will not be available after the application is uninstalled and reinstalled.

## Setting a Conversation Draft
Call the `ConvSetDraft` API ([Details](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvSetDraft.html)) to set a conversation draft.

Sample code:


```c#
DraftParam draft_param = new DraftParam
{
  draft_msg = new Message
  {
    message_conv_id = "1234",
    message_conv_type = TIMConvType.kTIMConv_Group,
    message_elem_array = new List<Elem>{new Elem
    {
      elem_type = TIMElemType.kTIMElem_Text,
      text_elem_content = Input.text
    }},
  }
}
TIMResult res = TencentIMSDK.ConvSetDraft(conv_id, conv_type, draft_param);
```
