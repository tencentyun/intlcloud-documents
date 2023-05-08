## 概述

日志服务（Cloud Log Service，CLS）支持使用 LogListener 采集腾讯云云服务器（Cloud Virtual Machine，CVM）与轻量应用服务器（TencentCloud Lighthouse）实例上的日志，在进行日志采集前，需要在 CVM 或 Lighthouse上部署安装 LogListener。为了更快捷的支持大量的 CVM 或 Lighthouse 部署安装 LogListener，现支持用户在控制台选择 CVM 或 Lighthouse 实例，接口批量下发部署 LogListener 任务，自动完成 LogListener 的安装部署（包括 accesskey、ID 配置、地域配置）。

## 前提条件

CVM 或 Lighthouse 已 [安装腾讯云自动化助手（TencentCloud Automation Tools，TAT）](https://intl.cloud.tencent.com/document/product/1147/46042)。

## 操作步骤

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 在左侧导航栏中，单击**概览机器组管理**，进入机器组管理页面。
3. 在页面右上方点击**实例批量部署**。

4. 在实例批量部署页面， 选择服务器类型：CVM 或 Lighthouse。（支持同时为 CVM 和 Lighthouse 服务器批量部署 LogListener）

5. 进一步勾选需要部署 LogListener 的 CVM 或 Lighthouse 实例，输入 SecretId 信息（SecretId 和 SecretKey），并根据需求自定义设置高级配置项 - 机器标识。

> ?
> - 安装LogListener需要提供SecretId和SecretKey，密钥信息用于上传日志，[查看获取方式](https://console.cloud.tencent.com/cam/capi)。
> - 请确保填写密钥信息对应的账号拥有日志上传的权限。 如何配置权限请参考[账号授权](https://www.tencentcloud.com/document/product/614/32854)。
> - 如果您的机器 IP 地址经常变动, 建议配置机器标识，详情请查看 [通过配置机器标识创建机器组](https://intl.cloud.tencent.com/document/product/614/17412)。



6. 单击**下一步**。
7. 在安装实例页面，待**执行状态**变为**已完成**，即安装完成后，单击**下一步**。
>? 如果安装失败，可以将鼠标移动到安装实例的**执行状态**查看失败原因。



8. 在导入机器组页面，根据实际需求，选择现有机器组或者创建机器组，单击**导入**，即可完成批量安装部署。


>? 批量安装的 LogListener 为2.6.0及以上版本。
