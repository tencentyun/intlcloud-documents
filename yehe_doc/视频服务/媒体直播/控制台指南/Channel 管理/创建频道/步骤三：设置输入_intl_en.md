The input list shows the inputs bound. You can click **Setting** to configure an input.
![](https://qcloudimg.tencent-cloud.cn/raw/ab177f714962ce78c8c311a5e5d189c9.png)

## Audio Selector
For RTP/UDP PUSH inputs, if MPEG-TS is used, there may be multiple audio tracks. You can specify the audio track to process and output by entering the **PID**. If you don’t set this, an audio track will be selected randomly. The name of an audio selector must be unique across the channel.
![](https://qcloudimg.tencent-cloud.cn/raw/b82435f92e7a7081c1d80d7453729f76.png)

>! 
>- Make sure the PID you enter is the same as that of the source stream, or the audio selector will fail to work, and the system will randomly select an audio track to output.
>- If input failover is enabled, the audio selectors configured for the primary input will apply to the backup input as well.

## Source End Behavior
You can set the **Source End Behavior** of a PULL input to tell StreamLive what to do after the input ends.
- **LOOP**: Pulls the input again after it ends.
- **ONCE**: Pulls the input only once.
![](https://qcloudimg.tencent-cloud.cn/raw/cb9adca89713d48324c87a4244a96eee.png)


## Failover
To prevent interruption of service caused by input exceptions, you can enable failover for RTMP_PUSH/RTP_PUSH inputs. If the primary input is down, StreamLive will automatically switch to the backup input.
![](https://qcloudimg.tencent-cloud.cn/raw/83713e5b3dc6269d86d7f1972847bf04.png)

- **Input Failover**: Toggle this on if you want to enable failover for an input.
- **Select Backup Input**: Select a backup input, whose type must be the same as the primary input.
- **Downtime Threshold**: Set the wait time (milliseconds) for failover. If the primary input is down, StreamLive will switch to the backup input after the wait time elapses to ensure data availability. The default is 3,000 ms.
- **Input Preference**: Set whether to switch back to the primary input after it recovers. **CURRENT_PREFERRED** (default): Continue to use the current input; **PRIMARY_PREFERRED**: Switch back to the primary input after it recovers.
- Click **Confirm**. In the input list, you will see that the **Bind Status** of the primary input has changed to **Primary** and that of the backup input has changed to **Backup**.
![](https://qcloudimg.tencent-cloud.cn/raw/d672160e188307359c705442e009d8f1.png)
>! 
>- You can specify only one backup for each input, and it must be of the same type and have the same number of pipelines as the primary input.
>- Once an input is used as a backup, the failover feature will be disabled for the input automatically, which means that you cannot configure a backup for this input. To change the primary and backup roles of two inputs, you must disable failover for the primary input first.
>- After successful configuration, **Primary** and **Backup** will appear next to the names of the primary and backup inputs.
>- In the input list, the backup input will appear below the primary input.


## Other operations
- Click **Details** to view the source address and other information of an input.
- Click **Set as First** to set an input as the default. The input will be moved to the top of the list. You cannot set a backup input as the default.
- Click **Delete** to remove an input.
- Click **Next** to proceed to the next step and configure outputs.


