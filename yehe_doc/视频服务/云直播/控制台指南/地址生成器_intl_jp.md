CSSコンソールはアドレスジェネレーター機能を提供し、ユーザーがプッシュ/再生アドレスを迅速に生成できるよう、入力されたアドレス情報のマージをサポートします。そのうち、ライブストリーミングアドレスは、主にドメイン名(domain)、アプリケーション名(AppName)、ストリーム名(StreamName)および認証Keyから構成されています。
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)
アドレス生成後、**選択してコピー**、**コピーボタンをクリック**または**QRコードを読み取る**などの方法でアドレス情報を抽出します。


## 注意事項
- CSSは現在、アドレス生成履歴機能がありません。アドレス生成後、コピーして保存してください。
-同時に複数のライブストリーミングアドレスを生成する場合は、ライブストリーミングURLの自動接合機能をお勧めします。具体的な操作方法については、[ライブストリーミングURLの自動接合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。
- CSSは、デフォルトでテストドメイン名 `xxxx.livepush.myqcloud.com`を提供しています。このドメイン名でプッシュテストを行うことができますが、正式なサービスでこのドメイン名をプッシュドメイン名として使用することはお勧めしません。
- ライブストリーミングアドレスを示すQRコードは、[Tencent CloudキットApp](https://intl.cloud.tencent.com/document/product/1071/38147)でスキャンして直接取得、使用することができます。
- ストリーム名の拡張子とトランスコードテンプレート名に矛盾があれば、ストリームが異常状態になるため、ストリーム名を変更してください。



##  前提条件
[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインし、 [プッシュ/再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加していること。

## 設定パラメータの説明

<table>
<thead><tr><th>設定パラメータ</th><th>説明</th></tr></thead>
<tbody><tr>
<td>タイプとドメイン名の生成</td>
<td><strong>プッシュドメイン名</strong>または<strong>再生ドメイン名</strong>を選択できます。</td>
</tr><tr><td>AppName</td>
<td>ライブストリーミングのアプリケーション名で、CSSストリームメディアファイルの格納パスを参照するために使用され、デフォルトはliveです。<br>アルファベット、数字および記号のみをサポートします。</td>
</tr><tr><td>StreamName</td>
<td>カスタマイズされたストリーム名で、CSSストリームの一意な識別子です。<br>アルファベット、数字および記号のみをサポートします。</td>
</tr><tr><td>有効期間</td>
<td><li>再生アドレスの有効期間は、設定されたタイムスタンプに、設定された再生認証の有効期間を加えた時間です。<li>プッシュアドレスの有効期間は設定時間です。</td>
</tr><tr><td>トランスコーディングテンプレート</td>
<td><li>生成するタイプが<strong>再生ドメイン名</strong>の場合のみ使用されます。<li><a href="https://intl.cloud.tencent.com/document/product/267/31071">トランスコーディングテンプレート</a>を選択した場合、生成した再生アドレスは、トランスコーディングしたライブストリーミングの再生アドレスです。<li><a href="https://www.tencentcloud.com/document/product/267/50271">アダプティブ・ビットレートテンプレート</a>を選択した場合、生成した再生アドレスは、アダプティブ・ビットレートライブストリーミングの再生アドレスです。オリジナルライブストリームで再生する場合、トランスコーディングテンプレートでアドレスを生成する必要はありません。</td>
</tr>
</tbody></table>

[](id:push)

## プッシュアドレスの生成
### 操作手順
1. CSSコンソールにログインし、[**アドレスジェネレーター**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択し、アドレスジェネレーターに移動します。
2. 生成タイプで**プッシュドメイン名**を選択し、ドメイン名管理に追加したプッシュドメイン名を選択します。
3. AppNameを入力します。デフォルト値はliveです。
4. StreamNameを入力します。例：`liveteststream`。
5. アドレスの有効期間を選択します。例：`2021-12-15 10:06:22`。
6. **アドレスを生成**をクリックすれば完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
## プッシュアドレスの説明
プッシュはRTMP、WebRTC、SRTプロトコルをサポートし、アドレスジェネレーター機能によって、プレフィックスが`rtmp://`、`webrtc://`、`srt://`のプッシュアドレスを生成できます。
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## 再生アドレスの生成
### 操作手順
1. CSSコンソールにログインし、[**アドレスジェネレーター**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択し、アドレスジェネレーターに移動します。
2. 生成タイプで**再生ドメイン名**を選択し、ドメイン名管理に追加した再生ドメイン名を選択します。
3. AppNameを入力します。デフォルト値はliveです。
4. StreamNameを入力します。例：`liveteststream`。
5. アドレスの有効期間を選択します。例：`2021-12-15 10:20:26`。
6. 作成済みのトランスコーディングテンプレートを参照するかを選択します。
7. **アドレスを生成**をクリックすれば完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### 再生アドレスの説明
トランスコーディングテンプレートを使用した場合、トランスコーディングしたライブストリーミングの再生アドレスです。再生はRTMP、FLV、HLSおよびWebRTCプロトコルをサポートし、アドレスジェネレーターによって、プレフィックスが`rtmp://`、`http://`および`webrtc://`の再生アドレスを発行できます。
>! UDPプロトコルの再生アドレスは、LEB (Live Event Broadcasting)アドレスです。詳しくは、[LEBクイックスタート](https://intl.cloud.tencent.com/document/product/267/41030)をご参照ください。LEBの料金については、[価格一覧](https://intl.cloud.tencent.com/document/product/267/2819)をご参照ください。

![](https://qcloudimg.tencent-cloud.cn/raw/daaef95da077e0182db6e07943f4f360.png)

### アダプティブ・ビットレートアドレスの説明
アダプティブ・ビットレートテンプレートを使用した場合、生成した再生アドレスは、アダプティブ・ビットレートの再生アドレスです。再生はHLSとWebRTCプロトコルをサポートし、アドレスジェネレーター機能によって、プレフィックスが`http://` と `webrtc://`のプッシュアドレスを生成できます。
![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
