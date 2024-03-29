

为满足企业中不同成员使用 **弹性微服务** 时具有不同的操作权限、资源权限的需求，当前弹性微服务支持**主账号**通过弹性微服务控制台中的权限配置，为子账号灵活配置操作和资源权限。

## 操作场景
弹性微服务权限策略支持配置**操作范围**与**资源范围**，一条完整的权限策略可以定义权限策略拥有者在资源范围内可以执行的操作。

|  资源类型 	|  资源范围                	|  操作范围  	|
|-----------	|--------------------------	|----------------------|
|  环境     	|  指定环境/全部环境       	|  <li>查看环境详情：包括环境相关的读操作和部署操作（将应用部署至环境、将网关关联至环境）。<li>管理环境：包括环境相关的读操作、部署操作和写操作 	|
|  应用     	|  指定应用/全部应用       	|  <li>查看应用详情：包括应用相关的读操作。 <li>管理应用：包括应用相关的读操作和写操作。                                                         	|
|  CLB 网关  	|  指定 CLB 网关/全部 CLB 网关 	|  <li>查看 CLB 网关详情：包括 CLB 网关相关的读操作。 <li>管理 CLB 网关：包括CLB网关相关的读操作和写操作。                                             	|
