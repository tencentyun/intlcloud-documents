After creating and testing a function, you can put it into actual business for use. You can use the function by selecting an appropriate execution method or view its execution conditions through logs and monitoring information.

## Execution Methods

There are several ways to execute a function:

* Calling through TencentCloud API: This is to trigger the function through the Invoke API in TencentCloud API. In this way, you can customize the triggering event of the function and choose sync or async triggering. For details, see [Executing a Function](https://cloud.tencent.com/document/product/583/17243) in the API document.
* Configuring a trigger: You can configure a trigger so that the function can be triggered by an event in the specific connected resource. In this way, the function can be automatically triggered when an event occurs in the connected resource. For details, see [Trigger Description](https://cloud.tencent.com/document/product/583/9705).
* Calling through TCCLI: This is to execute the function using the "tccli scf Invoke" command in TCCLI. Just like with TencentCloud API, you can customize triggering events and choose sync or async triggering in this way. For details, see [Testing a Function](https://cloud.tencent.com/document/product/583/14572).

## Execution Logs and Monitoring

The execution log generated after the function is executed can be queried on the function log page in the console. It can be filtered by the execution result (success or failure) or by the request ID of the function.

The monitoring status of the function can be queried on the function monitoring information page in the console. Information about the number of calls, duration of one single call, and number of errors can be queried.
