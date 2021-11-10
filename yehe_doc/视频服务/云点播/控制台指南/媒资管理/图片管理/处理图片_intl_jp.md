## 操作シナリオ
[VODコンソール](https://console.cloud.tencent.com/vod/pics)にログインして、画像処理操作を行うことができます。ここでは画像処理テンプレートによってリアルタイムで画像処理を行う方法や、URL画像作成方法によって画像処理効果を迅速に得られる方法についてご紹介します。

## 操作手順
### 手順1：画像のアップロード
1. [VODコンソール](https://console.cloud.tencent.com/vod/pics)に入り、非管理者（メインアプリケーション）を選択し、左側ナビゲーションバーの【メディア資産管理】>【[画像管理](https://console.cloud.tencent.com/vod/pics)】を選択し、【画像アップロード】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/fed2ab4f8f9b94f15bae2c3c734a0f41.png)
2. アップロードする画像を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/592b99b27e42cb3734132ee8acc5f51e.png)
3. 【アップロード開始】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/300743187dc0a04f37bfdbb839074a63.png)
4. アップロード完了です。【管理】をクリックすると、この画像をアップロードしたアクセラレーションURLアドレスを確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/ac55111bc39488563f7abc3412cd9a54.png)

### 手順2：テンプレートの作成

VOD APIにより画像処理テンプレートを作成し、APIのその他の詳細設定を行うことができます。

1. 240 x 240サムネイルテンプレートの作成を例に挙げます。
```shell
https://vod.tencentcloudapi.com/?Action=CreateImageProcessingTemplate
&Operations.0.Type=Scale
&Operations.0.Scale.Type=ShortEdgeFirst
&Operations.0.Scale.ShortEdge=240
&Operations.1.Type=CenterCut
&Operations.1.CenterCut.Type=Rectangle
&Operations.1.CenterCut.Width=240
&Operations.1.CenterCut.Height=240
&<パブリックリクエストパラメータ>
```
2. リクエストに返される画像処理テンプレート番号は1009です。
```javascript
{
  "Response": {
    "Definition": 1009,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```

### 手順3：画像処理

URL画像作成方法による画像処理の公式は次のとおりです。
#### 処理後の画像URL = 元画像のURL + 間隔識別子 + 画像テンプレート番号 + “.” + 出力画像フォーマット
  - 元画像のURL：画像ファイルを [VOD](https://console.cloud.tencent.com/vod/pics) にアップロード後、アクセラレーションURLアドレスが生成されます。
  - 間隔識別子： !
  - 出力画像フォーマット：JPG、JPEG、PNG。


### 手順4：処理タイプ
画像処理はズームとトリミングの2種類をサポートしています。

<Table>
<tbody>
<tr>
<th>操作タイプ</th>
<th>詳細操作</th>
</tr>
<tr>
<td rowspan=5>サムネイル</td>
<td>幅を指定し、高さは同じ比率でズームされます。</td>
</tr>
<tr>
<td>高さを指定し、幅は同じ比率でズームされます。</td>
</tr>
<tr>
<td>長辺を指定し、短辺は同じ比率でズームされます。</td>
</tr>
<tr>
<td>短辺を指定し、長辺は同じ比率でズームされます。</td>
</tr>
<tr>
<td>幅と高さを指定して強制的にズームします。</td>
</tr>
<tr>
<td rowspan=2>トリミング</td>
<td>内接円をトリミングします。トリミング半径を指定します。</td>
</tr>
<tr>
<td>矩形をトリミングします。トリミングの幅と高さを指定します。</td>
</tr>
</tbody>
</Table>

#### タイプ1、サムネイル

- **幅を指定し、高さは同じ比率でズーム**
 - 作成テンプレート：10033、指定幅：700、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10033.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/abf6f0699647efe9bef7f22d8f3fb939.png)

- **高さを指定し、幅は同じ比率でズーム**
 - 作成テンプレート：10034、指定高さ：700、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10034.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/df5c784021a55910a67bd3fcf1be1ac8.png)

- **長辺を指定し、短辺は同じ比率でズーム**
 - 作成テンプレート：10035、指定長辺：300、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10035.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/fca36a5152c013ec9f111923f1f37b97.png)

- **短辺を指定し、長辺は同じ比率でズーム**
 - 作成テンプレート：10036、指定短辺：300、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10036.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/e3f9bd39fe92b57758d8954d44715d93.png)

- **幅と高さを指定して強制的にズーム**
 - 作成テンプレート：10037、指定高さ：300、指定幅：300、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10037.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/4225aa7986ac5f2f58b6cf061b51f64d.png)

#### タイプ2、トリミング
- **内接円トリミング**
 - 作成テンプレート：10038、指定出力画像半径：300、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10038.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/e62ef7791ff9b129259bd3fa04afd6d2.png)

- **矩形トリミング**
 - 作成テンプレート：10039、出力画像幅：300、出力画像高さ：300、出力フォーマット：PNG
 - 画像処理後のリンク：`http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10039.PNG`
 - 最終的な効果の表示：
![](https://main.qcloudimg.com/raw/433ea68294a8b8af47bae088e7a89508.png)

