## 背景情報
WebShellサーバーの拡張とアップグレードのため、2021年4月1日以降、WebShell プロキシ IPアドレスに新しいCIDRブロックが追加されます。セキュリティグループで新しいWebShellプロキシIP CIDRブロックとリモートログインポート（デフォルトではポート22）を開いてください。　　　
>?WebShellログインの詳細については、[標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)ドキュメントをご参照ください。 
>



## 調整の詳細
- 新しいプロキシIP CIDRブロックは次のとおりです。
81.69.102.0/24
106.55.203.0/24
101.33.121.0/24
101.32.250.0/24
- 新旧のプロキシIPアドレス/ CIDRブロックは並行して使用されます。以下のIPアドレス/CIDR ブロックを含みます：
>?セキュリティグループのインバウンド（ソース）ルールで、新旧のプロキシIP CIDRブロックとリモートログインポートが開かれていることを確認してください。
>
81.69.102.0/24
106.55.203.0/24
101.33.121.0/24
101.32.250.0/24
115.159.198.247
115.159.211.178
119.28.7.195
119.28.22.215
119.29.96.147
211.159.185.38


## 関連する操作
- [標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)
- [セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)
