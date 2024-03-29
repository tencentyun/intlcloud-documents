如果公司内部有外网访问限制，需要添加防火墙白名单才能访问，相关的规则如下：

### 客户端 Native SDK（版本号≥2.2）

**防火墙端口：**

|  端口类型 | 白名单项目 |
|---------|---------|
| TCP 端口 | 443 |
| UDP 端口 | 8000 |


**域名白名单：**
```
tcloud.tim.qq.com
gmeconf.qcloud.com
yun.tim.qq.com
gmeosconf.qcloud.com
sg.global.gme.qcloud.com
```

>!
> - 因为腾讯云服务端 IP 地址是动态更新的，并不是固定的一批 IP 地址，所以我们无法提供固定的一组 IP 列表给您。
> - Windows XP 下使用 GME SDK 还需添加以下防火墙白名单。

**防火墙端口：**

|  端口类型 | 白名单项目 |
|---------|---------|
| TCP 端口 | 15000|

**域名白名单：**

```
cloud.tim.qq.com
openmsf.3g.qq.com
```


### 使用 H5 SDK

**防火墙端口：**

| 端口类型 | 白名单项目 |
|---------|---------|
| TCP 端口 | 443,8687 |
| UDP 端口 |8000；8800；843；443|

**域名白名单：**

```
qcloud.rtc.qq.com
rtc.qcloud.qq.com
```


### 使用语音消息及转文字服务

**防火墙端口：**

| 端口类型 | 白名单项目 |
|---------|---------|
| TCP 端口 | 80，443|

**域名白名单：**

```
gmespeech.qcloud.com
yun.tim.qq.com
gmeconf.qcloud.com
```
