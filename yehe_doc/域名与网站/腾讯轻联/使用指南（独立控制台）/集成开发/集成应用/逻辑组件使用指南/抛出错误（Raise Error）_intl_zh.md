## 简介

抛出错误（Raise Error）组件用来抛出异常，中断流的执行。该组件可以单独使用，也可以搭配“错误捕获”组件使用。单独使用时，命中“抛出错误”，集成流会中断执行，返回错误信息。搭配“错误捕获”组件使用时，可以在“捕获错误”中捕获本组件定义的异常，然后执行“捕获错误”中配置的子流。

## 操作指引

### 连接说明

无

### 参数配置

| 参数     | 数据类型 | 描述               | 是否必填 | 默认值   |
| :------- | :------- | :----------------- | :------- | -------- |
| 错误类型 | string   | 用户自定义错误类型 | 是       | 通用错误 |
| 错误描述 | string   | 错误的描述信息     | 是       | 无       |

![](https://staticintl.cloudcachetci.com/yehe/backend-news/IdFC224_1.png)

错误类型通过下拉列表选择，可以通过新增按钮添加新的错误类型，项目内所有应用可见。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3V2A270_2.png)

### 数据预览

无

### 输出

组件输出的 message 信息如下：

| message 属性 | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | 继承上个组件的 payload                                        |
| error       | error 为 dict 类型，包含“Code”和“Description”字段：<br>“Code”字段表示错误类型，使用内部编码表示，“Description”字段表示错误描述 |
| attribute   | 继承上个组件的 attribute 信息                                  |
| variable    | 继承上个组件的 variable 信息                                   |

## 案例

1. 添加“抛出错误”组件。
2. 新增错误类型“请求失败”。
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/d7ww138_3.png)
3. 选择错误类型，配置错误描述。
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/aD4X179_4.png)
4. 输出信息。
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/CNcz095_5.png)
