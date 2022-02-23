ユーザーはStreamLive CSSタイムシフトサービスを使用する前に、CSS、メディアサービスStreamLiveをアクティブ化しておく必要があります。CSSではタイムシフトドメイン名を再生ドメイン名とし、ドメイン名のフローに従って追加します。



### StreamPackage CSSタイムシフト機能のアクティブ化

[チケットを提出](https://console.cloud.tencent.com/workorder/category)してStreamLiveタイムシフト機能のアクティブ化を申請します。ユーザーアカウントのAPPID、タイムシフトドメイン名を提供する必要があります。


### StreamLive CSSタイムシフトの設定

チケットでタイムシフトの設定が完了すると、コンソールまたはAPIによってStreamLiveのOutputGroupのタイムシフト機能を有効にすることができます。タイムシフトドメイン名をバインドします。

>! HLS_ARCHIVEおよびDASH_ARCHIVEのみタイムシフトを有効にできます。

1. StreamLiveコンソールの**Channel Management**ページに進みます
2. 新しいチャネルを作成するか、またはタイムシフトを設定したいチャネルを選択し、「**edit channel**」をクリックします
3. 「**Output settings page**」ページで、「**Basic Information**」-「**Out put Group Type**」を**HLS_ARCHIVE / DASH_ARCHIVE**に設定します 
4. **TimeShift Information**カテゴリーで、タイムシフトを有効にし、タイムシフト時間を入力します

>! タイムシフト時間は300秒から1209600秒の間でなければなりません。

![](https://qcloudimg.tencent-cloud.cn/raw/46388651f1047edb0a1a8b8128ae2e02.png)
