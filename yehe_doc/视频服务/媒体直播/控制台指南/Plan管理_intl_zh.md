在StreamLive中，您可以在频道运行时对频道进行事件处理。具体方式是通过与频道关联Plan来设置执行时间、执行事件，那在该执行时间点时，频道将开始执行事件。

## 查看事件
在**Channel Management**中，选择需要设置Plan的频道，点击频道名称进入频道详情页面，选择详情页中的**Plan**标签页，即可看到当前频道下的**Plan**列表：
![](https://qcloudimg.tencent-cloud.cn/raw/1dd3eebf1e4e7714c29a1302d65a514b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/907a629dac8736d4780d411f2988d33f.png)

## 创建事件
点击页面左上角的**Create Event**，来创建新的事件。当前可支持的事件类型包括：
- Input Switch：对运行中的频道，切换正在接收的输入。
- Time Record:  对正在运行的频道，执行分时段录制。

### 创建输入切换类型的事件
<img src="https://qcloudimg.tencent-cloud.cn/raw/8136ad53ef809a22070e80f29a86cf84.png" style="zoom:80%;" />

- **Event Type**：选择Input Switch。
- **Input Attachment**：选择已在该频道绑定并想切换的Input名称。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **Start Type**：可选择Fixed Time或者Immediate。Fixed Time: 在指定的特定时间执行事件，该时间为UTC时间，指定的时间必须在事件开始前至少10秒且不能小于当前时间。Immediate：立即执行设定的事件。

### 创建定时录制类型的事件
<img src="https://qcloudimg.tencent-cloud.cn/raw/395c7b5bc4023a9160ada53913eea58c.png" style="zoom:80%;" />

- **Event Type**：选择Time Record。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **OutputGroupName**：选择需要进行录制的OutputGroup名称，具体名称可在Output Group Setting页面查看。
- **ManifestName**：输入录制生成的Mainfest文件名。无需输入.m3u8 或.mpd后缀。
- **DestinationUrl**：输入需要保存文件的COS地址。
- **Timing**：选择录制的时间段，该时间为UTC时间。

## 删除事件
选择需要删除的事件，在该事件最右侧**Operation**中点击**Delete**按钮，在弹出的确认框中点击**Confirm**后即可删除该事件。正在执行中的Event无法删除，只有未开始或已执行完的Event才能进行删除操作。
![](https://qcloudimg.tencent-cloud.cn/raw/dae329be1090cbeb1b1705fe98fdef3d.png)