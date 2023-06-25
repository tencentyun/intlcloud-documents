## 背景情報
一部のTencent Cloud CentOS 7 パブリックイメージには、CentOSディストリビューションに付属するPython 2-pip 8.1.2 がデフォルトでインストールされますが、このバージョンの pip では、ユーザーはインストールする互換性のあるパッケージバージョンを選択できません。デフォルトで最新のパッケージがインストールされます。ただし、pipの最新バージョンと、NumPy などの一般的に使用される一部のアプリケーションツールは、Python 2をサポートしていません、pip をアップグレードするコマンド (pip install pip --upgrade) を実行するとき、または特定のアプリケーションツールをインストールするときに、互換性の問題が発生する可能性があります。この問題を解決するために、Tencent Cloud は CentOS 7 シリーズの一部のイメージのpipを更新しました。


## 更新内容と範囲
以下の表に、更新された pip を含む CentOS 7パブリックイメージを示します。リスト内のパブリックイメージはデフォルトでPython 2 がインストールされており、pip は pip 8.1.2 から [pip 20.3.4](https://pypi.org/project/pip/20.3.4/)にアップグレードされています。
<dx-alert infotype="explain" title="">
アップグレードは段階的に実行され、2022 年12 月12 日に終了しました。対応するパブリックイメージのアップグレード後に購入したインスタンスは自動的に更新されますが、アップグレード前に購入したインスタンスは更新されません。操作ガイドを参照して手動でアップグレードを行うことができます。
</dx-alert>

| イメージバージョン | イメージID |
|---------|---------|
| CentOS 7.9 64-bit |img-180g963d |
| CentOS 7.6 64-bit |img-9qabwvbn |
| CentOS 7.9 64-bit+SG1-pv1.5 |img-all2luul |
| CentOS 7.9 64-bit+SG1-pv1.6 |img-ojhiw86l |
| CentOS 7.4(arm64) |img-k4xgkxa5 |

## 操作ガイド
###  pip のアップグレード
次のコマンドを実行すると、インスタンスの pip バージョンを表示できます。
```plaintext
pip --version
```
インスタンスのpip2のバージョンが pip 9.0 より前の場合、pipをアップグレードするとき、またはアプリケーションツールをインストールするときにエラーが発生する可能性があります。 この問題を回避するには、次のコマンドを実行して、最初にpipを最新バージョンの pip2 pip 20.3.4 にアップグレードします。
```plaintext
pip2 install --upgrade pip==20.3.4
```
### pip2のインストール
次のコマンドを実行して、pip2 の最新バージョンをインストールできます。
```plaintext
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python2 ./get-pip.py -i http://mirrors.tencentyun.com/pypi/simple --trusted-host mirrors.tencentyun.com
```
製品に関するご質問がある場合は、 [チケットを送信](https://console.intl.cloud.tencent.com/workorder/category)してください。
