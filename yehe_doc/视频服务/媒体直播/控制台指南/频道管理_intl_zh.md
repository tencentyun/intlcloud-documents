
MediaLive 支持通过导出/导入频道配置文件及频道克隆功能来快速完成频道创建工作。
## 操作方法
### 步骤1：频道导出
MediaLive 的【Channel Management】界面会显示您所有创建的频道及状态，点击右侧的「Export」按钮可快速导出频道配置 json 文件。
 ![](https://main.qcloudimg.com/raw/a594a0763bbadf85dcc5df7fb44d6309.jpg)

### 步骤2：频道导入
打开「Channel Management」界面点击「Create Channel」按钮，选择「Import Configuration」，选中修改后的频道配置 json 文件保存。
提交 json 文件后即进入频道编辑状态，接着按照常规配置过程保存并提交频道即可。
 ![](https://main.qcloudimg.com/raw/a9c515f9a211a36c621d32674b605d01.jpg)

>!
>- 频道导入功能实际上是一次快速填写的过程，我们会基于您导入的 json 文件快速帮您自动填写「Basic Information」、「Output Group Setting」两部分内容，「Input Setting」部分会被忽略，需要您重新选择 input。因此如果您需要通过此方法快速创建一个 channel，可以提前创建好一个新的 input。
>- 编辑频道时如果导入新的配置文件，则原来频道配置信息会被覆盖。

### 步骤3：频道克隆
频道克隆本质是一次快速且特殊的频道导出/导入操作，打开「Channel Management」界面点击 Operation 下的Clone 按钮后即可进入克隆频道的配置状态。
此时频道会自动填写被克隆频道的基本信息（「Input Setting」部分除外），接着按照常规配置过程保存并提交频道即可。
![](https://main.qcloudimg.com/raw/2a8e3bc4beecc3be1f67de8aed62512f.jpg)
