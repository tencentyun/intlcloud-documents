<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
</style>

## Native Demo
<table>
<tr>
<th>iOS</th><th>Android</th><th>Windows</th><th >Mac OS</th>
</tr>
<tr>
<td><img style="width:150px" src="https://main.qcloudimg.com/raw/a1a6fd4a9bc3ad2b5fe60e31202c8fda.png" data-nonescope="true"></td>
<td><a onclick="window.open('https://dldir1.qq.com/hudongzhibo/liteav/TRTCDemo.apk')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
<td><a onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2')"><button style="width:150px;height: 150px;border:none;background-image:url(https://main.qcloudimg.com/raw/e80b8f4462e2904b31dcdcaabe71c484.png);background-size: cover;">
</button></a></td>
</tr>
</table>


## クロスプラットフォームDemo
<table>
<tr>
<td>
<input type="button" value="ビデオ通話" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html')" /><br><br>
<input type="button" value="インタラクティブライブストリーミング" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html')" />
</td>
<td>
<a onclick="window.open('https://www.pgyer.com/KP03')" value="Flutter_ios_版">
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/6d4d839ef8050cd3839b86f98bd7c35f.png);background-size: cover;">
</button>
</a>
<br>
<a onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk')" value="Flutter_android_版"> 
	<button style="width:150px;height: 83px;border:none;background-image:url(https://main.qcloudimg.com/raw/f53741b9ad7567c475841e68cc65dbc3.png);background-size: cover;">
</button>
</a></td>
<td>
<input type="button" value="Windows版" class="inbuttom"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" /><br><br>
<input type="button" value="MacOS版" class="inbuttom" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" /></td>
</tr>
</table>





## ビデオ通話シーン
ビデオ通話シーンとは、2人または多人数で行うビデオ通話で、720P、1080Pの高画質をサポートしています。1つのルームで最大300人の同時オンライン、最大50人のカメラ同時起動をサポートします。よくあるユースケースとしては、1対1のビデオ通話、300人のビデオミーティング、オンライン医療相談、ビデオチャット、ビデオカスタマーサービス、ビデオインタビュー、ビデオダブルレコーディング、オンライン申し立て、ビデオ人狼ゲームなどがあります。
<dx-tabs>
::: iOS&Android

<table>
<tr>
   <th>発呼側</th>
   <th>着呼側</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/group-recv.gif"/></td>
</tr>
</table>
:::
::: Flutter\s(iOS/Android)
![](https://imgcache.qq.com/operation/dianshi/other/8d81a52d-ffd3-4bbd-bd09-1a1648569b2d.453825bf12c01b9fe937ca8d7291f3c44b48cced.gif)
:::
::: Windows
![](https://imgcache.qq.com/operation/dianshi/other/win.836bd473a766ea962d0b40117888e99aad5db6c8.gif)
:::
::: macOS
![](https://imgcache.qq.com/operation/dianshi/other/macOS.cd7d6d7e8a7fcc388ec27e41c6952b8615ce9d34.gif)
:::
::: デスクトップブラウザ
![](https://imgcache.qq.com/operation/dianshi/other/058ffcf5-60f0-430c-96c7-e1760b93e444.fdd0f2c10a8242dadbf99108a48a59124124b437.gif)

<table>
<tr><th>発呼側</th><th>着呼側</th> </tr>
<tr>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videocall.gif"/></td>
<td><img src="https://webim-1252463788.cos.ap-shanghai.myqcloud.com/trtc-calling-doc-assets/videoaccept.gif"/></td>
</tr>
</table>

:::
</dx-tabs>

## 音声通話シーン
音声通話シーンとは、2人または多人数で行う音声通話で、48kHzのダブルサウンドチャンネルをサポートしています。1つのルームで最大300人の同時オンライン、最大50人のマイク同時起動をサポートします。よくあるユースケースとしては、1対1の音声通話、多人数音声チャット通話、ボイスチャット、音声ミーティング、音声カスタマーサービス、人狼ゲームなどがあります。
<dx-tabs>
::: iOS&Android

<table>
<tr>
   <th>発呼側</th>
   <th>着呼側</th>
 </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/call.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/recv.gif"/></td>
</tr>
</table>

## ビデオ・インタラクティブストリーミングシーン
ビデオ・インタラクティブストリーミングシーンは、キャスターと視聴者間のビデオ・マイク接続インタラクションやキャスターのルーム間（ライブストリーミングルーム間）PKをサポートしています。マイクのオン・オフはスムーズで、切り替え時に待つ必要がなく、キャスターの遅延は300ms未満です。1つのルームで接続できるマイク数は無制限で、最大50人の同時マイク接続が可能です。低遅延のライブストリーミングモードでは10万人の同時再生をサポートしており、再生遅延は低く、1000msです。CDN Relayed live streamingモードでは、視聴者数は無制限です。よくあるユースケースとしては、低遅延ライブストリーミング、10万人のインタラクティブ授業、ビデオライブストリーミングPK、ビデオお見合いルーム、インタラクティブ授業、リモートトレーニング、大規模ミーティングなどがあります。
<dx-tabs>
::: iOS&Android
<table>
<tr>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/beauty.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/join.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/msg.gif"/></td>
<td><img width="260" height="561" src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/pk.gif"/></td>
</tr>
</table>
:::
::: デスクトップブラウザ
![](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/doc-assets/demo-official-website.gif)
:::
</dx-tabs>

## ボイス・インタラクティブストリーミングシーン
ボイス・インタラクティブストリーミングシーンは、キャスターと視聴者間の音声・マイク接続インタラクションやキャスターのルーム間（ライブストリーミングルーム間）PKをサポートしています。マイクのオン・オフはスムーズで、切り替え時に待つ必要がなく、キャスターの遅延は300ms未満です。1つのルームで接続できるマイク数は無制限で、最大50人の同時マイク接続が可能です。低遅延のライブストリーミングモードでは10万人の同時再生をサポートしており、再生遅延は低く、1000msです。CDN Relayed live streamingモードでは、視聴者数は無制限です。よくあるユースケースとしては、音声低遅延ライブストリーミング、音声ライブストリーミングマイク接続、音声ライブストリーミングPK、音声チャットルーム、音声お見合いルーム、カラオケルーム、FMラジオなどがあります。
<table>
     <tr>
         <th>キャスターのマイク操作</th>  
         <th>視聴者のマイク操作</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_pick_seat.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/voiceroom_enter_seat.gif"/></td>
</tr>
</table>


## ビデオミーティングシーン
ビデオミーティングシーンは、1080pの高解像度画質と48kHzの高音質をサポートしています。オーディオ・ビデオの遅延は300ms未満で、スムーズな高解像度のミーティング体験をお楽しみいただけます。画面共有、ファイル共有をサポートし、より効率的なミーティングを行うことができます。また、インスタントメッセージと組み合わせて、テキストと写真といったさまざまな形のディスカッション支援機能をサポートしており、ミーティングの進行に支障をきたしません。よくあるユースケースとしては、すべてのメディアのカスタマーサービス、オンラインミーティング、政府・企業のライブストリーミングなどがあります。
<table>
     <tr>
         <th>ミーティングに参加</th>  
         <th>画面共有</th>  
     </tr>
<tr>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
<td><img src="https://liteav.sdk.qcloud.com/doc/res/trtc/picture/enterroom.gif"/></td>
</tr>
</table>

## インタラクティブ授業シーン
インタラクティブ授業シーンとは、教師と学生のマイク接続インタラクション、最大50人の同時マイク接続をサポートしています。マイクのオン・オフはスムーズで、切り替え時に待つ必要がなく、キャスターの遅延は低く、300ms未満です。学生10万人の同時視聴をサポートし、視聴遅延は低く、1000msです。CDN Relayed live streamingの場合、視聴者数は無制限です。画面共有、インタラクティブホワイトボード、録音・再生などさまざまな授業アプリケーション機能をサポートして、より豊かなオンライン教育を構築します。よくあるユースケースとしては、大規模クラス、小規模クラス、超小規模クラス、AI授業、体験授業、内部トレーニングライブストリーミングクラス、1V1eラーニングなどがあります。
<table>
     <tr>
         <th>教師側(Electron)</th>  
         <th>学生側(Electron)</th>  
     </tr>
<tr>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_teacher.76058b065f0b01ccc5d6bfd058c6b655e69a149c.gif"/></td>
<td><img src="https://imgcache.qq.com/operation/dianshi/other/Electron_stu.9e3f55291b657d94878963ad86471b331190f47c.gif"/></td>
</tr>
</table>
