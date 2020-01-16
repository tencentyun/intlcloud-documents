You can disassociate a function from an event source by deleting a trigger. After disassociation, the event source will no longer trigger the function.
A function trigger can be deleted in the console or through TCCLI.

## Deleting a Trigger in the Console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left.
2. In the "Service" column at the top, select a region to view all the functions in it.
4. The list page includes the function name, monitoring information, function runtime environment, creation time, and modification time.
5. Click the function to enter the details page. It includes the following tabs.
6. Open the "Triggers" tab, and click the **Delete** button for the trigger you want to delete.

## Deleting a Trigger Through TCCLI

Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).
Use the `tccli scf DeleteTrigger` command to delete a function trigger.
The sample below deletes a timer trigger using TCCLI:

```
$ tccli scf DeleteTrigger --FunctionName eventprint --TriggerName timer --Type timer
{
    "RequestId": "1341f09c-6909-421d-83ca-749ffd8546bb"
}

```

