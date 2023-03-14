## ユースケース

Cloud Infinite基本画像処理のウォーターマーク機能は画像上への[画像ウォーターマーク](https://intl.cloud.tencent.com/document/product/1045/33720)または[テキストウォーターマーク](https://intl.cloud.tencent.com/document/product/1045/33721)の追加をサポートしています。ただし、現実の業務シーンにおいては、1枚の画像上に、固定のロゴウォーターマークと動的に変化するテキストウォーターマーク（ユーザー名など）の両方がある状況がしばしば発生します。上記の状況について、参考までに以下の方法をご紹介します。実際の業務シーンに応じて、適切な統合方法を選択することができます。

## 方法の優位性比較

| 方法 | メリット | デメリット |
|---------|---------|---------|
| 方法1 | 統合が簡単で、手軽に実装できます。 | ウォーターマークのサイズを画像の大きさに合わせて動的に変えることができず、タイリング操作を行うことができません。 |
|方法2 | 画像サイズがよく変わる場合に、方法1に比べてよりアダプティブな効果が得られます。 | 統合のフローがより煩雑であり、2回分の処理料金がかかります。 |


## 操作方法

### 方法1：パイプラインオペレーターを使用してURLを実装すると同時に2種類のウォーターマークを付与する

Cloud Infiniteの基本画像処理機能では、[パイプラインオペレーター](https://intl.cloud.tencent.com/document/product/1045/33727) "|"を使用して、1回のリクエストで複数回の処理を行うことができ、なおかつ処理料金とトラフィック料金は1回分として計算されます。この方式ではリクエストの繰り返しによる遅延と追加料金を大幅に減らすことができます。

#### 操作手順

1. [画像ウォーターマーク](https://intl.cloud.tencent.com/document/product/1045/33720)のAPIドキュメントを参照し、画像ウォーターマークのパラメータを定義します。
APIパラメータに不慣れな場合は、[スタイル管理](https://intl.cloud.tencent.com/document/product/1045/33443)のドキュメントを参照し、コンソールでスタイルを追加してパラメータを生成することができます。


```
watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/dissolve/60/dx/10/dy/50/gravity/southeast
```
>? ここのコード`aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc`は、ウォーターマーク画像リンク（COS bucket上に保存されている画像のリンク）にURLセーフなBase64エンコードを経て生成されたものです。
>
2. [テキストウォーターマーク](https://intl.cloud.tencent.com/document/product/1045/33721)のAPIドキュメントを参照し、テキストウォーターマークのパラメータを定義します。
APIパラメータに不慣れな場合は、[スタイル管理](https://intl.cloud.tencent.com/document/product/1045/33443)を参照し、コンソールでスタイルを追加してパラメータを生成することができます。

```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```

>? ここのコード`VUlOOiAxMjM0NTY3OA`はテキスト情報`UIN: 12345678`にURLセーフなBase64エンコードを行って生成されたものです。
>
3. パイプラインオペレーターを使用して画像ウォーターマークとテキストウォーターマークの2つの部分のパラメータをスプライシングします。
```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```
4. スプライシングしたパラメータを画像のダウンロードリンクの後ろにつなげます。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```
これで混合ウォーターマークの画像が得られます。

URLの長さを短縮するには、[スタイル管理](https://intl.cloud.tencent.com/document/product/1045/33443)のドキュメントを参照し、コンソールで画像ウォーターマーク（変更なし）の部分をスタイル`watermark1`として追加します。

こうすることで、リンクは次のように短縮されます。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```
その後テキストの内容を変更したい場合は、リンク内の`VUlOOiAxMjM0NTY3OA`の部分を更新後のBase64エンコードに変更するだけで実現できます。例えば`UIN: 88888888`のコードは`VUlOOiA4ODg4ODg4OA`であり、この場合リンクを次の内容に変更するだけで、テキスト内容の入れ替えが実現できます。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiA4ODg4ODg4OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```



### 方法2：テキストおよび画像ウォーターマークを透明な画像上に印刷し、それを画像ウォーターマークにする

1. 400px * 400pxサイズの透明PNG画像1枚を用意し、 バケットにアップロードします。詳細については[ファイルのアップロード](https://intl.cloud.tencent.com/document/product/1045/37766)のドキュメントをご参照ください。
例：`https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png`
2. **方法1のステップ1 - ステップ3**を参照し、画像ウォーターマークとテキストウォーターマークの2つの部分のパラメータを生成し、スプライシングします。
3. スプライシングしたパラメータを透明PNG画像のダウンロードリンクの後ろにつなげます。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png?watermark/2/text/VUlOOiAxMjM0NTY/font/SGVsdmV0aWNhLmRmb250/fontsize/48/fill/IzAwMDAwMA/dissolve/60/gravity/south/dx/0/dy/60|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/center/dx/0/dy/0/dissolve/71
```


4. この透明画像をウォーターマーク画像とし、オリジナル画像に対してウォーターマーク付与操作を行えば完了です。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/gravity/southeast/dx/0/dy/0/dissolve/90
```


また、`scatype`パラメータによって、ウォーターマーク画像のサイズを画像の大きさに基づいて同じ比率でズームし、`batch`パラメータによってタイリングを設定することもできます。
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/scatype/3/spcent/30/gravity/southeast/dx/0/dy/0/dissolve/90/batch/1/degree/45
```


