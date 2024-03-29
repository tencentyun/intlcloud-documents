批量恢复归档操作可以用于恢复清单中归档类型的对象。该操作支持自定义配置 POST Object restore 的相关参数，这些配置信息会影响到副本的恢复时间和过期时间。有关 POST Object restore 的更多介绍，请参见 [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633)。

恢复操作支持两种归档类型：归档存储类型和深度归档存储类型。关于这两种类型的更多介绍，请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)。

要创建批量恢复归档任务，需指定以下两个参数：

- 恢复模式：分别为标准取回模式和批量取回模式。有关恢复模式的更多信息，请参见 [恢复归档对象](https://intl.cloud.tencent.com/document/product/436/30961)。
- 副本有效期：归档类型的对象被恢复后，会产生一个临时副本，该副本会在指定时间后自动过期删除。有关副本有效期的更多信息，请参见 [恢复归档对象](https://intl.cloud.tencent.com/document/product/436/30961)。

## 注意事项

1. 如果批量恢复归档任务中包含了已完成恢复的对象副本，则开启批量恢复归档任务会更新这些对象的副本有效期，以保证任务中的所有的对象副本的有效期相同。
2. 批量恢复任务仅用于发起对象恢复请求。当所有请求发送完成后，批量处理页面将显示该任务进度为已完成。但对象存储（Cloud Object Storage，COS）不会通知您对象什么时候已恢复完成。您可以配置事件通知来接收通知。有关更多信息，请参见 [事件通知](https://intl.cloud.tencent.com/document/product/436/31648)。

