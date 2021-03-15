## 操作シナリオ
Tencent Cloudはプッシュアドレスの迅速な作成して、CSS機能をオンラインでプッシュテストできるWebプッシュ機能を提供します。

## 前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
-  [プッシュドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。
- デバイスにカメラがインストール済みであり、かつブラウザがカメラ許可を呼び出すためのFlashプラグインをサポートしていること。

## 操作手順
1. CSSコンソールにログインし、[【Webプッシュ】](https://console.cloud.tencent.com/live/tools/webpush)を選択します。
2. Webプッシュページで次の設定を行います。
	- プッシュドメイン名を選択します。
	- カスタムされたストリーム名StreamNameを記入します（例:`test`）。
	- 期限切れ時間を選択します（例：`2020-04-13 23:59:59`）。
	- 同一ドメイン名の複数Appを区別するために使用されるアドレスパスであるAppNameを編集します。デフォルト値はliveです。
3. 【プッシュ開始】をクリックし、カメラの呼び出しが承認されると、プッシュを開始できます
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)
4. 【Domain Management】で再生ドメイン名を追加済みである場合は、その下の方に対応する作成された再生アドレスが表示されます。なお、再生アドレスは次の4つの部分で構成されます。
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
RTMP、FLV、HLSのプロトコルをサポートしています。再生アドレスの後ろにある2次元コードをクリックし、コードをスキャンして簡易版Demoで再生アドレスを表示できます。
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
