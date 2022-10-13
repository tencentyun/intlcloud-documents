StreamLiveはHLS/DASHのTencent Cloud COSへのアーカイブをサポートしています。

設定方法は、**Channel**の**Output Group Setting**で、**Output Group Type**にHLS_ARCHIVE/DASH_ARCHIVEを選択し、**COS Destination**にストレージパスを含むCOS URLアドレスを入力します。Channelの実行中、ライブストリーミングファイルはCOSにリアルタイムにアーカイブされます。
![](https://qcloudimg.tencent-cloud.cn/raw/2d18dc7f0100da76ffc40df26ea7e158.png)

アーカイブとライブストリーミングリレーの違いは、アーカイブの場合、Manifestファイルの内容にはチャネルの起動から終了時点までのすべてのオーディオビデオファイルリストが含まれるのに対し、ライブストリーミングリレーでは、Manifestファイルの内容はリアルタイムに更新され、最新部分のオーディオビデオファイルリストのみが含まれるという点にあります。

HLSおよびDASHのメインManifestファイルの形式は次のとおりです。
- HLS:${COS Desination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.m3u8
- DASH:${COS Desination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.mpd



