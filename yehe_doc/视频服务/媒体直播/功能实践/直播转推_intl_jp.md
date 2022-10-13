StreamLiveでは、HTTP PUT方式による、ライブストリーム（HLS/DASH）のHTTPサーバーへの出力をサポートしています。

設定方法はChannelの**Output Group Setting**で、**Output Group Type**にHLS/DASHを選択し、**Destination**にプッシュターゲットURLパスを入力します。Channelの実行中、ライブストリーミングファイルはターゲットURLにリアルタイムにプッシュされます。
![](https://qcloudimg.tencent-cloud.cn/raw/f03e405e1b2ebd07285e28e6b5fd1f49.png)

アーカイブとライブストリーミングリレーの違いは、アーカイブの場合、Manifestファイルの内容にはチャネルの起動から終了時点までのすべてのオーディオビデオファイルリストが含まれるのに対し、ライブストリーミングリレーでは、Manifestファイルの内容はリアルタイムに更新され、最新部分のオーディオビデオファイルリストのみが含まれるという点にあります。

HLSおよびDASHリレーのメインManifestファイルの形式は次のとおりです。
- HLS:${Destination}/${OutputGroupName}.m3u8
- DASH:${Destination}/${OutputGroupName}.mpd

プッシュはHTTP認証もサポートしています。Destinationで**Authentication**を有効にし、関連の認証情報を入力すれば完了です。
