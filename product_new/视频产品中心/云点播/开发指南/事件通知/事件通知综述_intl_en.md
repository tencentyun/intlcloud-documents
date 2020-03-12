An operation such as uploading, deleting, or video processing initiated on a video in VOD can be referred to as an event. The execution of an event takes a certain amount of time. Upon completion of the event, VOD will immediately notify the application service of the execution result, i.e., sending an event notification.

VOD supports the following types of event notifications:

<table>
    <tr>
        <th style="width:30%">
            Categorization
        </th>
        <th style="width:70%">
            Event Notification
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            Upload and deletion
        </td>
        <td>
				    <a href="https://intl.cloud.tencent.com/document/product/266/33950">Video upload completion</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33951">Video pull from URL completion</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33952">Video deletion completion</a>
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            Video processing
        </td>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33953">Task flow status change</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33954">Video editing completion</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33955">Publishing on WeChat completion</a>
        </td>
    </tr>
</table>

Event notification modes include "normal callback" and "reliable callback". You can log in to the [VOD Console](https://console.cloud.tencent.com/vod) to set the callback mode and select the events for which you want to receive callbacks. For details directions, please see [Callback Settings](https://intl.cloud.tencent.com/document/product/266/14055).

- Normal callback: configure a callback URL in the console. After an event is completed, the system will send an HTTP request to this URL, which contains the notification content.
- - Reliable callback: after an event is completed, the VOD system will put the notifications into a built-in message queue, and then the application service will consume the notifications in the queue through a server API.



## Normal Callback

Normal callback is a mode in which the application service passively receives event notifications. After the callback URL is configured and the normal callback mode is selected, VOD will initiate a callback to the callback URL after an event is completed.

A normal callback initiated by VOD is an HTTP request, where the request body is in JSON format and the content is the [`EventContent` structure]((https://intl.cloud.tencent.com/document/product/266/34187#EventContent)) excluding the `EventHandle` parameter.
Take [task status change notification](https://intl.cloud.tencent.com/document/product/266/33953) as an example. The `EventType` parameter in the callback is `ProcedureStateChanged`, and the information is represented by the `ProcedureStateChangeEvent` parameter ([`ProcedureTask`](https://intl.cloud.tencent.com/document/product/266/34187#ProcedureTask) structure).

## Reliable Callback
Reliable callback is a mode in which the application service actively pulls event notifications to VOD. After the reliable callback mode is selected, the VOD system will put event notifications into a queue, and the application service will consume the notifications in the queue through a server API.
After the application service gets a message through the [PullEvents](https://intl.cloud.tencent.com/document/product/266/34187) API, the [ConfirmEvents]https://intl.cloud.tencent.com/document/product/266/34184 API needs to be called for confirmation. The message must be confirmed for receipt before it can be removed from the queue in VOD, so the reliability of "reliable callback" is higher than that of "normal callback". **If the requirement for event notification reliability is high, you are recommended to use the "reliable callback" mode.**
