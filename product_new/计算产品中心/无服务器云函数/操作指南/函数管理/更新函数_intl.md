A function can be updated in the console or through TCCLI. Function update is divided into function configuration update and function code update.
## Function Configuration Update
### Updating Function Configuration in the Console
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select Functions on the left.
2. Select the region for which to update functions at the top of the main interface. Click the function you want to update in the list page and enter the function details page.
3. Switch to the function configuration tab and click **Edit** at the upper right corner to enter the editing mode.
4. Modify the description, memory, timeout, environment variable, and network configuration of the function as needed.
5. After the modification is completed, click **Save** to save the modified configuration. If you want to cancel, click **Cancel** to discard the changes.

### Updating Function Configuration Through TCCLI
The function configuration can be updated using the `tccli scf UpdateFunctionConfigration` command, where `FunctionName` is a required parameter indicating the name of the function you want to modify.
```
$ tccli scf UpdateFunctionConfiguration --FunctionName testcli --Timeout 30
{
    "RequestId": "153496c8-0cd2-40ef-a435-9d67ee6e4387"
}
```

## Function Code Update
### Updating Function Code in the Console
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Functions** on the left.
2. Select the region for which to update functions at the top of the main interface. Click the function you want to update in the list page and enter the function details page.
3. Switch to the function code tab. For scripting languages, you can see the function code editor. For non-scripting languages, you can only see the entry for code upload.
4. You can directly edit the entry function in the code editor. You can also switch to code upload mode to submit the function by uploading a zip package locally or through COS.
5. After the modification is completed, click **Save** to save or submit the new code. If you want to cancel, click **Cancel** to discard the changes.

### Updating Function Code Through TCCLI
The function code can be updated using the `tccli scf UpdateFunctionCode` command, where `FunctionName` is a required parameter indicating the name of the function you want to modify. The `Handler` parameter can be used to update the function execution method.
```
$ tccli scf UpdateFunctionCode --FunctionName testclifunc --CosBucketName gzcode --CosObjectName "/hello.zip" --Handler index.main
{
    "RequestId": "2a15e5bc-e6ec-409f-ba8c-8524e642e528"
}
```
