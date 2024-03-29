# 接口描述
 DescribeLoadBalancers 接口用来获取用户的负载均衡实例列表。可以根据您输入的参数来返回满足条件的负载均衡实例。

接口访问域名：`lb.api.qcloud.com`


## 请求参数
 以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/product/214/11594) 页面。其中，此接口的 Action 字段为 DescribeLoadBalancers。

|参数名称|必选|类型|描述|
|---|---|---|---|
|loadBalancerIds.n|否|String|负载均衡实例 ID。|
|loadBalancerType|否|Int|负载均衡实例的网络类型：<br>2：公网属性， 3：内网属性。|
|forward|否|Int|1：负载均衡，0：传统型负载均衡，-1：全部类型。|
|loadBalancerName|否|String|负载均衡实例名称。|
|domain|否|String|腾讯云为传统型公网负载均衡实例分配的域名，其他类型的负载均衡该字段无意义。|
|loadBalancerVips.n|否|String|负载均衡实例的 VIP 地址，支持多个。|
|backendWanIps.n|否|String|后端云服务器的外网 IP。|
|backendLanIps.n|否|String|后端云服务器的内网 IP。|
|offset|否|Int|数据偏移量，默认为 0。|
|limit|否|Int|返回负载均衡个数，默认为 20。|
|orderBy|否|String|排序字段，支持以下字段：loadBalancerName，createTime，domain，loadBalancerType。|
|orderType|否|Int|1：倒序，0：顺序，默认按照创建时间倒序。|
|searchKey|否|String|搜索字段，模糊匹配名称、域名、VIP。|
|projectId|否|Int|负载均衡实例所属的项目 ID，可以通过 <a href="https://intl.cloud.tencent.com/document/product/214/1261">DescribeProject</a> 接口获取。|
|withRs|否|Int|查询的负载均衡是否绑定后端服务器，0：没有绑定云服务器，1：绑定云服务器，2：查询全部。|

## 返回参数

|参数名称|类型|描述|
|----|---|----|
|code|Int|公共错误码，0表示成功，其他值表示失败。详见错误码页面的 <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="公共错误码">公共错误码</a>。|
|message|String|模块错误信息描述，与接口相关。|
|codeDesc|String|英文错误码，成功返回 Success，失败有相应的英文说明。|
|totalCount|Int|满足过滤条件的负载均衡实例总数。|
|loadBalancerSet|Array|返回的负载均衡实例数组。|

- loadBalancerSet结构

|参数名称|类型|描述|
|----|---|----|
|loadBalancerId|String|负载均衡实例 ID。|
|unLoadBalancerId|String|负载均衡实例 ID。|
|loadBalancerName|String|负载均衡实例的名称。|
|loadBalancerType|Int|负载均衡实例的网络类型<br>2：公网属性， 3：内网属性。|
|forward|Int|负载均衡类型标识，1：负载均衡，0：传统型负载均衡。|
|domain|String|腾讯云为传统型公网负载均衡实例分配的域名，其他类型的负载均衡该字段无意义。|
|loadBalancerVips|Array|负载均衡实例的 VIP 列表。|
|status|Int|负载均衡实例的状态，包括<br>0：创建中，1：正常运行。|
|createTime|String|负载均衡实例的创建时间。|
|statusTime|String|负载均衡实例的上次状态转换时间。|
|projectId|Int|负载均衡实例所属的项目 ID， 0表示默认项目。|
|vpcId|Int|私有网络的 ID 的数字部分， 0表示基础网络。|
|subnetId|Int|私有网络的子网 ID 的数字部分，0表示默认子网。|
|openBgp|Int|高防 LB 的标识，1：高防负载均衡 0：非高防负载均衡。|
|snat|Bool|在2016年12月份之前的传统型内网负载均衡都是开启了 snat 的。|
|isolation|Int|0：表示未被隔离，1：表示被隔离。|
|log|String|用户开启日志的信息，日志只有公网属性创建了 HTTP 、HTTPS 监听器的负载均衡才会有日志。|


## 示例

使用默认参数，查询负载均衡实例列表：
```
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancers
&<公共请求参数>
&forward=-1
```

返回
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "loadBalancerSet": [
        {
            "loadBalancerId": "lb-hc1vni0f",
            "unLoadBalancerId": "lb-hc1vni0f",
            "loadBalancerName": "cls-qbesvs66_ng1",
            "loadBalancerType": 2,
            "domain": "cls-qbesvs66-ng1.gz.1251707795.clb.myqcloud.com",
            "loadBalancerVips": [
                "111.230.83.36"
            ],
            "status": 1,
            "createTime": "2017-11-30 14:28:45",
            "statusTime": "2017-11-30 14:29:11",
            "vpcId": 2968,
            "uniqVpcId": "vpc-b2h3xykt",
            "subnetId": 1,
            "projectId": 0,
            "forward": 0,
            "snat": false,
            "openBgp": 0,
            "isolation": 0,
            "log": ""
        }
    ],
    "totalCount": 1
}
```
