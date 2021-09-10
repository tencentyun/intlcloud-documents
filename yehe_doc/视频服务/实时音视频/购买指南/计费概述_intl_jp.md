Tencent Real-Time Communication （TRTC）は、サービスタイプに応じて**基本サービス**と**付加価値サービス**の2つのタイプに分かれます。

## 基本サービス

基本サービスは、具体的なユースケースによって、ボイス・インタラクティブストリーミング、ビデオ・インタラクティブストリーミング、音声通話、ビデオ通話の4つに分けられ、4つの基本サービスは単独で使用することも、重複して使用することも可能です。各基本サービスに対応する課金説明は以下のとおりです。

<table>
<tr><th>サービス</th><th>サービス説明</th><th>課金説明</th></tr>
<tr>
<td>ボイス・インタラクティブストリーミング</td>
<td><ul style="margin:0">
<li>キャスターと視聴者の音声によるマイク接続交流をサポート。</li>
<li>キャスターのルーム間（ライブストリーミングルーム間）PKをサポート。</li>
<li>スムーズなマイクのオン・オフをサポート。切り替えプロセスを待つ必要がなく、キャスターの遅延は300ms未満です。</li>
<li>1つのルームのマイクオン人数を無制限にでき、最大50人のマイク同時接続をサポートします。</li>
<li>低遅延ライブストリーミングモードでは、視聴者10万人の同時再生をサポート、再生の遅延を1000msまで低減させています。</li>
<li>CDN Relayed live streamingモードの場合は、視聴者数が無制限です。</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39785">ボイス・インタラクティブストリーミングの課金説明</a></td>
</tr>
<tr>
<td>ビデオ・インタラクティブストリーミング</td>
<td><ul style="margin:0">
<li>キャスターと視聴者のビデオによるマイク接続交流をサポート。</li>
<li>キャスターのルーム間（ライブストリーミングルーム間）PKをサポート。</li>
<li>スムーズなマイクのオン・オフをサポート。切り替えプロセスを待つ必要がなく、キャスターの遅延は300ms未満です。</li>
<li>1つのルームのマイクオン人数を無制限にでき、最大50人のマイク同時接続をサポートします。</li>
<li>低遅延ライブストリーミングモードでは、視聴者10万人の同時再生をサポート、再生の遅延を1000msまで低減させています。</li>
<li>CDN Relayed live streamingモードの場合は、視聴者数が無制限です。</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39786">ビデオ・インタラクティブストリーミングの課金説明</a></td>
</tr>
<tr>
<td>音声通話</td>
<td><ul style="margin:0">
<li>2人または多人数音声チャット通話。48kHz、ダブルサウンドチャンネルをサポート。</li>
<li>1つのルームで最大300人のオンライン同時接続、最大50人のマイク同時起動をサポート。</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39787">音声通話の課金説明</a></td>
</tr>
<tr>
<td>ビデオ通話</td>
<td><ul style="margin:0">
<li>2人または多人数のビデオ通話。720P、1080PのHD画質をサポート。</li>
<li>1つのルームで最大300人のオンライン同時接続、最大50人のカメラ同時起動をサポート。</li></ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">ビデオ通話の課金説明</a></td>
</tr>
</table>

## 付加価値サービス

付加価値サービスとは、4つの基本サービスに加えて提供される付加価値機能のことで、基本サービスとは別に単独で使用することはできず、付加価値サービスの使用には別途付加価値費用の支払いが必要となります。TRTCは**クラウドレコーディング**と**Cloud MixTranscoding**の2種類の付加価値サービスを提供します。対応する課金説明は以下のとおりです。

| サービス                                                         | サービス説明                                                     | 課金説明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) | Relayed Push方式を採用し、**Cloud Streaming Services**の力を用いて、完全なクラウドレコーディング機能（録音/録画）を提供します。記録されたファイルを**VOD**プラットフォームに保存するため、随時ダウンロードまたは再生が可能です。 | [クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385) |
| [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) | MCUクラスターを使用して、TRTCルーム内の各種アップストリームのオーディオ・ビデオストリーミングを必要に応じてミクストランスコードし、トランスコード後に出力されたオーディオ・ビデオストリーミングはCloud Streaming ServicesへRelayed Pushし、**クラウドレコーディング**または**CDNライブストリーミング視聴の実現**を行うことができます。 | [Cloud MixTranscoding課金説明](https://intl.cloud.tencent.com/document/product/647/38929) |

## 無料トライアル

2021年8月20日以降、初めて[TRTCコンソール](https://console.cloud.tencent.com/trtc)でアプリケーションを作成するTencent Cloudアカウントを対象に、10000分間の無料お試しパックをプレゼントいたします。無料お試しパックは、 [ビデオ通話](https://intl.cloud.tencent.com/document/product/647/39788)、[音声通話](https://intl.cloud.tencent.com/document/product/647/39787)、[ビデオ・インタラクティブストリーミング](https://intl.cloud.tencent.com/document/product/647/39786)、[ボイス・インタラクティブストリーミング](https://intl.cloud.tencent.com/document/product/647/39785) のサービス利用量の引き落とし分として、お使いいただけます。さらなる詳細については[無料試用](https://intl.cloud.tencent.com/document/product/647/39784)をご参照ください。