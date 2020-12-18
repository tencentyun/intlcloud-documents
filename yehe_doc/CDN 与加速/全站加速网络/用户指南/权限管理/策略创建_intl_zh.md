为方便用户更加细粒度的配置域名查询、管理权限，ECDN 权限策略已全面完成升级，用户可通过自定义策略语句，实现域名级别的权限分配。
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview) ，单击【策略】菜单，即可进入策略管理页面，单击【新建自定义策略】：
![](https://main.qcloudimg.com/raw/cd17fa629afe272d53b84c1a17d044e8.png)
2. 选择【按策略生成器创建】：
![](https://main.qcloudimg.com/raw/6c6fdbed40dfcc561680299678feee43.png)
3. 在产品选框中选择【全站加速网络】，并选择需要授权的功能集合，若授权全读写权限，可勾选【All】选中全部服务，功能与控制台映射关系可查看  [Action 映射表](https://intl.cloud.tencent.com/document/product/570/35819)。
![3配图](https://main.qcloudimg.com/raw/19ca1a9ed6d5f89d49562e026c29a1b4.png)
4. 在资源处填充需要授权的域名，填写格式为：`qcs::ecdn::uin/xxxxxxxxxx:domain/xxx.com`，其中 uin/ 后的 xxxxxxxxxx 需要替换为您的账号 ID，xxx.com 需要替换为您要分配权限的具体域名。直接填写`*`代表分配所有域名权限，完成配置后，单击【添加声明】并单击【下一步】，即可创建策略，将创建好的策略关联已有用户 / 用户组，即可进行授权：
![配图4](https://main.qcloudimg.com/raw/243ebba2827f93c1aed48fc6a8a33ab6.png)

