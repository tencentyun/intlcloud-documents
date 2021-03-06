为方便用户更加细粒度的配置域名查询、管理权限，CDN 权限策略已全面完成升级，用户可通过自定义策略语句，实现域名级别的权限分配。	

>?因 CDN2.0 接口已不再更新维护，不建议用户使用【按产品功能或项目权限创建】新建策略，建议用户使用功能更全，操作更便捷的【按策略生成器创建】或【按标签授权】。

1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview) ，单击【策略】菜单，即可进入策略管理页面，单击【新建自定义策略】：
![img](https://main.qcloudimg.com/raw/b986334f0d3acde5eb9526fe01d669bb.png)

2. 选择【按策略生成器创建】：
![img](https://main.qcloudimg.com/raw/55a2e3b5b0011b2a8e520df6fc37ff57.png)

3. 在产品选框中选择【内容分发网络】，并选择需要授权的功能集合，若授权全读写权限，可勾选【全部操作】，功能与控制台映射关系可查看 [Action 映射表](https://intl.cloud.tencent.com/document/product/228/35229)。
![img](https://main.qcloudimg.com/raw/43b88d53d2beb2b2c167a4a732dc6ded.png)

4. 在资源处填写需要授权的域名，完成填写后，单击【确定】并单击【下一步】，即可创建策略。将创建好的策略关联已有用户/用户组，即可进行授权。
	- 所有域名：在资源处勾选【全部资源】，单击【确定】。
	![img](https://main.qcloudimg.com/raw/9ddd4b97828faeadd0063d0ede3283a0.png)
	- 单/多域名：勾选【特定资源】，单击【添加资源六段式】。
	![img](https://main.qcloudimg.com/raw/05dd24c7e96e3ae6cd6aa2b9ee64641d.png)
	在右边弹窗的【资源】处填写对应的单个域名后，单击【确定】即可。如需要加入多个域名，可单击【添加资源六段式】多次添加。
	![img](https://main.qcloudimg.com/raw/68715dd7708d3b79aac0d64ae713ae85.png)

5. 完成上述操作后，单击【下一步】，选择需要授权的子账号用户，单击【完成】即可。
![img](https://main.qcloudimg.com/raw/1232f5b90fa612ee32b560c83dd36c08.png)
