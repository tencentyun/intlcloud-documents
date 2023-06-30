## 概要
本テキストではCVMコンソールおよびTencent Cloud APIを介してシャットダウン状態のインスタンスを起動する方法について説明します。

## 操作手順
<dx-tabs>
::: コンソールを介したインスタンスの起動

#### 単一インスタンスの起動
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
   - **リストビュー**：下図のように、起動したいインスタンスを選択し、画面右のメニューから**さらに** &gt; **インスタンス状態** &gt; **起動**を選択します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/900a2d8fb4a48ef1e9746922d6447666.png)
   - **タブビュー**：下図のように、起動したいインスタンスページで、右上コーナーの**起動**を選択します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/c62f67a3415635ddf535442b4b73343c.png)


#### 複数インスタンスの起動
下図のように、すべての起動したいインスタンスにチェックを入れ、リスト上部で、**起動**をクリックすれば、インスタンスを一括起動できます。
![](https://qcloudimg.tencent-cloud.cn/raw/dd734cf2e58b3e9d1ee1114bb94fe41a.png)

:::
::: \sAPI\sを介したインスタンスの起動
[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236) インターフェースをご参照ください。

:::
</dx-tabs>

## 後続の操作
インスタンスが起動状態である場合のみ、次の操作を実行できます。
- **インスタンスにログイン**：インスタンスのOSに基づき、[Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436) または [Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435)します。
- **[Cloud Block Storage（CBS）の初期化](https://intl.cloud.tencent.com/document/product/362/31596)** ：マウントされたCBSのフォーマット、パーティションおよびファイルシステムの作成などの初期化操作を実行します。
