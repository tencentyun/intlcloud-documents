StreamLive提供冗余链路自动切换的能力，以实现更可靠的直播输入源，具体配置配置如下：

1. 创建一个频道进入基础信息编辑，若已有频道，可直接选择编辑即可。
![](https://qcloudimg.tencent-cloud.cn/raw/2299ba64984e13565781af9235aeb430.png)

2. 在**Input Setting**中绑定**Input**，容灾配置（Failover）只能在**Input Type**相同的Input上进行。
![](https://qcloudimg.tencent-cloud.cn/raw/d05b8b563e4a124e0fbd09514c9ae290.png)

3. 选择需要开启容灾切换的**Input**，并点击**Setting**按钮，进入设置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/9bec3699f616ac1ee76472728a46b557.png)

4. 此时，可开启**Input Failover**选项进入自动切换选项设置。
![](https://qcloudimg.tencent-cloud.cn/raw/2b28b7c0495c2718358b2f7823603b9a.png)
如上图所示  选择备份输入（**Backup Input**），该Input必须是已经绑定到该Channel下。然后设置故障切换时间的阈值，即主源无输入后多久会自动切换到备份输入，单位是毫秒，建议值是3000，故障转移时间越短，切换更加迅速，但是太短也会非常灵敏，容易在短时间丢包情况下频繁切换，这里客户需要根据业务特性自行把握。最后选择当主源故障恢复后的表现，**CURRENT_PREFERRED**表示当前输入优先，即主源恢复后不需要再次切换回去，保持现有输入即可。**PRIMARY_PREFERRED**表示主输入源优先，即主源恢复后，需要从当前输入源立即切换到主源，若当前输入源已经是主源则不需要有切换动作。

5. 点击**Confirm**按钮后，回到**Input列表**页面，可以看到Input属性有所变化，会显示该Input是主源还是备源。
![](https://qcloudimg.tencent-cloud.cn/raw/a9b76c8ce82c4cea993e8edf858aa646.png)
此时已完成Input的故障切换配置，继续完成Output配置即可，Output配置见Channel管理中的设置输出组。

