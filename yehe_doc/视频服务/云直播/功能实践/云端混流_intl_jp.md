CSSサービスはライブミクスストリーミング機能を提供します。設定済みのミクスストリーミングレイアウトに基づき、各入力ソースの複数のストリームを統合して同期時に新しいストリームとみなし、ライブストリーミングのインタラクティブ効果を実現します。また、CSSライブミクスストリーミング機能はAPI 3.0が接続されています。具体的には、[ライブミクスストリーミングインターフェース](https://intl.cloud.tencent.com/document/product/267/35997)をご参照ください。このテキストでは、例を挙げて、各種シナリオでライブストリーミングのミクスストリーミングを実現する方法を説明します。

## 注意事項
- クラウドミクスストリーミング機能を使用する場合は、標準的なトランスコード費用が発生します。
- ミクスストリーミングのクリッピング機能を使用する場合は、クリッピングパラメータの値をソースストリームのパラメータより大きくすることはできません。


## 機能サポート
- 最大**16**のストリームのミクスストリーミングを同時にサポートします。
- **5**種類の入力ソースタイプ（オーディオおよびビデオ、純粋なオーディオ、純粋なビデオ、画像、キャンバス）のミキシングをサポートします。
- ミキシング後のストリームを新ストリームとして出力することをサポートします。
- クリッピング、ウォーターマーク機能をサポートします。
- テンプレートの設定をサポートします。
- ミクスストリーミングのレコーディングをサポートします。
- 自動ミクスストリーミングをサポートします。
- リアルタイムでミクスストリーミングの種類と位置の切り替えをサポートします。
- ミクスストリーミングの開始とキャンセルの切り替えをシームレスに実行できます。


## 一般的なレイアウトテンプレート
一般的なテンプレートには、10、30、40、310、390、410、510および610があります。これら8つのテンプレートを使用する場合、入力ストリームに位置および長さと幅のパラメータを入力する必要はなく、**オリジナル画面と同等比率のスケーリング**になります。ただし、テンプレートIDが必要です。

**一般的なレイアウトテンプレート：**
<table>
<style>#m_img{width:90%;height:auto;display:block;margin-left:auto;margin-right:auto; }</style>
<thead><tr><th>テンプレート 10</th><th >テンプレート 30</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/a6b395f6fc7c1d07e4325836a3b725e6.jpg" id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/05fbe1c32bec1aed0624785d51b8a2ef.jpg"  id="m_img"></td>
</tr>
<thead><tr><th >テンプレート 40</th><th>テンプレート 310</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/06cd40976b29452fa297d52db0d3435c.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/e1f4aa6f198856c47d8175302c649448.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>テンプレート 390</th><th >テンプレート 410</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/50157bb0b01d511c10b3637c13b1471a.png"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/6a420d03e7921453cbc461d1f1176f6c.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>テンプレート 510</th><th>テンプレート 610</th></tr></thead>
<td><img src="https://main.qcloudimg.com/raw/c0e5bd29f275a6f055af9830ceea0a02.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/5ca8ba33cc08e80d6aeb403645e75aac.jpg"  id="m_img"></td>


</tr>
</tbody></table>	



## ミクスストリーミングの作成
### パラメータの説明
より詳細な説明をご覧になる場合は、 [ライブミクスストリーミング](https://intl.cloud.tencent.com/document/product/267/35997)をご参照ください。



### シナリオ1：ミクスストリーミングの申請-20テンプレートの使用
ミクスストリーミングを使用して、テンプレートミクスストリーミングをプリセットします。

#### 入力例
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=20
&OutputParams.OutputStreamName=test_stream1
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&<パブリックリクエストパラメータ>
```

#### 出力例
```
{
  "Response": {
    "RequestId": "e8fa8015-0892-40d5-95c4-12a4bc06ed31"
  }
}
```

#### キャスターのマイク接続のミクスストリーミング効果
![img](https://main.qcloudimg.com/raw/a9bdfd2622e3152e61d8cb15a1b21aa1.jpg)


### シナリオ2：ミクスストリーミングの申請-390テンプレートの使用
ミクスストリーミングを使用して、テンプレートミクスストリーミングをプリセットします。

#### 入力例

```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=390
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth=1920  (キャンバスの幅)
&InputStreamList.0.LayoutParams.ImageHeight=1080 （キャンバスの高さ）
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&<パブリックリクエストパラメータ>
```

#### 出力例

```
{
  "Response": {
    "RequestId": "9d8d5837-2273-4936-8661-781aeab9bc9c"
  }
}
```

#### キャスターPKのミクスストリーミング効果
![img](https://main.qcloudimg.com/raw/cad10f080a239725893e5221faa21c17.jpg)



###  シナリオ3：カスタマイズされたミクスストリーミングの例
カスタマイズされたレイアウトを使用します。そのうち、位置パラメータLocationXとLocationYは画面左上隅に対応する背景画面左上隅の絶対ピクセル距離です。
![](https://main.qcloudimg.com/raw/e1f81cd4a9b08af4ad7e4658fc643f0d.png)

#### 入力例
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth = 1920
&InputStreamList.0.LayoutParams.ImageHeight= 1080
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.1.LayoutParams.ImageWidth = 640
&InputStreamList.1.LayoutParams.ImageHeight= 360
&InputStreamList.1.LayoutParams.LocationX= 50
&InputStreamList.1.LayoutParams.LocationY= 720
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&InputStreamList.2.LayoutParams.ImageWidth = 640
&InputStreamList.2.LayoutParams.ImageHeight= 360
&InputStreamList.2.LayoutParams.LocationX= 740
&InputStreamList.2.LayoutParams.LocationY= 720
&<パブリックリクエストパラメータ>
```


#### 出力例
```
{
  "Response": {
    "RequestId": "8c443359-ba07-4b81-add8-a6ff54f9bf54"
  }
}
```


#### カスタマイズされたミクスストリーミングの効果
![](https://main.qcloudimg.com/raw/db6a87baba1f1891f514d4bea9b38ee4.png)

## ミクスストリーミングのキャンセル
### パラメータの説明
より詳細な説明をご覧になる場合は、 [一般的なミクスストリーミングのキャンセル](https://intl.cloud.tencent.com/zh/document/product/267/35998)をご参照ください。

### シナリオの例
session idに基づき、ミクスストリーミングをキャンセルします。
#### 入力例
```
https://live.tencentcloudapi.com/?Action=CancelCommonMixStream
&MixStreamSessionId=test_room
```

#### 出力例
```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```

>! 
>- ミクスストリーミングを申請後、5秒以上経ってから、ミクスストリーミングをキャンセルしてください。
>- ミクスストリーミングをキャンセルした後、30秒経たなければ、同一のsession idでミクスストリーミングを申請することができません。


## エラーコード
クラウドミクスストリーミングAPI3.0は大部分の一般的なエラーコードを [API3.0 エラーコード](https://intl.cloud.tencent.com/document/product/267/35997#6.-.E9.94.99.E8.AF.AF.E7.A0.81) のスタイルに変換されていますが、一部のエラーコードをカバーしきれていない可能性があります。これらエラーコードはInvalidParameterでエラー表示され、 Message中に`err_code [ $code ],msg [ $message ]`の形式で提示されます。具体的なcodeに対応する原因は次のとおりです。

<table>
<thead><tr><th>エラーコード</th><th>原因</th><th>原因調査の推奨</th></tr></thead>
<tbody><tr>
<td>-1</td>
<td>入力解析パラメータエラー</td>
<td><ul style="margin:0">
    <li>リクエストボディbody json形式が正しいかどうかをチェックします。</li>
    <li>InputStreamListが空かどうかをチェックします。</li>
    </ul></td>
</tr><tr>
<td>-2</td>
<td>入力パラメータエラー</td>
<td> 画面パラメータがオーバーフローしていないかチェックします。</td>
</tr><tr>
<td>-3</td>
<td>ストリーム数のエラー</td>
<td>入力ストリーム数が[1，16]の範囲内にあるかをチェックします。</td>
</tr><tr>
<td>-4</td>
<td>ストリームパラメータエラー</td>
<td><ul style="margin:0">
    <li>入力出力の長さと幅が（0，3000）の範囲内にあるかどうかをチェックします。 </li>
    <li>入力ストリーム数が（0、16]の範囲内にあるかどうかをチェックします。 </li>
    <li>入力ストリームがLayoutParamsを伴っているかどうかをチェックします。 </li>
    <li>InputTypeが（有効数値：0，2，3，4，5）をサポートしているかどうかをチェックします。 </li>
    <li>ストリームIDの長さが（1，80）を満たしているかどうかをチェックします。</li>
    </ul></td>
</tr><tr>
<td>-11</td>
<td>レイヤーエラー</td>
<td><ul style="margin:0">
    <li>レイヤー数と入力ストリーム数が一致しているかどうかをチェックします。</li>
    <li>レイヤーIDが重複していないかをチェックします。</li>
    <li>レイヤーIDが（0，16]の間にあるかどうかをチェックします。</li>
    </ul></td>
</tr><tr>
<td>-20</td>
<td>入力パラメータとインターフェースがマッチしません</td>
<td><ul style="margin:0">
    <li>入力ストリーム数がテンプレートIDとマッチしているかどうかをチェックします。</li>
    <li> カラーパラメータが正しいかどうかをチェックします。</li>
    </ul></td>
</tr><tr>
<td>-21</td>
<td>ミクスストリーミング入力ストリーム数のエラー</td>
<td>入力ストリームの本数が2本以上であるかどうかをチェックします。</td>
</tr><tr>
<td>-28</td>
<td>背景の長さと幅の取得に失敗しました</td>
<td><ul style="margin:0">
    <li>キャンバスを設定する場合は、キャンバスの長さと幅が設定されているかどうかをチェックします。 </li>
    <li>バックグラウンドストリームが存在しているかどうかをチェックします（プッシュ後、5秒経ってから、再びミクスストリーミングする必要があります）。</li>
    </ul></td>
</tr><tr>
<td>-29</td>
<td>クリッピングパラメータのエラー</td>
<td>クリッピング位置がストリームの長さと幅を超過していないかチェックします。</td>
</tr><tr>
<td>-33</td>
<td>ウォーターマーク画像IDエラー</td>
<td>入力画像IDが設定さているかどうかをチェックします。</td>
</tr><tr>
<td>-34</td>
<td>ウォーターマーク画像URLの取得に失敗しました</td>
<td>画像が正常にアップロードされているかどうか、URLが生成済みかどうかをチェックします。</td>
</tr><tr>
<td>-111</td>
<td>OutputStreamName パラメータと OutputStreamType がマッチしません</td>
<td><ul style="margin:0">
    <li>OutputStreamTypeが0である場合、OutputStreamNameはInputStreamListに表示される必要があります。 </li>
    <li>OutputStreamTypeが1である場合、OutputStreamNameはInputStreamListに含まないでおく必要があります。</li>
    </ul></td>
</tr><tr>
<td>-300</td>
<td>出力ストリームIDがすでに使用されています</td>
<td>現在の出力ストリームが別のミクスストリーミングの出力ストリームとなっていないかどうかをチェックします。</td>
</tr><tr>
<td>-505</td>
<td>入力ストリームがuploadで見つかりません</td>
<td>プッシュの成功から5秒後に、ミクスストリーミングを開始します。 再生できるかどうかをチェックします。</td>
</tr><tr>
<td>-507</td>
<td>ストリームの長さと幅パラメータのクエリーに失敗</td>
<td><ul style="margin:0">
    <li>キャンバスの幅、高さが設定されているかどうかをチェックします。 </li>
    <li>プッシュが正常に実施されたかどうかをチェックし、プッシュから5秒後にミクスストリーミングを再開することを推奨します。</li>
    </ul></td>
</tr><tr>
<td>-508</td>
<td>出力ストリームIDエラー</td>
<td>同様のMixStreamSessionIdに異なる出力ストリームIDを使用する状況が存在するかどうかをチェックします。</td>
</tr><tr>
<td>-10031</td>
<td>ミクスストリーミングの起動に失敗</td>
<td>プッシュから5秒後に再びミクスストリーミングすることを推奨します。</td>
</tr><tr>
<td>-30300<br>-31001<br>-31002</td>
<td>ミクスストリーミングキャンセル時のsessionidが存在しません</td>
<td>MixStreamSessionIdが存在するかどうかをチェックします。</td>
</tr><tr>
<td>-31003</td>
<td>出力ストリームIDとsessionの出力ストリームID がマッチしません</td>
<td>ミクスストリーミングキャンセル時に入力した出力ストリームIDをチェックします。</td>
</tr><tr>
<td>-31004</td>
<td>出力ストリームのビットレートが不正です</td>
<td>出力ストリームのビットレートが[1，50000]の間であるかどうかをチェックします。</td>
</tr><tr>
<td>その他</td>
<td>その他エラーについては、 <a href="https://intl.cloud.tencent.com/contact-sales">でカスタマサービス</a> に連絡し、テクニカルサポートを要請してください</td>
<td>-</td>
</tr>
</tbody></table>

## よくあるご質問
- [プッシュ後にミクスストリーミングした場合に、-505エラーコードが返されるのはなぜですか？](https://intl.cloud.tencent.com/document/product/267/38255#que1)
- [ミクスストリーミングの申請後、ミクスストリーミングをキャンセルしない状態を継続した場合、どうなりますか？](https://intl.cloud.tencent.com/document/product/267/38255#que5)
- [ミクスストリーミングのアシスタントキャスター画面が予想される位置とは異なることがあるのはなぜですか？](https://intl.cloud.tencent.com/document/product/267/38255#que9)

>?これら以外のクラウドミクスストリーミングに関連する質問については、 [クラウドミクスストリーミング関連](https://intl.cloud.tencent.com/document/product/267/38255)をご参照ください
