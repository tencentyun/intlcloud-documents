チャネル入力は、StreamLiveのメディアストリーム入力チャネルであり、通常はセキュリティグループとStreamLiveチャネルに関連付けられています。

## 前提条件
- [StreamLive](https://www.tencentcloud.com/products/mdl)が有効化されています。 
- [StreamLiveコンソール](https://console.intl.cloud.tencent.com/mdl/input)にログインしています。

## Input管理
左側のナビゲーションバーで**Input Management**をクリックして、作成されたinput名、タイプ、バインディング状態、IDなどの情報を表示できます。各Inputは通常、セキュリティグループとStreamLiveチャネルに関連付けることができ、チャネルに関連付けられたInput状態はattachedが示されています。各入力には、チャネルの2つのコネクションに対応する2つの物理的に分離されたコネクションAとBがあり、アップストリームの可用性を確保するためにストリームを同時にプッシュできます。

![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


## Inputの作成
チャネル入力には、PULLとPUSHの2つの入力方法があります。Inputを作成する必要がある場合は、ページの左上隅にある【Create Input】ボタンをクリックし、ポップアップウィンドウで設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/0a58997dcc3241c77a07a05a458569c4.png)

- **Name**：Input名です。ユーザーがカスタマイズ可能です。1～32桁の数字、大文字と小文字、およびアンダーバー「_」をサポートできます。
- **Type**：Inputタイプです。現在、RTMP_PUSH、RTP_PUSH、RTP-FEC_PUSH、UDP_PUSH、SRT_PUSH、RTMP_PULL、HLS_PULL、MP4_PULL、RTSP_PULL、SRT_PULLなどのプロトコルをサポートしています。
- **Security Group**：入力タイプがPUSHの場合、セキュリティ検証のためにInputセキュリティグループをバインディングしてください。

##### Type：RTMP_PUSH
TypeにRTMP_PUSHを選択した場合は、それぞれapplication nameとstream nameであるDestinationを入力してください。
![](https://qcloudimg.tencent-cloud.cn/raw/0f449d8038bed66bcada1faa0481c92c.png)

##### Type：SRT_PUSH
TypeにSRT_PUSHを選択した場合は、Destinationはstreamidを表しますが、必須ではありません。
![](https://qcloudimg.tencent-cloud.cn/raw/f4a9ec18c0de6d127fce99d8c91aad89.png)

##### Type：PULL
TypeにPULLタイプを選択した場合は、PULLのソースとしてInputAddressを入力してください。
![](https://qcloudimg.tencent-cloud.cn/raw/28291755993b3efb3b3bdd4b63bfd40d.png)


## Inputの修正
Inputを修正する必要がある場合は、修正の必要があるInputの右側にある**Edit**をクリックし、ポップアップウィンドウで修正し、修正完了後、**Confirm**をクリックして修正を完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/45f415840a5b45d0a97baa965f05a45c.png)

## Inputの削除
Inputを削除する必要がある場合は、削除を必要とするInputの右側にある**Delete**をクリックし、ポップアップウィンドウで**Confirm**をクリックして削除を完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


>! 
> - コンソールは、デフォルトで最大5つのinputの存在のみをサポートします。
> - 入力のメディアソースには、現在、少なくとも1つのビデオデータチャネルが含まれている必要があります。
> - MPEG-TS多重化チャネルを使用する場合、最大8チャネルを同時に送信できます。

