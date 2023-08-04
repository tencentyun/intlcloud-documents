## 操作场景

本文介绍如何使用 Dataway 脚本来辅助进行集成流设计。

## 前期准备
1. 已有腾讯云账号可直接登录 [腾讯轻联控制台](https://ipaas.tencentcloud.com/login)，暂无账号请先注册账号。
2. 登录成功后，新建一个应用并创建一条集成流。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9jec667_17-en.png)


## 使用 Dataway 表达式（以代码模式 Python 脚本为例）
以一个简单的字符串连接为示例，使用步骤如下：
1. 在**腾讯轻联**的 [**应用集成**](https://ipaas.tencentcloud.com/login) 页面，单击**新建应用**，新建一个**"配置Payload"**组件。
2. 在右侧自动弹出组件配置。其中，**“值”**配置项需要 Dataway 表达式填写。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/btEa722_18-en.png)
3. 鼠标移至**“值”**配置项的编辑文本框，弹出模式选择按钮，单击**代码**，进入代码输入模式。
	![选择输入模式](https://staticintl.cloudcachetci.com/yehe/backend-news/x5M2781_19-en.png)
4. 单击编辑文本框，弹出代码编辑器，输入 Dataway 脚本。输入时会实时进行语法检查，若出错则会有对应提示。
```python
def dw_process(msg):
    return 'Hello' + 'World'
```
	- 完整的 DataWay 代码模式下的 Python 脚本需符合语法定义的 Python3 代码段，其中包含入口函数定义 def dw_process(msg)。
	- DataWay 基于 Python3 语法进行实现，同时内置了多个第三方模块，如 time、json、math等，使用时直接引用模块名即可。

5. 验证 Dataway 运行结果：在通过语法检查并单击**确定**保存表达式之前，可以对 Dataway 脚本的正确性进行验证。
<br>在编辑框右上角单击**Debug**，在弹出的对话框中单击**开始测试**。

测试结束后， Dataway 代码编辑框的下方会有输出结果的展示，可以看到 Dataway 脚本的运行结果为 `HelloWorld`，符合预期。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5DMw447_21-en.png)
同时可以切换到**"日志"**项，查看 print 的输出结果。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HUKh613_22-en.png)

6. 单击**确定**，完成 Dataway 脚本的保存。

### 表达式模式
对于简单表达式输入，用户可以使用表达式模式。
1. 当鼠标移至**“值”**配置项的**编辑文本框**，弹出模式选择按钮时，点击**"表达式"**，进入表达式模式。
2. 单击编辑文本框，即可填写 Dataway 表达式。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Knfk949_23-en.png)

### 文本模式
对于字面量数据的创建或 [集成流数据引用](#dataref) 等简单输入，用户可以使用文本模式。

以生成时间数据为示例，使用步骤如下：
1. 当鼠标移至**“值”**配置项的**编辑文本框**，弹出模式选择按钮时，单击**文本**，进入文本模式。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VZKb896_24-en.png)
2. 单击左侧类型选择下拉菜单，菜单展开后，找到并单击**datetime**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/puYV342_25-en.png)
3. 单击编辑文本框，弹出时间设定交互界面，在此界面上设定时间信息。
4. 设定完成后，单击**确定**完成输入。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8e3t393_26-en.png)



### 代码模式 Java 脚本
除了 Python 语法，Dataway 提供对 Java 语法的支持，用户可以使用代码模式输入 Java 脚本。

1. 鼠标移至**“值”**配置项的编辑文本框，弹出模式选择按钮，单击**代码**，进入代码输入模式。
	![选择输入模式](https://staticintl.cloudcachetci.com/yehe/backend-news/Afe6498_27-en.png)
2. 单击编辑文本框，进入代码编辑交互界面，然后单击**Java**，开始 Java 脚本编辑。

3. 单击**确定**，完成 Dataway 脚本的保存。


[](id:dataref)
### 集成流数据面板和引用

Dataway 支持可视化引用集成流的上下文数据，打通组件间的数据流转捷径，提升用户体验。所有模式均支持集成流数据面板的数据引用功能，包括 [文本模式](https://www.tencentcloud.com/document/product/1165/51656)、[表达式模式](https://www.tencentcloud.com/document/product/1165/51657)、[代码模式 Python ](https://www.tencentcloud.com/document/product/1165/51659) 和 [代码模式 Java ](https://www.tencentcloud.com/document/product/1165/51661)。

编辑 Dataway 输入文本框时自动弹出**集成流数据面板**。单击面板中的数据按钮，即可引用相应数据，并以数据标签的形式显示在文本框中。


