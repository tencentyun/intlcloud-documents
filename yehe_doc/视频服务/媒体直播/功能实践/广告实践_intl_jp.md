StreamLiveはライブストリームに広告を挿入する機能をサポートしています。ニーズに応じて、次のいくつかの方法で広告統合ソリューションを実現できます。

1. 代替画像方式
VODファイルまたはライブストリーミングリンクを事前に準備し、これらの入力をすべて事前にchannel下にバインドしておきます。その後、Plan管理ページでInput Switchイベントを作成し、ある決まった時刻またはイベント追加後にただちに広告挿入アクションが実行されるようにします。下の図は、現在のライブストリームに、指定の時刻にVODファイルを挿入する場合の例です。
![](https://qcloudimg.tencent-cloud.cn/raw/0e5789754fc7fd86e362f55adbe30e8b.png)
utc時刻が指定の時刻に達すると、ライブストリーミングの入力ソースがこのinputに切り替わり、指定の広告ファイルを再生します。ファイルの再生が終了すると、ライブストリームはまた元のライブストリーミングソースに自動的に切り替わります。プロセスはすべて自動で行われ、手動の操作は必要ありません。切り替えるファイルを事前に設定しておくだけで実現できます。

2. SCTE-35方式
MPEG-2 TSストリームをライブストリーミングの入力ソースとして用いる場合も、ソース内にSCTE-35のpayloadを含めることができます。システムはその中の情報を自動認識し、出力での表示に適した情報に変換し、プレーヤーが認識できる標準の方式を提供し、広告ソースにリダイレクトします。SCTE-35機能の有効化は非常に簡単で、対応するOutputでSCTE-35伝達機能をオンにするだけです。具体的な設定についてはSCTE-35のセクションをご参照ください。
