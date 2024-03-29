
文本模式针对各数据类型进行定制化的交互设计，用户仅需要进行简单操作即可生成所需数据。

## IDE 使用
1. 对于任意 Dataway 编辑文本框，将鼠标移至编辑文本框，会自动弹出模式选择按钮，单击**文本**进入文本模式。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/TQxd420_1.png" width="80%">>
2. 单击选择左侧下拉菜单中的类型选择所需数据类型，Dataway 会提供针对性的输入交互界面。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/RNGd469_2.png" width="80%">


## 数据类型
<dx-accordion>
::: 任意类型（any，默认类型）
可直接输入文本生成字符串，也支持 [集成流数据面板](https://www.tencentcloud.com/document/product/1165/51655#dataref) 引用集成流上下文数据。当文本和集成流数据面板引用存在多项时，将以这些数据项为元素，组建列表。

:::
::: 整数（int）、浮点数（float）、字符串（string）、十进制（decimal）、布尔值（bool）
可直接输入字面量生成对应数据，也支持 [集成流数据面板](https://www.tencentcloud.com/document/product/1165/51655#dataref) 引用，方便用户使用集成流的上下文数据。集成流数据面板引用的数据会转化为字符串，拼接到字面量中。

:::
::: 时刻（datetime）、日期（date）、时间（time）
点击文本框弹出相应可视化交互界面，在可视化交互界面上点选相应时间数据。
时刻：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ww3B486_8.png)
日期：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CbHC059_897d13ebc424719da2e5d0a087cc7666.png" width="60%">
时间：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/4Pin469_963a8a91e520dc62d157eb8414faf3dc.png" width="60%">
:::
::: 空值（None）
该类型代表输入数据为空值，禁止文本框输入。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UIj5524_9.png)

:::
::: 字典（dict）、列表（list）、消息（Message）、表单（FormData）
1. 单击文本框，弹出相应交互界面。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Y83v622_55c6cc1e164870911993951565ff80c7.png" width="80%">
2. 在交互界面上逐项添加内容并确认。

:::
::: JSON 二进制（Entity.json）、XML 二进制（Entity.xml）
1. 单击文本框，弹出相应文本输入界面。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/6uUJ066_5777c31eb67eb33404ef39c5ab30e278.png" width="80%">
2. 在文本输入界面填写相应文本并单击**确定**进行保存，自动生成对应 MIME 类型（json/xml）的 UTF-8 编码的 Entity 数据。

:::
::: 数据集（DataSet）、单条数据（Record）
文本模式支持 [集成流数据面板](https://www.tencentcloud.com/document/product/1165/51655#dataref) 引用集成流上下文的"数据集成"数据：数据集和单条数据。数据集和单条数据作为数据集成的专有数据类型，需要通过特定组件（"构造数据集"组件等）生成，Dataway 不提供生成方法。

:::
</dx-accordion>

