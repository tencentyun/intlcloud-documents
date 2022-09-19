## 操作场景
该任务指导您按照标签授权，实现子用户 cvmtest01 只能管理 ins-duglsqg0 的资源级接口权限。
[查看详细操作场景 >>](https://intl.cloud.tencent.com/document/product/598/47825)

## 策略内容
按照标签授权，最终实现上述预期结果时，对应的策略内容如下：
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cvm:*",
                "vpc:DescribeVpcEx",
                "vpc:DescribeNetworkInterfaces"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "game&webpage"
                    ]
                }
            }
        }
    ]
}
```


## 操作步骤
### 步骤1：创建策略并授权
1. 使用管理员账号登录访问管理控制台，在 [策略](https://console.cloud.tencent.com/cam/policy/createV3) 页面，按照标签创建自定义策略（参考 [创建自定义策略 - 按标签授权](https://intl.cloud.tencent.com/document/product/598/35596)）。
	![](https://qcloudimg.tencent-cloud.cn/raw/34feadcd7fe7865521f48909b3f2ab36.png)
	- 授予用户：cvmtest01
	- 绑定标签：game：webpage
	- 操作权限：云服务器的全部操作权限和 VPC 的 DescribeVpcEx 和 DescribeNetworkInterfaces（说明：无法确定涉及的其他接口时，可以参考 [按照资源 ID 授权-步骤3进行验证添加](https://www.tencentcloud.com/document/product/598/47826#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E4.BD.BF.E7.94.A8.E7.AE.A1.E7.90.86.E5.91.98.E8.B4.A6.E5.8F.B7.E8.B0.83.E6.95.B4.E7.AD.96.E7.95.A5.E5.86.85.E5.AE.B9)）      
2. 单击**下一步**，填写策略名称。
3. 单击**保存**，完成授权。
![](https://qcloudimg.tencent-cloud.cn/raw/a9175a9975d4e91bedd13855f54f6a08.png)    


### 步骤2：验证结果
使用子用户 cvmtest01 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index?rid=1)，访问实例列表页面，达到预期效果。
至此，子用户 cvmtest01 可以对实例进行开关机、重启、更名、重置密码等操作。
<img src="https://qcloudimg.tencent-cloud.cn/raw/21d3450e703909023e6ffa18c5920f57.png" >         
