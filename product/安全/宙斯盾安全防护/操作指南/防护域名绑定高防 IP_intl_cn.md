
在 [宙斯盾高防产品控制台](https://console.cloud.tencent.com/gamesec) 左侧目录中，选择 “业务域名列表”，在右侧页面中，单击 “创建业务和域名” 创建业务，并自动生成防护域名。用户可通过将业务域名 CNAME 到防护域名接入高防。

## 流程图
![](https://main.qcloudimg.com/raw/320d44047dc9745f8d802bbe595b6a17.png)

## 防护域名绑定高防 IP 的流程
1. **创建业务**
a. 单击【业务域名列表】，在 “业务域名列表” 下，单击【创建业务和域名】。
![1](https://main.qcloudimg.com/raw/26808fa32108113f2ab584deeca6426b.png)
b. 填写好相关信息，单击【创建】，创建成功后立即在 “业务域名列表” 生成业务和免费的防护域名。
![2](https://main.qcloudimg.com/raw/d5b8306d4884245e470120490b0d4ac4.png)
2. **添加高防 IP**
a. 在业务域名列表管理页下，单击 “添加  IP”，跳转到业务详情页。
![3](https://main.qcloudimg.com/raw/224f702e08ca2d2d2d90ea98a0a83616.png)
b. 在业务详情页下的 IP 资源和解析设置单击 “添加 IP”。
![4](https://main.qcloudimg.com/raw/db021706af6b3986fd284825634ad3d4.png)
c. 勾选高防 IP，单击【确定】。
![5](https://main.qcloudimg.com/raw/69a94067fe25cc514bb66001936ad313.png)
3. **开启域名解析**
添加高防 IP 成功后，开启 “域名解析”。防护域名提供智能解析，即根据用户来源 IP 解析到对应线路的 IP。如电信用户会解析到电信的高防 IP，联通用户会解析到联通的高防 IP 等。若某一线路的高防 IP 因攻击超峰被封堵，则会自动解析到其他可用的高防 IP。
BGP 线路优先开关开启时，若有绑定 BGP 线路 IP，则防护域名会优先调度所有业务请求解析到 BGP 的 IP 地址。（其他开启解析开关的三网高防 IP 处于备用状态）。若发生大流量攻击导致 BGP 高防 IP 被封堵，则系统会智能调度业务请求到开启域名解析开关的三网高防 IP，以提供高带宽防护能力。若 BGP 高防 IP 解除封堵，则系统会恢复将所有业务请求调度到 BGP 高防 IP。
![](https://main.qcloudimg.com/raw/545082a6e322da966ac0dd8b640dbf6b.png)
4. **主域名 CNAME 到防护域名**
线路解析开启后，业务主域名可通过 CNAME 到防护域名，智能解析到高防 IP。
用户验证，比如在本地用 ping 或者 nslookup 方式检查是否域名能够解析到高防 IP。
