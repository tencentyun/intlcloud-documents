本文档主要指导您如何通过控制台进行规则管理。

## 前提条件
已在 [GPM 控制台](https://console.cloud.tencent.com/gpm) 通过内测申请。详情可参见[ 快速入门](https://intl.cloud.tencent.com/document/product/1072/39200)。

## 操作步骤
### 创建规则
1.登录 [游戏玩家匹配控制台](https://console.cloud.tencent.com/gpm) ，单击左侧 **规则管理**。
2.进入规则管理页面，单击 **创建**。
![](https://main.qcloudimg.com/raw/042efc9b905fc04536a38d0e751928f7.jpg)

3. 填写规则名称、描述和规则脚本。填写规则脚本后，可单击**验证规则脚本**进行验证。
![](https://main.qcloudimg.com/raw/eea71ddf1090dae3990745a22988feb5.jpg)
 - 名称：输入规则名称，必填，长度限制在128字节以内。
 - 描述：规则的相关描述，非必填，长度限制在1024字节以内。
 - 规则脚本：必填，长度限制在65535字节以内。关于规则脚本的语法，详情请参见 [规则脚本设计指南](https://intl.cloud.tencent.com/document/product/1072/39869)。

4. 单击**确定**。新建规则后，在规则管理页面，就会生成相应的规则 RuleCode。
![](https://main.qcloudimg.com/raw/60e5ff0061efa06c64d1eaea89998c1d.jpg)

### 查看规则
进入规则管理页面，单击规则列表中的**RuleCode**，即可查看规则详情。
![](https://main.qcloudimg.com/raw/bb9bddeda1fcc10f82a7da6e12712e41.jpg)

### 编辑规则
![](https://main.qcloudimg.com/raw/7603d7caf67cd8f6875bcacfb6830735.jpg)
您可以在规则详情页，对规则的名称和描述进行编辑。规则一旦创建，规则脚本不支持编辑。您可以通过克隆规则的方式获得规则的拷贝，并在此拷贝上重新设计您的规则脚本。

### 克隆规则
进入规则管理页面，选择规则列表中的**克隆**操作，即可复制创建一个新的规则。
![](https://main.qcloudimg.com/raw/57882f396537016cc31a47a663a844e6.jpg)

### 删除规则
进入规则管理页面，选择规则列表中的**删除**操作，即可删除无匹配关联的规则。
>!规则删除后无法恢复。如果您希望删除正在被匹配关联的规则，可以先修改匹配信息，解除匹配与规则的关联。
>
![](https://main.qcloudimg.com/raw/e88d043965ac7ec0d2a631da8925be53.jpg)




