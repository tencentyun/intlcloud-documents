## 概述

访问策略可用于授予访问 Prometheus 监控服务实例的权限。访问策略使用基于 JSON 的访问策略语言。您可以通过访问策略语言授权指定委托人（principal）对指定的 Prometheus 监控服务资源执行指定的操作。

访问策略语言描述了策略的基本元素和用法，有关策略语言的说明可参考 [CAM 策略管理](https://intl.cloud.tencent.com/document/product/598/10600)。

## 访问策略中的元素

访问策略语言包含以下基本意义的元素：

- **语句（statement）**：描述一条或多条权限的详细信息。该元素包括效力、操作、资源、条件等多个其他元素的权限或权限集合。一条策略有且仅有一个语句元素。
- **效力（effect）**：描述声明产生的结果是“允许”还是“显式拒绝”，包括 allow 和 deny 两种情况。该元素是必填项。
- **操作（action）**：描述允许或拒绝的操作。操作可以是 API（以 name 前缀描述）或者功能集（一组特定的 API，以 permid 前缀描述）。该元素是必填项。
- **资源（resource）**：描述授权的具体数据。资源是用六段式描述。每款产品的资源定义详情会有所区别。该元素是必填项。
- **条件（condition）**：描述策略生效的约束条件。条件包括操作符、操作键和操作值组成。条件值可包括时间、IP 地址等信息。有些服务允许您在条件中指定其他值。该元素是选填项。

## 元素用法

### 指定效力

如果没有显式授予（允许）对资源的访问权限，则隐式拒绝访问。同时，也可以显式拒绝（deny）对资源的访问，这样可确保用户无法访问该资源，即使有其他策略授予了访问权限的情况下也无法访问。下面是指定允许效力的示例：

```json
"effect" : "allow"
```

### 指定操作

云监控定义了可在策略中指定一类控制台的操作，指定的操作按照操作性质分为读取部分接口（monitor:Describe\*）和全部接口（monitor:\*）。

指定允许操作的示例如下：

```
"action": [
  "name/monitor:Describe*"
]
```

### 指定资源

资源（resource）元素描述一个或多个操作对象，如腾讯云 Prometheus 监控服务资源等。所有资源均可采用下述的六段式描述方式。

```plaintext
qcs:project_id:service_type:region:account:resource
```

参数说明如下：

| 参数         | 描述                                                         | 是否必选 |
| ------------ | ------------------------------------------------------------ | -------- |
| qcs          | 是 qcloud service 的简称，表示是腾讯云的云服务               | 是       |
| project_id   | 描述项目信息，仅为了兼容 CAM 早期逻辑，一般不填              | 否       |
| service_type | 产品简称，这里为 monitor                                     | 是       |
| region       | 描述地域信息                                                 | 是       |
| account      | 描述资源拥有者的主账号信息，即主账号的 ID，表示为 `uin/${OwnerUin}`，如 uin/100000000001 | 是       |
| resource     | 描述具体资源详情，前缀为 instance                            | 是       |

下面是一个 Prometheus 监控服务的六段式信息：

```plaintext
"resource":["qcs::monitor:ap-guangzhou:uin/100000000001:prom-instance/prom-73jingds"]
```

### 指定条件

访问策略语言可使您在授予权限时指定条件。主要是用于设置标签鉴权，标签条件只对绑定了该标签的集群生效，标签策略示例如下：

```json
"condition": {
    "for_any_value:string_equal": {
        "qcs:tag": [
            "testkey&testvalue"
        ]
    }
}
```

这个语句含义是策略包含标签 key 为 testkey，value 为 testvalue 的资源。

## 实际案例

### 基于标签

如下案例中，策略的含义是允许访问 UIN 为1250000000下面的实例 ID 为 prom-73jingds 的资源，以及绑定了标签键为 testkey，标签值为 testvalue 的资源（如果该实例未属于标签 testkey& testvalue ，则仍不允许访问）。

```json
{
   "version": "2.0",
    "statement": [
        {
            "action": [
                "name/monitor:*"
            ],
            "condition": {
               "for_any_value:string_equal": {
                    "qcs:tag": [
                        "testkey&testvalue"
                    ]
                }
            },
            "effect": "allow",
            "resource": [
                "qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds"
            ]
        }
    ]
}
```

### 基于资源

基于资源 ID，分配指定资源的读写权限，主账号ID 为 1250000000：

- 配置广州地域（资源）只读权限。
示例：为子用户分配， instance1(prom-73jingds)、instance2(prom-65jidfafk) 资源的只读权限。
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
			"name/monitor:Describe*"
		],
		"resource": [
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds",
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-65jidfafk"
		],
		"condition": []
	}]
}
```

- 配置广州地域（资源）部分读写权限。
示例：为子用户分配，instance1(prom-73jingds) 资源的删除操作权限。
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"resource": [
			"qcs::monitor:ap-guangzhou:uin/1250000000:prom-instance/prom-73jingds"
		],
		"action": [
			"name/monitor:TerminatePrometheusInstances"
		]
	}]
}
```

