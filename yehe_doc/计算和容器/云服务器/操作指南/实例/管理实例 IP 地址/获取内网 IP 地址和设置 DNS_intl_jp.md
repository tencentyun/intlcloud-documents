## 概要
このドキュメントでは、インスタンスのプライベートIPアドレスを取得し、プライベートDNSを設定する方法について説明します。

## 操作手順
### インスタンスのプライベートIPアドレスの取得
<dx-tabs>
::: コンソールを利用した取得
1.   [CVMコンソール]( https://console.cloud.tencent.com/cvm/)にログインします。
2. インスタンス管理ページで、実際に使用されているビューモードに従って操作します。
   - **リストビュー**：下図のように、プライベートIPを表示したいインスタンスを選択し、マウスを「プライマリIPv4アドレス」列に移動して、<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;">をクリックすれば、プライベートIPをコピーできます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/14720408f77509b0dced407f75adbd21.png)
 - **タブビュー**：下図のように、インスタンスページで、「IPアドレス」のプライベートネットワークアドレス後の<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: -3px 0px;">をクリックすれば、プライベートIPをコピーできます。
![](https://qcloudimg.tencent-cloud.cn/raw/3a251c153caddfb6cf62bb6e6e6ff2cd.png)

:::
::: \sAPI\sを利用した取得
[DescribeInstancesインターフェース](https://intl.cloud.tencent.com/zh/document/product/213/33258)をご参照ください。
:::
::: インスタンスメタデータを利用した取得
1. CVMにログインします。
2. cURLツールまたはHTTPのGETリクエストを介して、インスタンスのメタデータにアクセスします。
<dx-alert infotype="explain" title="">
以下の操作は、cURLツールを例とします。
</dx-alert>
次のコマンドを実行し、プライベートIPを取得します。
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
``` 下図のように、返される情報はプライベートIPアドレスです。
![](//mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)
インスタンスメタデータのさらに詳細な情報については、 [インスタンスメタデータの確認](https://intl.cloud.tencent.com/zh/document/product/213/4934)をご参照ください。
:::
</dx-tabs>

### プライベートネットワークDNSの設定 
ネットワーク解析にエラーが発生した場合、CVMのOSの種類に応じてプライベートネットワークDNSを手動で設定できます。
<dx-tabs>
::: Linux\sシステム
1.  Linux CVMにログインします。
2.次のコマンドを実行して、 `/etc/resolv.conf`ファイルを開きます。
```
vi /etc/resolv.conf
```
3. 「**i**」キーを押して編集モードに切り替え、[プライベートネットワークDNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns)に対応するリージョンに従ってDNS IPを変更します。
たとえば、プライベートネットワークDNS IPを北京リージョンのプライベートネットワークDNSサーバーに変更します。
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. ** Esc**キー を押して、**:wq**を入力し、ファイルを保存して戻ります。
:::
::: Windows\sシステム
1. Windows CVMにログインします。
2. OSのインターフェースで、**コントロールパネル** &gt; **ネットワークと共有センター** &gt; **アダプターの設定の変更**を開きます。
3. **イーサネット**を右クリックして、**プロパティ**を選択し、「イーサネットのプロパティ」ウィンドウを開きます。
4. 下図のように、「イーサネットのプロパティ」ウィンドウで、**インターネットプロトコルバージョン4（TCP/IPv4）**をダブルクリックして開きます。
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. **次のDNSサーバーのアドレスを使う** にチェックをして、[プライベートネットワーク DNS](https://intl.cloud.tencent.com/zh/document/product/213/5225?from_cn_redirect=1#.E5.86.85.E7.BD.91-dns) に対応するリージョンに従ってDNS IPを変更します。
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
6. **OK**をクリックします。
:::
</dx-tabs>
