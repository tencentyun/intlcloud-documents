## 概述

用户在使用日志服务过程中可选择在不同地域创建日志集与日志主题。地域是指物理的数据中心的地理区域，不同地域之间网络完全隔离。用户可以根据自己的业务场景以及目标用户所在的地理位置，选择就近的地域存储，以降低日志数据的访问时延、提高访问速度。

#### 可用地域及简称

| 地域     | 域名简称         | 内网域名                            | 外网域名                           |
| -------- | ---------------- | ----------------------------------- | ---------------------------------- |
| 北京     | ap-beijing       | ap-beijing.cls.tencentyun.com       | ap-beijing.cls.tencentcs.com       |
| 广州     | ap-guangzhou     | ap-guangzhou.cls.tencentyun.com     | ap-guangzhou.cls.tencentcs.com     |
| 上海     | ap-shanghai      | ap-shanghai.cls.tencentyun.com      | ap-shanghai.cls.tencentcs.com      |
| 成都     | ap-chengdu       | ap-chengdu.cls.tencentyun.com       | ap-chengdu.cls.tencentcs.com       |
| 中国香港 | ap-hongkong      | ap-hongkong.cls.tencentyun.com      | ap-hongkong.cls.tencentcs.com      |
| 硅谷     | na-siliconvalley | na-siliconvalley.cls.tencentyun.com | na-siliconvalley.cls.tencentcs.com |
| 多伦多   | na-toronto       | na-toronto.cls.tencentyun.com       | na-toronto.cls.tencentcs.com       |



## 注意事项

如果日志服务中接入了其他云产品，请您尽量选择与其他云产品相同地域的日志集。相同地域的云产品之间通过内网读写数据，能有效降低延迟和提高访问速度。
