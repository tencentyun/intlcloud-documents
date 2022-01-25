CSSコンソールはアドレスジェネレーター機能を提供し、ユーザーがプッシュ/再生アドレスを迅速に発行できるよう、アドレス情報の入力をサポートします。このうち、ライブストリーミングアドレスは、主にドメイン名（domain）、アプリケーション名（AppName）、ストリーム名（StreamName）および認証Keyで構成されます。
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

アドレス発行後、**コピーの選択**、**コピーボタンをクリック**または**2次元コードをスキャン**する方法によってアドレス情報を抽出します。


## 注意事項
- CSSは現在、アドレス発行履歴機能がありません。アドレス発行後、コピーして保存してください。
-同時に複数のライブストリーミングアドレスの発行が必要な場合は、ご自分でスプライシングする方法により発行することをお勧めします。具体的な操作ドキュメントについては、[自身でのライブストリーミングURLの接合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。
- CSSは、デフォルトでテストドメイン名 `xxxx.livepush.myqcloud.com`を提供しています。このドメイン名でプッシュテストを行うことができますが、正式なサービスでこのドメイン名をプッシュドメイン名として使用することはお勧めしません。
- ライブストリーミングアドレス2次元コードは、[Tencent CloudツールキットApp](https://intl.cloud.tencent.com/document/product/1071/38147)でスキャンして直接取得し、使用することができます。
- ストリーム名の拡張子とトランスコードテンプレートIDが競合する場合は、ストリーム状態の異常が発生します。ストリーム名を変更してください。



##  前提条件
[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインし、 [プッシュ/再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加していること。

## 設定パラメータの説明

<table>
<thead><tr><th>設定パラメータ</th><th>説明</th></tr></thead>
<tbody><tr>
<td>タイプとドメイン名の発行</td>
<td><strong>プッシュドメイン名</strong>または<strong>再生ドメイン名</strong>を選択できます。</td>
</tr><tr><td>AppName</td>
<td>ライブストリーミングのアプリケーション名で、CSSストリームメディアファイルの格納パスを参照するために使用され、デフォルトはliveです。<br>アルファベット、数字および記号のみをサポートします。</td>
</tr><tr><td>StreamName</td>
<td>カスタマイズされたストリーム名で、各CSSストリームの固有識別子です。<br>アルファベット、数字および記号のみをサポートします。</td>
</tr><tr><td>有効期限</td>
<td><li>再生アドレスの有効期限は、設定されたタイムスタンプに再生認証設定の有効期限を加えたものです。<li>プッシュアドレスの有効期限は設定時間です。</td>
</tr><tr><td>トランスコードテンプレート</td>
<td><li>発行タイプとして<strong>再生ドメイン名</strong>を選択した時のみ使用できます。<li> <a href="https://intl.cloud.tencent.com/document/product/267/31071">トランスコードテンプレート</a>を選択した場合、発行される再生アドレスはトランスコード後のライブストリーミング再生アドレスになります。元のCSSストリームを再生する必要がある場合は、トランスコードテンプレートの選択とアドレスの発行は必要ありません。</td>
</tr>
</tbody></table>

[](id:push)
## プッシュアドレスの発行
### 操作手順
1. CSSコンソールにログインし、[**アドレスジェネレーター**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択し、アドレスジェネレーターに移動します。
2. 発行タイプに**プッシュドメイン名**を選択し、ドメイン名管理に追加したプッシュドメイン名を選択します。
3. AppNameを入力します。デフォルト値はliveです。
4. StreamNameを入力します（例：liveteststream）。
5. アドレスの期限切れ時間を選択します（例：`2021-12-15 10:06:22`）。
6. **アドレスの発行**をクリックすれば完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
## プッシュアドレスの説明
プッシュはRTMP、WebRTC、SRTプロトコルをサポートしており、アドレスジェネレーター機能によって、プレフィックスが`rtmp://`、`webrtc://`、`srt://`のプッシュアドレスを発行できます。
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## 再生アドレスの発行
### 操作手順
1. CSSコンソールにログインし、[**アドレスジェネレーター**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択し、アドレスジェネレーターに移動します。
2. 発行タイプに**再生ドメイン名**を選択し、ドメイン名管理に追加した再生ドメイン名を選択します。
3. AppNameを入力します。デフォルト値はliveです。
4. StreamNameを入力します（例：liveteststream）。
5. アドレスの期限切れ時間を選択します（例：`2021-12-15 10:20:26`）。
6. 作成済みのトランスコードテンプレートを引用するかどうか選択します。
6. **アドレスの発行**をクリックすれば完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### 再生アドレスの説明
トランスコードテンプレートを使用する場合、発行される再生アドレスはトランスコード後のライブストリーミング再生アドレスになります。このうち、再生はRTMP、FLV、HLSおよびWebRTCプロトコルをサポートします。アドレスジェネレーターによって、プレフィックスが`rtmp://`、`http://`および`webrtc://`の再生アドレスが発行できます。
>! UDPプロトコルの再生アドレスは、ライブイベントストリーミングアドレスです。[ライブイベントストリーミングクイックスタート](https://intl.cloud.tencent.com/document/product/267/41030)で使用方法について確認できます。ライブイベントストリーミングの料金の詳細については、[価格一覧](https://intl.cloud.tencent.com/document/product/267/2819)をご参照ください。

![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
