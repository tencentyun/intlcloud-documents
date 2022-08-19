可以在Input List中看到已经添加好的Input，对于需要有特殊配置类型的Input，可以选择**Setting**进行相关设置，如下图：
![](https://qcloudimg.tencent-cloud.cn/raw/ab177f714962ce78c8c311a5e5d189c9.png)

## 音频选择器设置
对于RTP/UDP PUSH类型输入，若负载使用的是MPEGF-TS协议，可能存在多音轨，这里可以根据音频的**Pid**来设置选择需要进行媒体处理和输出的音频。如果不设置，默认会选择随机选择其中一个音频作为输出。此外，在创建一个音频选择器时，首先需要输入选择器名称，并且在相同频道内不得重复。
![](https://qcloudimg.tencent-cloud.cn/raw/b82435f92e7a7081c1d80d7453729f76.png)

>! 
>- PID需要和源流中的PID保持一致。若不匹配，该项选择器则失效，系统会随机选择其中一路音频做为该Pid的最终输出。
>- 当开启输入源的主备容灾（Failover）时，主输入源的Selector配置将自动复用到备输入源中，以确保故障切换后音频的有效性。

## 拉流行为设置
对于PULL类型的输入，您可以设置以下**Source End Behavior**，来控制输入的有效时间：
- **LOOP**：循环拉取输入源。
- **ONCE**：只拉取一次输入源，然后断开。
![](https://qcloudimg.tencent-cloud.cn/raw/cb9adca89713d48324c87a4244a96eee.png)


## 主备容灾设置
如果您需要防止输入源异常断开时影响使用，您可以为RTMP_PUSH/RTP_PUSH类型的输入开启主备容灾功能，从而可以在StreamLive主输入源发生故障时，自动切换到备输入源上。
![](https://qcloudimg.tencent-cloud.cn/raw/83713e5b3dc6269d86d7f1972847bf04.png)

- **Input Failover**：对于需要进行主备容灾的Input，开启**Input Failover**开关。
- **Select Backup Input**：选择一个备用Input，备用Input的类型必须和主Input类型保持一致。
- **Downtime Threshold**：设置故障转移的阈值，单位是毫秒，默认值为3000毫秒，当主输入发生故障时，系统在等待阈值时间后，会自动切换到备用输入上，从而确保整个链路的数据可用性。
- **Input Preference**：设置当主输入恢复后如何进行重新选择。CURRENT_PREFERRED：默认选项，保持当前输入不变。PRIMARY_PREFERRED：主输入优先。即如果当前在使用备输入，主输入源恢复正常后，需要切换到主输入源。
- 点击**Confirm**确认后，回到Input List界面，可以看到**Bind Status**值会发生变化。主输入源为显示为Primary，备输入源会显示为Backup。
![](https://qcloudimg.tencent-cloud.cn/raw/d672160e188307359c705442e009d8f1.png)
>! 
>- 您只能为Input设置一个备输入流，且要求主输入流和备输入流要求输入源类型相同、通道数量相同。
>- 当一个Input被选择为Backup后，该输入的Failover属性将会被自动禁用，即您不能再为该Input设置备份输入。如果想更换两个Input的角色，需要先将第一个Input的Failover属性关掉，然后重新重新设置。
>- 主备容灾设置成功后，会在主流和备流输入名旁边出现“Primary”和“Backup”的标志字段。
>- 备输入流在input list中的位置会自动展示在主输入的下面。


## 其它操作
- **Details**：查看该Input的输入地址和其他基础信息。
- **Set as First**：可以将该Input设置为默认输入，当作为默认输入时将会置顶展示。注意：此操作不能对备输入流进行。
- **Delete**：删除某个输入流。
- **Next**：进入下一步，进行输出配置。


