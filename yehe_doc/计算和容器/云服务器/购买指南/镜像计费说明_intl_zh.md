本文档将对云服务器镜像的费用进行说明。

## 计费概述
使用镜像可能会产生一定的费用，各类型镜像费用说明如下：
<table class="tg">
<thead>
  <tr>
    <th width="10%">镜像类型</th>
    <th width="90%">说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">公共镜像</td>
    <td class="tg-0pky">包含开源镜像及商业镜像：<br><li>开源镜像均免费提供服务。</li><li>商业镜像会产生一定的 License 许可费用，请以实际下单时为准，目前公共镜像包含 Windows Server、Red Hat Enterprise Linux 两款商业镜像，请您继续阅读本文档查看详细说明。</td></li>
  </tr>
  <tr>
    <td class="tg-0pky">自定义镜像</td>
    <td class="tg-0pky">计费包含以下两部分：<br><li>快照费用：由于镜像底层使用了云硬盘快照服务，保留自定义镜像会产生一定的快照费用。国内地域提供80 GB 的  <a href="https://intl.cloud.tencent.com/document/product/362/32415">赠送额度</a> ，超额后将按容量计费，详情请参见  <a href="https://intl.cloud.tencent.com/document/product/362/32415">快照计费概述</a>。</li><li>镜像费用：若自定义镜像的最终来源为付费镜像，且您使用了该自定义镜像，则需要收取镜像费用。</li></td>
  </tr>
  <tr>
    <td class="tg-0pky">共享镜像</td>
    <td class="tg-0pky">共享镜像是将创建好的自定义镜像分享给其他腾讯云账户的镜像。若该镜像最终来源为付费镜像且使用了该共享镜像，则收取镜像费用。</td>
  </tr>
</tbody>
</table>

<span id="redhat"></span>

## Windows Server 镜像计费说明
#### 计费示例

示例背景：新加坡一区，实例为标准型 S5.MEDIUM2，选择按量计费模式。
- Windows 实例费用为0.05美元/小时，“镜像”项不单独计费，即显示为0美元。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)


## Red Hat Enterprise Linux 镜像计费说明
Red Hat Enterprise Linux 为商业操作系统，通过腾讯云获取正版授权时（以下简称**腾讯云授权**）将收取镜像费用（包含 License 费用），不同地域同价。
<dx-alert infotype="explain" title="">
- 腾讯云授权的 Red Hat Enterprise Linux 镜像，使用 Red Hat 官方正版授权，您在腾讯云购买授权时不支持其它形式的折扣（包括竞价实例的折扣）、不支持使用代金券抵扣；
- 您在购买云服务器 CVM 时，选中已经通过 Red Hat Enterprise Linux 认证的实例类型，即可选用 Red Hat Enterprise Linux 镜像，您可以点击 [Red Hat Enterprise Linux 镜像使用指引](https://www.tencentcloud.com/document/product/213/55135) 查看支持的镜像版本和实例类型。
- Red Hat Enterprise Linux 镜像处于内测阶段，您可通过 [提交工单](https://console.tencentcloud.com/workorder/category) 获取使用权限。
</dx-alert>

###  腾讯云授权的Red Hat Enterprise Linux 镜像价格如下表所示

| 实例规格 | 按量计费（小时计费，小时结算，不足1小时按照1小时计费）|
|---------|---------|
| 4 vCPU 及以下 | 0.06美元/小时 |
| 4 vCPU 以上 | 0.13美元/小时 |

<dx-alert infotype="explain" title="">
若您创建**竞价实例**时选用腾讯云授权的 Red Hat Enterprise Linux 镜像，将按照按量计费的价格进行计费，且镜像不享受**竞价实例**的折扣。
</dx-alert>

### 重装系统镜像计费说明
- 支持 Red Hat Enterprise Linux 操作系统与其他操作系统互相重装（说明：境外地域不支持与Windows互相重装），将根据重装的目标镜像计算费用。
- 采用按量计费计费模式的实例，重装系统为腾讯云授权的Red Hat Enterprise Linux 操作系统后，镜像按照按量计费的价格进行计费，在实例的一个计费周期内，使用过腾讯云授权的Red Hat Enterprise Linux 镜像，则该计费周期会产生镜像授权费用。
**案例**：
2023年1月1日上午8:00购买一台CentOS实例，8:00～9:00的计费周期不产生镜像授权费用；在上午9:30，对该实例重装系统选用Red Hat Enterprise Linux商业镜像，9:00～10:00的计费周期需要支付镜像授权费用；在上午10:30，对该实例重装系统为CentOS；10:00～11:00的计费周期需要支持镜像授权费用；11:00之后则不需要支付镜像授权费用。

### [预留实例](https://www.tencentcloud.com/document/product/213/30571)模式下的镜像计费说明
- 选用Linux平台的预留实例，不包含Red Hat Enterprise Linux镜像授权费用，镜像授权费用需单独扣费。
- 使用腾讯云授权的Red Hat Enterprise Linux镜像的按量计费实例，配置与预留实例相匹配时，实例可以享受账单折扣，镜像授权费用不享受账单折扣，镜像授权费用需单独扣费。


### 变更配置

使用 腾讯云授权的Red Hat Enterprise Linux 商业操作系统的实例，暂不支持调整配置，暂不支持调整计费模式。



