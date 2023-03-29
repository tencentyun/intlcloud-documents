## 参数模板使用案例
参数模板是安全组添加规则时一种高效、快捷、易维护的添加方式，例如当您需要添加多个地址段、指定 IP，及多个类型的协议端口时，可以定义参数模板，后期也可以通过参数模板来维护安全组规则中的 IP 来源和协议端口。
>?文中所有 IP 地址和协议端口均为举例，实际配置时，请根据业务实际情况进行替换。
>


## 示例描述
假设某用户期望配置如下安全组规则，且后续需要更新入站的来源 IP 范围和协议端口：
+ 入站规则：
 + 允许来源 IP 范围：10.0.0.16-10.0.0.30，协议端口：TCP:80,443
 + 允许来源 CIDR 网段：192.168.3.0/24，协议端口：TCP:3600-15000

+ 出站规则：
 拒绝目标 IP 地址：192.168.10.4，协议端口为：TCP:800


## 解决方案
由于用户多个 IP 网段和协议端口有相同的安全组策略，且后续需要更新来源 IP 范围，因此可结合参数模板来实现安全组规则的添加维护。



### 步骤一：新建参数模板
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 选择左侧目录中的**安全** > **参数模板**，进入管理页面。
3. 在**IP 地址**页签，单击**+新建**，分别新建用于添加入站、出站规则的 IP 地址参数模板。
4. 在弹框中，输入来源 IP 地址范围，并单击**提交**。</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/581bf5c79ec186d05290c8ab73138338.png" width="45%" />
</br>
新建成功的 IP 地址参数模板如下图所示。
<img src="https://qcloudimg.tencent-cloud.cn/raw/67f474a18a1f4cca9001995700d80559.png">
5. 在“协议端口”页签，单击**+新建**，分别新建用于添加入站、出站规则的协议端口参数模板。
<img src="https://qcloudimg.tencent-cloud.cn/raw/fa453b19c81e823dee3afc0e5b473d72.png" width="45%" /> 
</br>
新建成功的协议端口参数模板如下图所示。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce16cdc7fdbeec0f3117ca4c8e3a863.png">

### 步骤二：添加安全组规则
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 选择左侧目录中的**安全** > **安全组**，进入管理页面。
3. 在列表中，找到需要引用参数模板的安全组，单击其 ID，进入详情页。
4. 在入站规则 / 出站规则页签中，单击**添加规则**。
5. 在弹框中选择自定义类型，来源/目标分别选择对应的 IP 参数模板，协议端口分别选择对应的协议端口参数模板，并单击**完成**。
![](https://qcloudimg.tencent-cloud.cn/raw/9039d1de4a8a2891873faaec92627fee.png)
	
### 步骤三：更新参数模板
假设用户需要增加 IP 来源为10.0.1.0/27网段，协议端口为 UDP:58 的入站规则。可以直接更新 IP 地址 ipm-0ge3ob8e 和协议端口 ppm-4ty1ck3i 的参数模板。
1. 在参数模板的“IP 地址”页签，找到 ipm-0ge3ob8e 参数模板。
2. 在右侧单击**编辑**。
![](https://qcloudimg.tencent-cloud.cn/raw/f7f28bf7fdb77f25c6c1e2fbf5555809.png)
3. 在弹框中，换行增加10.0.1.0/27网段，单击**提交**。
![](https://qcloudimg.tencent-cloud.cn/raw/0be07de1ae0e9858ec94327cb0b3ba75.png)
4. 在参数模板的“协议端口”页签，找到 ppm-4ty1ck3i 参数模板。
5. 在右侧单击**编辑**。
![](https://qcloudimg.tencent-cloud.cn/raw/9ba28cdac71dbded7259eee9e74d128a.png)
6. 在弹框中，换行增加 UDP:58 入站协议端口，单击**提交**。</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b4f15b9ef711caae75920b2f70780667.png" width="45%" />
