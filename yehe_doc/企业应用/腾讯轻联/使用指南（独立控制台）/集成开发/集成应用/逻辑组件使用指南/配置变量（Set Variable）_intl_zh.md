## 简介

配置变量（Set Variable）的作用是声明一个变量，并保存在 message 的 variables 中，后续节点可通过 msg.vars.get('name') 形式引用该变量。




[](id:method1)
##  方法

### 参数配置

| 参数   | 数据类型 | 描述         | 是否必填 | 默认值 | 备注 |
| :----- | :------- | :----------- | :------- | ------ |------ |
| 变量名 | string   | 变量名称     | 是       | 无     |无     |
| 变量值 | any      | 变量的具体值 | 是       | 无     |无     |
| 变量类型 | string      | 变量的类型 | 是       | string     |无     |
| 操作 | string      | 变量的操作 | 否       | 无     |仅当变量类型为 list 或 dict，并且已存在该变量时支持 |

### 配置界面

![image-20210325155553571](https://staticintl.cloudcachetci.com/yehe/backend-news/sTJS778_1.png)

### 输出

对 variables 变量的引用，需要使用表达式：msg.vars.get('company')。

组件输出的 message 信息如下：

| message 属性 | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | 继承上个组件的 payload                                        |
| error       | <ul style="margin:0;"><li>执行成功后，error 为空</li><li>执行失败后，error 为 dict 类型，包含“Code”和“Description”字段：“Code”字段表示错误类型，“Description”字段表示错误具体信息</li></ul> |
| attribute   | 继承上个组件的 attribute 信息                                  |
| variable    | 上个组件的 variable 信息加上当前组件添加的变量                 |

### 数据预览
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/g9Dw732_2.png" alt="https://staticintl.cloudcachetci.com/yehe/backend-news/g9Dw732_2.png" style="zoom:50%;" />

