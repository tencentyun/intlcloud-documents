
## 操作シナリオ
アドレスジェネレーターを使用して、追加済みのプッシュ/再生ドメイン名を迅速に選択し、対応するプッシュ/再生アドレスを生成できます。

## 前提条件
 [LVBコンソール](https://console.cloud.tencent.com/live) の [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056) に1つ以上の使用可能なドメイン名があること。

## 操作手順
1. LVBコンソールにログインし、【補助ツール】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を選択し、アドレスジェネレーターに移動します。
3. アドレスジェネレーターで次の設定を行います。
	1. **プッシュドメイン名**または**再生ドメイン名**の生成タイプを選択します。
	2. ドメイン名管理内に追加済みの対応するドメイン名を選択します。
	- 同一ドメイン名の複数Appを区別するために使用されるアドレスパスであるAppNameを編集します。デフォルト値は liveです。
> AppName はカスタム編集をサポートし、アルファベット、数字および記号のみをサポートします。
	4. カスタマイズされたカスタムストリーム名StreamNameを入力します（例：liveteststream）。
	5. アドレスの期限切れ時間を選択します（例：`2019-11-30 23:59:59`）。
3. 【アドレスの生成】をクリックすれば、対応するドメイン名アドレスが生成されます。
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>
>- 生成されたプッシュ/再生アドレスは次の4つの部分で構成されます。
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
>- 生成された再生アドレスはRTMP、FLV、HLSのプロトコルをサポートしています。再生アドレスの後ろにある2次元コードをクリックし、コードをスキャンして簡易版Demoで再生アドレスを表示できます。
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
