## 应用型负载均衡相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeTaskStatus](https://cloud.tencent.com/document/api/214/30683) | 查询异步任务状态 |
| [CreateLoadBalancer](https://cloud.tencent.com/document/api/214/30692) | 购买负载均衡实例 |
| [DescribeLoadBalancers](https://cloud.tencent.com/document/api/214/30685) | 查询负载均衡实例列表 |
| [ModifyLoadBalancerAttributes](https://cloud.tencent.com/document/api/214/30680) | 修改负载均衡实例的属性 |
| [DeleteLoadBalancer](https://cloud.tencent.com/document/api/214/30689) | 删除负载均衡实例 |
| [CreateListener](https://cloud.tencent.com/document/api/214/30693) | 创建负载均衡监听器 |
| [DescribeListeners](https://cloud.tencent.com/document/api/214/30686) | 查询应用型负载均衡监听器列表 |
| [ModifyListener](https://cloud.tencent.com/document/api/214/30681) | 修改负载均衡监听器属性 |
| [DeleteListener](https://cloud.tencent.com/document/api/214/30690) | 删除负载均衡监听器 |
| [CreateRule](https://cloud.tencent.com/document/api/214/30691) | 创建负载均衡七层监听器转发规则 |
| [ModifyDomain](https://cloud.tencent.com/document/api/214/30682) | 修改七层转发规则的域名 |
| [ModifyRule](https://cloud.tencent.com/document/api/214/30679) | 修改应用型负载均衡监听器转发规则 |
| [DeleteRule](https://cloud.tencent.com/document/api/214/30688) | 删除应用型七层负载均衡监听器规则 |
| [RegisterTargets](https://cloud.tencent.com/document/api/214/30676) | 绑定后端机器到监听器上 |
| [DescribeTargets](https://cloud.tencent.com/document/api/214/30684) | 查询应用型负载均衡云服务器列表 |
| [ModifyTargetPort](https://cloud.tencent.com/document/api/214/30678) | 修改监听器绑定的后端机器的端口 |
| [ModifyTargetWeight](https://cloud.tencent.com/document/api/214/30677) | 修改监听器绑定的后端机器的转发权重 |
| [DeregisterTargets](https://cloud.tencent.com/document/api/214/30687) | 解绑应用型负载均衡监听器上注册的后端机器 |

## 传统型负载均衡相关接口

| 接口名称 | 接口功能 |
|---------|---------|
| [DescribeClassicalLBListeners](https://cloud.tencent.com/document/api/214/31791) | 获取传统型负载均衡监听器列表 |
| [RegisterTargetsWithClassicalLB](https://cloud.tencent.com/document/api/214/31789) | 绑定后端服务到传统型负载均衡 |
| [DescribeClassicalLBTargets](https://cloud.tencent.com/document/api/214/31790) | 获取传统型负载均衡绑定的后端服务器列表 |
| [DescribeClassicalLBHealthStatus](https://cloud.tencent.com/document/api/214/31792) | 获取传统型负载均衡后端的健康状态 |
| [DeregisterTargetsFromClassicalLB](https://cloud.tencent.com/document/api/214/31794) | 解绑传统型负载均衡的后端服务器 |
| [DescribeClassicalLBByInstanceId](https://cloud.tencent.com/document/api/214/31793) | 通过后端主机反向查找其绑定的传统型负载均衡 |

