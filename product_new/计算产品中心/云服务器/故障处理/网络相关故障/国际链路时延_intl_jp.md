## 問題の説明
北米リージョンのCVMにログインする時レイテンシーが長すぎます。

## 問題の分析
国内の国際ルーティング出口の数が少ないおよびその他要因により、並列処理数が高くなると、国際リンクが非常に混雑になり、アクセスが不安定になります。Tencent Cloudはすでにこの問題ををキャリアに報告しています。
現在、北米リージョンのCVMを購入して、中国国内で管理及びメンテナンスする必要がある場合、中国香港リージョンで購入したCVMを経由して、北米リージョンのCVMにログインすることで問題を解決できます。

## ソリューション
1. 中国香港リージョンのWindows CVMを購入して、「ジャンプサーバー」として利用します。
> 
> - 「カスタマイズ設定」ページの「1.リージョンとモデル選択」で、【中国香港】リージョンを選択します。
> [ここをクリックして購入する >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&regionId=5&zoneId=0&instanceType=S2ne.SMALL2&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=BANDWIDTH_PREPAID&loginSet=SET_PASSWORD)
> - Windows CVMは、北米リージョンにあるWindowsとLinuxのCVMへのログインをサポートしているので、購入することを推奨します。
> - **中国香港リージョンのWindows CVMを購入する場合、1Mbps以上の帯域幅を購入する必要があります。そうしないと、ジャンプサーバーにログインできません。**
>
2. 購入が成功した後、実際のニーズに応じて、中国香港リージョンのWindows CVMのログイン方法を選択する：
 - [RDPファイルを利用してWindows CVMにログインする](https://intl.cloud.tencent.com/document/product/213/5435)
 - [リモートデスクトップを利用してWindows CVMにログインする](https://cloud.tencent.com/document/product/213/35703)
 - [VNC を利用してWindows CVMにログインする](https://intl.cloud.tencent.com/document/product/213/32496)
3. 中国香港リージョンのWindows CVMで、実際のニーズに応じて、北米リージョンにあるCVMへのログイン方式を選択する：
 - 北米リージョンのLinux CVMにログインします。
    - [標準ログイン方式を利用してLinux CVM にログインする](https://intl.cloud.tencent.com/document/product/213/5436)
    - [リモートデスクトップを利用してLinux CVMにログインする](https://cloud.tencent.com/document/product/213/35699)
    - [VNCを利用してLinux CVMにログインする](https://intl.cloud.tencent.com/document/product/213/32494)
 - 北米リージョンのWindows CVMにログインします。 
    -  [RDPファイルを利用してWindows CVMにログインする](https://intl.cloud.tencent.com/document/product/213/5435)
    - [リモートデスクトップを利用してWindows CVMにログインする](https://cloud.tencent.com/document/product/213/35703)
    - [VNCを利用してWindows CVMにログインする](https://intl.cloud.tencent.com/document/product/213/32496)
