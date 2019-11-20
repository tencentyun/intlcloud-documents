
打开[控制台](https://console.cloud.tencent.com/autoscaling)，选择导航条中的【伸缩组】。

选择要修改的伸缩组，单击伸缩组ID进入伸缩组基本信息页面。
![](https://mc.qcloudimg.com/static/img/06a1ca079f41a7cd825b47c68304f6f5/1.jpg)

在该页面中可查看该伸缩组所绑定的云主机列表。
- 如需手动添加CVM实例到伸缩组，单击【添加云主机】，选择要添加的实例（按住Shift可多选），然后单击【确定】；
- 如需解绑某个云主机，在相应的云主机条目后单击【移出】。
![](https://mc.qcloudimg.com/static/img/32296300304a228286b919c41ab30613/2.jpg)

对自动生产的机器，移出后会销毁。
对手动加入的机器，移出后不会销毁，只会从伸缩组中移出，以及解绑负载均衡。
