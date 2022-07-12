## 操作シナリオ
ここでは、OSがCentOS 8.2およびCentOS 7.9のTencent Cloud CVMを例にとり、CentOS視覚化インターフェースの構築方法についてご紹介します。

## 説明事項
- 性能と汎用性の観点から、Tencent Cloudの提供するLinuxパブリックイメージには、デフォルトではグラフィックコンポーネントをインストールしていません。
- インストールが不適切な場合はインスタンスが正常に起動しなくなるおそれがあります。[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)または[スナップショットの作成](https://intl.cloud.tencent.com/document/product/362/5755)によってデータバックアップを作成することをお勧めします。

## 操作手順
実際に使用するCVMのOSに応じて、次の手順を参照して操作を行ってください。
<dx-tabs>
::: CentOS\s8.2
1. インスタンスにログインします。詳細については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 以下のコマンドを実行し、グラフィックインターフェースコンポーネントをインストールします。
```
yum groupinstall "Server with GUI" -y
```
3. 以下のコマンドを実行し、デフォルトのグラフィックインターフェースを設定します。
```
systemctl set-default graphical
```
4. 以下のコマンドを実行して、インスタンスを再起動します。
```
reboot
```
5. VNC方式でインスタンスにログインします。詳細については[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)をご参照ください。
インスタンスにログイン後、視覚化インターフェースが確認できれば構築は成功です。インターフェースの表示に従って設定を行い、デスクトップに入った後、必要に応じて関連の操作を行うことができます。下図に示します。
![](https://main.qcloudimg.com/raw/58e12a33b38e0114f5b3116b31f7b026.png)
:::
::: CentOS\s7.9
1. インスタンスにログインします。詳細については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 以下のコマンドを実行し、グラフィックインターフェースコンポーネントをインストールします。
```
yum groupinstall "GNOME Desktop" "Graphical Administration Tools" -y
```
3. 以下のコマンドを実行し、デフォルトのグラフィックインターフェースを設定します。
```
ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
```
4. 以下のコマンドを実行して、インスタンスを再起動します。
```
reboot
```
5. VNC方式でインスタンスにログインします。詳細については[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)をご参照ください。
インスタンスにログイン後、視覚化インターフェースが確認できれば構築は成功です。インターフェースの表示に従って設定を行い、デスクトップに入った後、必要に応じて関連の操作を行うことができます。下図に示します。
![](https://qcloudimg.tencent-cloud.cn/raw/246952ae60c02724727029b6a3c0ef1a.png)
:::
</dx-tabs>
