## VPCでのAvailability Zone間のアクセス

複数台のCVMが同じ地域の異なるAvailability Zoneに分布されているが、ファイルストレージの共有が必要とされた場合、それらのCVMとCFSを同一VPCで設定できます。すなわち、Availability Zone間でリソースの相互アクセスを実現します。

広州は例として挙げられると、広州1区のCVMが既に存在し、この場合CFSファイルストレージを利用しようとするが、広州1区のリソースが売り切れになったためファイルシステムを作成できません。
CVMがVPCの「広州1区」サブネット内である場合、[VPCコンソール](https://console.cloud.tencent.com/vpc)にログインしてこのVPCのためにAvailability Zoneが「広州2区」であるサブネットを作成できます。
![](https://main.qcloudimg.com/raw/d25fc9283b76f114a772bebb1b703548.png)
![](https://main.qcloudimg.com/raw/74ffa38cc8774e6534617aed6f4476df.png)
![](https://main.qcloudimg.com/raw/344f0c3bfce47031137fa66351bbb11c.png)

サブネットを作成した後、CFSコンソールに戻り、広州2区のリソースを作成したとき、このVPCと作成したばかりのサブネットを選択します。このVPCの広州1区サブネット配下のCVMはそのままCFSファイルシステムをマウントできます。[ファイルシステムマウントヘルプ](https://cloud.tencent.com/document/product/582/11523)を参照してください。


## VPC間および地域間のアクセス
ファイルストレージCFSはリソースアクセスを行うために以下のシナリオをサポートします。

- 複数台のCVMが異なるVPCに分布されているが、ファイルストレージの共有が必要とされるとき。 
- またはCVMとCFSは異なるVPCにあるとき。
- またはCVMとCFSは異なる地域に分布されるとき（最も優れたアクセス性能を達成するため、CVMとCFSを同一地域にすることをおすすめします）。

VPC-A/VPC-Bに分布されるCVMおよびVPC-Cに分布されるCFSを、「ピアツーピア接続」を設定することでVPC-A、VPC-B、VPC-C間の相互アクセスを実現できます。[ピアツーピア接続設定方法](https://cloud.tencent.com/document/product/215/5000)を参照してください。


## ネットワーク間のアクセス
複数台のCVMが基本ネットワークまたはVPCに分布され、ファイルストレージの共有が必要とされるとき、VPC配下のCFSファイルシステムを作成できます。
- 基本ネットワーク内のCVMからVPC配下のCFS：「Classiclink」を設定することにより、基本ネットワーク配下のCVMとVPC間のリソース相互アクセスを実現できます。[Classiclink設定方法](https://cloud.tencent.com/document/product/215/5002)を参照してください。
- VPC-A配下のCVMからVPC-B配下のCFS：前の章節の設定方法を参照してください。

>!
>- CFSは、基本ネットワーク内でVPCにおけるCVMとの連携をサポートしません。
>- クライアントとCFSはそれぞれ基本ネットワークとVPCネットワークにあるが、異なる地域にある場合、連携をサポートしません。

