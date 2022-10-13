StreamLiveではHLS&DASHタイムシフトをサポートしています。Cloud Streaming Services（CSS）と併せて使用する必要があります。

タイムシフトの設定手順は次のとおりです。
1. CSSをアクティブ化します。CSSでタイムシフトドメイン名を再生ドメイン名として追加し、CNAMEを設定します。
2. チケットを提出してStreamLiveタイムシフト機能のアクティブ化を申請します。ユーザーアカウントのAPPID、タイムシフトドメイン名を提供する必要があります。
3. バックエンドの設定がアクティブ化されてから、Channelの**TimeShift Information**でスイッチ**Switch**をオンにし、タイムシフトドメイン名を**PlayDomain**に入力し、タイムシフト時間**Startover Window**（単位は秒）を設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/661fcb79490e1de61a10b5d7ab90f494.png)

タイムシフト再生アドレスの形式は次のとおりです。
- HLS:http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.m3u8?txMaster=1&delay={$delay}"
- DASH:http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.mpd?delay={$delay}"

>?
>- ${region}はStreamLiveのChannel所属リージョンに対応します。マッピング関係は、Bangkok -> ap-bangkok；Mumbai -> ap-mumbai；Seoul->ap-seoul；Tokyo->ap-tokyo；Frankfurt->eu-frankfurtとなります。
>- ${delay}はタイムシフト間隔であり、単位は秒です。最小値は180、最大値はStartover Windowです。



例：
- HLS:http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.m3u8?txMaster=1&delay=180
- DASH:http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.mpd?delay=180

