## 概述

日志服务（Cloud Log Service，CLS）支持使用 LogListener 采集腾讯云云服务器（Cloud Virtual Machine，CVM）实例上的日志，在进行日志采集前，需要在 CVM 上部署安装 LogListener。为了更快捷的支持大量的 CVM 部署安装 LogListener，现支持用户在控制台选择 CVM 实例，接口批量下发部署 LogListener 任务，自动完成 LogListener 的安装部署（包括 accesskey，ID 配置，地域配置）。

## 前提条件

CVM 已安装腾讯云自动化助手（TencentCloud Automation Tools，TAT）。

## 操作步骤
1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 在左侧导航栏中，单击**概览**，进入概览页面。
3. 在**快速接入 > 云产品日志**栏中，单击**云服务器CVM**。

4. 在实例批量部署页面，勾选需要部署 LogListener 的 CVM 实例，输入 SecretId 信息（SecretId 和 SecretKey），并根据实际自定义设置机器标识，设置高级配置项。

5. 单击**下一步**。
6. 在安装实例页面，待**执行状态**变为**已完成**，即安装完成后，单击**下一步**。
>? 如果安装失败，可以将鼠标移动到安装实例的**执行状态**查看失败原因。
> 

7. 在导入机器组页面，根据实际需求，选择现有机器组或者创建机器组，单击**导入**，即可完成批量安装部署。

>? 批量安装的 LogListener 为2.6.0及以上版本。
>



