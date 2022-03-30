该文档介绍如何将通用文件类型的制品存储在 CODING 制品库中。其内容包括创建制品库、推送、拉取和删除制品。

## 进入制品库功能页

1. 登录 CODING 控制台，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击左侧菜单栏的**制品管理**，进入制品仓库功能页面。

## 创建制品仓库

进入项目，在左侧栏选择**制品库**，再单击**创建仓库**。

-   仓库类型选中 Generic File
-   提供一个仓库名称
-   提供一段仓库描述（非必填）
-   决定当前创建的制品仓库对不同类型角色的操作权限，默认将对当前项目成员开放**推送**和**拉取**操作。 
-   准备就绪，单击**确认新建**

![](https://qcloudimg.tencent-cloud.cn/raw/24e8a6b622523ee751b8dc25e975d9c2.png)

## 推送 Generic 制品

Generic 类型制品库支持两种方式推送制品：
-   命令行方式
-   通过页面直接上传

### 通过命令行上传

参考**指引**当中的命令行进行推送：
![](https://qcloudimg.tencent-cloud.cn/raw/8f70e94aeacacf1c193d5519ac66101d.png)
以推送一个文件 demo.properties 为例。

```bash
curl -T demo.properties -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1"
```
![](https://main.qcloudimg.com/raw/c9917d9dc36fa929b8cb1df1fa3f5490.png)

### 通过页面直接上传

在制品仓库页面，单击**直接上传**或者将文件拖拽至当前页面。
![](https://qcloudimg.tencent-cloud.cn/raw/c4cd765c2248ff2217bcd3eb615201b9.png)
选择一个文件、勾选上传内容的打包形式、填写版本、确认包名，单击**开始上传**。
![](https://qcloudimg.tencent-cloud.cn/raw/6f5b960483bcd8af8e74e41f93024d4c.png)

## 查看 Generic 制品

上传制品成功后，页面右下角会有弹窗提示任务成功。单击**包列表**即可查看到上传的包信息。
![](https://qcloudimg.tencent-cloud.cn/raw/2353edc7072a5aab8921294e11911b3e.png)

## 拉取 Generic 制品

Generic 类型制品库支持两种方式拉取制品：
-   命令行方式
-   通过页面直接下载

### 通过命令行拉取

参考**指引**当中的命令行进行拉取：
![](https://qcloudimg.tencent-cloud.cn/raw/693c5120552978f94b6f925ae6513061.png)

```bash
curl -L -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1" -o demo.properties
```

### 通过页面直接下载

在仓库页面，在**包列表**中单击包名，在右侧栏中单击**版本列表**，下载您需要的版本即可。
![](https://qcloudimg.tencent-cloud.cn/raw/9b1c775927650b07cabd3f4678f5fcfa.png)

## 删除 Generic 制品

需通过命令行删除 Generic 制品。
![](https://qcloudimg.tencent-cloud.cn/raw/92a23568c63c00dacd4e66a5506e29a6.png)

参考指引页面中给出的删除指令即可。

```bash
curl -X DELETE -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1"
```
![](https://main.qcloudimg.com/raw/af6adb31cfd9957e457251383c5e7df6.png)