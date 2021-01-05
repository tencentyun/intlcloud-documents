1. 登录弹性伸缩控制台，选择左侧导航中的【[伸缩组](https://console.cloud.tencent.com/autoscaling/group?rid=1)】。
2. 选择需修改的伸缩组，单击伸缩组 ID 进入该伸缩组基本信息页面。如下图所示：
![](https://main.qcloudimg.com/raw/6c9d3876e1d343ae8ddd6fc2ad912112.png)
3. 在伸缩组详情页面，选择【关联实例】页签，可查看该伸缩组所关联的实例列表。如下图所示：
![](https://main.qcloudimg.com/raw/2c4c7f20ccfbb5b72588aaaf3d61a7ba.png)
 - 如需手动添加 CVM 实例到伸缩组，选择【添加实例】并在弹出窗口中进行选择（按住 Shift 可多选），并单击【确定】。
 - 如需解绑某个实例，单击实例所在行右侧的【移出】。
>?
>-  自动生产的机器，移出后会销毁。
> - 手动加入的机器，移出后不会销毁，只会从伸缩组中移出，以及解绑负载均衡。
