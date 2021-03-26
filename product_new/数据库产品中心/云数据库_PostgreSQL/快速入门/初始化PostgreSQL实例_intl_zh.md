创建 PostgreSQL 实例后，您还需要进行 PostgreSQL 实例的初始化，以轻松启用实例。

## 前提条件
1. 已注册腾讯云账号并完成实名认证。
如需注册腾讯云账号：
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">点此注册腾讯云账号</a></div>
2. 已购买云数据库 PostgreSQL。


## 操作步骤
1. 登录 [PostgreSQL 控制台](https://console.cloud.tencent.com/pgsql)，在实例列表，选择状态为“待初始化”的实例，在“操作”列单击【初始化】。

   ![](https://main.qcloudimg.com/raw/63731685a6c959999e938a9132b99196.png)

2. 在弹出的初始化对话框，配置初始化相关参数，单击【确定】开始初始化。
  

 - **管理员用户名**：帐号名需要1-16个字符，由字母、数字或特殊字符组成；以字母开头，字母或数字结尾；特殊字符为\_；不区分大小写；不能为: postgres，不能以 pg\_ 开头。
 - **密码**：密码需要8-32个字符，至少包含英文、数字和符号_+-&=!@#$%^*()中的2种。
 - **确认密码**：再次输入密码。
 - **支持字符集**：支持 LATIN1 、UTF8 字符集。
3. 返回实例列表，待实例状态变为“运行中”，即可正常使用。
