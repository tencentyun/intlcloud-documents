### CNAME 域名
CNAME 域名（CNAME domain name）在腾讯云 ECDN 控制台接入加速域名后，系统会为加速域名分配一个“CNAME 域名”（域名后缀为：```.ecdn.dnsv1.com```）。用户需要在域名服务商处，添加一条  CNAME 记录，记录生效后，域名解析的工作就正式转向腾讯云 ECDN，该域名所有的请求都将转向腾讯云 ECDN 的节点。
下图描述了 **源站域名/IP**、**加速域名**、**CNAME 域名**，三者在用户发起一次请求到达源站过程中出现的次序：
![](https://main.qcloudimg.com/raw/333d3a43e95f272787bd45332cca21fd.jpg)
用户访问加速域名，域名被解析到加速节点的 CNAME 域名上，经过腾讯云 ECDN 网络加速后到达源站。

### 加速域名
加速域名（accelerated domain name）区别于源站域名（domain name of origin server），是您提供给 ECDN 加速节点进行 CNAME 的域名。

>源站域名不能与加速域名相同。

### 源站域名
源站域名（domain name of origin server）即客户的业务服务器的域名。
### 源站 IP
源站 IP（IP of origin server）即客户的业务服务器的 IP 地址。




