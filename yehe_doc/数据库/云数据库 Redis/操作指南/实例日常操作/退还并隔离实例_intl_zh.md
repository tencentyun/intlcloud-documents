## 操作场景

- 按量计费后付费实例，腾讯云账户未欠费时，如不再需要实例资源，而想退还实例时，可在控制台直接销毁实例，以免继续扣费。销毁的实例被隔离在回收站保留2小时，2小时之内，您可以开机恢复实例资源；2小时之后，系统将直接下线实例资源，所有数据将被销毁不可恢复。

## 使用须知

自助退还实例之后，实例的状态将变为已隔离或待删除时，不再产生与该实例相关的费用。
>!
> - 实例销毁后，所有数据将被清除且不可恢复，请务必确认完成数据备份后再提交销毁。
> - 实例销毁后 IP 资源同时释放。

## 销毁按量计费实例

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在右侧实例列表页面上方，选择地域。
3. 在实例列表中，选择需销毁的按量计费实例，在**操作**列，选择**更多** > **销毁**。 
![](https://qcloudimg.tencent-cloud.cn/raw/d58f890f17d7a7be5f63268235724493.png)
4. 在**销毁实例**对话框，确认预销毁实例的信息，了解销毁实例的影响，单击**销毁**。
5. 在左侧导航栏，选择**回收站**，可查看到销毁的按量计费实例被隔离在回收站中。实例状态为**已隔离**，将不再产生费用。
![](https://qcloudimg.tencent-cloud.cn/raw/66441a757e4107270e7489521e8fe401.png)
6.  （可选）单击**开机**，可恢复该实例；单击**立即下线**，将直接销毁实例资源。具体操作，请参见 [回收站](https://intl.cloud.tencent.com/document/product/239/46561)。

## 相关 API

| 接口名称                                                     | 接口功能         |
| ------------------------------------------------------------ | ---------------- |
| [DestroyPostpaidInstance](https://intl.cloud.tencent.com/document/product/239/32063) | 按量计费实例销毁 |

