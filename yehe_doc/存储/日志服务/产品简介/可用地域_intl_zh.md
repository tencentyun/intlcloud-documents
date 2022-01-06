## 概述

用户在使用日志服务过程中可选择在不同地域创建日志集与日志主题。地域是指物理的数据中心的地理区域，不同地域之间网络完全隔离。用户可以根据自己的业务场景以及目标用户所在的地理位置，选择就近的地域存储，以降低日志数据的访问时延、提高访问速度。

#### 可用地域及域名

| 地域     | 简称             | 内网域名                         | 外网域名                                 |
| :------- | :--------------- | -------------------------------- | ---------------------------------------- |
| 北京     | ap-beijing       | cls.internal.tencentcloudapi.com | cls.ap-beijing.tencentcloudapi.com       |
| 广州     | ap-guangzhou     | cls.internal.tencentcloudapi.com | cls.ap-guangzhou.tencentcloudapi.com     |
| 上海     | ap-shanghai      | cls.internal.tencentcloudapi.com | cls.ap-shanghai.tencentcloudapi.com      |
| 成都     | ap-chengdu       | cls.internal.tencentcloudapi.com | cls.ap-chengdu.tencentcloudapi.com       |
| 南京     | ap-nanjing       | cls.internal.tencentcloudapi.com | cls.ap-nanjing.tencentcloudapi.com       |
| 重庆     | ap-chongqing     | cls.internal.tencentcloudapi.com | cls.ap-chongqing.tencentcloudapi.com     |
| 中国香港 | ap-hongkong      | cls.internal.tencentcloudapi.com | cls.ap-hongkong.tencentcloudapi.com      |
| 中国台北 | ap-taipei        | cls.internal.tencentcloudapi.com | cls.ap-taipei.tencentcloudapi.com        |
| 硅谷     | na-siliconvalley | cls.internal.tencentcloudapi.com | cls.na-siliconvalley.tencentcloudapi.com |
| 弗吉尼亚 | na-ashburn       | cls.internal.tencentcloudapi.com | cls.na-ashburn.tencentcloudapi.com       |
| 新加坡   | ap-singapore     | cls.internal.tencentcloudapi.com | cls.ap-singapore.tencentcloudapi.com     |
| 曼谷     | ap-bangkok       | cls.internal.tencentcloudapi.com | cls.ap-bangkok.tencentcloudapi.com       |
| 孟买     | ap-mumbai        | cls.internal.tencentcloudapi.com | cls.ap-mumbai.tencentcloudapi.com        |
| 法兰克福 | eu-frankfurt     | cls.internal.tencentcloudapi.com | cls.eu-frankfurt.tencentcloudapi.com     |
| 东京     | ap-tokyo         | cls.internal.tencentcloudapi.com | cls.ap-tokyo.tencentcloudapi.com         |
| 首尔     | ap-seoul         | cls.internal.tencentcloudapi.com | cls.ap-seoul.tencentcloudapi.com         |
| 莫斯科   | eu-moscow        | cls.internal.tencentcloudapi.com | cls.eu-moscow.tencentcloudapi.com        |
| 雅加达   | ap-jakarta       | cls.internal.tencentcloudapi.com | cls.ap-jakarta.tencentcloudapi.com       |
| 多伦多   | na-toronto       | cls.internal.tencentcloudapi.com | cls.na-toronto.tencentcloudapi.com       |



## 注意事项

- 通过外网访问时也可使用统一域名cls.tencentcloudapi.com (仅支持非金融区)，将根据调用接口时客户端所在位置，自动解析到最近的某个具体地域的服务器，对时延敏感的业务，建议指定带地域的域名。
- 如果日志服务中接入了其他云产品，请您尽量选择与其他云产品相同的地域。相同地域的云产品之间通过内网读写数据，能有效降低延迟和提高访问速度。
- 以上域名仅支持日志服务API 3.0，LogListener及[日志服务 API 2017](https://intl.cloud.tencent.com/document/product/614/16907)使用域名见下表，使用Kafka协议上传日志参见[使用 Kafka 协议上传日志操作指南](https://intl.cloud.tencent.com/document/product/614/43574)

| 地域     | 简称             | 内网域名                            | 外网域名                           |
| -------- | ---------------- | ----------------------------------- | ---------------------------------- |
| 北京     | ap-beijing       | ap-beijing.cls.tencentyun.com       | ap-beijing.cls.tencentcs.com       |
| 广州     | ap-guangzhou     | ap-guangzhou.cls.tencentyun.com     | ap-guangzhou.cls.tencentcs.com     |
| 上海     | ap-shanghai      | ap-shanghai.cls.tencentyun.com      | ap-shanghai.cls.tencentcs.com      |
| 成都     | ap-chengdu       | ap-chengdu.cls.tencentyun.com       | ap-chengdu.cls.tencentcs.com       |
| 南京     | ap-nanjing       | ap-nanjing.cls.tencentyun.com       | ap-nanjing.cls.tencentcs.com       |
| 重庆     | ap-chongqing     | ap-chongqing.cls.tencentyun.com     | ap-chongqing.cls.tencentcs.com     |
| 中国香港 | ap-hongkong      | ap-hongkong.cls.tencentyun.com      | ap-hongkong.cls.tencentcs.com      |
| 中国台北 | ap-taipei        | ap-taipei.cls.tencentyun.com        | ap-taipei.cls.tencentcs.com        |
| 硅谷     | na-siliconvalley | na-siliconvalley.cls.tencentyun.com | na-siliconvalley.cls.tencentcs.com |
| 弗吉尼亚 | na-ashburn       | na-ashburn.cls.tencentyun.com       | na-ashburn.cls.tencentcs.com       |
| 新加坡   | ap-singapore     | ap-singapore.cls.tencentyun.com     | ap-singapore.cls.tencentcs.com     |
| 曼谷     | ap-bangkok       | ap-bangkok.cls.tencentyun.com       | ap-bangkok.cls.tencentcs.com       |
| 孟买     | ap-mumbai        | ap-mumbai.cls.tencentyun.com        | ap-mumbai.cls.tencentcs.com        |
| 法兰克福 | eu-frankfurt     | eu-frankfurt.cls.tencentyun.com     | eu-frankfurt.cls.tencentcs.com     |
| 东京     | ap-tokyo         | ap-tokyo.cls.tencentyun.com         | ap-tokyo.cls.tencentcs.com         |
| 首尔     | ap-seoul         | ap-seoul.cls.tencentyun.com         | ap-seoul.cls.tencentcs.com         |
| 莫斯科   | eu-moscow        | eu-moscow.cls.tencentyun.com        | eu-moscow.cls.tencentcs.com        |
| 雅加达   | ap-jakarta       | ap-jakarta.cls.tencentyun.com       | ap-jakarta.cls.tencentcs.com       |
| 多伦多   | na-toronto       | na-toronto.cls.tencentyun.com       | na-toronto.cls.tencentcs.com       |

