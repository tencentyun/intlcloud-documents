

If you use a [TencentCloud API](https://intl.cloud.tencent.com/document/product/583/17235) to manage a function (i.e., CRUD operations), as the API is async, you need to query its current status first.

## Function Status

When you create, update, delete, or publish a function, it will be in one of the following statuses:

| Status Value (Returned by API) | Description                                                 |
| --------------------------- | ---------------------------------------------------- |
| Creating                    | The function is being created                                           |
| CreateFailed                | The function failed to be created (if the function information has been generated, you can delete it and create the function again) |
| Active                      | The function is available                                             |
| Updating                    | The function is being updated                                           |
| UpdateFailed                | The function failed to be updated                                         |
| Publishing                  | The function version is being published                                        |
| PublishFailed               | The function version failed to be published                                     |
| Deleting                    | The function is being deleted                                           |
| DeleteFailed                | The function failed to be deleted                                         |



>! If a function failed to be published or updated, its versions that have already been published normally will not be affected, and when it is invocated, its content before the update will be invocated normally.

The change process of the function creation and update statuses is as shown below:
![](https://main.qcloudimg.com/raw/a49f5ac2e5c0340c87e6cd3aaa17ffe7.png)



The change process of the function version release statuses is as shown below:
![](https://main.qcloudimg.com/raw/e4ee43d6c507a14b7bd5b2247af83bed.png)



## Function Billing Status

| AvailableStatus Value (Returned by API) | Description                 |
| -------------------------------------------- | -------------------- |
| Available                                    | The function is available             |
| InsufficientBalance                          | The function is unavailable due to overdue payment |



## Layer Status

| Status Value (Returned by API) | Description                                                 |
| --------------------------- | ---------- |
| Publishing                  | The layer is being published   |
| PublishFailed               | The layer failed to be published |
| Active                      | The layer is available     |
| Deleting                    | The layer is being deleted   |
| DeleteFailed                | The layer failed to be deleted |
| Deleted                     | The layer has been deleted   |

