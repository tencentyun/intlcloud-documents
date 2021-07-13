SCF is a typical event-triggered serverless runtime environment. Its core components are SCF functions and event sources, where an event source is a Tencent Cloud service or user-defined code that publishes an event, an SCF function is the handler of the event, and a function trigger is a set of correspondences between functions and event sources. For example, in the following scenarios:

* **Image/video processing**: the application crops the images uploaded by users into an appropriate size, stores the images in COS, creates thumbnails of each image, and displays them on the user page. In this scenario, you need to select COS as the event source and publish the event to the SCF function when the file is created. The event data provides all the information about the bucket and the file.
* **Data processing**: the data collected during the day (such as clickstreams) is analyzed with a report generated at 00:00. In this scenario, you need to select a timer as the event source to publish an event to the SCF function at a specific time.
* **Custom application**: the first image is invoked in your application to handle the SCF function as a module of the application. In this scenario, you need to call the `Invoke` API in the application to publish an event.

These event sources can be any of the following:

* **Internal event sources**: these are pre-configured Tencent Cloud services that can be used with SCF. If you configure one of these event sources as a function trigger, the function will be invoked automatically when an event occurs. The relationship between the event source and the function (i.e., event source mapping) will be maintained on the event source side. 
* **Custom applications**: you can let custom applications publish events and invoke SCF functions.

## Sample 1. COS publishes an event and invokes a function

You can configure the event source mapping for COS to determine what behaviors of COS will trigger an SCF function (such as object PUT or DELETE). The COS event source mapping is stored in COS and uses the bucket notification feature to direct COS to invoke the function when an event of a particular type occurs:

- A COS trigger is created.
- The user creates/deletes an object in the bucket.
- COS detects an object creation/deletion event.
- COS automatically invokes a function. It will be determined which function should be invoked based on the event source mapping stored in the COS configuration. The bucket and object information will be passed to the function as event data.

## Sample 2. A timer publishes a time and invokes a function
The event source mapping of the timer is saved in the SCF function configuration to determine when the function should be automatically triggered:

- A timer trigger is created.
- The timer automatically invokes the function at the configured time.

## Sample 3. A custom application invokes a function
If you need to invoke an SCF function in a custom application, you do not need to configure a function trigger or set up an event source mapping in this case; instead, you can use the `Invoke` API as the event source.

- The custom application uses the `Invoke` API to invoke the function and pass in the event data.
- The function receives the triggering request and is executed.
- If sync invocation is used, the function will return the result to the application.

In this example, since the custom application and the function are produced by the same user, the user credentials (`APPID`, `SecretId`, and `SecretKey`) can be specified.

## Notes
- The current trigger-related restrictions for a single function can be viewed in [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).
2. There are specific restrictions on event source mappings due to the limitations of different Tencent Cloud services. For example, for a COS trigger, the same event (such as file upload) in the same COS bucket cannot trigger multiple different functions.
