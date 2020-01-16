A function can be deleted in the console or through TCCLI.
## Viewing a Function in the Console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select Functions on the left.
2. Select the region for which to view functions at the top of the main interface. In the function list, you can view all the functions in the specified region.
3. In the list page, click the **Delete** button to the right of the function you want to delete in the action column and then click **OK** to delete the function.


## Deleting a Function Through TCCLI
Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://intl.cloud.tencent.com/document/product/1013/33463).

The function list can be obtained using the `tccli scf DeleteFunctions` command, where `FunctionName` is a required parameter indicating the name of the function you want to delete.
```
$ tccli scf DeleteFunction --FunctionName printtest
{
    "RequestId": "753e4273-a626-4c5d-b1b2-37b8b9db766e"
}
```
