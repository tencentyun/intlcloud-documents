## UE Application Operations in the Cloud
### Why is the cloud window resolution different from the expected resolution?
This may be because the support for a high DPI isn't added during UE4 application packaging.

### Why doesn't the cloud application respond after the user clicks a screen interaction button?
If the UE application hides the cursor by default, the cursor will actually be locked at the center of the Windows image. In this case, CAR cannot convert a click event on the mobile device to a cloud click event with the corresponding coordinates. You need to make sure that the mouse position is changeable at any time, so that users can directly click in the cloud environment.

### Why does a notification of an early graphics card driver version pop up when the user starts a UE5 application?
Currently, because M and S concurrency packs only support early driver versions, this notification will pop up. We recommend you use L concurrency packs for your business.

## Unity Application Operations in the Cloud
### The user presses and holds the left mouse button and drags the mouse to rotate the image angle on the local device, but why doesn't this operation take effect in the cloud?
This is generally because the cloud application doesn't hide the cursor when the user presses and holds the mouse to drag it.

## Input Peripheral Device
### Which peripheral device messages can be obtained by a cloud application?
Currently, a cloud application can get mouse, keyboard, and controller messages, and the business frontend can send mouse, keyboard, and controller messages to the cloud through a touchscreen or other input. For the specific implementation process, see the API documentation of the SDK for each client type:
- [SDK for JavaScript APIs](https://intl.cloud.tencent.com/document/product/1158/49627)
- [SDK for Android APIs](https://intl.cloud.tencent.com/document/product/1158/49628)
- [SDK for iOS APIs](https://intl.cloud.tencent.com/document/product/1158/49629)

## Process
### Why does CAR start multiple processes?
Check whether processes in the process list are complete, and if yes, check whether the application starts multiple processes on its own.
