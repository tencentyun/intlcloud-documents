## 简介
条件重试（Until Successful）组件的作用是对其子流执行重试操作。



[](id:method1)
##  方法


### 参数配置

| 参数         | 数据类型                               | 描述                                                         | 是否必填 | 默认值 |
| :----------- | :------------------------------------- | :----------------------------------------------------------- | :------- | ------ |
| 重试条件     | bool                                   | 定义重试的条件，当满足条件时触发重试| 否       | -      |
| 重试次数     | int                                    | 重试次数，取值范围1 - 100                                      | 是       | 3      |
| 重试时间间隔 | int                                    | 重试间隔，取值范围1 - 300，单位秒                              | 是       | 60     |

![](https://staticintl.cloudcachetci.com/yehe/backend-news/QTEI011_2.png)

### 数据预览

无

### 输入到子流中的 message

| message属性 | 值                                      |
| ----------- | --------------------------------------- |
| payload     | 继承**条件重试**上一个组件的 payload       |
| error       | 空                                      |
| attribute   | 继承**条件重试**上一个组件的 attribute 信息 |
| variable    | 继承**条件重试**上一个组件的 variable 信息  |

### 输出

| message属性 | 值                                                           |
| ----------- | ------------------------------------------------------------ |
| payload     | 继承子流输出的 payload                                        |
| error       | <ul style="margin:0; "><li>执行成功后，error 为空</li><li>执行失败后，error 为 dict 类型，包含“Code”和“Description”字段：“Code”字段表示错误类型，“Description”字段表示错误描述</li></ul> |
| attribute   | 继承子流的 attribute 信息                                      |
| variable    | 继承子流的 variable 信息                                       |

