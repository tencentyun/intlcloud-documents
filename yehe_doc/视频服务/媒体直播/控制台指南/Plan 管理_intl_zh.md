在StreamLive中，您可以在频道运行时对频道进行事件处理。具体方式是通过与频道关联Plan来设置执行时间、执行事件，那在该执行时间点时，频道将开始执行事件。

## 查看事件
在**Channel**中，选择需要设置Plan的频道，点击频道名称进入频道详情页面，选择详情页中的**Plan**标签页，即可看到当前频道下的**Plan**列表：
![](https://qcloudimg.tencent-cloud.cn/raw/56bfba4ce4744f143c35d1e354137ec2.png)


## 创建事件
点击页面左上角的**Create Event**，来创建新的事件。当前可支持的事件类型包括：
- **Input Switch**：对运行中的频道，切换正在接收的输入。
- **Time Record**:  对正在运行的频道，执行分时段录制。
- **SCTE35 Time Signal**：设置SCTE-35 time_signal事件。
- **SCTE35 Splice Insert**：设置SCTE-5 splice_insert事件。
- **SCTE35 Return to Network**：设置SCTE-35 return to network事件。

### 创建输入切换类型的事件
![](https://qcloudimg.tencent-cloud.cn/raw/1d3a818301802f9756723b7613530ff0.png)
- **Event Type**：选择Input Switch。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **Start Type**：可选择Fixed Time或者Immediate。Fixed Time: 在指定的特定时间执行事件，该时间为UTC时间，指定的时间必须在事件开始前至少10秒且不能小于当前时间。Immediate：立即执行设定的事件。
- **Input Attachment**：选择已在该频道绑定并想切换的Input名称。


### 创建定时录制类型的事件
![](https://qcloudimg.tencent-cloud.cn/raw/fb95ca51acbcb52561e06323c7585f74.png)
- **Event Type**：选择Time Record。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **OutputGroupName**：选择需要进行录制的OutputGroup名称，具体名称可在Output Group Setting页面查看。
- **ManifestName**：输入录制生成的Mainfest文件名。无需输入.m3u8 或.mpd后缀。
- **DestinationUrl**：输入需要保存文件的COS地址。
- **Timing**：选择录制的时间段，该时间为UTC时间。


对于SCTE-35类型的事件，可以先参考官方文档《SCTE STANDARD - SCTE 35 2022》。
### 创建SCTE-35 Time Signal事件
![](https://qcloudimg.tencent-cloud.cn/raw/8131d583336c1a07c561ed63b184c011.png)
- **Event Type**：选择SCTE-35 Time Signal。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **Start Type**：可选择Fixed Time或者Immediate。Fixed Time: 在指定的特定时间执行事件，该时间为UTC时间，指定的时间必须在事件开始前至少10秒且不能小于当前时间。Immediate：立即执行设定的事件。

其中，可以通过**Add**增加多个SCTE-35 Descriptor。
![](https://qcloudimg.tencent-cloud.cn/raw/700fe3d0d3b8ff43354bad9eba9481a2.png)

对于每个SCTE-35 Descriptor支持配置以下信息：
![](https://qcloudimg.tencent-cloud.cn/raw/7d6b78592a0dc65f6d8ccb788621c6f0.png)

- **Segmentation Event ID**：Event标识。支持整数，最小值为0、最大值为4294967295。
- **Segmentation Event Cancel Indicator**：标明前一个Event是否取消。
- **Delivery Restrictions**：设置播放端限制。
- **Segmentation Duration**：Segment时长。单位为90kHz，支持整数，最小值为0、最大值为1099511627775。
- **Segmentation UPID Type**：对应SCTE-35 segmentation_upid_type参数。支持整数，最小值为0、最大值为255。
- **Segmentation UPID**：对应SCTE-35 segmentation_upid参数。支持字符串，最大255个字符。只有在Segmentation UPID Type 为0时  Segmentation UPID才允许为空。
- **Segmentation Type ID**：对应SCTE-35 segmentation_type_id参数。支持整数，最小值为0、最大值为255。
- **Segment Num**：对应SCTE-35 segment_num参数。支持整数，最小值为0、最大值为255。
- **Segments Expected**：对应SCTE-35 segment_expected参数。支持整数，最小值为0、最大值为255。
- **Subsegment Num**：对应SCTE-35 sub_segment_num参数。支持整数，最小值为0、最大值为255。
- **Subsegments Expected**：对应 SCTE-35 sub_segments_expected参数。支持整数，最小值为0、最大值为255。

### 创建SCTE-35 Splice Insert事件
![](https://qcloudimg.tencent-cloud.cn/raw/60de004766d426563b929e69579345f2.png)
- **Event Type**：选择SCTE-35 Splice Insert。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **Start Type**：可选择Fixed Time或者Immediate。Fixed Time: 在指定的特定时间执行事件，该时间为UTC时间，指定的时间必须在事件开始前至少10秒且不能小于当前时间。Immediate：立即执行设定的事件。
- **Splice Event ID**：Event标识。支持整数，最小值为0、最大值为4294967295。
- **Duration**：Segment时长。单位为90kHz，支持整数，最小值为0、最大值为8589934591。

### 创建SCTE-35 Return to Network 事件
![](https://qcloudimg.tencent-cloud.cn/raw/66fc49414496b2dc5caf4fb5cc7bf7d2.png)
- **Event Type**：选择SCTE-35 Return to Network。
- **Event Name**：输入该事件的名称，可支持数字、下划线、大小写字母，最大长度为32个字符。事件名称在该频道下不能重复。
- **Start Type**：可选择Fixed Time或者Immediate。Fixed Time: 在指定的特定时间执行事件，该时间为UTC时间，指定的时间必须在事件开始前至少10秒且不能小于当前时间。Immediate：立即执行设定的事件。
- **Splice Event ID**：Event标识。支持整数，最小值为0、最大值为4294967295。

## 删除事件
选择需要删除的事件，在该事件最右侧**Operation**中点击**Delete**按钮，在弹出的确认框中点击**Confirm**后即可删除该事件。正在执行中的Event无法删除，只有未开始或已执行完的Event才能进行删除操作。
![](https://qcloudimg.tencent-cloud.cn/raw/6a12ab835292e5ceb7af23a849991ce7.png)