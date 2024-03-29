## 操作场景
DTS 支持通过事件总线平台对数据迁移、数据同步、数据订阅任务过程中的事件进行监控并设置告警规则，在事件触发时，及时通知用户采取措施。 

本操作用于指导用户设置事件告警的通知规则，包括事件告警的范围、通知的形式、通知的时段、通知的用户群组等。 

## 操作步骤
1. 登录 [事件总线控制台](https://console.cloud.tencent.com/eb)。
2. 首次登录系统会提醒用户进行授权，请参考 [开通事件总线](https://intl.cloud.tencent.com/document/product/1108/42272) 进行操作，如果已授权请跳过此步骤。
3. 在左侧导航选择**事件规则**页签，然后在右侧地域选择**广州**，事件集选择 **default**，单击**新建事件规则**。
因为云服务产品的事件集默认统一存储在广州，所以此处的地域和事件集不可选择其他内容。
![](https://qcloudimg.tencent-cloud.cn/raw/01bd03e8bdad4b11276e2a8fdfa516a9.png)
4. 配置事件规则，完成后单击**下一步**。
 - **NewDTS（迁移/同步/订阅 Kafka 版）**
    ![](https://qcloudimg.tencent-cloud.cn/raw/5feb1408d29bc9c825423fd77449a30d.png)
 - **老版本 DTS（仅数据订阅）**
    ![](https://qcloudimg.tencent-cloud.cn/raw/29819a0c4d5a00137927c171c49ab374.png)
<table>
<thead><tr><th>参数</th><th>配置说明</th></tr></thead>
<tbody><tr>
<td>规则名称</td>
<td>请输入能区分业务的规则名称，配置后不可修改。</td></tr>
<tr>
<td>事件模式</td>
<td>请选择<strong>云服务预设事件</strong>。</td></tr>
<tr>
<td>云服务类型</td>
<td><ul><li>对于 NewDTS 任务（迁移/同步/订阅 Kafka 版），请选择<strong>数据传输服务（DTS）</strong>。</li><li>对于老版本 DTS 任务（仅支持订阅），请选择<strong>数据订阅（DTS）</strong>。</li></ul></td></tr>
<tr>
<td>事件类型</td>
<td><ul><li>对于 NewDTS 任务（迁移/同步/订阅 Kafka 版），请勾选<strong>数据迁移任务中断</strong>，<strong>数据同步任务中断</strong>，<strong>数据订阅任务中断</strong>。</li><li>对于老版本 DTS 任务（仅支持订阅），默认选择<strong>全部事件</strong>。</li></ul></td></tr>
</tbody></table>
5. 配置事件的通知方式、接收对象、渠道等，触发方式选择**消息推送**。配置完成后单击**完成**。
如果需要新增接收用户/用户组，请先在 [访问管理](https://console.cloud.tencent.com/cam) 中进行配置，然后在本步骤中的**接收对象**才可选择。
如果需要配置不同的触发方式，可以单击最下方的**添加**增加事件目标。
6. 返回事件规则列表，确认创建的事件规则已启动 。后续当任务异常触发告警时，用户即可接收到消息通知。
![](https://qcloudimg.tencent-cloud.cn/raw/cda96cd6cc44dbd7c139bab1a13e0972.png)

